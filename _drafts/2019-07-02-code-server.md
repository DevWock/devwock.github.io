# Code Server 설치하기

## 1. 서론

[Code Server](https://github.com/cdr/code-server)는 Visual Studio Code를 웹으로 돌릴 수 있게 해주는 오픈소스 프로젝트이다.

다만 몇가지 제약이 있는데.

- iOS 사파리에서 한글 입력 버그
- iOS에서 단축키 제약으로 단축키를 제대로 쓸 수 없음
- 파일 조회 권한이 code-server를 실행한 계정에 종속됨
- MS 공식 익스텐션등은 마켓에서 검색이 안되고 직접 설치해야함
- 잔버그가 많음 (폴더 로드 한 후 브라우저 껐다 켜면 로딩때문에 쓸수가 없다던가)

실제로 셋팅해봤는데 생각보다 버그가 좀 있어서 실사용은 힘들지 싶었다.
Visual Studio Online이 나왔지만, 유료 서비스이고 VSCode랑은 조금 개념이 다르기 때문에 웹에서 VSCode를 쓰고싶다면 어쩔 수 없는 선택.

설치 환경은 우분투 16.04이며 CentOS나 맥의 경우 상이할 수 있다.

## 2. 설치방법

### 다운로드

현재 글 쓴 시점 이후 버전업 되었을 수 있으니 [깃허브 페이지](https://github.com/cdr/code-server)에서 최신 버전을 확인하자.

```bash
wget https://github.com/cdr/code-server/releases/download/1.1156-vsc1.33.1/code-server1.1156-vsc1.33.1-linux-x64.tar.gz
mkdir vscode
tar xzf code-server1.1156-vsc1.33.1-linux-x64.tar.gz
mv ./code-server1.1156-vsc1.33.1-linux-x64/* ./vscode/
rm -rf./code-server1.1156-vsc1.33.1-linux-x64
cd vscode
mkdir workspace
```

TODO: Docker 설치 추가

이 중 workspace는 익스텐션부터 이거저거 설정파일이 들어갈 폴더이다. 다른 곳에 만들어줘도 무방하다.

### 서비스 등록

시스템 시작시 서비스로 등록하여 쉘이 꺼져도 항상 동작하게 만든다.

#### 서비스 생성

```bash
sudo vi /etc/systemd/system/code.service
```

#### /etc/systemd/system/code.service 내용

``` bash
[Unit]
Description=Visual Studio Code on the server
After=network.target
[Service]
ExecStart=<vscode 경로>/code-server -H -d <workspace경로>
User=<서비스 실행할 사용자 권한>
Restart=always
RestartSec=1
Environment=PASSWORD=<접속할 때 쓸 비밀번호>
[Install]
WantedBy=multi-user.target
```

서비스를 생성했으면 다음 명령어로 시작 서비스로 등록한 후 서비스를 시작해준다.

``` bash
systemctl daemon-reload
systemctl start code
systemctl enable code
journalctl -u code
```

웹으로 실행한 VSCode는 서비스 실행한 권한을 따라가므로 비밀번호 탈취에 주의한다.
