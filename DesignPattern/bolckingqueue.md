# BlockingQueue
- Produce-Consumer pattern을 기반으로한 Multi Thread 디자인 패턴 중 하나
- 특정 상황에서 쓰레드를 대기하도록 하는 큐의 처리 패턴
	- 특정상황
		- Dequeue 때 큐가 비어있을 때
		- Inqueue 때 큐가 꽉 차있을 때
	- 다른 쓰레드가 상황을 해결해 줄 때까지 대기상태를 유지한다

## BlockingQueue의 종류
: java 에서 구현된 블로킹 큐의 구현체

### ArrayBlockingQueue
- 고정배열에 일반적인 Queue를 구현한 클래스, 생성 후 크기 변경 불가
- 꽉찼을 때 inqueue, 비었을 때 dequeue에 대해 각각을 block
- 공평성을 따진다

#### 특징
- 선택적 공평성 정책을 두고, block한 thread들의 순차적 대기열을 생성한다
- 대기열 처리에 대한 정확한 순서 보장이 안된다

### LinkedBlockingQueue
- 선택적으로 bound가 가능한 Linked list로 구현된 Queue
- capacity를 초기에서 정해주지 않는 경우 integer.MAX_VALUE로 자동 설정된다
	- node는 동적으로 삽입시마다 생성된다

### PriorityBlockingQueue
- PriorityQueue와 같은 정렬 방식을 갖는 용량제한이 없는 Queue
	- dequeue에 대해 block기능을 갖는다
	- unBounded 이므로, 작업 수행중 fail이 나면 자원고갈이 난 것

#### 특징
- null element 및 non-comparable object를 수용하지 않으며, natural ordering을 지원함

### SynchronousQueue
- 수행중인 thread의 object의 queue에 대한 동작이 다른 살아있는 스레드 object의 queue에 대한 동작과 sync-up되어야 하는 handoff design에 적합하다
	- 주로 information, event, task를 전달 한다
- Collection 함수들에 emepty collection으로서의 목적성을 지닌다
	
#### 특징
- Queue 내부로의 insert 작업이 다른 스레드의 remove 작업과 반드시 동시에 일어나야한다
	- remove 작업도 동일, insert 작업이 있어야만 수행된다
- 서로 대칭되는 작업이 없을 경우 생길 때까지 대기한다
- 추출 될 것이 없으므로 추출함수 사용이 불가능하다
- poll()을 수행했을 때 삽입 시도한 thread가 없으면 null을 return한다

---
## 참고링크
- [블로킹 큐(Blocking Queues)](http://parkcheolu.tistory.com/29)
- [[Java]BlockingQueue의 종류와 용법](http://oniondev.egloos.com/558949)
- [Class LinkedBlockingQueue<E>](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedBlockingQueue.html)
