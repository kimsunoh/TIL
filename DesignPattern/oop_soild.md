# SOILD
- 로버트 마틴의 OOP 및 설계의 다섯가지 기본 원칙을 마이클 패더스가 두문자어 기억술로 소개한 것
- 시간이 지나도 유지보수와 확장이 쉬운 시스템을 만들고자 할 때 사용하는 원칙
- Source code를 리팩토링 할 때 가독성, 확장성을 높이기 위해 적용할 수 있는 지침
- Agile Development과 Adaptive Software Development(ASD, 적응적 소프트웨어 개발) 전략의 일부이다

## SOILD 원칙 
- SRP : Single Responsibility Principle (단일 책임의 원칙)
- OCP : Open Close Principle (개방 폐쇄의 원칙)
- LSP : The Liskov Substitution Principle (리스코브 치환의 원칙)
- ISP : Interface Segregation Principle (인터페이스 분리의 원칙)
- DIP : Dependency Inversion Principle (의존성 역전의 원칙

## SRP : Single Responsibility Principle
> A class should have one, and only one, reason to change.
- 작성된 클래스는 하나의 기능만 가지며, 클래스가 제공하는 서비스는 그 하나의 책임을 수행하는 데 집중되어 있어야 한다
- 적용 장점
	- 책임 영역이 확실해지므로, 한 책임의 변경에서 다른 책임의 변경으로의 연쇄 작용에서 벗어날 수 있다
	- 클래스의 기능이 명확해진다
- 기능에 따라 클래스를 생성하거나, 분할 하여 적용 할 수 있다

## OCP : Open Close Principle
> 	You should be able to extend a classes behavior, without modifying it.
- 소프트웨어의 구성요소는 확장에는 열려있고, 변경에는 닫혀 있어야 한다는 원리
	- 요구사항의 변경이나 추가사항이 발생해도, 기존 구성요소는 수정이 일어나지 말아야 하며, 기존 구성요소를 쉽게 확장해서 재사용 할 수 있어야 한다는 의미
- 관리가능하고 재사용 가능한 코드를 만드는 기반 (로버트 C. 마틴)
- OCP를 가능하게 하는 중요 메커니즘은 추상화와 다형성이다
	- OCP는 다형성을 통한 확장 원리

### 주의점
- 변경/확장 될 것과 변하지 않을 것을 엄격히 구분한다
- 이 두 모듈이 만나는 지점에 인터페이스를 정의한다
- 구현에 의존하기보다 정의한 인터페이스에 의존하도록 코드를 작성한다

## LSP : The Liskov Substitution Principle
> Derived classes must be substitutable for their base classes.
- 상속을 통한 재사용은 상속관계에서 IS-A 관계가 있을 경우로만 제한되어야 한다
	- 이외의 경우애엔 compposition을 이용한 재사용을 해야한다
		- LSP를 지키기 어려운 경우

### 적용 방법
- 같은 일을 하는 객체는 클래스로 표현해야 한다
	- 동통된 연산이 없다면 별개의 클래스로 만든다
- 같은 연산이 사용되지만, 연산의 로직이 다르다면 공통 인터페이스를 이용해 이를 구현하는 방식을 사용한다
- 두 개체가 하는 일에 추가적으로 무언가를 더 한다면 구현 상속을 사용해야 한다
- 상속 구조가 필요 하다면 Extract Subclass, Push Down Field, Push Down Method 등의 리팩토링 기법을 이용하여 LSP를 준수하는 상속 계층 구조를 구성한다

## ISP : Interface Segregation Principle
> Make fine grained interfaces that are client specific.

> CLIENTS SHOULD NOT BE FORCED TO DEPEND UPON INTERFACES
> THAT THEY DO NOT USE.
(The Interface Segregation Principle, p.5)
- 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다
	- 어떤 클래스가 다른 클래스에 종속될 때에는 가능한 최소한의 인터페이스만을 사용해야 한다
	- SRP가 클래스의 단일책임을 강조한다면 ISP는 인터페이스의 단일책임을 강조한다
- ISP는 어떤 클래스 혹은 인터페이스가 여러 책임 혹은 역할을 갖는 것을 인정한다
	- ISP는 인터페이스 분리,SRP는 클래스 분리 각각을 통해 변화에의 적응성을 획득한다

## DIP : Dependency Inversion Principle
> Depend on abstractions, not on concretions.

> A. HIGH LEVEL MODULES SHOULD NOT DEPEND UPON LOW LEVEL MODULES. BOTH SHOULD DEPEND UPON ABSTRACTIONS.
> 
> B. ABSTRACTIONS SHOULD NOT DEPEND UPON DETAILS. DETAILS SHOULD DEPEND UPON ABSTRACTIONS.
(Wikipedia. Dependenby inversion principle)
- 의존성 역전의 원칙
	- 하위 레벨 모듈의 변경이 상위 레벨의 모듈 변경을 요구하는 위계관계를 끊는 것
- 실제 사용 관계는 바뀌지 않으며, 추상을 매개로 메시지를 주고 받음으로써 관계를 최대한 느슨하게 만드는 원칙
- 복잡하고 지난한 컴포넌트간의 커뮤니케이션 관계를 단순화하기위한 원칙
- 키워드 세가지가 있다
	- IOC
	- HOOK method
	- 확장성

## IOC : Invesion of Control (제에의 역전)
- 어떠한 일을 하도록 만들어진 프레임워크에 제어의 권한을 넘김으로써 클라이언트 코드가 신경써야 할 것을 줄이는 개발전략
- DI(Dependency Injection : 의존성 주입)를 이용해 제어의 권한을 넘길 수 있다.

## HOOK method
- super 클래스에서 default 기능을 정의해두거나, 비워뒀다가 sub 클래스에서 선택적으로 오버라이드 할 수 있도록 만들어둔 method( abstracr or stub)
	- sub클래스에서 추상 메서드를 구현하거나, method override 하는 방법을 이용해 기능의 일부를 확장한다

---
## 참고링크
- [객체지향 개발 5대 원리: SOLID](http://www.nextree.co.kr/p6960/)
- [제어의 역전 IoC Inversion of Control 이란 무엇인가?](http://vandbt.tistory.com/43)
- DI 관련 : [Inversion of Control Containers and the Dependency Injection pattern](https://martinfowler.com/articles/injection.html)
- [Dependency inversion principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle)
- [The Interface Segregation Principle](http://condor.depaul.edu/dmumaugh/OOT/Design-Principles/isp.pdf)
- [리스코프 치환 원칙](https://ko.wikipedia.org/wiki/리스코프_치환_원칙)
- [Liskov substitution principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle)
- [PrinciplesOfOod](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod)