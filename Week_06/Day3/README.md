## 1. 가상머신에 `Flask` 프로젝트 배포하기

- [Azure에서 네트워크 보안 그룹이 네트워크 트래픽을 필터링하는 방법](https://learn.microsoft.com/ko-kr/azure/virtual-network/network-security-group-how-it-works)

### 가상머신, 가상 네트워크 만들기

가상 네트워크를 만들어 가상 머신에 연결해주고, 가상 머신의 네트워킹 탭에서 `인바운드 포트 규칙 추가` 에서 **3389, 5000** 포트를 열어줬다.

### 🧐 **네트워크 인터페이스 vs 네트워크 보안 그룹의 서브넷, 뭐가 다른가?**

인바운드 트래픽의 경우 Azure는 서브넷에 연결된 네트워크 보안 그룹이 있으면 이 그룹의 규칙을 먼저 처리한 후 네트워크 인터페이스에 연결된 네트워크 보안 그룹이 있으면 이 그룹의 규칙을 처리한다.

![image](https://user-images.githubusercontent.com/79077316/214495923-7466e6a7-a94c-4d3b-afbf-22219fecf05a.png)

가상머신의 네트워킹 탭을 선택한 화면이다. 위와 같이 인바운드 포트 규칙에서 서브넷에 연결된 네트워크 보안 그룹이 위에 있고, 네트워크 인터페이스에 연결된 네트워크 보안 그룹이 아래에 위치해 있다.

특별한 이유가 없다면 네트워크 보안 그룹을 서브넷 또는 네트워크 인터페이스 중 한 쪽에만 연결하는 것이 좋다. 서브넷에 연결된 네트워크 보안 그룹의 규칙이 네트워크 인터페이스에 연결된 네트워크 보안 그룹의 규칙과 충돌할 수 있으므로 예기치 않은 통신 문제가 발생할 수 있다.

**나는 위 상태에서 네트워크 보안 그룹 myVNet의 서브넷 mySubNet과 가상머신 myVM을 분리시켰다.**

![image](https://user-images.githubusercontent.com/79077316/214495955-5a762a6f-1fd9-4241-8887-742d88d48570.png)

### 로컬에서 가상 환경 만들기

1. 다운로드 폴더에 `helloflask` 폴더를 만들어줬다. 
2. Window Powershell 관리자 권한으로 실행
3. `cd helloflask~경로`  경로 이동
4. Powershell 보안 설정 해제

```powershell
Set-ExecutionPolicy Unrestricted
```

1. 파이썬 가상 환경 만들기

`venv` 는 파이썬 가상환경 라이브러리 및 표준 라이브러리이므로 별도의 설치가 필요 없다. 

```powershell
python -m venv .venv
.venv\scripts\activate
```

![image](https://user-images.githubusercontent.com/79077316/214496025-5c838199-f6dd-4f5b-8aab-8e28db2a82e7.png)

계속 실행이 안되다가 Set~ 명령어 입력해주고 나니깐 잘 실행되었다. 

### 원격 데스크톱에서 파이썬 설치하기

1. 원격 데스크톱에서 파이썬 설치하기
2. 파이썬 환경변수 추가하기
3. cmd에서 `python` 명령어로 확인하기

![image](https://user-images.githubusercontent.com/79077316/214496053-0ee15994-a095-48a2-9d62-7c3044f6648e.png)

### 로컬에서 `Flask` 프로젝트 만들기

1. vs code 터미널에서 다음 명령어 실행

```powershell
python -m pip install --upgrade pip
python -m pip install flask
```
![image](https://user-images.githubusercontent.com/79077316/214496098-5dc7174d-3baf-4468-94db-56e176283d77.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f81e2341-72b5-4d22-ae51-af7bc2b4c5ad/Untitled.png)

2. `app.py` 파일 생성

```powershell
from flask import Flask
app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, Flask!"
```

3. 로컬 호스트 5000번 포트로 플라스크 웹 서버 연결

```powershell
python -m flask run --host=0.0.0.0 --port=5000
```

![image](https://user-images.githubusercontent.com/79077316/214496282-b483dfdc-1b1d-4fae-abf2-5482cbead5eb.png)

4. 플라스크 프로젝트 zip 파일로 압축하고 원격 데스크톱에 붙여넣기한다.

![image](https://user-images.githubusercontent.com/79077316/214496326-d501674d-ac1c-462f-979e-8dab9fa05a93.png)

### 원격 데스크톱에서 `Flask` 실행하기

1. Flask 설치하기

원격 데스크톱 cmd에서 다음 명령어 실행

```powershell
python -m pip install flask
```

2. Flask 웹 서버 접속하기

```powershell
python -m flask run --host=0.0.0.0 --port=5000
```

![image](https://user-images.githubusercontent.com/79077316/214496430-b8438539-cee2-4023-9ab8-fce8261dd3d3.png)

3. 로컬에서 5000번 포트로 연결하기

3389로 원격 데스크톱 연결, 5000번 포트로 로컬-원격데스크톱 연결이 되는지 확인해본다. 

윈도우 방화벽 때문에 로컬에서 접속이 되지 않는다.

4. 원격데스크톱의 윈도우 방화벽에서 인바운드 규칙 추가

포트 5000번 추가해준다.

![image](https://user-images.githubusercontent.com/79077316/214496503-69fe6333-8c4b-4208-9b3e-42406a913650.png)

인바운드 규칙 이름은 flask로 하여 5000번 포트를 열어줬다.

![image](https://user-images.githubusercontent.com/79077316/214496560-e5b5d12b-92d3-4c0e-b9ec-c196bc21e801.png)

5. 로컬에서 5000번 포트로 연결이 되었다!
![image](https://user-images.githubusercontent.com/79077316/214496600-7417a668-9bcf-4ee3-8071-307187c283f0.png)

## 2. 인터넷: 서버와 클라이언트

- [생활코딩 인터넷을 여는 열쇠: 서버와 클라이언트](https://opentutorials.org/course/3084/18890)

인터넷이 동작하기 위해서는 컴퓨터가 최소 2대 이상 필요하다. 컴퓨터 2대가 있을 때 하나는 웹브라우저, 웹서버라고 한다. 웹브라우저와 웹서버는 서로 정보를 주고 받는다. 

웹브라우저는 웹서버한테 정보를 요청(request)하고, 웹서버는 웹브라우저의 요청에 응답(response)한다. 이처럼 정보를 요청하는 컴퓨터를 클라이언트, 응답하는 컴퓨터를 서버라고 부른다. 

## 3. PaaS `Azure Bastion` 이용해서 Load Balancer 만들기

- [Azure Portal을 사용하여 VM 부하를 분산하는 공용 부하 분산 장치 만들기](https://learn.microsoft.com/ko-kr/azure/load-balancer/quickstart-load-balancer-standard-public-portal)
- [Azure Bastion이란](https://learn.microsoft.com/ko-kr/azure/bastion/bastion-overview)
