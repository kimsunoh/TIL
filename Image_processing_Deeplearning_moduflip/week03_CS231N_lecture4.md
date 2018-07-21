1. lecture 4
공부를 한 상태에서 오로지 자신이 가진 지식으로 1부터 6을 해보세요. 다 하신 뒤에 자기가 잘 몰랐던 부분을 다시 공부해주세요.
1) slide 12 에 나와있는 함수 f를 빈 공책에 적고 슬라이드를 공부한 지식을 이용하여 forward propagation 과 back propagation 을 계산해보세요.
2) slide 30 에 나와있는 함수 f 를 빈 공책에 적고 1) 과 같이 해보세요. 저번 시간에 공부했던 “어떤 함수“랑 비슷하게 생겼죠?
3) scalar가 아닌 경우에는 어떻게 해야할까요? jacobian matrix가 뭐죠? slide 53에 있는 그림을 이해해보세요
4) slide 58에 나와있는 함수를 1) 과 같이 해보세요.
5) 빈 공책에 neural network 를 적고 neural network 가 뭔지 공부했던걸 떠올려 정의해보세요. neural network의 모티브가 되었던 생물학적 발견을 떠올리고 둘을 엮어서 설명해보세요.
6) slide 96 에 있는 activation function 6가지를 보고 왜 이렇게 생겼을까 상상해보세요.

+ lecture를 공부할 시간이 없으신분들은 꼭 이 동영상을 한 번 시청하고 와주세요! 한국어 설명이고 합쳐서 30분밖에 안되고 굉장히 설명 잘하십니다. 
https://www.youtube.com/watch?v=n7DNueHGkqE&list=PLlMkM4tgfjnLSOjrEJN31gZATbcj_MpUm&index=22
https://www.youtube.com/watch?v=AByVbUX1PUI&list=PLlMkM4tgfjnLSOjrEJN31gZATbcj_MpUm&index=23

---
# 지난주 학습 내용
## loss function
- 모델을 정했을 때, 모델의 정확도를 측정할 수 있는 

## optimization
- 최적화
- loss를 최소화 해주는 작업

## gradient decent (경사하강법)
- loss function을 optimization을 하기 위해 사용하는 방법
- 미분을 이용해 최적의 답을 찾아내는 것
- 잘못된 구덩이에 빠질 수 있음

## sigmoid
- sigmoid면 optimization을 쓸 수 있는 것

---
** 이번주 학습 내용 : W를 어떻게 조정할 것인가? **

# Backpropagation (역전파)
-  chain rule을 사용해서 각 노드가 결과 f에 어떠한 영향을 미쳤는지를 예측하는 것

# Sigmoid
- 계단식 Activation function을 하면, 미분이 불가해서 sigmoid를 사용해서 미분 가능한 결과를 나타내고 싶을 때 사용
- 하지만, sigmoid를 너무 많이 사용하게 되면, 베니싱(날라가버리는) 현상이 발생해서, sigmoid만 사용하는 것이 아닌 ReLU 를 사용하게 됨

# thread holed regreission 

# hidden layer
- feature에 대해 명확한 의미를 인간의 입장에서 설명할 수 없는 layer

# Fully-connected layers
- 모든 출력 값이, 결과값에 연결되어 있는 layer

? 왜 0을 무시하는가?