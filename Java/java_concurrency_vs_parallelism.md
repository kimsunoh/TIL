# Concerrency (동시성)
- 한 어플리케이션이 하나 이상의 task를 가지고, 동시에 실행된다
- 하나 이상의 task를 동시에 가지는 것

# Parallelism (병행성)
- 한 어플리케이션이 다수의 subtasks로 나뉘고 이 subtasks들이 병렬로 작동하는 것
- 같은 시간에 작동하는 다수의 CPU를 예로 들 수 있다
- task를 subtask로 나누어 병렬로 작동시키는 것

## Concerrency vs Parallelism
- 컨커런시는 한 어플리제이션이 다수의 task를 어떻게 다루는가와 관련 있다
	- 어플리케이션은 한번에 한 task를 순차적으로 가지거나, 다수의 task를 동시에 가질 수 있다
- 페러렐리즘은 한 어플리케이션이 각각의 task를 어떻게 다루는가와 관련이 있다
	- 어플리케이션은 task를 처음부터 끝까지 연속적으로 가지거나, 한 task를 다수의 subtask로 나누고 이들이 병렬로 작동하게끔 한다

---
## 참고링크
- [자바 컨커런시 / 멀티쓰레딩 튜토리얼](http://parkcheolu.tistory.com/5)
- [컨커런시 vs. 페러럴리즘](http://parkcheolu.tistory.com/9)