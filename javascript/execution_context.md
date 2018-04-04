# Execution Context( 실행 컨텍스트 )
: scope, hoistiong, this, sunction, closure 등의 동작원리를 담고 있는 자바스크립트의 핵심원리
- 실행 가능한 코드를 형상화하고 구분하는 추상적인 개념
- 실행 가능한 코드가 실행되기 위해 필요한 환경

### 자바스크립트 엔진 실행시 필요한 정보
* 변수 : 전역변수, 지역변수, 매개변수, 객체의 프로퍼티
* 함수 선언
* 변수의 유효범위(Scope)
* this

## Execution Context Stack
- 논리적 스택 구조를 갖음

### Execution Context Stack 동작 원리
- 컨트롤이 실행 가능한 코드로 이동하면 논리적 스택 구조를 가지는 새로운 실행 컨텍스트 스택이 생성됨
- Global code로 컨트롤이 진입하면 전역 실행 컨텍스트가 생성되고 실행 컨텍스트 스택에 쌓임
	- 전역 실행 컨텍스트는 애플리케이션이 종료될 때 까지 유지됨
- 함수를 호출하면 해당 함수의 실행 컨택스트가 생성되며 직전에 실행된 코드 블럭의 실행 컨텍스트 위에 쌓임
- 함수 실행이 끝나면 해당 함수의 실행 컨텍스트를 파기하고 직전의 실행 컨텍스트에 컨트롤을 반환함

## Execution Context 3가지 객체
- Variable Object ( VO / 변수 객체)
	- {vars, function declarations, arguments... }
- Scope chain
	- [ Variable object + all parent scopes ]
- thisValue
	- Context object

### Variable Object ( VO / 변수 객체)
- 실행 컨텍스트가 생성되면 자바스크립트 엔진이 생성하는 정보를 담을 객체
	- 이 값은 다른 객체를 가르킴
- 변수, 매개변수(parameter)와 인수 정보(arguments), 함수 선언(함수 표현식 제외)
- 코드가 실행될 때 엔진에 의해 참조되며 코드에서는 접근할 수 없음
- 전역 컨텍스트와 함수 컨텍스트는 가리키는 객체가 다름
	- 전역코드와 함수의 내용이 다름으로
	- ex) 전역 코드에는 매개변수가 없음, 함수에는 매개변수가 있음

#### 전역컨텍스트의 경우
- VO는 유일하며 최상위에 위치하고 모든 전역 변수, 전역 함수 등을 포함하는 전역 객체를 가리킨다. 
- 전역 객체는 전역에 선언된 전역 변수와 전역 함수를 프로퍼티로 소유함
	
#### 함수 컨텍스트의 경우
- VO는 Activation Object(AO / 활성객체)를 가리킴
- argument object가 추가됨
	- 매개변수와 인수들의 정보를 배열의 형태로 담고있음

### Scope Chain (SC)
- 중첩된 함수의 스코프의 레퍼런스를 차례로 저장하고 있는 개념
- 실행 컨텍스트가 참조할 수 있는 GO 또는 AO를 가르킴
	- 실행 컨텍스트의 AO를 선두 순차적으로 상위 컨텍스트의 AO를 가리키며 마지막 리스트는 GO를 가리킴
		- 함수가 중첩 상태일 때 하위 함수 내에서 상위 함수의 유효범위까지 참조할 수 있게됨
		- 함수 실행중 변수가 호출 > 현재 실행 Scope(여기선, AO)에서 검색 > 실패시, 스코프 체인을 따라 올라가며 상위 Scope를 탐색함
			- 검색에 실패하면 정의지 않는 것으로 판단, Reference 에러를 발생
- 함수가 중첩되있으면 중첩될 때마다 부모 함수의 Scope가 자식 함수의 스코프 체인에 포함됨
- 엔진은 이를 통해 Scope를 파악함
- SC는 [[scope]]프로퍼티로 참조할 수 있다

#### this value
- this 프로퍼티에는 this값이 할당됨
- 값은 함수 호출 패턴에 의해 결정됨

### Excution Context의 실행 과정
#### 전역 코드에의 진입
- 초기상태의 전역객체에는 빌트인 객체(Math, String, Array)와 BOM, DOM이 설정되어 있음
- 전역 코드로 컨트롤이 진입하면 전역 실행 컨텍스트가 생성되고 실행 컨텍스트에 쌓임
- 이후는 실행 컨텍스트를 바탕으로 실행
	- SC의 생성과 초기화
	- Variable Instantiation 실행
	- this value 결정

##### SC의 생성과 초기화
- SC는 전역 객체의 레퍼런스를 포함하는 리스트가됨

##### Variable Instantiation 실행
- Variable Instantiation(변수 객체화) 
	: Variable Object에 프로퍼티와 값을 추가하는 것을 의미함
	: 매개변수와 인수 정보(arguments), 함수선언을 VO에 추가하여 객체화 하기 때문
- 변수 객체와의 순서
	: 아래의 순서로 VO에 프로퍼티와 값을 set함
	- 매개변수(parameter)가 Variable Object의 프로퍼티, 인수(argument)가 값으로 설정됨
	- 대상 코드 내의 함수 선언을 대상으로 함수명이 VO의 프로퍼티로, 생성된 함수 객체가 값으로 설정됨 : 함수 호스팅
	- 대상 코드 내의 변수 선언을 대상으로 변수명이 VO의 프로퍼티로, undefind가 값으로 설정됨 : 변수 호스팅

~3.1.2.1 함수 foo의 선언 처리 까지 정리함~

---
## 참고링크
* [실행 컨텍스트와 자바스크립트 동작원리](http://poiemaweb.com/js-execution-context)
