# ES6 (ES2015)
- 개선된 JavaScript 문법
- ES6 browser compatibility의 훌륭한 지원
- ES6를 기반으로 한 JavaScript 생태계 확산

## 전략
- ES6로 개발 > babel로 ES5로 변경해서 지원
	- 거의 모든 브라우저에서 지원 가능

---
*생활코딩 WEB2 강좌*

# WEB2 - JavaScript
- 동적인 페이지를 동적으로 처리하기 위한 스크립트형 언어
- HTML 위에서 동작하도록 만들어짐

## 실습 중 학습내용
- array, for, if else, function 
- 대부분의 프레임워크, 라이브러리가 나오게 된 결정적인 이유는 `중복의 제거` 때문이다

### Event
- tag에 일어난 이벤트를 처리하는 것
- e.g. onclick, onchange, onkeydown

### Data Type (기본자료형)
- Boolean
- Null
- Undefined
- Number
- String
- Symbol
- Object
    - ES6에도 추가

### CSS
- CSS 선택자 
    - class 선택자 : .xxx
    - id 선택자 : \#xxx
    - tag 선택자 : xxx
- tag의 class보다 id 선택자가 더 우선순위가 높다

### function
- input(argument),output(result) 으로 이루어져 있음

### Object & methods
- 객체와 함수의 관계는 함수에서 객체를 사용하는 관계이다
- 생성법
```javascript   
var coworkers = {
    "programmer" : "kimsno",
    "author" : "a. d. 보통"
};
```
- property 사용법
```javascript
alert(coworkers.programmer);
```
- property 순회하는 방법
    - 이 값은 순서를 보장하지 않으므로 순회를 할 때마다 다른 순서로 나올 수 있다
```
for( var key in coworkers ) {
    documenrt.write(coworkers[key]+'<br>');
}
```
- method 정의 방법
```javascript
coworkers.showAll = function() {
    for( var key in this ) {
        documenrt.write(coworkers[key]+'<br>');
    }
} 
or

coworkers[showAll] = function() {...} 

or

coworkers = {
    ...,
    ...,
    showAll : function() {...}
}
```

