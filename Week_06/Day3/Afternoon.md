# Azure로 VM을 Load Balancing하기

---

1. Virtual Network 만들기
2. 부하 분산 장치 만들기
3. 가상머신 생성
4. Bastion 생성

```shell
# Install IIS server role
 Install-WindowsFeature -name Web-Server -IncludeManagementTools

 # Remove default htm file
 Remove-Item  C:\inetpub\wwwroot\iisstart.htm

 # Add a new htm file that displays server name
 Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
```

Public IP로 접속해보기

로드밸런서 설정에서 2개가 설정되어 있는 것을 확인 할 수 있다.
![load_balancer_state](https://user-images.githubusercontent.com/4527194/214746238-5a8ab937-6c15-439b-a7ed-346030b1a960.png)

시스템 구성도
![structure](https://user-images.githubusercontent.com/4527194/214746442-537ce313-c6c8-4d28-b90d-671394590830.png)


## NAT

---

IP 패킷의 포트와 Source, Destination의 IP 주소등을 재기록하여 라우터를 통해 네트워크 트래픽을 주고 받는 기술

내부에서 연결하는 IP, 외부에서 연결하는 IP

내부로 연결 할 때는 내부 IP에서 하고 외부로 연결 할 때는 외부 IP로 전달

사설 네트워크에 속한 여러 개의 호스트가 하나의 공인 IP 주소를 사용하여 인터넷에 접속하기 위함


## OSI 7-layer

---


