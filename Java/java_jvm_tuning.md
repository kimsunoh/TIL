# Java 성능 튜닝에 필요한 지식 : JVM 동작과정에 대한 지식
- GC
- HotSpot
- etc, 위의 두개가 가장 기본

## JVM 선택
- 동일 조건이고, 4GB 이상의 힙을 사용하지 않을 경우 32bit JVM이 사용하는 것이 좋다
	- 32bit의 논리적 최대 사용 가능 힙 크기가 4GB
	- 단, 32bit OS/64bit OS 모두 실제 사용 할당 크기는 2~3GB 정도** ~~확인필요~~




---
## 참고링크
* [Naver D2 - 자바 애플리케이션 성능 튜닝의 도(道)](http://d2.naver.com/helloworld/184615)
* [Naver D2 - Garbage Collection 튜닝](http://d2.naver.com/helloworld/37111)