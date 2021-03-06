# Domain Logic Pattern
- 웹 어플리케이션의 비즈니스 로직 처리와 관련된 패턴

## Transaction Script ( 트랜잭션 스크립트 ) 패턴
* Transaction Script는 이 문서에선 TS로 표기합니다
- 도메인 로직 패턴 중 하나, 모델 1의 구조
- All or Nothing을 기본으로 하는 패턴
- 하나의 트랜잭션으로 구성된 로직을 단일 함수 또는 단일 스크립트에서 처리하는 구조
	- 개별 프로시저가 프레젠테이션 레이어에서 단일 요청을 관리할 때 비즈니스 로직을 프로시저로 사용하여 조직화 하는 패턴

### 장점
- 구현이 매우 쉽다

### 단점
- 비즈니스 로직이 복잡해질수록 난잡한 코드를 만들게 된다
	- 중복코드의 발생을 막기 어려워진다

## Domain model
- 객체 지향 분석 설계에 기반해서 구현하고자 하는 도메인의 모델을 생성하는 패턴
	- 도메인 : 비즈니스 영역
- 비즈니스 영역에서 사용되는 객체를 판별하고, 객체가 제공해야 할 목록을 추출하며, 각 객체간의 관계를 정립하는 과정을 거친다
- 명사와 동사를 구분해서 명사로부터 객체를 추출해내고, 동사로부터 객체의 기능 및 객체 사이의 관계를 유추해낸다
- 대이터와 프로세스가 혼합되어 있으며 객체간 복잡한 연관관계를 갖고 있고, 상속 등을 통해서 객체의 기능과 역할을 확장할 수 있다

---
## 참고링크
- [도메인 로직 패턴 1 - 트랜잭션 스크립트, 도메인 모델](http://javacan.tistory.com/entry/94)
- [[SA강좌]Part 4-6 Transaction Script 패턴](http://zetlos.tistory.com/1179902795)