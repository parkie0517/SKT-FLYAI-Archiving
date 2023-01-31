## 챗봇

자연어처리를 통해 구현된다.

챗봇 : 대화형식

질문 > 답변이 반복되는 방식이다.

이러한 챗봇은 의도 파악 후 답변을 잘 하는지가 중요하다.

## Chat GPT

[OpenAI](https://openai.com/)

## KoGPT2 활용해서 간단한 챗봇 만들기

[KoGPT2_챗봇_ipynb의_사본.ipynb](%E1%84%8E%E1%85%A2%E1%86%BA%E1%84%87%E1%85%A9%E1%86%BA%20672ee8d635e2461ba6c853f1aa21052e/KoGPT2_%25EC%25B1%2597%25EB%25B4%2587_ipynb%25EC%259D%2598_%25EC%2582%25AC%25EB%25B3%25B8.ipynb)

## 나만의 데이터셋으로 KoGPT2 활용해서 챗봇 만들기

## Docker에 구동하기 환경설정
### Windows 10 환경에서 Docker에 Ubuntu 설치

[[Docker] Windows10 환경에서 Docker에 Ubuntu 설치](https://hermeslog.tistory.com/498)

#### 1. 버전 확인
```bash
docker version
```
![image](https://user-images.githubusercontent.com/90374185/215736106-e9d5c4f5-e0be-4460-82b2-8d7af881134f.png)


#### 2. docker 우분투 찾기

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e3a5ee84-fbbc-4067-a828-942756eff979/Untitled.png)

#### 3. docker 우분투 내려받기
    
```bash
docker pull mysql 로 하지 말고
docker pull mysql:8.0.22로 버전을 지정해줘야 한다.
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/08536c1b-d4cb-44c5-afaf-d0ba31d7769e/Untitled.png)

#### 4. docker 이미지를 Container 파일로 생성한다.
```bash
docker create -it --name ubuntu_server ubuntu:20.04
```
![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0acc7834-4730-4fdb-af46-186076fd8617/Untitled.png)

#### 5. docker에서 start 버튼으로 서버 실행
#### 6. docker 우분투 서버 접속
```bash
docker attach ubuntu_server
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de1fa53d-c83f-4153-b674-f6058dd9b6d6/Untitled.png)

cd / : 루트로 이동

ll : 파일 리스트

#### 7. docker 우분투 업그레이드
```bash
apt-get update
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5f63d149-0380-4739-957b-2670eac0aa69/Untitled.png)

### 우분투 업그레이드시 에러 고치는법
```bash
Some index files failed to download. They have been ignored, or old ones used instead.
```
업그레이드 시 해당 에러가 발생한다면

먼저 apt-get install vim 또는 apt-get install nano를 통해 진행한다.

[[Linux] 리눅스 텍스트 에디터 vi와 vim, nano, gedit 차이 설명](https://blog.naver.com/PostView.naver?blogId=ycpiglet&logNo=222367301056)

[sudo apt-get upgrade 다운로드 서버 변경](https://wooriel.tistory.com/3)

vim을 통해서 외국 주소를 한국 주소로 바꿔주면 에러가 해결된다.

