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
- 

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
- 

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
    - 인스턴스
 
## scope chain
- 내부함수에서의 우회법
- Object의 내부 function에서 object의 this객체를 변수에 저장해 object 자체의 scope를 탐색하는 방법

