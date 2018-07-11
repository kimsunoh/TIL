# Linear Combination (선형결합)
- 다른 방향을 가진 두 벡터의 결합으로 R^2의 평면의 모든 벡터를 설명할 수 있다.
```
span(vector_a, vector_b) = R^2
```
- span(0) = 0 // 0벡터의 결합값은 0이다
- 벡터 a의 span(vector_a)는 단순 상수배한 벡터a 이다
- span(v1, v2, v3, ... vn) = { c1v1 + c2v2 + ... + cnvn | ci extends R for i <= i < n }
- 증명
```
a = (1,2), b = (0,3) 일 때, x = (x1, x2) 라면
c1a + c2b = x이면 된다

1c1 + 0c2 = x1 //c1 = x1
2c1 + 3c2 = x2

2c1 +     = 2x1
2c1 + 3c2 = x2
---
3c2 = x2 - 2x1
c2 = (x2 - 2x1)/3
```
- 결국 상수배로 결정되는 것을 볼 수 있다.
	- x = (2,2)가 되고자 할 때
		- c1 = 2, c2 = (2 - 2*2)/3 = -2/3
		

---
## 참고링크
- [linear-combinations](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces#linear-combinations)