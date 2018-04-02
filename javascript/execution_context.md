# Execution Context( 실행 컨텍스트 )
: scope, hoistiong, this, sunction, closure 등의 동작원리를 담고 있는 자바스크립트의 핵심원리
- 실행 가능한 코드를 형상화하고 구분하는 추상적인 개념
- 실행 가능한 코드가 실행되기 위해 필요한 환경

* 이 문서에서는 Execution Context를 문장에서 'EC'라 표기한다

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


---
## 참고링크
* [실행 컨텍스트와 자바스크립트 동작원리](http://poiemaweb.com/js-execution-context)
