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




---
## 참고링크&문헌
- [learning javascript](http://www.yes24.com/Product/Goods/18723024)