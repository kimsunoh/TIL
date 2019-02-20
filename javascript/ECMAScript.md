# ECMAScript
* ECMAScript는 본 문서에서는 ES로 표기했습니다 *
> ECMAScript is a standard script language

- Ecma international의 ECMA-262 기술 규격에 정의된 표준화된 `스크립트 프로그래밍 언어`
- JavaScript, JScript와는 다른 스크립트 언어
- JavaScript 언어의 표준

## JavaScript, JScript 다른점
- 1997년 6월 ECMA-262의 초판이 발행된 이후, ECMA-262 기술 규격에 맞추어 표준화된 언어
- JavaScript, JScript는 모두 ECMAScript와의 호환이 목표
    - 두 언어는 규격에 포함되지 않은 확장 기능을 제공
- JavaScript, JScript가 만들어진 이후 표준 규격이 정해지고, 이후 ES가 만들어짐

# ECMAScript6
- ECMAScript의 6번째 에디션

## ES6 new Feature
- class 문법 제공
    - extends 를 이용한 상속 가능, constructor 제공
- let & const
    - const : final 변수
    - let : block 지정 변수

### arrow Functions
- 축약형 함수. 

### classes

### object literals

### template iterals
- 템플릿 리터럴은 이중 따옴표나 작은 따옴표 대신 백틱(` `)을 이용한다
- 플레이스 홀더(${expression})를 이용하여 표현식을 넣을 수 있다 
- multi-line
```javascript
`string test line 1
string txt line 2`
```
- expression interpolation (표현식 삽입법)
```javascript
var a = 5;
var b = 10;
console.log(`Fifteen is ${a + b} and 
not ${2 * a + b}.`);
```

### destructuring
- 배열과 객체에 패턴 매칭을 통한 데이터 바인딩을 제공함
- 구조 분해 할당
- 할당 실패에 유연하며, 실패시 undefined 값이 자동할당된다

### default + rest + spread 
- function의 인자값에 default,rest parameter를 설정할 수 있게 되었다
- func을 호출할 때 spread argument 배열을 일련의 인자에 나누어 주입시킬 수 있게 되었다   

#### rest parameter
- 구분된 이름이 주어지지 않은 유일한 대상
- Array 인스턴스이다
- 함수의 마지막 파라메터 앞에 `...`를 붙여 (사용자가 제공한) 모든 나머지 인수를 "표준" 자바스크립트 배열로 대체한다
- 마지막 파라미터만 "Rest 파라미터"가 될 수 있

### let + const
- let : 블록 유효 범위를 갖는 새로운 변수 선언
    - var의 유효 범위는 전체 외부 함수까지 이지만 let은 변수를 선언한 블록과 그 내부 블록들에서 유효하다
- const : 재할당 및 재선언이 불가능함

### iterators + for...of

#### for ...of 반복문
- ES6에 추가된 컬렉션 전용 반복 구문
- for of 구문을 사용하기 위해선 컬렉션 객체가 [Symbol.iterator] 속성을 가지고 있어야만 한다

#### for ...in 반복문
- 객체의 모든 열거 가능한 속성에 대해 반복
- 모든 객체에서 사용가능
- 객체의 key값에 접근할 수 있지만, value값에 접근하는 방법은 제공하지 않는다

```javascript
Object.prototype.objCustom = function () {};
Array.prototype.arrCustom = function() {};

var iterable = [3,5,7];
iterable.foo = "hello";

for( var key in iterable ) { console.log(key); }
/*
0
1
2
foo
isArray
compact
each
contains
copy
size
uniq
getFirst
getLast
arrCustom
objCustom
*/

for( var key of iterable ) { console.log(key); }
/*
3
5
7
*/
```

### generators
- function*와 yield 키워드를 이용하여 iterator 선언을 단순하게 작성할 수 있게 도와준다
- function*로 선언한 함수는 Generator 객체를 반환한다
- Generator는 iterator의 하위 타입이며 next와 throw 메서드를 가지고 있다
- 이 메서드들로 인해 yiled 키워드로 반환된 값은 다시 generator에 주입하거나 예외처리를 할 수 있게 되었다

### unicode
- 완전한 유니코드를 지원하기 위해 문자열에 새로운 유니코드 리터럴과 정규표현식에 u모드가 추가됨
- 21비트 형식까지 처리하기 위한 신규 API가 추가됨

### modules
- 언어 차원에서 컴포넌트 정의를 위한 모듈을 지원함
- 유명한 JavaScript 모듈 로더들(AMD,CommonJS)의 패턴을 적용함
- 런타임 동작은 호스트에 정의된 기본 로더에 의해 정의됨
- 묵시적 비동기 형태로 요구되는 모듈들이 정상적으로 로드 되기 전까지 코드가 실행되지 않음

### module loaders
- 지원하는 것
    - Dynamic loading (동적로딩)
    - State isolation (상태격리)
    - Global namespace isolation (전역 네임스페이스 격리)
    - Compilation hooks (컴파일 훅)
    - Nested virtualization (중첩 가상화)
```javascript
System.import('lib/math').then(function(m){ // Dynamic loading
    console.log('2π = ' + m.sum(m.pi, m.pi));
});

var loader = new Loader({ // 실행 샌드박스 생성
    global: fixup(window)
});
loader.eval('console.log("hello, world!");')

System.get('jquery'); //모듈 캐시 직접 조작
```


### map + set + weakmap + weakset
- key, value로 이루어진 map, 그것보다 더 갼략한 prototype을 갖고 있어 속도가 더 빠르게 나타나는 weakmap
- 중복 값을 허용하고 있지 않는 set, 더 간략한 weakset
- weak* 들은 메모리 누수를 자동으로 관리해준다
    - 이들 내에 저장된 객체에 다른 참조가 없는 경우, garbage collection 될 수 있다 

### proxies
- 호스트 객체에 다양한 기능을 추가하여 객체를 생성할 수 있다
- interception, 객체 추상화, 로깅/수집, 값 검증 등에 사용될 수 있다
- Proxy 객체는 기본적인 동작(속성 접근, 할당, 순회, 열거, 함수 호출 등)의 새로운 행동을 정의할 때 사용한다
    - ES6에서 추가된 메타프로그래밍 기능. 프로그램이 자기 자신을 수정하는 것을 가능하게 한

### Symbols
- 객체 상태의 접근 제어를 가능하게 한다
- Symbol은 새로운 원시 타입으로 이름 충돌의 위험 없이 property(속성)의 key로 사용할 수 있다
- 옵션 파라미터인 description은 디버깅 용도로 사용되며 식별 용도는 아니다
- Symbol은 unique하며, Object.getOwnPropertySymbols와 같은 reflection 기능들로 접근할 수 있기 때문에 private gkwls  dksgek

### subclassable built-ins

### promises

### math + number + string + array + object APIs

### binary and octal literals

### reflect api

### tail calls
    
---
## 참고링크
- [wikipedia korea ECMA스크립트](https://ko.wikipedia.org/wiki/ECMA스크립트)
- [wikipedia ECMAScript](https://en.wikipedia.org/wiki/ECMAScript)
- [ecma international](https://www.ecma-international.org/ecma-262/6.0/)
- [자바스크립트 개발자 포럼 ES6 문법 정리](https://jsdev.kr/t/es6/2944)
- [GitHub ES6시대의 JavaScript](https://gist.github.com/marocchino/841e2ff62f59f420f9d9)
- [HACKS ES6 In Depth: 심볼 (Symbol)](http://hacks.mozilla.or.kr/2015/09/es6-in-depth-symbols/)

