# JavaScript

# BrowserAPI
- 브라우저에 설치된 API

## DOM (Document Object Model) API
- 동적으로 페이지의 스타일을 정하는 등 HTML, CSS를 조정하는 역할

## Geolocation API
- 지리적인 정보 탐색 및 제공하는 역할

## Canvas & WebGL API
- 2D와 3D 그래픽을 만들 수 있도록 해줌
- e.g. Chrome Experiments, webglsamples

## HTMLMediaElement, WebRTC, Audio and Video API
- 멀티미디어를 활용할 수 있는 기술 지원
    - e.g. 음악, 비디오를 웹 페이지 상에서 재생하고, 웹캠으로 캡처하고 다른 컴퓨터에 표시하는 등 

# 리터럴과 변수, 상수, 데이터타입
- const, let, var
    - const, 상수
    - let, 범위 지정 (블록) 변수
    - var, 변수
- literal
    - 값을 프로그램 안에서 직접 지정한다

## 데이터타입

### 객체된 객체 타입
- Array
- Date
- RegExp
- Map과 WeakMap
- Set과 WeakSet
- Symbol

### 원시타입
- Number
    - 모든 숫자는 Double이다
- String
    - unicode문자열 텍스트
- Boolean

### null & undefined
- null이 가질 수 있는 값은 null 하나, undefined가 가질 수 있는 값은 undefined 하나임
- 존재하지 않는 값을 나타냄
- 굳이 구분하자면
    - null : 프로그래머에게 허용된 데이터 타입
    - undefined : 자바스크립트 자체에서 사용하는 타입
        - 규칙이 강제는 아니지만(개발자도 사용은 할 수 있음), 꼭 필요할 때만 사용하도록 주의해야함
            - e.g. 아직 값이 주어지지 않은 변수의 동작을 고의로 흉내내야 할 때
- 변수의 값을 모르거나 적용할 수 없는 경우에는 대부분 null이 더 나은 선택이다
- 변수를 선언하기만 하고 명시적으로 값을 할당하지 않으면 그 변수에는 기본적으로 undefined가 할당됨

### Object
- 본질은 container
    - 컨테이너의 내용물은 시간이 지나면서 바뀔 수 있지만, 내용물이 바뀐다고 컨테이너가 바뀌는 건 아니다
- object의 content는 property 또는 member 라고 부른다
- property는 key&name으로 구성됨

### Map & Set, WeakMap & WeakSet
- ES6에서부터 생긴 데이터타입
- Map은 Object와 비슷하지만, 특정상황에서 객체보다 유리한 부분이 있음
- Set은 중복이 허용되지 않고, 순서가 없다
- Weak* 는 기존의 것과 동일하게 동작하지만, 특정 상황에서 성능이 더 높아지도록 일부 기능을 제거한 버전

# 제어문
- 조건문과 반복문 두가지로 나뉜다

## for ... of
- ES6에서 새로 생긴 반복문, 컬렉션의 요소에 루프를 실행하는 방법
- iterable 객체에 모두 사용할 수 있는 범용적인 루프
```javascript
for(variable of object)
    statement
```

# expression과 operator

## expression
- expression은 값으로 대체될 수 있는 문장
    - 결과가 값으로 되어 있음

## operator

### 비교연산자
- strict equality : ===
```javascript
console.log(`33` === 33 ? true : false ); // false
```
- loose equality : ==
    - 두 값이 같은 객체를 가리키거나 같은 값을 갖도록 변환할 수 있다면 두 값을 동등하다고 한다
```javascript
console.log(`33` == 33 ? true : false ); // true 
```
   - 문자열은 미리 숫자로 변환해서 일치하는지 비교해야함 (권장)

## 숫자비교
- NaN은 그 자신을 포함하여 무엇과도 같지 않다
    - 숫자가 NaN인지 알아보려면 isNaN 함수를 사용해야한다
- JS의 모든 숫자는 더블 형식이다. 더블 형식은 근사치이므로 숫자비교를 할 때 주의해야한다


### 숫자형 상수 Number.EPSILON
- 약 2.22e-16 정도의 매우 작은 값
- 숫자 두 개를 구별하는 기준으로 사용한다
```javascript
let n = 0;
while(){
    n += 0.1;
    if(n === 0.3) {
        console.log(`strict true`);
        break;
    }
    
    if(Math.abs(n-0.1) < Number.EPSILON ){
        console.log(`EPSILON true`);
        break;
    }
}
```

## 논리연산자
- 논리값
    - false : undefined, null, false, 0, NaN, ``(빈문자열)
    - true : 모든 객체, 배열, 공백만 있는 문자열, 문자열 `false` etc

## 비트연산자
| 연산자 | 설명 |
| :--- | :--- |
|& | 비트 AND|
| \|  | 비트 OR|
|^ | 비트 XOR|
|~ | 비트 NOT|
|<< | 왼쪽 시프트|
|>> | 오른쪽 시프트|
|>>> | Zeso-fill 오른쪽 시프트|

