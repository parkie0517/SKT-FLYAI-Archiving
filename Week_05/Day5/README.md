# 가상 네트워크 (virtual network)
## Vnet
### 생성 방법
1. 가상 네트워크를 생성하면 주소 공간이 할당
2. 주소 공간을 다시 나누는 서브넷 생성 가능
<!-- <img width="842" alt="image" src="https://user-images.githubusercontent.com/28096454/213591077-03bdacee-4ce1-48d9-acf1-1838cb8ca408.png"> -->
![Vnet 생성화면](https://user-images.githubusercontent.com/28096454/213591077-03bdacee-4ce1-48d9-acf1-1838cb8ca408.png)
<!-- <figcaption style="center">Vnet 생성 화면</figcaption>    -->

3. VM에 Vnet 할당 가능

<img width="907" alt="image" src="https://user-images.githubusercontent.com/28096454/213597879-6f7e274d-ddd2-4dee-be7a-5a6b866fa167.png">
<figcaption style="center">Vnet 구성도</figcaption>   

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

## Subnet
