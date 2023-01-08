# CNN (합성곱 신경망)

---
음성 인식이나 이미지 인식에서 주로 사용되는 신경망의 한 종류

합성곱이라는 수학적 연산을 통해 이미지의 특성을 추출, 이미지 처리에 탁월한 성능을 보임


## 합성곱 연산

![Calculation of Convolution](https://www.researchgate.net/publication/339578955/figure/fig4/AS:863732028669952@1582941171319/Calculation-process-of-a-filter-in-the-convolutional-layer-The-first-matrix-is-the.ppm)

### 합성곱 연산 요소

- 필터 개수
  - N개의 특징을 갖는 필터를 만들어낸다.
- 커널 크기
  - 레이어 출력의 크기와 관련되어 있음 
  - 필터개수 만큼
- Padding & Stride
  - 합성곱 연산은 원래 이미지의 크기보다 감소되어 출력되는 특징이 있다.
  - 가로, 세로 Padding만큼 추가하여 연산 결과를 입력과 출력 동일한 형태로 결과를 뽑을 수 있다.
  - 

## 합성곱 신경망 구조
### Activation Function
  - ReLU
### Pooling
  - MaxPooling
  - GlobalAveragePooling

## 이미지 분류
이미지 분류를 위한 딥러닝 모델 구축 과정은 대개 다음과 같다.

1. 데이터 준비 및 확인
   - 내가 학습할 이미지 데이터는 어떤 것인지
   
2. 검증 데이터 분리
3. 데이터 전처리
- 이미지 정규화
  - 픽셀 0 ~ 255를 0 ~ 1로 변환 과정
  - 혹은 영상처리 라이브러리 (OpenCV)를 사용하여 이미지 자체에 대한 처리
  - 레이블을 변경 
    - 클래스 분류라면 OneHot encoding으로 라벨을 변경한다거나..
  - 이미지 데이터 numpy화

4. 모델 선언 및 학습
   - 여러개의 합성곱 연산으로 이루어진 유닛을 연결한다거나
   - 누군가 만들어 둔 모델 구조를 착안한다거나 (Resnet, MobileNet...)
   
5. 학습 결과 시각화 그리고 추론 결과 확인하기
   - 학습의 과정에서 정의한 Loss가 수렴하는지?
   - 정확도가 수렴하는지?


Grayscale 이미지 분류 -> $(H, W, 1)$

`Fashion-MNIST` $(28, 28, 1)$

Color 이미지 분류     -> $(H, W, 3)$

`CIFAR-10` $(32, 32, 3)$


원핫벡터 분류 일 때는 `CategoricalCrossEntropy` 

정수형 분류 일 때는 `SparseCategoricalCrossEntropy` 

## 과적합 방지를 위한 기법들
1. Dropout
3. Batch Normalization
4. 훈련데이터 증가
5. 가중치 규제 (L1, L2) 추가
6. 네트워크 구조 변경