## destructuring assignment (해체할당)
- 객체나 배열을 변수로 `destructuring` 할 수 있는 기능
- 객체를 destructuting 할 때는 반드시 변수 이름과 객체의 프로퍼티 이름이 일치해야함
    - property이름이 유효한 식별자인 property만 해체 후 할당된다
```javascript
// Object의 destrictuting assignment 

// 개체선언
const obj = {b:2, c:3, d:4};

// destructuting assignment
const {a,b,c} = obj;
a;  // undefined, obj에는 `a` 프로퍼티가 없다
b;  // 2
c;  // 3
d;  // ReferrenceError, `d`는 정의되지 않음
```
- 배열을 해체할 때는 배열 요소에 대응할 변수 이름을 마음대로 쓸 수 있음
    - 이들은 배열 순서로 대응함, 일부는 지정하고 나머지 요소는 spread operator를 사용하면 남은 요소를 새 배열에 할당할 수 있다

# Function
- 하나의 단위로 실행되는 문의 집합

## 함수 호출과 참조
- JS에서는 함수도 Object이다
    - 다른 객체와 동일하게 넘기거나 할당할 수 있다
- 함수 호출과 참조의 차이를 이해하는 것이 중요함 

### 매개변수 해체
```javascript
function funca({a, b, c}) {}

funca({a:1, b:123, c:aa});
```

### 매개변수 기본값
- ES6에서 추가된 기능
- 매개변수에 default value를 지정하는 기능
```javascript
function funca(a, b=`default`, c=33}) {}
```
- default값을 설정하지 않은 매개변수에 값을 제공하지 않으면 undefind가 값으로 할당됨

## Enhanced Object Literals
- ES6에서 객체 리터럴은 선언문에서 프로토타입 설정, foo:foo 선언을 위한 단축 표기법, 메서드 정의, super 클래스 호출 및 동적 속성명을 지원하도록 향상 되었다
```javascript
let obj = {
    // __proto__
    __proto__ : theProtoObj,
    
    // `foo :foo` 의 단축 표기
    foo,
    
    // Methods
    toStroing() {
        // Super calls
        return `d ` + super.toString();
    }
}
```

## Arrows function
- => 문법을 사용하는 축약형 함수
- 표현식의 결과 값을 반환하는 expression bodiles 뿐만 아니라 statement block bodies도 지원한다
- 코드의 lexical scope를 가리키는 lexical this를 가진다
    - 일반 함수의 자신을 호출하는 객체를 가리키는 dynamic this와 다름
```javascript
var evens = [2,3,4,5,];

// Expression bodies (표현식의 결과가 반환됨)
var addNums = evens.map(v => v + 1); // [3,4,5,6]
var nums = evens.map((v, i)=> v + i); // [2,4,6,8]
var pairs = events.map(v => ({even: v, odd: v+1})); // [{even: 2, odd: 3}, ...]

// Statement bodies (블럭 내부를 실행만 함, 반환을 위해선 return을 명시)
nums.forEach(v=> {
    if (v % 5 === 0)
        fives.push(v);
});

// Lexical this
var bob = {
    _name : `kimsunoh`,
    _subject : [`javascript`, `ES6`, `React`, `babel`,],
    printSubjects() {
        this._subject.forEach( s => console.log(this.__name + ` learn to ` + s ));
    }
}
```

## call, apply, bind

### call
- 정의된 함수를 호출하면서 `call`을 사용하고 this로 사용할 객체를 넘기면 해당 함수가 주어진 객체의 method인 것처럼 사용할 수 있다
```javascript
const bruce = {name:`Bruce`};

function sayHello() {
    return `Hello, I`m ${this.name}!`;
}

sayHello.call(bruce); // Hello, I`m Bruce
```
- 매개변수는 call(this로 사용할 객체 [, args ...])

### apply
- 함수 매개변수를 처리하는 방법을 제외하면 call과 완전히 같다
- apply는 매개변수를 배열로 받는다
    - call은 매개변수를 직접 받는다

### bind
- 함수의 this 값을 변경할 수 있다

# 배열과 배열 처리
- 배열은 객체와 달리 본질에서 순서가 있는 데이터 집합이다
- 0으로 시작하는 숫자형 인덱스를 사용한다
- 자바스크립트의 배열은 nonhomogeneous(비균질적)하다
- 배열 자체를 method의 실행결과가 배열 자체를 수정하는 것과 사본반환을 하는 것으로 나뉜다
    - 배열 자체를 수정 : push, pop, unshift, shift, splice, copyWhithin, fill, reverse, sort, reduce
    - 사본 반환 : concat, slice, map, filter, join

# Object & OOP
- 문법
```javascript
class Car {
    constructir() {
        
    }
}

