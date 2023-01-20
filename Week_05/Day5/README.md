# 가상 네트워크 (virtual network)
## Vnet
### 생성 방법
1. 가상 네트워크를 생성하면 주소 공간이 할당
2. 주소 공간을 다시 나누는 서브넷 생성 가능

|![](https://user-images.githubusercontent.com/28096454/213591077-03bdacee-4ce1-48d9-acf1-1838cb8ca408.png)|
|:---:|
|*Vnet 생성화면*|

3. VM에 Vnet 할당 가능

|![](https://user-images.githubusercontent.com/28096454/213597879-6f7e274d-ddd2-4dee-be7a-5a6b866fa167.png)|
|:---:|
|*Vnet 구성도*|

### ping 명령어 제한 해제
~~~
New-NetFirewallRule –DisplayName "Allow ICMPv4-In" –Protocol ICMPv4
~~~

### 사설 IP 주소 (RFC 1918)

|네트워크 주소|IP 범위|
|:---:|:---:|
|10.0.0.0/8|10.0.0.0 ~ 10.255.255.255|
|172.16.0.0/12|172.16.0.0 ~ 172.31.255.255|
|192.168.0.0/16|192.168.0.0 ~ 192.168.255.255|

## VPC 피어링
서로 다른 Vnet끼리 연결하는 것

# 보안 그룹

## 인바운드 & 아웃바운드
인바운드(inbound)와 아웃바운드(outbound)
인바운드와 아웃바운드는 트래픽에 네트워크 간에 이동하는 방향을 말한다.

인바운드
- 인바운드 트래픽은 네트워크에 들어오는 정보
- 메시지가 클라이언트에서 서버로 향하는 것
ex) 첨부파일을 서버에 저장할 때(업로드)

아웃바운드
- 아웃바운드 트래픽은 네트워크에서 나가는 정보
- 클라이언트의 요청을 처리하고 메시지가 서버에서 클라이언트로 다시 향하는 것
ex) 첨부파일을 다운로드 할 때

|![](https://user-images.githubusercontent.com/28096454/213602687-1450e047-0785-41f1-ae7c-e2c25f6cae8d.png)|
|:---:|
|*인바운드와 아웃바운드*|



|![](https://user-images.githubusercontent.com/28096454/213606727-fe3f2948-0d5a-4bb3-a807-186a241ed079.png)|
|:---:|
|*VPC 실습 구성도*|
