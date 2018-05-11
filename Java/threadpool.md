# ThreadPool
- 프로그램에서 동시 실행을 달성하기 위한 SW 디자인 패턴
- 동시 실행을 위해 작업이 할당되기를 기다리는 여러 쓰레드를 유지함, 감독 프로그램에 의해서 관리됨
- Replication workers || worker-crew model 이라고 불리기도 함
- 쓰레트 풀을 유지함으로서 성능을 향상시키고, 수명이 짧은 작업에 대한 스레드의 빈번한 생성,삭제로 인한 시간 지연을 방지함
	- 반복적인 쓰레드의 생성/소멸에 의한 비효율적인 자원 소모를 방지
- java.util.concurrent.Executors으로 적용 가능

---
## 참고링크
- [Thread Pooling](https://www.joinc.co.kr/w/Site/Thread/Advanced/ThreadPool)
- [Thread pool](https://en.wikipedia.org/wiki/Thread_pool)
- [[Java] Thread Pool(스레드 풀)](http://limkydev.tistory.com/55)
- [자바에서 스레드풀(Thread Pool)관리](http://yookeun.github.io/java/2015/06/17/java-thread-pool/)