const car1 = new Car();
car instanceof Car // true
```
- (ES6 전까지) 클래스를 만든다는 것은 곧 클래스 생성자로 사용할 함수를 만든다는 의미, class 문법이 생기며 직관적이고 단순한 문법으로 표현할 수 있게됨
    - class == function

## prototype
- 자바스크립트 객체는 속성을 저장하는 동적인 `Object`와 prototype 객체에 대한 링크를 가진다
- 객체의 어떤 속성에 접근하려 할 때 그 객체 자체 속성뿐만 아니라 객체의 prototype, 그 prototype의 prototype 을 타고 prototype 체인의 끝까지 타고 올라가 속성을 탐색한다
- 프로토타입 체인의 길이는 성능을 저해하지 않도록 줄이는 방법을 고안해야 한다
**- 빌트인 프로토타입은 새로운 자바스크립트 기능과 호환성을 갖기 위한 이유가 아닌 이상 절대 확장해서는 안된다**
- 속성 접근 순서
    1. 새 객체의 속성에 접근할 떄, 해당 객체가 직접적으로 속성을 소유하고 있는지 먼저 체크한다
    2. 없다면, [[Prototype]]을 체크한다
    3. 1-2를 프로토타입 체인을 따라서 모든 객체의 프로토타입 체인의 최상위에 있는 객체인 Object.prototype에 도달할 때 까지 반복한다

### prototype 상속의 종류

#### Delegation inheritance (위임형 상속)
- Delegation 상속에서 prototype의 객체는 다른 객체의 기반이 된다
    - Delegation prototype을 상속받을 경우 새 객체는 해당 프로토타입에 대한 참조를 가지고 있다
- 장점
    - 메소드를 위임 상속할 경우 모든 객체가 각 메소드에 대해 하나의 코드를 공유하므로 메모리를 절약할 수 있다
- 단점
    - 객체나 배열의 상태를 변경하게 되면 같은 프로토타입을 공유하는 모든 객체의 상태가 변경된다
        - 상태를 저장하는데 그리 좋은 방법이 아니라는 점
        - 상태 변경이 전파되는 것을 막으려면 각 객체마다 상태 값의 복사본을 만들어야 한다
```javascript
class Greeter {
    constructor (name) {
        this.name = name || `Jhon Doe`;
    }
    
    hello() {
        return `Hello, my name is ${ this.name }`;
    }
}

const george = new Greeter(`George`);
const msg = george.hello();
console.log(msg); //Hello, my name is George
```

#### Concatenative inheritance (연결형 상속)
- 연결형 상속은 한 객체의 속성을 다른 객체에 모두 복사함으로써 상속을 구현하는 방법
- Javascript 객체의 동적 확장성을 이용한 방법
    - 객체 복사는 속성의 초기값을 저장하기 위한 방법
- 클로져와 같이 사용한다면 훨씬 효과적으로 사용할 수 있는 상속방식
```javascript
const proto = {
    hello: function hello() {
        return `hello, my name is ${ this.name }`;
    }
}

const george = Object.assign({}, proto, {name: `George``});
const msg = george.hello();
console.log(msg); // Hello, my name is George
```

#### Funcional inheritance (함수형 상속)
- 새 속성들을 연결형 상속으로 쌓되 상속 기능을 Factory함수로 만들어 사용하는 방식
- 기존의 객체를 확장하는데 쓰이는 함수를 일반적으로 믹스인 함수라 칭한다. 객체 확장에 함수를 사용하는 가장 큰 이점은 Private Data를 클로져를 통해 캡슐화 시킬 수 있다는 점
    - private 상태를 지정할 수 있다는 의미
- 특정 함수를 통할 필요 없이 public 접근이 가능한 속성에 대해 접근 제한을 거는 것은 문제가 있다. 따라서, private 클로져에 속성 값을 숨겨야 하며 이는 아래와 같이 구현한다
```javascript
const rawMixin = function() {
    const attrs = {};
    return Object.assign(this, {
        set(name, value) {
            attrs[name] = value;
            this.emit(`change`, {
                prop: name,
                value: values
            })
        },
        get(name) {
            return attrs[name];
        }
    }, Events.prototype);
}

const mixinModel = (target) => rawMixin.call(target);
const george = {name: `george`};
const model = mixinModel(george);
model.on(`change`, data => console.log(data));
model.set(`name`, `Sam`);
```
- `attrs`을 public 속성에서 private 영역으로 옮겨서 public API를 통해 접근을 차단할 수 있다
    - 접근할 수 있는 유일한 방법은 Privileged 메소드를 사용하는 방법
        - Privileged : 클로져 영역에 정의된 함수로 private data에 접근 가능한 함수들을 일컫는다

- 
---
## 참고링크&문헌
- [learning javascript](http://www.yes24.com/Product/Goods/18723024)
- [JSDEV ES6문법 정리](https://jsdev.kr/t/es6/2944)
- [MDN Javascript Docs](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide)
