# NumPy (넘파이)
- 수학 및 과학 연산을 위한 파이썬 패키지
	- Python의 Numarray, Numeric 패키지를 계승
- 파이썬으로 수치해석, 통계 관련 기능을 구현할때 기본으로 사용되는 모듈
	- 수치해석을 편리하게 할 수 있음
- 내부 상당부분 C나 포트란으로 개발되어 실행 속도가 빠른편
- 기본적으로 array라는 자료를 생성하고 색인,처리,연산 등을 하는 기능을 수행함
- 다른 Python 패키지와 함께 쓰이는 경우가 많음
	- Scipy, Pandas, Matplotlib 등

## Different Python Package 
### Scipy
- Scipy를 사용할 때 NumPy를 많이 사용함
- 수치해석을 NumPy를 이용하여 보다 본격적으로 이용 할 수 있게 해 줌
- NumPy만으로 길게 코딩되는 기법들을 2~3줄로 구현 할 수 있게함
	- 수치 미분법, 수치 적분법, 수치 미분 방정식 해법(Runge–Kutta method 등)
- NumPy로 구현하기 힘든 것들을 구현 할 수 있음

### Sympy
- Python의 대표적인 기호계산 패키지
- NumPy에 적용 가능한 함수를 구현할 수 있음
	- Sympy로 원하는 함수를 구현하고, 이 함수를 바탕으로 NumPy를 이용하여 배열형 자료를 구할 수 있음

### Matplotlib 
- 그래픽 패키지
- 데이터를 그래프화 하기 위해 이용

### Pandas
- NumPy를 이용해 만든 array자료를 이용해, Pandas에서 제공하는 형태의 자료를 생성하거나 수정할 수 있음
	- Series, DataFrame
- NumPy보다 더 복잡한 형태의 자료를 다룸

### Matplotlib
- 그래프를 그리기 위해 사용하는 라이브러리
	- 그래픽 라이브러리
- 주요 사용 모듈
	- pyplot 모듈

## Example
``` python
import numpy as np 

x = np.array([1, 2.0, 3, 10])
print(x)
[  1.   2.   3.  10.]

y = np.array([10, 3, -1, -5])
print( type(y) )
# <type 'numpy.ndarray'>

# 산술연산, 연산객체의 구조가 같은 경우 1:1 매칭(index 기준)으로 연산됨

print( x+y )
# [ 11.,   5.,   2.,   5.] 

print( x-y )
# [ -9.,  -1.,   4.,  15.]

print( x*y )
# [ 10.,   6.,  -3., -50.]

print( x/y )
# [ 0.1       ,  0.66666667, -3.        , -2.        ]

print( x/2 )
# [ 0.5,  1. ,  1.5,  5. ]

# numpy array 형상 확인
print( vector.shape )
# (2,)

print( metrix.shape )
# (2, 2)

# numpy array dataType 확인
print( vector.dtype )
# int64

```

## Broadcast (브로드캐스트)
- 넘파이 배열과 스칼라값의 연산을 넘파이 배열의 원소 각각과 스칼라값의 연산으로 바꿔 수행하는 것
	- 형상이 다른 배열끼리 연산하는 것
``` python
metrix = np.array([[1,2],[9,-1]])
 
print( metrix * 10 )
# [[ 10  20]
#  [ 90 -10]]

vector = np.array( [2, 4] )

print( metrix * vector )
# [[ 2  8]
#  [18 -4]]
```

---
## 참고링크
* [나무위키 - NumPy](https://namu.wiki/w/NumPy) 