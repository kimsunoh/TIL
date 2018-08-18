# A의 역행렬은
- SA = I
	- 가 되는 S 가 A의 역행렬이다
- 즉 SA = I가 되는 S가 없는 행렬 A는 역행렬이 없다
- A의 역행렬은
```
1/ad-bc [ [d -b],[-c a] ] 
```
	- ab - dc가 0일 경우 역행렬을 구할 수 없다
- A (nxn)의 determinent를 구하는 식
	- det(A) = a_11 det(A_11) - a_12 det(A_12) ...


# A가 있을 때, det(A) = -det(S)와 같다
- S = [A_i A_i+2 Ai+1]
- A의 두 행이 바뀐 행렬

# Upper trianfular metrux
- 주 대각선의 밑의 요소들이 모두 0인 행렬

## 이 UTM 의 determinant는 
- 주 대각선 요소들의 제곱값을 더한 게 된다
	- 곱할 수있는 나머지 값들이 0 값이므로 곱하기 값이 나올 수 없게 된다
- 매트리스의 행 연산을 이용해 UTM으로 변환한 후, 그것을 이용해 determinant를 쉽게 구할 수 잇다
	- 행 연산 = 행들 사이에서 곱을 한 후 요소를 0으로 만드는 연산작업


# determinant는 결국 두 벡터로 만든 평행사변형의 넓이이다

** upper triangle 을 만들지 못한다는게 determinant를 구하지 못한다는 것과 iff 한가?