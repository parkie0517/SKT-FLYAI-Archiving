## Hyper-V로 우분투 가상 머신 만들기

- `Hyper-V 관리자`에서 `Ubuntu 20.04 LTS` 가상 컴퓨터 설치하기
- 로그인하고 가상 컴퓨터에 접속하면 다음과 같은 화면이 나옴

![image](https://user-images.githubusercontent.com/79077316/216868235-697a4d67-763e-41cc-ba21-3d2eaeaf3b5c.png)

## 가상 머신에 도커 세팅하기

### 1) **도커 vs 가상머신**

![image](https://user-images.githubusercontent.com/79077316/216868309-8b85b47e-cb83-47d6-95fd-9670a9e24141.png)

- 도커와 가상 머신의 가장 큰 차이는 게스트 OS의 유무
- VM에는 Guest OS가 설치되는 반면 도커의 컨테이너에는 Guest OS를 설치하지 않음 → 자원의 효율성에서 차이가 생김
- VM은 하나씩 늘어날 때마다 OS를 위한 자원을 할당해주어야 하는 반면 도커는 어플리케이션을 구동하는데 필요한 패키지만 있으면 컨테이너를 구동시킬 수 있음

### 2) [비교 실습] ****[Azure Portal에서 Virtual Machine Scale Set 만들기](https://learn.microsoft.com/ko-kr/azure/virtual-machine-scale-sets/quick-create-portal)****

- Azure Portal에서 Load Balancer 만들기
- Virtual Machine Scale Set 만들기

![image](https://user-images.githubusercontent.com/79077316/216868353-ef122afb-aae0-48fd-82e2-d10f7346a35b.png)

![image](https://user-images.githubusercontent.com/79077316/216868374-e2d4d5ad-651c-4383-82a2-f850fb74c378.png)

### 3) `Hyper-V` 우분투 가상 컴퓨터 실습

- 우분투 터미널에서 다음 코드 실행

```powershell
sudo passwd # 새로운 비밀번호 설정 !Seoul2023
sudo apt-get update # 패키지 업데이트
sudo apt-get install vim
```

![image](https://user-images.githubusercontent.com/79077316/216868393-f01aa8f1-bc9c-43e9-a071-4979a41297c3.png)

- [우분투 고급 세션 모드 설정하기](https://lucidmaj7.tistory.com/343)
    - 윈도우 Hyper-V로 우분투에 접속하면 마우스랑 키보드 입력이 느려지는 문제를 해결하기 위해 `고급 세션 모드(enhanced session mode)`가 추가됨
    - 고급 세션 모드는 내부적으로 RDP를 이용해서 VM에 접속하는 방식
