# Java EE 근황
## 웹서비스를 개발하는 방법 : spring, java EE 
## java EE 8 ( 2017/09오픈 )
- servlet 4.0 지원
- 비동기 이벤트

# MicroProfile - Enterprise Java Microservices
## 마이크로서비스를 위한 엔터프라이즈 자바 최적화
## 탄생배경
- 마이크로서비스 아키텍처 급부상
- spring의 AOP,CI가 CDI라고 2009년에야 반영됨
- 결국 너무 느림!!!
- 엔터프라이즈 버전을 오픈소스로 주도적으로 개발
	- EE를 사용하는 벤더들이 모임

## 지원 컨테이너
- WildFly Swarm
	- JBOSS 커뮤니티의 EE 버전
- TomEE
- ...

## 8가지 핵심기능 - 마이크로서비스 최적화를 위한
### Config
- 동적 설정값 사용 == Spring @value
- 메타파일로 사용가능
### Health Check
- 시스템 가용성 체크 ( UP, DOWN )
-  M2M 메커니즘 구현을 위해 사용( 컨테이너 기반 환경 )
- HealthCheck interface를 사용해 간단하게 구현 가능
	- 살았니 죽었니 확인
	- 로드밸런싱에 사용
### Metrics
- 시스템 모니터링
- Counter, Gauge, Meter, Timer, Histogram 방식 지원
- 3가지 Scope
	- Base 기본 ( JVM, Thread, Class Loader, OS Stats )
	- Vender : Vender 제공
	- Application : 사용자 정의
- Prometheys( 무료 모니터링 툴 )
	- MicroProfile로 받은 파일을 프로메테우스에 연결하면 그래프 형태로 제공받을 수 있음
### Fault Tolerance (결함 내성)
- 전체 시스템 중 일부에 결함(고장)이 발생하더라도 전체 시스템의 운영에 문제가 발생하지 않는 것
- 통합지점( Intergration Points )
	- 하나의 시스템이나 응용프로그램에서 N/W를 통해 다른 시스템 또는 응용 프로그램으로 이동하는 지점
	- 애플리케이션 간에 연결이 생기면 문제가 발생할 수 밖에 없다
#### 지원 패턴
- @Timeout : 지정된 시간동안 기다림, 실패일 경우 처리하기 위해
- @Retry : 더 시도 할 경우 적용
- @Fallback : 후퇴전략, 계속대기가 아닌 이상 발생시 대체 서비스를 제공하는 것
- @CircuitBreaker
	- 요청에 대한 실패회수가 임계치를 초과할 경우 자동으로 접속을 차단
	- 반복되는 Timeout, Retry를 방지 -> fail fast
	- 3가지 상태가 있음
		- CLOSED
			- 응답이 성공했을 경우
		- OPEN
			- 응답이 계속 실패할 경우
		- HALP-OPEN
			- 시간이 지난다음, 1회 호출을 받아보는 단계
- @Bulkhead
	- 하나의 요소가 고장 나더라도 나머지는 정상적으로 동작하도록 응용 프로그램 요소를 여러 풀에 격리하는 패턴
	- 기능 영역별 공간 사용
	- 2가지 방식
		- Thread Pool
			- 모든 요청을 별도의 대기큐를 가진 Thread Pool에 할당하는 방식
		- 세마포어 방식
- @JWT Propagaton
	- Json Web Token Propagation == Spring Security
	- IANA 표준 & 비표준 을 제공

### Open API
- OpenAPI v3 문서 자동생성
- YAML & JSON 형식의 '/endpoint' 제공
### OpenTracing
- OpenTracing 기반 분석 추적 기능
- 코드 비사용& 코드사용( @Tracing )을 사용해서 이용 가능
- Zipkin 이라는 오픈소스를 사용해서 시각화해서 볼 수 있음
### RestClient
- Type-Safe한 일관성 있는 호출 지원
	- Spring RestTemplate
	- 응답데이터에 대한 type을 보장 받을 수 있음

---
## 참고링크
* [SpringCamp2018 - MicroProfile : for Enterprise Java Microservices]