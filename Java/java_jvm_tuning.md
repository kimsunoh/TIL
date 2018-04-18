# Java 성능 튜닝에 필요한 지식 : JVM 동작과정에 대한 지식
- GC
- HotSpot
- etc, 위의 두개가 가장 기본

## JVM 선택
- 동일 조건이고, 4GB 이상의 힙을 사용하지 않을 경우 32bit JVM이 사용하는 것이 좋다
	- 32bit의 논리적 최대 사용 가능 힙 크기가 4GB
	- 단, 32bit OS/64bit OS 모두 실제 사용 할당 크기는 2~3GB 정도** ~~확인필요~~

## JVM 옵션
- New 영역 사이즈 관련 옵션
	- New 영역의 사이즈 관리로 인해 Old 영역으로 이동되는 객체가 줄고, FGC의 횟수를 줄일수 있게됨
		- 새로 생성되는 객체가 짧은 생존시간을 갖는 경우 유용함
	- 일정 수치 이상으로 New 영역의 크기가 커지면 오히려 응답 반응성이 떨어질 수 있음
		- Survivor 영역간 복사 작업이 길어져서
	- 대표 옵션
		- XX:NewRatio
			- 전체 힙 크기중 New 영역의 비율을 지정
		- XX:NewSize
			- 원하는 크기 만큼의 New 영역 크기를 지정

### NewRatio
- NewRatio를 지정하면 전체 힙 크기 중에서 1/(NewRatio+1) 만큼이 New 영역의 크기가 됨

### NewSize
- 지정한 만큼 New 영역이 생성됨
- MaxNewSize를 같이 지정하면, NewSize 지정영역 사이즈부터 MaxNewSize까지 영역이 커짐
	- Eden이나 Survivor 또한 지정된 비율 또는 기본 비율에 따라 같이 커짐
	- NewSize와 MaxNewSize를 같게 지정하는 것이 좋다
		- 크기의 동적인 변경에 의한 오버 헤드를 최소화 하기 위해
		- Xms와 Xmx 크기를 같게하는 것과 동일 

### NewRatio vs NewSize
- 둘을 같이 지정할 경우, 둘 중 큰값을 사용함

## 애플리케이션 성능 측정

### 파악해야할 정보
- 정보 종류
	- TPS (Transaction Per Second) / OPS (Operation Per Second)
		- 개념적으로 해당 애플리케이션의 성능을 이해하는데 필요한 정보
	- RPS (Request Per Second)
	- RPS 표준편차
		- 편차가 발생한다면 GC 튜닝이나 연동 시스템에 대한 점검이 필요함
- 10분 이상 특정 기능에 대한 부하를 준 뒤 성능 수치를 측정하는 것이 좋음
	- HotSpot JIT에 의해 바이트 코드가 컴파일된 상태가 되기를 기대하기 때문

## 튜닝 팁
- GC는 생성된 객체가 얼마나 오래 남아있는가가 더 중요함
	- 객체가 보다 빨리 GC 대상이 될 수록 Stop-the-wolrd 시간은 줄어들 가능성이 높음
- CPU 사용률이 낮다
	- TPS가 낮은데 CPU 사용률이 낮다면 Blocking Time이 원인임
	- 연동 시스템의 문제 혹은 동시성(Concurrency)문제 일 수 있음
	- 스레드 덤프 결과 분석, 프로파일러를 이용해 확인 가능
	- jvisuakvn에 있는 CPU 분석 만으로도 충분한 결과를 얻을 수 있음
- CPU 사용률이 높다
	- TPS가 낮은데 CPU 사용률만 높다면 효율적이지 못한 구현 때문일 가능성이 높음
	- 프로파일러를 이용한 병목 지점 파악 필요
	- jvisualvm이나 eclipse의 TPTP, JProbe 등을 이용해 분석
	
### 객체가 빨리 GC 되게 만드는 팁
- 객체의 크기를 가급적 작게 유지
- Collection이나 기타 Container 형태의 자료구조 안에서 배열의 크기를 변경하는 작업은 가급적 피하자
- SoftReference는 사용하지 않는 게 좋음

## 튜닝 접근 방법 생각할 사항
- 성능 튜닝이 필요한지 파악 필요함
> 문제는 단 한 곳에 있고 그 하나만 수정하면 된다: 파레토 이론은 성능 튜닝에도 적용된다. 
>		문제는 반드시 하나라는 의미보다는 가장 성능에 영향을 미치는 하나에만 집중해 접근할 필요가 있다는 뜻으로 해석하자.
>		하나에 집중해서 해결하고 난 다음에 다른 문제 해결을 위해 노력하도록 하자.

>	풍선 효과: 무엇을 얻기 위해 무엇을 포기해야 하는지 결정해야 한다. 
>		캐시를 적용해 응답 반응성을 높일 수는 있지만 캐시의 크기가 커지면 풀 GC 시간이 길어질 수 있다. 
>		적은 메모리 사용량을 선택하면 대개 처리 용량이나 응답 반응 시간이 나빠진다. 
>		하나를 선택하면 하나를 포기해야 한다는 것을 염두에 두고 우선순위를 정해 선택하자.


## GC 튜닝의 절차
1. GC 상황 모니터링
2. 모니터링 결과 분석 후 GC 튜닝 여부 결정
	- GC의 수행시간을 보고 결정
3. GC 방식/메모리 크기 지정
4. 결과분석

### 결과 분석 체크 리스트
- Full GC 수행 시간
- Minor GC 수행 시간
- Full GC 수행 간격
- Minor GC 수행 간격
- 전체 Full GC 수행 시간
- 전체 Minor GC 수행 시간
- 전체 GC 수행 시간
- Full GC 수행 횟수
- Minor GC 수행 횟수

---
## 참고링크
* [Naver D2 - 자바 애플리케이션 성능 튜닝의 도(道)](http://d2.naver.com/helloworld/184615)
* [Naver D2 - Garbage Collection 튜닝](http://d2.naver.com/helloworld/37111)
* [SlideShare - Everything I Ever Learned About JVM Performance Tuning](https://www.slideshare.net/aszegedi/everything-i-ever-learned-about-jvm-performance-tuning-twitter/52-Responsiveness_still_not_good_enough)
