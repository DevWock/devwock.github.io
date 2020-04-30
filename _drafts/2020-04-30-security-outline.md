# 컴퓨터 보안의 개요

## 개념

* 정보를 여러가지 위협으로부터 보호하기 위한 정책 및 기법
  * 정보의 상태: 저장, 전달
  * 위협의 종류: 허락되지 않은 접근, 수정, 훼손, 유출 등
* 정보보호의 한 영역
* 컴퓨팅 환경이 관여된 모든 상황에 대한 정보보호
* 컴퓨팅 환경에 저장되거나 처리되는 정보를 다양한 위협으로부터 보호하기 위한 정책 및 기법

## 목표

* 핵심목표 (CID Triangle)
  * 기밀성(Confidentiality)
    * 허락되지 않은 자가 정보의 내용을 알 수 없도록 하는 것
    * 지키는 방법
      * 허락되지 않은 자가 정보에 접근을 아예 못하도록 함
      * 정보에 접근하더라도 무의미한 내용만 보이게 함
  * 무결성(Integrity)
    * 허락되지 않은 자가 정보를 함부로 수정할 수 없도록 함
    * 만약 허락되지 않은 자에 의한 수정이 발생했다면 이를 확인할 수 있는 것
  * 가용성(Availability)
    * 허락된 자가 정보에 접근하고자 할 때 이것이 방해 받지 않도록 하는 것
    * 즉, 정보에 대한 접근 권한이 있는 자는 필요할 때 언제든지 정보를 사용할 수 있어야 함
    * 정해진 시간 내에 정보를 볼 수 있음을 보장
* 그외
  * 부인방지(non-repudiation)
    * 정보에 관여한 자가 이를 부인하지 못하도록 하는 것
    * 발신 부인방지
      * 정보를 보낸 사람이 나중에 정보를 보냈다는 것을 부인하지 못하도록 함
    * 수신 부인방지
      * 정보를 받은 사람이 나중에 이를 부인하지 못하도록 하는 것
  * 인증(authetication)
    * 어떤 실체가 정말 주장하는 실체가 맞는지 확인할 수 있고 신뢰할 수 있는 것
    * 실체: 정보 자체, 정보를 이용하는 사용자 등
  * 접근제어(access control)
    * 정보에 대한 허락된 접근만 허용하고 그 외의 접근은 허용하지 않는 것
    * 즉, 접근 권한이 있는 자와 없는 자를 구분하여 제어
    * 접근 권한은 정보에 따라, 사용자에 따라 다양하게 부여될 수 있음

## 정보화 환경과 역기능

* 정보화 사회의 선진화
  * 과거에는 정보의 전파가 굉장히 느렸으나 통신회선 설치 이후 빨라짐
  * 인터넷을 통한 지구 반대편에서 일어나는 일도 실시간으로 알 수 있음

* 정보화 사회의 역기능도 증가
  * 악성 댓글, 스팸 메일, 개인정보 유출, 금전적인 목적을 대상으로 하는 피싱이나 파밍, 스미싱에 대한 개인적인 피해 증가
  * 불건전 정보 유통, 개인 사생활 침해 등과 같은 부작용
  * 심각한 사회 문제 대두

* 새로운 수법의 지속적인 등장
  * 과거 이메일을 이용하던 피싱은 보이스 피싱과 스미싱 등으로 다양화
  * 랜섬웨어처럼 안전한 암호 알고리즘을 악용하여 금전을 요구하는 수법도 등장
  
* 주요 기반 시설 위협에 따른 국가안보적인 측면의 위협
  * 주요 기반 시설이 점차 정보통신 네트워크에 의해 관리 및 통제됨
  * 사이버 공격의 주요 목표가 됨

## 역사