# Synchronized
- 자바에서 동기화 영역
- 객체에 대한 동기화로 이루어짐
- 같은 객체에 대한 모든 동기화 블록은 한 시점에 오직 한 쓰레드만이 블록 안으로 접근하도록 한다
	-	블록에 접근을 시도하는 다른 쓰레드들은 블록 안의 쓰레드가 실행을 마치고 블록을 벗어날 때까지 blocked 상태가 된다
- 네가지 유형의 블록에 사용 가능한다
	- Instance method
	- Static method
	- Instance method code block
	- Static method code block

## Instance method
``` java
public synchronized void counting(int number) {
	this.count += number;
}
```
- 인스턴스 메소드의 동기화는 인스턴스(Object)를 기준으로 이루어진다
	- 한 인스턴스에 한 쓰레드만 이 메소드를 실행 할 수 있다

## Instance method code block
``` java
public void counting(int number) {
	synchronized(this) {
		this.count += number;
	}
}
```
- 메소드 안에 동기화 블록을 따로 작성하는 것
- 동기화 블록 안에 전달된 객체(this)를 모니터 객체라 한다
	- 모니터 객체를 기준으로 동기화가 이루어진다
- 동기화된 인스턴스 메소드는 자신의 내부에 가지고 있는 객체를 모니터 객체로 사용한다

## Static method
``` java
public static synchronized void counting(int number) {
	count += number;
}
```
- 메소드를 가진 클래스 객체를 기준으로 이루어진다
	- JVM 안에 클래스 객체는 클래스 당 하나만 존재할 수 있다
	- 즉, 같은 클래스에 대해서는 한 쓰레드만 동기화된 스태틱 메소드를 실행 할 수 있다 

## Static method code block
``` java
public class Calculator {

	public static synchronized void counting(String msg1, String msg2){
	   log.writeln(msg1);
	   log.writeln(msg2);
	}


	public static void counting2(String msg1, String msg2){
		synchronized(MyClass.class){
			log.writeln(msg1);
			log.writeln(msg2);  
		}
	}
}
```

---
## 참고링크
- [Java의 고유 락(intrinsic lock)에 대해](http://happinessoncode.com/2017/10/04/java-intrinsic-lock/)
- [자바 동기화 블록(Java Synchronized Blocks)](http://parkcheolu.tistory.com/15)