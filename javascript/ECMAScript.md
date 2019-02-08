# ECMAScript
*ECMAScript는 본 문서에서는 ES로 표기했습니다*
- Ecma international의 ECMA-262 기술 규격에 정의된 표준화된 `스크립트 프로그래밍 언어`
- JavaScript, JScript와는 다른 스크립트 언어
- JavaScript 명세

## JavaScript, JScript 다른점
- 1997년 6월 ECMA-262의 초판이 발행된 이후, ECMA-262 기술 규격에 맞추어 표준화된 언어
- JavaScript, JScript는 모두 ECMAScript와의 호환이 목표
    - 두 언어는 규격에 포함되지 않은 확장 기능을 제공
- JavaScript, JScript가 만들어진 이후 표준 규격이 정해지고, 이후 ES가 만들어짐

# JavaScript 동향 (2016 참고)

## React
- MV* 구조에서 View 영역에 대한 구현체
- UI쪽 DOM 관리 Library
    - Service에 해당하는 영역은 다루지 않음
        - 데이터 흐름과 액션을 처리하는 도구(e.g. Flux), 데이터 상태를 관리하는 컨테이너 (e.g. Redux)를 함께 사용하는 경우가 많음

### 특징
- virtual Dom
- data binding

## AngularJs

### 특징
- Aurelia 프레임워크를 참조하지 않고도 ES6의 객체를 사용한 애플리케이션 개발 가능
    - ES 표준이 적용이 될 때, 코드를 큰 어려움 없이 바로 적용 할 수 있게됨

## WebComponent
- 주요 프레임워크와 컴포넌트 인터페이스 개발등에 포함되는 웹 표준 기술 모음

### WebComponent를 이루는 4가지 표준기술
- Custom element : 사용자 정의 태그를 이용한 요소 생성
- HTML import : HTML 페이지 로딩
- HTML template : 템플릿
- Shadow DOM : DOM과 스타일의 캡슐화

## Node.js
- V8~(Google의 JavaScript 엔진)~을 기반으로 한 오픈소스, 런타임 환경을 제공
- 엔터프라이즈 영역에서 기존 .NET, JAVA를 대체해 도입되고 있음

# 주요키워드
- Transpiler 

---
## 참고문헌
- [wikipedia korea ECMA스크립트](https://ko.wikipedia.org/wiki/ECMA스크립트)
- [wikipedia ECMAScript](https://en.wikipedia.org/wiki/ECMAScript)
- [Naver D2 2016년과 이후 JavaScript의 동향](https://d2.naver.com/helloworld/3618177)
- [Naver D2 2017년과 이후 JavaScript의 동향 - JavaScript(ECMAScript)](https://d2.naver.com/helloworld/2809766)
- [Naver D2 2017년과 이후 JavaScript의 동향 - 라이브러리와 프레임워크](https://d2.naver.com/helloworld/7229119)
- [Naver D2 2018년과 이후 JavaScript의 동향 - JavaScript(ECMAScript)](https://d2.naver.com/helloworld/7495331)
- [javascript is eating the world](https://www.applause.com/blog/javascript-is-eating-the-world/)