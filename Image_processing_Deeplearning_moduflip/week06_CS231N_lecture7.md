# CS231n - lecture 7. 2017
- [Lecture 7: Training Neural Networks, Part 2](http://cs231n.stanford.edu/slides/2017/cs231n_2017_lecture7.pdf)

## Summary
- Optimization
	- Momentum, RMSProp, Adam, etc
- Regularization
	- Dropout, etc
- Transfer learning

## Today
- Fancier optimization
- Regularization
- Transfer Learning

---
---
# Fancier optimization

## Optimization: Problems with SGD
- Very slow progress along shallow dimension, jitter along steep direction
- Zero gradient, gradient descent gets stuck
- Saddle points much more common in high dimension
- SGD, SGD+Momentum, Adagrad, RMSProp, Adam all have learning rate as a hyperparameter
	- SGD, SGD + 모멘텀, Adagrad, RMSProp, Adam 모두 학습 속도가 하이퍼 매개 변수입니다.

## SGD + Momentum
- Poor Conditioning
	- 지그재그로 반복하진 않게 되었다.

## Nesterov Momentum
- 가중치를 주어 벡터내적으로 이동

## AdaGrad
- Added element-wise scaling of the gradient based on the historical sum of squares in each dimension

### Q2: What happens to the step size over long time?

## RMSProp

## Adam (almost)
- Momentum + AdaGrad/RMSProp

## Adam (full form)
- Momentum + Bias correnction + AdaGrad/RMSProp
- Bias correction for the fact that first and second moment estimates start at zero

## First-Order Optimization
- Use gradient form linear approximation
- Step to minimize the approximation
- 1차원 함수의 기울기 만큼 을 이동 기준으로 함
	- 낮은 곳을 그냥 지나쳐 버릴 수 있다

## Second-Order Optimization
- Use gradient and Hessian to form quadratic approximation
- Step to the minima of the approximation
