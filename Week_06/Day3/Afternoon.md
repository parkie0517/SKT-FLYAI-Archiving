# Azure로 VM을 Load Balancing하기

---

1. Virtual Network 만들기

    1. rg53-after-exec-virtual-network 이름으로
    2. IPv4 → 10.1.0.0/16
    3. Subnet → 10.1.0.0/24
    4. bastion 새로 생성 → rg53-bastion-pengpark
        - 10.1.1.0/26
    5. 공용 IP 생성 → rg53-pengpark-public-ip

3. 부하 분산 장치 만들기
    1. 형식 공개 설정
    2. 프론트엔드 IP 추가
        - 공용 IP 추가 -> rg53-frontend-ip
    3. 백엔드 풀 추가 -> rg53-backend-pool
    4. 인바운드
        - 부하분산 규칙 추가
            1. 상태프로브 추가
            2. 유휴 제한시간 15분
            3. 기본 아웃바운드 엑세스 선택 **
            <br>
            
            | 부하 규칙 생성 1 | 부하 규칙 생성 2 |
            |:-----:|:-----:|
            |![Image](https://user-images.githubusercontent.com/4527194/214748119-e353bbd3-51e7-41c9-9722-c4fae56d2012.png)|![image](https://user-images.githubusercontent.com/4527194/214751099-44652d59-15d5-4640-a7a7-5f9a22aca53b.png)|


4. 가상머신 생성

| VM2 리소스 생성 | VM2 네트워킹 생성 |
|----------|-----------|
|![image](https://user-images.githubusercontent.com/4527194/214747302-e6feea71-3005-4dcf-ad29-8f3bb652c45d.png)|![image](https://user-images.githubusercontent.com/4527194/214747337-c9ccb8ac-5e37-4eb3-9da8-be11864dc87c.png)|



6. Bastion 생성


| 베스천으로 VM1에 접속하기 | 베스천으로 VM2에 접속하기 |
|---------------------|----------------------|
|![access_through_bastion_to_vm1](https://user-images.githubusercontent.com/4527194/214747600-c60d0220-26d0-4fb5-9439-b8bb226ff7f0.png) | ![access_through_bastion_to_vm2](https://user-images.githubusercontent.com/4527194/214747660-bf4b9038-8cc1-4db0-9f5b-d6e5cc7f3844.png) |



Bastion 접속 중인 세션 확인 해보기

 ![Bastion 접속 세션](https://user-images.githubusercontent.com/4527194/214747251-980da3ef-3067-41ae-8fad-e2af3f4d24db.png)




```shell
# Install IIS server role
 Install-WindowsFeature -name Web-Server -IncludeManagementTools

 # Remove default htm file
 Remove-Item  C:\inetpub\wwwroot\iisstart.htm

 # Add a new htm file that displays server name
 Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
```

Public IP로 접속해보기

| 웹에서 접속 | 모바일에서 접속 |
|-----|-----|
|![access_vm_1](https://user-images.githubusercontent.com/4527194/214747020-fb9eccf6-7676-414a-91b6-b0a7739fedae.png)|![access_vm_2](https://user-images.githubusercontent.com/4527194/214747050-3a37d1e7-2431-4321-a6c8-fda10d51265d.png)|



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


