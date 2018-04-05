# Garbage Collection (GC, 가비지 컬렉션)
- 더이상 필요없는 (쓰레기)객체를 찾아 지우는 작업을 함
- weak generational hypothesis에 의한다
	- 대부분의 객체는 금방 접근 불가능 상태(unreachable)가 된다
	- 오래된 객체에서 젊은 객체로의 참고는 아주 적다
- 가설의 장점을 최대한 살리기 위해 HotSpot VM에서는 크게 2개로 물리적 공간으로 나누어짐

## stop-the-world
- GC를 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것
- 발생하면 GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춤
- GC 작업을 완료한 이후에야 중단했던 작업을 다시 시작함
- 어떤 GC알고리즘을 사용하더라도 발생함
- 대개의 경우 GC튜닝이란 이 stop-the-world 시간을 줄이는 것
	- Java는 프로그램 코드에서 메모리를 명시적으로 지정하여 해제하지 않음

## HotSpot VM의 2개의 물리 공간
- Young Generation
	- 새롭게 생성한 객체의 대부분이 위치함
	- 이영역에서 객체가 사라질 때 Minor GC가 발생한다고 말함
- Old Generation
	- 접근 불가능 상태로 되지 않아 Young 영역에서 살아남은 객체가 여기로 복사됨
	- 대부분 Young 영역보다 크게 할당됨
	- Young영역보다 GC는 적게 발생함
	- 이 영역에서 객체가 사라질 때 Major GC(혹은 Full GC)가 발생

### 영역별 이동 흐름
- -( Allocation )-> [Young Generation] -(Promotion)-> [Old Generation],[Permanent Generation]
* Permanent Generation 영역 ( Perm 영역 )
	- ~Method Area 라고도 함(?)~
	- JVM클래스와 메서드 객체를 위한 영역
	- JVM의 모든 스레드들이 공유하는 데이터 영역
	- Runtime constant pool과 각 클래스에 대한 생성자와 메서드들에 대한 코드를 저장
		* Runtime constant pool 
			- 각 클래스에 대한 인스턴스 변수와 인스턴스의 멤버 변수, static 변수와 static 인스턴스의 멤버들이 저장되는 영역
			- Method area에 의해 할당되고 관리됨, JVM의 모든 스레드들이 공유하게 됨
	- 여기서 GC가 발생하면 Major GC의 횟수에 포함됨

#### 카드테이블
- Old영역의 512바이트의 덩어리(chunk)로 되어있는 테이블
	- Old영역 객체가 Young 영역 객체를 참조할 때마다 정보가 표시됨
- Young 영역의 GC를 실행할 때는 Old 영역에 있는 카드테이블만 뒤져서 GC 대상인지 식별함
- write barrier를 사용하여 관리함
	- Minor GC를 빠르게 할 수 있도록 하는 장치
	- 약간의 오버헤드는 발생하지만 전반적인 GC 시간은 줄어들게 됨

## Young 영역
- 3개의 영역으로 나뉨
	- Eden 영역
	- Survivor 영역(2개)
- GC 처리 절차
	1. 새로 생성한 대부분의 객체는 Eden 영역에 위치함
	2. Eden 영역에서 GC가 한 번 발생한 후 살아남은 객체는 Survivor 영역 중 하나로 이동 됨
	3. Eden 영역에서 GC가 발생하면 이미 살아남은 객체가 존재하는 Survivor 영역으로 이동 됨
		1) 가득찬 Survivor 영역은 아무 데이터도 없는 상태가 됨
		* 즉, Survivor 영역 중 하나는 반드시 비어있는 상태여야함
		* 두 Survivor 영역에 모두 데이터가 존재하거나, 두 영역 모두 사용량이 0이면 시스템이 비정상적인 것
	4. 1-3과정을 반복하다가 계속해서 살아남아 있는 객체는 Old영역으로 이동하게 됨

### MinorGC
- GC 수행 방법
	1. MinorGC가 발생하면 Eden과 S1에 Alive 되어있는 객체를 S2로 복사함
		- S1에 Alive 되어있지 않은 객체는 자연히 S1에 남아있게됨
	2. S1과 Eden 영역을 Clear함
	3. Minor GC를 수행하다가 Survivor 영역에서 오래된 객체는 Old 영역으로 이동
	
## Old 영역
- 데이터가 가득 차면 GC를 실행함

### Full GC
: Mark & Compact 알고리즘 이용
- 수행방법
	1. 전체 객체들의 reference를 쭉 따라가며 reference가 연결되지 않는 객체를 Mark 함
	2. 1작업이 끝나면 Mark된 객체를 삭제함
		: 실제로는 Compact라고 해서, Mark된 객체로 생기는 부분을 사용하는 객체로 메꾸어 버린다
