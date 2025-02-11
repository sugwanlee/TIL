# 250210 학습반 숙제(퍼셉트론, 경사하강법)

## 단층 퍼셉트론 이란?

입력이 여러개로 주어지면 각 입력에 가중치를 부여해서 하나의 출력을 생성하는 모델

아래 그림이 단층 퍼셉트론입니다.

![Image](https://github.com/user-attachments/assets/41b3c327-24f4-4e29-b2f7-5973a90074f7)

위 그림을 등식으로 표현하면

$$
y = x_1 w_1 + x_2 w_2 + x_3 w_3 + x_4 w_4 + b
$$

위 수식을 행렬곱셈으로 표현하면


$$
\begin{bmatrix} x_1 & x_2 & x_3 & x_4 \end{bmatrix}
\begin{bmatrix} w_1 \\ w_2 \\ w_3 \\ w_4 \end{bmatrix} + b
= x_1 w_1 + x_2 w_2 + x_3 w_3 + x_4 w_4 + b
$$


위 모델로 인해 AND연산 OR연산 NAND연산을 선형 분리 할 수 있었습니다.

![Image](https://github.com/user-attachments/assets/ff3dfd41-9256-4eac-9108-bb6c437cb324)

위 모델의 한계는

![Image](https://github.com/user-attachments/assets/d88e2c9f-536a-4ec9-89a2-61eee23d4cf5)

위 xor연산 경우는 선형분리로 표현할 수 없었습니다.

대신, XOR연산은 AND, OR, NAND 연산을 조합하여 표현 할 수 있습니다.

![Image](https://github.com/user-attachments/assets/9ab2f77c-def5-457f-a179-690f092f1688)

위 개념을 구현하기 위해 다층 퍼셉트론이 고안되었고

각 노드간의 간선에는 다른 가중치를 적용하고 활성함수를 적용해서 구현했습니다.

- 행렬곱

$$
\begin{bmatrix} x_1 & x_2 \end{bmatrix}
\begin{bmatrix} 
w_{11} & w_{12} \\ 
w_{21} & w_{22} 
\end{bmatrix}
=\begin{bmatrix} 
x_1 w_{11} + x_2 w_{21} & x_1 w_{12} + x_2 w_{22} 
\end{bmatrix}
$$

아마? 위 개념을 행렬곱으로 표현하고 각 요소값에 활성함수를 적용하면 같을 겁니다.

## 선형회귀 모델

선형회귀는 실제값(답지)이 주어지고 입력값이 주어졌을 때 예측값을 도출(순전파) 실제값을 이용해

오차값을 구하고 가중치와 편향치를 업데이트(역전파) 합니다.

여기서 가중치를 변화하는 방법은 경사 하강법으로 이루어집니다.

- 순전파(예측+활성함수)

$$
\hat{y}=X⋅W+b
$$

$$
a = f(\hat{y})
$$

여기서 y hat은 예측값, X는 입력, W가중치 ,b는 편향치, f()는 활성함수입니다

- 역전파

주어진 답을 y값과 y hat값을 비교하여 w와 b값을 최신화 하여 오차를 최소화 하는 것

경사하강법을 사용

### 경사 하강법

경사 하강법은가중치와 편향치를 조정해  실제값과 예측값의 오차(손실함수) 최소화 하는 방법입니다.

![Image](https://github.com/user-attachments/assets/4566b672-b469-4a5f-a884-e520e480ccf4)


위 함수가 손실 함수라고 가정한다면 기울기가 음수일 때 양의 방향으로 가중치와 편향치를 조정하고

기울기가 양수일 때 음의 방향으로 가중치와 편향치를 조정하게 됩니다.

따라서 손실함수의 기울기의 부호에 반대방향으로 진행하게 됩니다.

## 손실 함수를 최소화 하는 방법

우선 손실함수를 구함

예를 들어 MSE를 그래프로 나타내면 아래와 같다

![Image](https://github.com/user-attachments/assets/1ee81f9f-f8ae-4a1e-af06-0c5f9aae431f)

여기서 위 그래프에서 y값이 최솟값인 점을 찾는게 손실함수의 최솟값을 찾는 과정이고

가로축은 가중치(W)입니다 따라서 y값(손실함수의 결괏값)이 최소가 되는 w값과 b값(y절편)을 찾는 겁니다.

따라서 이를 수식으로 표현하면 아래와 같고

- 최적의 w값을 찾는 수식

$$
w_{n+1} = w_n - \text{Gradient}(w)
$$

$$
w_{n+1} = w_n - \alpha \nabla L(w)
$$

위 수식에서 알파값을 적절히 설정 했다면 
위 수식을 반복했을 때
y(손실함수의 값)가 최솟값(local minimum)이 되는 w값을 찾을 수 있습니다

최적의 b값을 찾는 방법도 b에 대해 미분하고 학습률을 곱한값을 빼고 그 수식을 반복하면

최적의 b값을 찾을 수 있습니다.

위 방식의 약점…..

- 아래 상황처럼 처음 손실함수를 구한 지점이 local minimum(베타)에 가까우면
    
    global minimum(알파)를 구할 수 없음
    
    ![Image](https://github.com/user-attachments/assets/ec95c1d3-3357-410e-a184-31687d9736ac)
    
- 학습률을 너무 크게 설정하면 특정 값에 수렴하지 않고 발산하게 됨
- 너무 작으면 학습시간이 너무 오래걸리거나, 최적의 값에 거의 이동하지 않을 수 있음

![Image](https://github.com/user-attachments/assets/21a9f6e8-21c3-4c55-b454-3b4df5f9f070)