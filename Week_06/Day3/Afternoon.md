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


## NAT

---


