* 이 문서에서는 java8이후 Java를 'Modern Java', 그 이전의 Java를 'Classic Java'라 말한다

#### Functional Interface(함수형 인터페이스)
- 추상 메서드가 하나 뿐인 모든 인터페이스
- ex) Runnable 
```java
package java.lang;

public
interface Runnable {
	public abstract void runc();
}
```

#### 쓰레드 생성 코드 비교
- Classic Java
```java
public class AsyncHelloWorld {

	/* inner 클래스 정의 */
	public static class HelloWorld implements Runnable {

		@Override
		public void run() {
			System.out.println("Hello World!");
		}
	}

	public static void main(String[] args) {
		new Thread(new HelloWorld()).start();
	}
}
```

- Modern Java
```java
public class AsyncHelloWorld {

	public static class HelloWorld implements Runnable {

		@Override
		public void run() {
			
		}
	}

	public static void main(String[] args) {
		new Thread(() -> { /* 람다식 */
			System.out.println("Hello World!");
		}).start();
	}
}
```

#### 람다식 문법
```
인자 -> 구문 || 식

ex)
(String str, int n) -> {return str + n;}
(str, n) -> {return str + n;}
n -> n++
() -> "hello"
() -> {}
```

### 람다식
- 람다식 = 익명 메서드
- 대상타입 추론
- 매개변수 타입 추론

### Thread 예제
```java
Runnable runnable = () -> {System.out.println("is run thread!!";)}
Thread threa = new Thread( runnable );
```

### 함수형 프로그래밍
- Pure Funtion(순수한 함수)
	- side-effect이 없는 함수, 함수의 실행이 외부에 영향을 끼치지 않는 함수
	- 병렬적인 계산 가능
- Anonymous Function(익명 함수)
	- 이름없는 함수, 일급 객체로 사용될 수 있는 함수
- Higher-order Function(고계 함수)
	- 함수를 다루는 함수
	- 힘수를 인수, 결과값으로 다루는 함수

---
## 참고링크
* [SlideShare - java 8 람다식 소개와 의미 고찰](https://www.slideshare.net/gyumee/java-8-lambda-35352385)
* [BLOG - Java 8 람다 표현식 자세히 살펴보기](https://skyoo2003.github.io/post/2016/11/09/java8-lambda-expression)
* [NAVER D2 - 람다가 이끌어 갈 모던 Java](http://d2.naver.com/helloworld/4911107)
* [WIKI pedia - 함수형 프로그래밍](https://ko.wikipedia.org/wiki/함수형_프로그래밍)
* [나만 모르고 있던 모던 - Java9](http://www.popit.kr/나만-모르고-있던-java9-빠르게-보기/)