# Linear independence (선형독립)
- 다른 방향성을 가진 벡터들의 집합
- e.g. 
	- a = (0,3), b = (4,5)
	- (2,0,0) && (0,1,0) && (0,0,7)
		- 각각의 요소가 다른 벡터들의 같은 위치의 요소와 다른 방향성을 가지므로

# Linear dependence (선형종속)
- 다른 벡터들의 선형결합으로 표현되는 한 벡터
- 필요충분조건(=iff)으로 c1*v1 + c1*v1 + ... + cn*vn = 0 = (0,0)을 만족할 때 
	- for some ci's not all one zero == at least one is non-zero
```
v1 = a2*v2 + a3*v3 + ... + an*vn
0 = -1*v1 + a2*v2 + a3*v3 + ... + an*vn
// v1의 상수는 -1 == none zero 이므로 필요 충분 조건을 만족
// 다른 벡터들의 선형결합으로 하나의 v1이 표현됨
```
- 같은 방향을 가진 벡터들
- e.g. 
	- a = (2,3), b = (4,6) = 2a
	- (2,3) + (7,9) = (9,5)
		- Span(v1, v2) = R^2 이므로

## 구분법
- A = (2,1), B = (3,2)이고 c1*A + c2*B = 0
	- 판단조건
		- c1 or c2 none zero => dependent
		- c1 and c2 both zero => independent
	- 풀이
		- 2c1 + 3c2 = 0, 1c1 + 2c2 = 0 를 만족하는 c1,c2가 있는가?
		- c2/2 = 0, c1 = 0 이므로 이 벡터집합은 independent하다
		- S = {A,B}의  Span(S) = R^2 이다
- (2,1), (3,2), (1,2)가 independent? dependent?
	- 나머지 둘의 linear combinations로 다른 하나의 벡터를 표현가능

## Questions
: {(1,-1,2), (2,1,3), (-1,0,2) } = S라 했을 때

### Q1. span(S) = R^3?
- c1*A + c2*B + c3*C = (a,b,c)
	- 스칼라 곱의 법칙으로 풀어 쓴 후 증명 진행

### Q2. Linearly Independent?

---
## 참고링크
- [linear-independence](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces#linear-independence)