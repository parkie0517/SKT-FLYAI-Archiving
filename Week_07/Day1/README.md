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

![Untitled](%E1%84%8E%E1%85%A2%E1%86%BA%E1%84%87%E1%85%A9%E1%86%BA%20672ee8d635e2461ba6c853f1aa21052e/Untitled.png)

#### 2. docker 우분투 찾기

![Untitled](%E1%84%8E%E1%85%A2%E1%86%BA%E1%84%87%E1%85%A9%E1%86%BA%20672ee8d635e2461ba6c853f1aa21052e/Untitled%201.png)

#### 3. docker 우분투 내려받기
    
    docker pull mysql 로 하지 말고
    
    docker pull mysql:8.0.22로 버전을 지정해줘야 한다.
    

![Untitled](%E1%84%8E%E1%85%A2%E1%86%BA%E1%84%87%E1%85%A9%E1%86%BA%20672ee8d635e2461ba6c853f1aa21052e/Untitled%202.png)

#### 4. docker 이미지를 Container 파일로 생성한다.
    
    docker create -it --name ubuntu_server ubuntu:20.04
    

![Untitled](%E1%84%8E%E1%85%A2%E1%86%BA%E1%84%87%E1%85%A9%E1%86%BA%20672ee8d635e2461ba6c853f1aa21052e/Untitled%203.png)

1. docker에서 start 버튼으로 서버 실행
2. docker 우분투 서버 접속
    
    docker attach ubuntu_server
    

![Untitled](%E1%84%8E%E1%85%A2%E1%86%BA%E1%84%87%E1%85%A9%E1%86%BA%20672ee8d635e2461ba6c853f1aa21052e/Untitled%204.png)

cd / : 루트로 이동

ll : 파일 리스트

1. docker 우분투 업그레이드

![Untitled](%E1%84%8E%E1%85%A2%E1%86%BA%E1%84%87%E1%85%A9%E1%86%BA%20672ee8d635e2461ba6c853f1aa21052e/Untitled%205.png)

### 에러 고치는법

먼저 apt-get install vim 또는 apt-get install nano를 통해 진행한다.

[[Linux] 리눅스 텍스트 에디터 vi와 vim, nano, gedit 차이 설명](https://blog.naver.com/PostView.naver?blogId=ycpiglet&logNo=222367301056)

[sudo apt-get upgrade 다운로드 서버 변경](https://wooriel.tistory.com/3)

vim을 통해서 외국 주소를 한국 주소로 바꿔주면 에러가 해결된다.

### 다음
