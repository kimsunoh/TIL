# Deadlock (교착상태)
- 두 개 이상의 작업이 서로 상대방의 작업이 끝나기만을 기다리고 있기 때문에, 결과적으로 아무것도 완료되지 못하는 상태를 가리킨다
	- 작업들이 대기상태에서 벗어나지 않게 되므로
- 4가지 필요조건에서 한 가지라도 만족하지 않으면 deadlock은 발생하지 않는다

## Deadlock의 4가지 필요조건
- Mutual exclusion (상호배제)
	- 프로세스들이 필요로 하는 자원에 대해 배타적인 통제권을 요구
- Hold and wait (점유대기)
	- 프로세스가 할당된 자원을 가진 상태에서 다른 자원을 기다린다
- No preemption (비선점)
	- 프로세스가 어떤 자원의 사용을 끝낼 때까지 그 자원을 뺏을 수 없다
- Circular wait (순환대기)
	- 각 프로세스는 순환적으로 다음 프로세스가 요구하는 자원을 가지고 있다
	- 점유대기 조건과 비선점 조건을 만족해야 성립하는 조건
		- 4가지 조건은 서로 완전히 독립적인 것은 아니다

### Mutual exclusion
- Mutex는 멀티프로세스 프로그래밍에서 공유 불가능한 자원의 동시 사용을 피하기 위해 사용되는 알고리즘
- Critical section(임계구역, 이하 CS)으로 불리는 코드 영역에 의해 구현된다
	- 공유 데이터를 접근하는 프로그램 내부의 CS부분은 홀로 수행 되도록 보호되어야 한다
- 구현하는 가장 단순한 방법은 인터럽트를 억제해서 공유 데이터가 손상되는 것을 막는 것이다

## Deadlock의 관리

### 예방
- Mutual exclusion의 제거
- Hold and wait의 제거
	- 한 프로세스에 수행되기 전에 모든 자원을 할당시키고 나서 점유하지 않을 때에는 다른 프로세스가 자원을 요구하도록 하는 방법
	- 자원 과다 사용으로 인한 효율성, 프로세스가 요구하는 자원을 파악하는 데에 대한 비용, 자원에 대한 내용을 저장 및 복원하기 위한 비용, 기아 상태 등의 문제점이 있다
- No preemption의 제거
	- 비선점 프로세스에 대해 선점 가능한 프로토콜을 만들어 준다
- Circular wait의 제거
	- 자원 유형에 따라 순서를 매긴다
 
---
## 참고링크
* [교착 상태](https://ko.wikipedia.org/wiki/교착_상태)