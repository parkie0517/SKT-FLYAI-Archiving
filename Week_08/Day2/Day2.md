| 컨테이너 | 가상머신 |
| --- | --- |
| 프로세스 가상화 | OS 가상화 |

## python 경로 확인

```bash
which python3.9
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.9 3
sudo update-alternatives --config python
```

## minikube 설치

```bash
curl -LO https://storage.googleapis.com/minikube/releases/v1.22.0/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube --help #설치확인
```

## kubectl 설치

- kubectl : 쿠버네티스 API 호출을 위한 `command-line tool`

```bash
curl -LO https://dl.k8s.io/release/v1.22.1/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl --help
```

## 드라이버를 docker 로 설정

```bash
minikube start --driver=docker
minikube status #확인
```

- 오류 : Docker is nearly out of disk space, …
    
    ![image](https://user-images.githubusercontent.com/67251510/217166326-a5931672-0e36-4cc2-8201-09c44e270929.png)
    
    ```bash
    kubectl get pod -n kube-system
    
    minikube delete
    minikube start --driver=docker
    ```
    

## POD

- POD : 쿠버네티스에서 `가장 작은` 단위
- `1개 이상의 컨테이너가 캡슐화` 되어 클러스터 안에서 배포
    - 대부분 하나의 POD는 하나의 컨테이너가 구성되어 있음 (→ 한 Pod를 컨테이너로 생각해도 됨)
- 외부에서 연결하기 위해 포트포워딩이 필요함.

```bash
kubectl run nginx --image nginx --port=8080
kubectl get pod # nginx running 을 확인 가능
docker images
docker ps -a # gcr.io/k8s-minikube/... 확인
```

### 포트포워딩 (추후 다시 진행)

```bash
kubectl port-forward nginx 18080:8080
```

## YAML

[Transform YAML into JSON - Online YAML Tools](https://onlineyamltools.com/convert-yaml-to-json)

- `---` : 구분선. 여러개의 Yaml document 작성 가능.

```bash
$ vi pod.yaml
```

```yaml
apiVersion: v1 # kubernetes resource 의 API Version
kind: Pod # kubernetes resource name
metadata: # 메타데이터 : name, namespace, labels, annotations 등을 포함
  name: counter
spec: # 메인 파트 : resource 의 desired state 를 명시
  containers:
  - name: count # container 의 이름
    image: busybox # container 의 image
    args: [/bin/sh, -c, 'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done'] # 해당 image 의 entrypoint 의 args 로 입력하고 싶은 부분
```

```bash
$ kubectl apply -f pod.yaml
$ kubectl get pod
$ kubectl describe pod counter
```

### 로그 확인

```bash
kubectl logs <pod-name> {-f} # -f 옵션 : 로그를 계속 보여줌.
kubectl logs <pod-name> -c <container-name> {-f}
```

### 용량 늘리기
- [참고 링크1](https://www.nucleiotechnologies.com/increasing-disk-space-on-file-system-root-ubuntu-20-04)
- [참고 링크2](https://hiseon.me/linux/ubuntu/modify-partition-size)
- Hyper-V로 디스크 용량 늘려주고 
-`sudo apt-get update && sudo apt-get install gparted` 설치 후 파티션 조정

### Deployment 실습
https://visionhong.tistory.com/41


```
apiVersion: apps/v1 # kubernetes resource 의 API Version
kind: Deployment # kubernetes resource name
metadata: # 메타데이터 : name, namespace, labels, annotations 등을 포함
  name: nginx-deployment
  labels:
    app: nginx
spec: # 메인 파트 : resource 의 desired state 를 명시
  replicas: 3 # 동일한 template 의 pod 을 3 개 복제본으로 생성
  selector:
    matchLabels:
      app: nginx
  template: # Pod 의 template
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx # container 의 이름
        image: nginx:1.14.2 # container 의 image
        ports:
        - containerPort: 80 # container 의 내부 Port
```
pod는 `외부 노출 x`
- kubectl get pod -o wide 더 많은 내용 출력
- minikube ssh 쿠버네틱스 내부로 들어가기
- curl -X GET 172.17.0.4 -vvv