- Full GC는 매우 속도가 느림
- Full GC가 일어나는 도중에 순간적으로 stop-the-world가 발생한다

## JVM의 GC의 방식
### Serial GC (-XX:+UseSerialGC, 이하 S-GC)
- 데스크톱의 CPU 코어가 하나만 있을 때 사용하기 위해서 만든 방식, 사용하면 안됨
- Old 영역의 GC는 mark-sweep-compact라는 알고리즘을 사용함
	- mark-sweep-compact
		1. Old 영역에 살아있는 객체를 Mark함
		2. Heap의 앞 부분부터 확인하여 살아 있는 것만 남김(Sweep)
		3. 각 객체들이 연속되게 쌓이도록 힙의 가장 앞 부분부터 채워서 객체가 존재하는 부분과 객체가 없는 부분으로 나눔(Compaction)
- CPU 코어 개수가 적고 메모리가 적을 때 적합한 방식

### Parallel GC(-XX:+UseParallelGC, 이하 P-GC)
: Throughput GC 라고도 함
- S-GC와 기본적인 알고리즘은 같음, 그러나 S-GC와는 다르게 Parallel GC는 처리하는 쓰레드가 여러개
	- S-GC보다 빠르게 객체를 처리할 수 있음
- 메모리가 충분하고 코어의 개수가 많을 때 유리함
	
### Parallel Old GC(-XX:+UseParallelOldGC)
- P-GC와 비교하여 Old영역의 GC 알고리즘만 다름
- Mark-summaty-Compaction 단계를 거침
	1. Summary단계
	: 앞서 GC를 수행한 영역에 대해서 별도로 살아있는 객체를 식별한다는 점에서 Mark-Sweep-Compaction 알고리즘의 Sweep 단계와 다름
	
### CMS GC(-XX:+UseComcMarkSweepGC)
: Low Latency GC라고도 함
- 실행단계
	1. Initial Mark 단계
		- 클래스 로더에서 가장 가까운 객체 중 살아 있는 객체만 찾는 것으로 끝냄
		- stop-the-world 시간이 매우 짧음
	2. Concurrent Mark 단계
		- 방금 살아있다고 확인한 객체에서 참조하고 있는 객체들을 따라가면서 확인함
		- 이 작업을 다른 스레드가 실행 중인 상태에서 동시에 진행됨
	3. Remark단계
		- Concurrent Mark 단계에서 새로 추가되거나 참조가 끊긴 객체를 확임함
	4. Concurrent Sweep 단계
		- 쓰레기를 정리하는 작업을 실행함
		- 다른 스레드가 실행되고 있는 상황에서 진행함
- stop-the-world 시간이 매우 짧음
- 모든 애플리케이션의 응답 속도가 매우 중요할 때 CMS GC를 사용
- 단점
	- 다른 GC 방식보다 메모리와 CPU를 더 많이 사용함
	- Compaction 단계가 기본적으로 제공되지 않음
		- 조각난 메모리가 많아 Compaction 작업을 실행하면, 다른 GC 방식의 stop-the-world 시간이 더 길기 때문에 Compaction 작업이 얼마나 자주, 오랫동안 수행되는지 확인 필요

### G1 GC
: Young 영역에서 데이터가 Old 영역으로 이동하는 단계가 사라진 GC 방식이라고 이해하면 됨
- CMS GC를 대체하기 위해서 만들어짐
- 장점
	- 위에서 설명된 GC들 중에서 가장 빠르다
		- JDK 7에서부터 정식 포함됨

---
## 참고문헌
* [NAVER D2 - Java Garbage Collection](http://d2.naver.com/helloworld/1329)
* [Understanding the G1 Garbage Collector ? Java 9](https://www.dynatrace.com/news/blog/understanding-g1-garbage-collector-java-9/)
* [JVM 메모리구조](http://huelet.tistory.com/entry/JVM-%EB%A9%94%EB%AA%A8%EB%A6%AC%EA%B5%AC%EC%A1%B0)
* [JVM PermGen ? where art thou?](https://dzone.com/articles/jvm-permgen-%E2%80%93-where-art-thou)
* [자바 웹 프로그래밍 - JVM memory와 GC 종류](https://www.slipp.net/wiki/pages/viewpage.action?pageId=26641949)
* [Java Reference와 GC](http://d2.naver.com/helloworld/329631)
* [JVM GC와 메모리 튜닝](http://levin01.tistory.com/441)