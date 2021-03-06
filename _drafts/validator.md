---
layout: post
title: "주민등록번호/외국인등록번호 검증"
excerpt: "주민등록번호/외국인등록번호를 검증해보자"
categories: [C#]
tags: [C#, 주민등록번호, 외국인등록번호]
author: Devwock
comments: true
---

## 주민번호 검증

### 주민번호 앞자리 검증

주민번호의 앞자리, 즉 생일을 검증한다.

```C#
public static bool IsValidSsnFirst(string ssn)
{
    if (string.IsNullOrWhiteSpace(ssn)) // 공백이나 NULL 검사
    {
        return false;
    }

    if (ssn.Length != 6) // 길이 검사
    {
        return false;
    }

    // DateTime 클래스의 TryParseExact로 파싱하여 날짜인지 확인
    DateTime temp;
    bool isValid = DateTime.TryParseExact(ssn, "yyMMdd", CultureInfo.InvariantCulture, DateTimeStyles.None, out temp);
    return isValid;
}
```

DateTIme 클래스의 TryParse를 이용해 년월일(yyMMdd)을 파싱, 파싱에 실패할 경우 생년월일이 아님을 알 수 있다.

### 주민번호 뒷자리 1번째까지 검증

생일 부분은 상기 방법으로 검사, 뒤 첫자리는 정해진 규격이 있으므로 숫자가 일치하는지만 보면 된다.

<script src="https://gist.github.com/DevWock/eabdf9b945b0cccd8e3df4846bb5c336.js?&lines=1-16"></script>

```C#
private static readonly int[] ssnFirstCode = { 1, 2, 3, 4, 5, 6, 7, 8 };

public static bool IsValidSsnOne(string ssn)
{
    if (string.IsNullOrWhiteSpace(ssn))
    {
        return false;
    }

    if (ssn.Length != 7)
    {
        return false;
    }

    if (!IsValidSsnFirst(ssn.Substring(0, 6)))
    {
        return false;
    }

    int[] lastSsnNumber = ssn.Substring(6, 1).Select(c => c - '0').ToArray();
    return ssnFirstCode.Contains(lastSsnNumber[0]);
}
```

### 주민번호 전체 검증

주민등록번호는 다음과 같이 구성되어 있다.
|년|년|달|달|일|일| - |코드|지역코드6자리|검증값|

주민등록번호를 쪼개서 특정한 공식으로 검증값을 계산, 입력된 값과 일치한가 확인하면 된다.

```C#
public static bool IsValidSsn(string ssn)
{
    if (string.IsNullOrWhiteSpace(ssn))
    {
        return false;
    }

    if (ssn.Length != 13)
    {
        return false;
    }

    if (!IsValidSsnOne(ssn.Substring(0, 7)))
    {
        return false;
    }

    int[] firstSsnNumber = ssn.Substring(0, 6).Select(c => c - '0').ToArray();
    int[] lastSsnNumber = ssn.Substring(6, 7).Select(c => c - '0').ToArray();

    int calculated = firstSsnNumber[0] * 2 + firstSsnNumber[1] * 3 + firstSsnNumber[2] * 4 + firstSsnNumber[3] * 5 + firstSsnNumber[4] * 6 + firstSsnNumber[5] * 7
                    + lastSsnNumber[0] * 8 + lastSsnNumber[1] * 9 + lastSsnNumber[2] * 2 + lastSsnNumber[3] * 3 + lastSsnNumber[4] * 4 + lastSsnNumber[5] * 5;

    int result = 11 - (calculated % 11);
    if (result >= 10)
    {
        result %= 10;
    }
    return result == lastSsnNumber[lastSsnNumber.Length - 1];
} 
```

## 사업자 등록번호

```C#
private static readonly int[] crnCheckId = { 1, 3, 7, 1, 3, 7, 1, 3, 5 };

public static bool IsValidCrn(string crn)
{
    if (string.IsNullOrWhiteSpace(crn))
    {
        return false;
    }

    if (crn.Length != 10)
    {
        return false;
    }

    int[] crnNumber = crn.Select(c => c - '0').ToArray();
    int checkSum = 0;
    for (int i = 0; i < 9; i++)
    {
        checkSum += crnCheckId[i] * crnNumber[i];
    }
    int checkSum2 = Convert.ToInt32(Math.Floor(Convert.ToDecimal(crnNumber[8] * crnCheckId[8]) / 10));
    checkSum += checkSum2;
    var result = 10 - (checkSum % 10);
    if (result >= 10)
    {
        result %= 10;
    }
    if (crnNumber[9] == result)
    {
        return true;
    }
    else
    {
        return false;
    }
}
```
