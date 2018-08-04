# CS231n - lecture 6. 2017

## Overview
1. One time setup
activation functions, preprocessing, weight
initialization, regularization, gradient checking
2. Training dynamics
babysitting the learning process,
parameter updates, hyperparameter optimization
3. Evaluation
model ensembles

## Part 1
- Activation Functions
- Data Preprocessing
- Weight Initialization
- Batch Normalization
- Babysitting the Learning Process
- Hyperparameter Optimization

---
---

# Overview
---
1. One time setup
---
## gradient vanishing (기울기 손실)
- 활성화 함수를 설정 할 때, 잘못된 표준편차(e.g. 1)를 사용하여 각 층의 활성화값 분포를 구했을 때,분포가 특정 값(0,1)에 치우쳐 나타나는 현상
- 역전파의 기울기 값이 점점 작아지다가 사라지게 되는 현상
- 층을 깊게 하는 딥러닝에서 심각한 문제가 될 수 있다

2. Training dynamics
- babysitting the learning process
- parameter updates
- hyperparameter optimization

3. Evaluation
- model ensembles

---
# Part1
---
# Activation functions (활성화 함수)
- 입력 신호의 총합을 출력 신호로 변환하는 함수
- 입력신호의 총합이 활성화를 일으키는지를 정하는 역할
- 임계값을 경계로 출력이 바뀜
	- 이런 성질을 가진 함수를 '계단 함수(step function)'이라 한다
	- 즉, 퍼셉트론에서는 활성화 함수로 계단 함수를 이용한다
		- 활성화 함수로 쓸 수 있는 여러 후보 중에서 퍼셉트론은 계단함수를 사용함

## 비선형 함수
- 직선 1개로는 그릴 수 없는 함수
	- 시그모이드 함수(곡선), 계단함수(계단과 같은 형태로 구부러진 직선)

### 선형함수
- 함수에 어떤값을 입력했을 때 출력이 입력의 상수배 만큼 변하는 함수
- 곧은 1개의 직선으로 표현되는 함수
- 주의점
	- 선형함수를 이용하면 신경망의 층을 깊게하는 의미가 없어진다
	- 신경망에서 사용하면 안되는 형태
- 주의하는 이유
	- 층을 아무리 깊게 해도 '은닉층이 없는 네트워크'로도 똑같은 기능을 할 수 있기 때문

## 종류
### 시그모이드 함수
```math
h(x) = 1 / ( 1 + exp(-x) )
```
- 입력이 중요하면 큰값을 출력하고, 입력이 중요하지 않으면 작은값을 출력한다
	- 입력이 작을 때의 출력은 0에 가깝고, 입력이 커지면 출력이 1에 가까워지는 구조이므로
- 입력이 아무리 작거나 커도 출력은 0에서 1 사이이다

### ReLU 함수
```math
h(x) = x (x>0) && 0 (x<= 0)
```
- 0을 넘으면 그 입력을 그대로 출력하고, 0 이하이면 0을 출력하는 함수

### Leaky ReLU / Maxout / ELU 확인 필요

# Data Preprocessing
# Weight Initialization (가중치 초기화)
- 가중치의 초깃값을 무엇으로 설정하느냐가 신경망 학습에 영향이 높다
- 주의점
	- 가중치를 균일한 값으로 설정하면 안된다
		- 오차역전파법에서 모든 가중치의 값이 똑같이 생신되게 된다
	- '가중치가 고르게 되어버리는 상황'을 막아야한다

## 가중치 감소 기법
- 오버피팅을 억제해 범용 성능을 높이는 테크닉
- 가중치 매개변수의 값이 작아지도록 학습하는 방법
- 가중치 값을 작게 하여 오버피팅이 일어나지 않게 하는 것
- 학습 과정에서 큰 가중치에 대해서는 그에 상응하는 큰 페널티를 부과하여 오버피팅을 헉제하는 방법

### 오버피팅
- 신경망이 훈련 데이터에서만 지나치게 적응되어 그 외의 데이터에는 제대로 대응하지 못하는 상태
	- 훈련 데이터에는 포함되지 않는, 아직 보지 못한 데이터가 주어져도 바르게 식별해내는 모델이 바람직하다

#### 오버피팅이 일어나는 경우
- 매개변수가 많고 표현력이 높은 모델
- 훈련 데이터가 적음


# Batch Normalization
- 레이어를 기준으로 입력 데이터를 정규화하는 것

# Babysitting the Learning Process

# Hyperparameter Optimization (매개변수 최적화)
- 신경망 학습의 목적은 손실 함수의 값ㅇ르 가능한 한 낮추는 매개변수를 찾는 것
	- optimization : 매개변수 최적값을 찾는 문제
- SGD(확률적 경사 하강법)
	- 매개변수 값을 찾는 단서로 미분(매개변수의 기울기)을 이용하는 방법
	- 매개변수의 기울기를 수해, 기울어진 방향으로 매개변수 값ㅇ르 갱신하는 일을 몇 번이고 반복해서 점점 최적의 값에 다가가는 방법

## SGD
- 장점
	- 단순하고 구현이 쉽다
- 단점
	- 비등방성 함수에서는 탐색 경로가 비효율적이다.
		- 방향에 따라 성질이 달라지는 함수
		- e.g. 공책을 구부린 모양일 경우 탐색을 돌아돌아 해서 가게된다

### Momenteum
- 갱신 경로는 공이 그릇 바닥을 구르듯 움직인다.
	- SGD와 비교할 때, 지그재그 정도가 덜하다.
		- x축의 힘은 아주 작지만, 방향을 변하지 않아서 한 방향으로 일정하게 가속하기 때문
		- y축의 힘은 크지만 위아래로 번갈아 받아서 상충하여 y축 방향의 속도는 안정적이지 않음
- 물리에서 기울기 방향으로 힘을 받아 물체가 가속되어 속도가 올라가는 것을 모방
	- 물체가 하무언 힘을 받지 않을 때 서서히 하강시키는 역할을 한다

### AdaGrad
### Adam

---
용어
---
# 에폭
- 전체 데이터를 한번 다 돌려서, 전체 데이터에 대해서 가중치 업데이트 작업을 모두 완료한 횟수
# 배치
- 전체 데이터의 가중치를 업데이트하는 단위

---
## 참고링크
- [batch normalization](https://jsideas.net/python/2018/01/28/batch_normalization.html)