---
*[inflearn Javascript 핵심 개념 알아보기 - JS Flow (by. 정재남)](https://www.inflearn.com/course/핵심개념-javascript-flow/)*

# javascript Data Type
- primitive type, reference type이 있음

## Primitive Type
- Number, String, Boolean, null, undefined
- 값을 그대로 할당함

## Reference Type
- Object(Array, Function, RegExp)
- 객체가 저장된 주소만 기억함
    - 값이 저장된 주소값을 반환함
- 기본형데이터의 집합
    - 메모리에 저장할 때, 기본형 데이터가 저장될 때까지 value를 저장하는 작업을 반복함
- Nested하다 : reference type 객체 안에 reference type 객체가 있는경우

# Function

## Hoisting
- JS는 변수'선언', 함수'선언'을 끌어올린다
- JS를 파일 로드하면서 선언부를 상단으로 올려서 파일을 load하게 됨
    - 만약 중복 name 함수가 있을 경우, cascading 원칙에 의해서 나중에 선언된 함수의 내용으로 function이 할당됨
- e.g.
    - 작성 code
```javascript
console.log(a());

function a() {
    ...
}

var b = function() {...}
```
   - 실제 load된 코드순서 
```javascript
function a() {
    ...
}

var b;

console.log(a());

b = function() {...}
```

## Function declaration vs Function expression
- named function expression을 사용하는 곳이 거의 없어짐
    - browser의 지원이 확대되며 필요성이 없어짐
- Douglas Crockford는 **`unnamed/annonymous` function expression의 사용을 권장**함
    - 중복 named 함수의 처리, 함수 선언의 불필요성 등등 

### Function declaration (함수선언문)
```javascript
function a() {
    return 'a';
}
```

### named function expression (기명 함수표현식)
```javascript
var b = function bb() {
    return 'bb';
}
```

### (unnamed/annonymous) function expression ((익명) 함수표현식)
```javascript
var c = function() { //변수 선언 & 익명함수 선언
    return 'c';  // 변수에 익명함수를 할당
}
```

## Fcuntion scope, Execution context

### Scope
- 변수의 유효범위
- 함수가 정의될 때 결정됨
    - 함수의 context가 정의될 때 생성됨 
- Global Scope & Global Context, function Scope & function Context

### Execution context
- 함수가 실행이 될 때 결정됨
- 실행자가 함수를 호출했을 때 내부적으로 함수를 실행하기 위한 정보를 저장해 놓은 것
    - 실행되는 코드덩어리
    - 추상적 개념
    - 호이스팅, this 바인딩 등의 정보가 담긴다

## Method
- Method는 this를 binding 함
    - function과의 차이는 this를 binding 하는가 안하는가
- Object method

## callback function
- something will call this function back sometime somehow.
- 제어권을 넘기고 맡기는 것, 제어권을 대상에게 넘겨주면 대상이 제어권을 다시 넘겨주는 것
- 함수가 매개변수로 콜백함수를 전달받으면, 콜백함수의 제어권을 전달받은 함수가 제어권을 갖게된다
- 특별한 요청(bind)이 없는 한, 함수에 정해진 방식에 따라 콜백함수를 호출한다 
- callback 함수는 
    
### function list

#### setInterval(callback, millisecond);
- callback 함수는 setInterval 함수의 제어로 millisecounds마다 실행된다.
- e. g.
```javascript
setInterval(function() {
    console.log('1초마다 실행될 겁니다.');
}, 1000); 
// setInteval(callback, millisecounds)
```

#### arr.forEach(callback[, thisArg]);
- callback.call(currentValue, index, array)
- e.g. (by. [MDN example](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach))
```javascript 
function Counter() {
  this.sum = 0;
  this.count = 0;
}

Counter.prototype.add = function(array) {
  array.forEach(function(entry) {
    this.sum += entry;
    ++this.count;
  }, this);
};

var obj = new Counter();
obj.add([2, 5, 9]);
obj.count
// 3
obj.sum
// 16
```

#### element.addEventListener(type, listener[, useCapture]);
- param example
    - type : 등록할 event type을 나타내는 문자열
    - listener :  특정타입의 이벤트가 발생할 때 알림을 받을 객체, 반드시 EventListener 인터페이스를 수하는 객체이거나, javascript function 이어야 한다

# this

## 호출하는 위치에 따른 값
- 전역함수, 함수 내부에서 호출시 window(전역객체)를 처리
    - default가 window로 되어있다
    - function은 전역 method라 생각하면 유추하기 편하다
- method 내부에서
    - 메소드 호출 주체 
- callback에서
    - 기본적으로 함수 내부에서 호출하는 것과 동일
    - bind, call, apply
- 생성자 함수에서
    - 인스턴
 
## scope chain
- 내부함수에서의 우회법
- Object의 내부 function에서 object의 this객체를 변수에 저장해 object 자체의 scope를 탐색하는 방법

# Closure
- 함수와 함수가 선언된 정보를 담은 lexical enviroment의 조합이다
    - 함수와 "그 함수가 선언될 당시의 환경정보"사이의 조합
- 함수 내부에서 생성한 데이터와 그 유효범위로 인해 발생하는 특수한 현상/상태 
    
## lexical enviroment
- 사전적인 한경
- 선언 당시의 환경에 대한 정보를 담는 객체, **변하지 않음**
- return function을 하게되면 변하지 않는다
    
## 사용 방법
- 접근 권한 제어
- 지역 변수 보호
    - function의 내부에 선언된 변수의 경우 외부에선 호출 불가능하다
- 데이터 보존 및 활용
    - function a()을 외부의 변수 c에 생성한다면, c에선 a()내부에 선언된 x값을 가져올 수 있게된다
    - 외부에서 권한을 주려면, 외부에서 접근할 수 있는 권한을 줘야함
        - 함수에서 반환 값에 getter&setter를 넣어서 반환하면 됨 
```javascript
function a() {
    var _x = 1;
    return {
        get x() { return _x; },
        set x(v) { _x = v; }
    }
}

var c = a();
c.x = 10;
```
    - 이렇게 되면 `_x`에 대해서는 직접적으로 접근을 할 수는 없지만, getter&setter를 이용해서 접근 할 수 있게됨
```javascript
function setCounter() {
    var count = 0;
    return function() {
        return ++count;
    }
}

var count = setCounter();
count(); // count에는 setCounter의 익명함수가 들어있음. 그러므로 named function으로 count()가 전역에 선언되어 있지 않으면 count()를 실행했을 때. 익명함수가 실행되고 그 결과가 return 되게 됨 
```

## private member
- 외부에서 값을 변경할 수 없게 만들기 위해서 필요함
    - 값을 변경할 수 없게 하려면, scope 안에 넣으면 되지 않을까?

### 만들기
1. 함수에서 지역변수 및 내부함수 등을 생성한다
2. 외부에 노출시키고자 하는 멤버들로 구성된 객체를 return한다
    - return한 객체에 포함되지 않은 멤버들은 private하다
    - return한 객체에 포함된 멤버들은 public하

# Prototype

## prototype, constructor, __proto__
- constructor로 생성한 instance의 __proto__는 constructor의 prototype과 매칭이 된다
    - prototype이라고 하는 property는 객체이다
        - Array 타입의 prototype엔 array의 function들이 들어있다 
    - instance의 __proto__는 (__proto__)를 `명시하지 않고 접근할 수 있다`

### 접근 방법
- 생성자함수의 prototype에 접근할 수 있는 방법
```javascript
[CONSTRUCTOR].prototype
[instance].__proto__
[instance]
Object.getPrototypeOf([instance])
```
- 생성자함수에 접근할 수 있는 방법
```javascript
[CONSTRUCTOR]
[CONSTRUCTOR].prototype.constructor
(Object.getPrototypeOf([instance])).constructor
[instance].__proto__.constructor
[instance].constructor
```

## method 상속 및 동작 원리
```javascript
function Person(n,a) {
    this.name = n;
    this.age = a;
}

Person.prototype.setOlder = function() { this.age += 1; }
Person.prototype.getAge = function() { return this.age; }
``` 
- 생각해 볼 것, `.prototype`을 명시 했을때와 안했을 때 property `setOlder`를 호출할때의 차이

# Class
- 공통적인 속성을 모아서 한데 묶은 집단
- Class는 어떤 공통된 속성이나 기능을 정의한 추상적인 개념, 이 Class에 속한 객체를 instance라 함. instance에서 접근할 수없는 static method, static property와 instance에서 접근할 수 있는 method,property로 이루어져 있다

## prototype static 메소드 및 static 프로퍼티
- Class의 prototype으로 선언되지 않고 직접적으로 선언되어 있는 method를 `static method`, property를 `static property`라고 한다
- 보통 소속인 instance들의 공동체 여부 확인이나, 소속부여 같은 공동체 적인 처리를 하기위해 사용한다
- instance에서는 static멤버들엔 접근 할 수 없다

## Class 상속 구현
```javascript
function Bridge() {}; //method만 prototype에 받기 위해 커넥션 용으로 사용할 객체
Bridge.prototype = Parent.prototype;
Child.prototype = new Bridge();
Child.prototype.constructor = Child //기본적으로 constroctor를 생성해주므로, 이것을 명시적으로 제시해줘야함 (그렇지 않으면 Parent의 constructor를 prototype으로 갖게됨)
Child.prototype.newfunction = function() { ...; }
``` 
- Douglas Crockford는 Clouser를 사용해서 반복적인 클래스 상속 코드를 Object로 만들어서 사용하길 권고함
```javascript
var extendClass = (function() {
    function Bridge(){}
    return function()(Parent, Child) {
        Bridge.prototype = Parent.prototype;
        Child.prototype = new Bridge();
        Child.prototype.constructor = Child;
        Child.prototype.superClass = Parent;
    }
})();
extendClass(Person, Employee);
Employee.prototype.getPosition = function() {
    return this.position;
}
```

---
*[누구든지 하는 리액트 by.velopert(김민준)](https://www.inflearn.com/course/react-velopert/)*

# React는 무엇인가?
- 프론트엔드 라이브러리
- virtual DOM을 이용해서 DOM을 수정하는 일을 간편하게 하고싶은 마음에서 시작됨
- 웹 개발을 할 때, 귀찮은 DOM 관리와 상태값 업데이트 관리를 최소화하며 기능개발, 인터페이스 구현에 집중할 수 있도록 하기위해 만들어진 프론트엔드 라이브러리

## react 특징
- "component" 개념에 집중한 라이브러리
    - 데이터를 넣으면 우리가 지정한 유저 인터페이스를 조립해서 보여줌
- 생태계가 넓다
    - 다양한 개발자, 회사가 사용하고 피드백과 결과의 순환이 빠르다
- HTTP 클라이언트, 라우터, 심화적 상태관리 등의 기능은 내장되어있지 않음
    - 많이 사용하는 외부 라이브러리 예시
        - 라우터 : React-router, Next.js, After.js
        - 상태 관리 라이브러리 : Redux, ModX, fr(e)actal

## 리액트의 Virtual DOM
- facebook의 생각, "Mutation을 하지 말자. 그 대신에, 데이터가 바뀌면 그냥 뷰를 날려버리고 새로 만들어버리면 어떨까?" 라는 생각에서 시작
    - 기존의 모델들에선 Model이 변경되면 View도 바뀌는 양방향 binding 방식을 사용하고 있었음
- 가능하게 하기 위한것이 Virtual DOM, 변화가 필요한 곳만 Update를 하는 것
    - html 페이지는 DOM 형식으로 되어 있기 때문에, 필요한 위치만 수정하는 것이 불가능 함
- 바뀐 데이터로 그려넣은 다음에 바뀐부분이 어딘지 파악하고 수정하는 것
    - DOM 객체이므로 바뀐 부분을 찾아서 부모까지 올라가서 수정을 함

# React 프로젝트 시작하기

## Webpack
- 코드들을 의존하는 순서대로 하나 이상의 결과물로 만들어내는 역할

## babel
- Javascript변환 도구
- JS의 발전에 따라 문법이 달라졌는데, 그것을 다른 프레임워크들에서 모두 지원을 해주지 않기 때문에, 그것을 지원가능한 문법으로 변화 시켜서 사용하기 위해서 사용함

## 실습
```
# nvm 설치
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# node install
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
nvm install --lts

npm install -g eslint

npx create-react-app learning-javascript

cd learning-javascript
eslint --init

npm start # react app 기동
```

# JSX
- Component를 만들때에는, render()가 반드시 있어야 하고, render()의 return 값은 반드시 JSX여야한다
- 파일에서 JSX를 사용하려면, 꼭 React를 import 해주어야한다
- 가장 상위에있는 element는 무조건 하나여야 한다
    - e.g. ``` <div>...</div>, <Fragement>...</Fragement> // ( V.16.2 이후 ) ```

## css
- Object 객체를 이용해서 선언 후 사용
- `-`를 사용하는 옵션의 경우, 카멜 표기법을 사용해서 대체함
    - e.g. background-color > backgroundColor


*나머지 내용은 [react.md](https://github.com/kimsunoh/TIL/blob/master/javascript/react.md)에 이어서 작성함*


# Props & State

## Props 
- 부모 컴포넌트가 자식 컴포넌트한테 전달될 때 사용된다
- 자식의 입장에선 읽기만 가능함

### code

#### App.js
```jsx harmony
import React, { Component } from "react";
import MyName from "./MyName";

class App extends Component {
  render() {
    return <MyName name="리액트" />;
  }
}

export default App;
```

#### MyName.js 
```jsx harmony 
import React, { Component } from "react";

class MyName extends Component {
    static defaultProps = {
      name: "kimsno"
    };
    
    render() {
        return (
            <div>
                안녕하세요! 제 이름은 <b>{this.props.name}</b>입니다.
            </div>
        );
    }
}

export default MyName; 
```
     
#### MyName.js - 함수형
```
import React from "react";
const MyName = ({ name }) => {
  return <div>안녕하세요. 제 이름은 {name} 입니다.</div>;
};

MyName.defaultProps = { name: "kimsno" };
export default MyName;
```

## State
- 자식 컴포넌트에서 이미 만들어진 객체, 자기자신이 들고있는 객체
- 내부에서 변경 할 수 있다
    - 부모에서 렌더링이 된 후 event를 통해서 값이 변경될 수 있다
- 값을 변경할 때는 언제나 setState라는 함수를 사용한다
    - setState를 사용하지 않으면 rerendering 되지 않는다

### 예시
```jsx harmony
import React, { Component } from "react";

class Counter extends Component {
  state = {
    number: 0
  };

  handleIncrease = () => {
    this.setState({
      number: this.state.number + 1
    });
  };

  handleDecrease = () => {
    this.setState({
      number: this.state.number - 1
    });
  };

  render() {
    return (
      <div>
        <h1>카운터</h1>
        <div>값: {this.state.number}</div>
        <button onClick={this.handleIncrease}>+</button>
        <button onClick={this.handleDecrease}>-</button>
      </div>
    );
  }
}

export default Counter;
```

# LifeCycle API
- Conponent가 우리 화면에서 Mountion(나타날 때), Updating(업데이트 될 때), Unmounting(사라질 때) 각각의 시점 중간에 처리하고 싶은 작업이 있을때 사용할 수 있는 것

## [주요 API](https://react-anyone.vlpt.us/05.html)
- componentDidMount
    - 컴포넌트가 나타나고난 시점에 어떤 작업을 할때 사용한다
    - API를 요청하거나, event를 등록할때
    - DOM에 관련된 작업을 할 때 사용가능
- shouldComponentUpdate
    - virtualDom에 그리는 성능이 아까울때 성능 최적화를 이용해 사용한다
        - 부모컨테이너가 리렌더링 되면 자식 함수들도 다 리렌더링 된다
    - virtualDom에도 render를 할지 말지에 대해서 작업 처리를 할 때 사용
- getSnapshotBeforeUpdate
    - 화면에 Dom이 뿌려지기 전에 Snapshot을 update하는 함수
- componentDidUpdate
    - 컴포넌트가 변경이 되었을 때, 이전의 snapshot과 비교후 업데이트 되었으면 처리를 설정 할 수 있다
- ComponentDidCatch 등등이 있다

