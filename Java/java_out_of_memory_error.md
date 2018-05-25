# Out Of Memory ERROR
* Out Of Memory ERROR를 아래에서 OOME로 대체한다
- JVM이 일정한 크기의 메모리를 할당할때 메모리 사이즈가 할당이 안될경우 발생하는 에러다
- -XX: MaxPermSize 옵션으로 사이즈를 조절해서 해결이 가능하다
	- 무턱대고 늘리게 되면 시스템이 무거워질수 있으니 주의하자
- 

## JVM이 사용하는 메모리 공간
### Java Heap
- 프로세스를 처리하며 Object들이 자원을 할당받는 공간이다
- Xms, Xmx Option에 의해 크기가 결정된다
- 세 영역으로 구분된다
	- Old Generation + Yong Generation + Permanent Space 

#### Permanent Space
- Class에 대한 메타 정보를 저장하는 공간이다
- XX:PermSize, XX:MaxPermSize 두 옵션에 의해 크기가 결정된다

### Native Heap
- Native Object들이 할당받은 공간
- 이 공간의 크기는 JVM Option으로 지정할 수 없으며, OS 차원에서 결정된다

## 각 공간에서의 OOME

### Java Heap
> Exception in thread "main": java.lang.OutOfMemoryError: Java heap space 또는
> Exception in thread main: java.lang.OutOfMemoryError: Requested array size exceeds VM limit
- Java Heap Space의 부족으로 Object를 생성하지 못하는 경우 발생한다
- Java Heap의 최대 크기보다 큰 Array가 요청되는 경우 발생한다

#### 발생 이유
- Java Heap의 크기가 작은 경우
- [Memory Leak](https://github.com/kimsunoh/TIL/blob/master/Java/java_memory_leak.md)이 발생하는 경우
	- Application Logic에 의한 Memory Leak
	- JDK Bug나 AWS Bug에 의한 Memory Leak
- finalize 메소드에 의한 Collection 지연
	- 특정 Class Type의 Object는 GC 발생시 Collection되지 않고, Finalization Queue에 들어간 후 Finalizer에 의해 정리가 된다
		- Class에 finalize 메소드가 정의되어 있는 경우
		- Finalizer는 Object의 finalize 메소드를 실행한 후 메모리 정리 작업을 수행한다
			- finalize메소드를 수행하는데 시간이 오래 걸린다면, 그만큼 객체의 메모리 점유 시간이 증가하고, OOME 발생 확률이 높아진다

### Permanent Space
> Exception in thread "main": java.lang.OutOfMemoryError:Perm Gen space
- 많은 수의 Class를 로딩하는 Application의 경우 Permanent Space의 크기가 작으면 OOME가 발생할 수 있다

### Native Heap
> java.lang.OutOfMemoryError: request bytes for . Out of swap space? 
- VM code 레벨에서 메모리 부족 현상이 발견된 경우
> java.lang.OutOfMemoryError: (Native method)
- JNI나 Native Method에서 메모리 부족 현상이 발견된 경우에 해당
> java.lang.OutOfMemoryError: unable to create new native thread
- Thread를 생성할 수 없을 때 발생
	- Native Heap 공간의 메모리를 필요로 하기 때문

#### 발생 이유
- Thread Stack Space가 부족한 경우
- Virtual Space Address가 소진된 경우
- Swap Space가 모자란 경우
- JNI Library에서 Memory Leak이 발생하는 경우

##### Thread Stack Space와 OOM
* Thread Stack Space는 아래에서 TSS로 대체한다
- TSS의 크기는 -Xss옵션을 통해 지정된다
	- 지정되는 공간은 개별 Thread가 사용하는 공간이다
	- N개의 Thread가 생성되었을 경우, N*XssSize 메모리공간이 필요하다

##### Virtual Address Space와 OOME
* Virtual Address Space을 아래에서 VAS로 대체한다
- JVM에 따라 사용가능한 Virtual Address Space의 최대 크기는 OS에 따라 제한된다
- Java Process의 경우 Java Heap과 Permanent Space를 제외한 나머지 공간을 NativeHeap이 사용가능하다
	- ex) VAS가 2G일 때, JavaHeap이 1G, Permanent Space가 200MB를 사용한다면 NativeHeap이 사용 가능한 최대 크기는 800MB이다

---
## 참고링크
- [Java에서의 Out Of Memory Error(OOME)에 대한 나름대로의 정리...](http://ukja.tistory.com/61) 
- [OutOfMemoryError 해결](http://xpace.tistory.com/30)
- [java.lang.OutOfMemoryError – How to solve OutOfMemoryError](https://examples.javacodegeeks.com/java-basics/exceptions/java-lang-outofmemoryerror-how-to-solve-outofmemoryerror/)
- [[PDF]OutOfMemory 장애조치 방법 - Technet - TmaxSoft](https://technet.tmaxsoft.com/download.do?filePath=/nas/technet/technet/upload/kss/tdoc/jeus/2014/01/&fileName=FILE-20140105-000045_140105151928_1.pdf)