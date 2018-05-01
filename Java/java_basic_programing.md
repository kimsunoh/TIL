# Basic Programing : New Thing and Translation for Java 9

---
# Useful Tips

- NaN(Not a Number) 검사방법
	- 숫자가 아닌 값은 모두 서로 다른 값으로 간주된다
```java
// 양의 무한대, 1.0/0.0
Double.POSITIVE_INFINITY
// 음의 무한대, -1.0/0.0
Double.NEGATIVE_INFINITY
// NaN, -number의 루트 계산
Double.NaN

Double infinity = 1.0/0.0;
if( Double.isInfinite(infinity) ) 
	Sysout.out.println( "true" );
```

- 숫자 > 문자열 변환
```java
int number1 = 40;

// Integer.toString(int number, int radix) : number를 radix 진수 String으로 반환함
String binaryStr = Integer.toString( number1, 2); // "101000"

// Integer.parseInt(String str, int radix) : radix 진수로 표현된 str을 Integer으로 반환함
int number2 = Integer.parseInt(binaryStr, 2); 
```

- String 클래스는 Immutable(불변) 특성을 갖는다
	- 생성된 String객체에 변화를 줄 수 없다
	- method나 연산을 통해 리턴되는 결과는 새로운 String객체이다


---
## 참고문서
- [도서 - 가장 빨리 만나는 코어 자바]
