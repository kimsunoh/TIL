# React 이해
- 리액튼느 자바스크립트 라이브러리이다
	- 유저 인터페이스를 만드는 데 사용
	- 오직 V(view)만 신경씀
- 다양한 유저 인터페이스와 인터렉션을 제공할때 DOM 요소들을 직접 관리하고 코드를 정리하기 위해 사용하는 라이브러리
- `Component`라는 개념에 집중 되어있는 라이브러리
- HTTP 클라이언트, 라우터, 심화적 상태 관리 등의 기는은 내장되어 있지 않음 

## framework vs library

### Angular
- framework
- 앵귤러만의 문법이 있다. 특정 기능을 구현 할 때, 편리하게 대신 해주는 것들이 많다
- 라우터, HTTP 클라이언트 등 웹 프로젝트에서 필요한 대부분의 도구들이 프레임워크 안에 내장되어 있음
- 주로 타입스크립트와 함께 사용됨

### React
- `Component` 개념에 집중되어있는 라이브러리
- 생태계가 넓고 사용하는 곳이 많음
- 오픈소스 라이브러리 이지만, 리더그룹(페이스북)이 있어서 성능과 개발자 경험을 개선하기 위한 연구를 하고 반영함
- 자유도가 높은 라이브러리이다
    - 개발자가 원하는 스택을 골라서 사용 가능
    - 리액트 라이브러리는 뷰 쪽만 관리하게 하고, 나머지 기능은 써드파티 라이브러리가 담당함

### Vue
- progressive javascript framework
- 프로젝트에 점진적으로 채택하며 반영할 수 있음  
    - 다른 자바스크립트 라이브러리를 사용하는 프로젝트에 통합하기 쉬움

# 프로젝트 시작하기
- Component를 여러가지 파일로 분리해서 저장할 예정, Component는 JSX 문법으로 작성한다
    - Webpack 사용 (여러가지 파일을 한개로 결합하기 위해서)
    - Babel 사용 (JSX, ES-N의 문법을 사용하기 위해서)
- react 프로젝트를 제대로 작업 하려면 Node, yarn, Webpack, Babel 등의 도구가 설치되어 있어야 한다

## 환경설정
```
# nvm 설치
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# node install
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
nvm install --lts

brew install yarn --ignore-dependencies

yarn global add create-react-app

npm install -g eslint

create-react-app learning-javascript

cd learning-javascript
eslint --init

yarn start # react app 기동
```

# JSX
- ```import React, {Component} from 'react' ```는 리액트와 그 내부의 Component를 불러오는 것
    - JSX를 사용하려면 꼭 React를 import 해줘야 한다
    - import가 가능한 것은 webpack을 사용하기 때문에 가능한 작업

## React Doc 실습 코드
```jsx harmony
import React, {Component} from "react";
import "./App.css";

const name = "Kim sno";

function formatName(user) {
	if (user) {
		return user.firstName + " " + user.lastName;
	} else {
		return <h1>Not found user</h1>;
	}
}

let user = {
	firstName: "sno",
	lastName: "kim"
}

let element = (<h1>Hello, {formatName(user)}</h1>);

const createElement = React.createElement("h1", {className: "greeting"}, formatName(user) + ", Hi!");

function intervalRend() {
	const createElement = React.createElement("h1", {className: "greeting"}, formatName(user) + ", Hi! " + new Date().toLocaleTimeString());

	ReactDOM.render(
		createElement,
		document.getElementById("root")
	);
}

setInterval(intervalRend, 1000);
``` 

# Components and Props
- Components는 UI를 independent 하게 분할할 수 있게 해준다. 

---

# shouldComponentUpdate
- 변화가 있는 컴포넌트만 랜더링 하도록 하는 것
    - 변화가 없는 컴포넌트는 재렌더링 하지 않도록 함
- 구현하지 않았을 시에는 ```return true;```로 처리되도록 default 구현되 있

--- 
*[React & Expression를 이용한 웹 어플리케이션 개발하기 -  by.velopert](https://www.inflearn.com/course/react-강좌-velopert)*

# React.js
- javascript library

## 장점과 단점

### 장점
- VirtualDOM
- 배우기 간단하다
    - 복잡함이 별로 없어서 
        - 코드를 분리하지 않고 component만 관리하기 때문에 복잡함이 없다
- 뛰어난 GC
    - 메모리 관리, 성능이 효율적이다
- 서버 & 클라이언트 렌더링이 가능하다
    - 초기 구동 딜레이 & SEO (검색엔진최적화)
        - 초기에 서버에서 만든 html을 뿌릴수 있다
        - SEO 
- 매우 간편한 UI 수정 및 재사용성
- 다른 프레임워크나 라이브러리와 혼용가능

### 단점
- view only
- IE8 이하  지원 안함
    - react version 14 이하버전을 사용하고, 이를 호환시켜주는 polyfill을 사용하면 사용 가능

## 실습

### JSX
- javascript 사용 : {...javascript code...}
- JSX안에서 style을 사용할 때는 key가 camelCase인 객체가 사용된다

### props
- 컴포넌트 내부의 immutable Data
- JSX 내부에 {this.props.propsName}
- 컴포넌트를 사용 할 때, <> 괄호 안에 propsName="value"
- this.props.children은 기본적으로 갖고있는 props로서, <Cpnt> 여기에 있는 값들이 들어간다 </Cpnt>

#### defaultProps : 기본값 설정
- Component의 선언이 끝난후, ```ComponentName.defaultProps = {...}```로 설정
```jsx harmony
class ToyComponent extends Component { render() { return ({ /*...*/ }); }}

ToyComponent.defaultProps = {
  name:'Unknown'
}
```

#### propsType : props data type설정
- props 값의 data type을 설정함
```jsx harmony
class ToyComponent extends Component { render() { return ({ /*...*/ }); }}

ToyComponent.propTypes = {
  name:React.PropTypes.string,
  number:React.PropTypes.number.isRequired
}

ToyComponent.defaultProps = {
  name:'Unknown',
  number:0
}
```

### state
- 유동적인 데이터
- JSX 내부에 {this.state.stateName}
- 초기값 설정이 필수, 생성자(constructor)에서 this.state = {}로 설정
- 값을 수정할 때에는 this.setState({...}), 렌더링 된 다음엔 this.state = 절대 사용하지 않아야한다
    - this.state 에 직접 대입 연산자를 사용하는 것은 react의 일부 component만 리렌더링하는 장점을 사용하지 않는 것. 즉, react의 컨셉을 무시하는 행동
    - *즉, ```state```에는 페이지에 렌더링되는 정보들이 저장되어야함*

### Component Mapping
- 데이배열을 리액트에서 렌더링할 땐, JS 내장함수인 ```Map```을 사용한다
- map() 메소드는 파라미터로 전달 된 함수를 통하여 배열 내의 각 요소를 처리해서 그 결과로 새로운 배열을 생성한다
    - map() 함수 call할때의 파라미터 ```arr.map(callback[, thisArg])```
        - callback: 새로운 배열 요소를 생성하는 함수. 세가지 인수를 가진다
            - currentValue: 현재 처리되고 있는 요소
            - index: 현재 처리되고 있는 요소의 index 값
            - array: 메소드가 불려진 배열
        - thisArg: callback 함수 내부에서 사용 할 this 값을 설정
- e.g.
```jsx harmony
let number = [1,2,3,4,5];

let result = numbers.map((num) => {
	return num*num;
});
```

### 절대경로로 파일 불러 올 수 있도록 설정하기
- `.env` `NODE_PATH` 설정
```
NODE_PATH=src
```
- `jsconfig.json` 에디터 설정
```json
{
  "compilerOptions": {
      "baseUrl": "./src"  // all paths are relative to the baseUrl
  }
}
```

## ReactProject 만들기
- ```package.json```의 ```scripts```에서 프로젝트 build 시에 사용 할 수 있는 스크립트를 설정할 수 있다

## Component LifeCycle API
- component 생성 & 완료 API
    - constructor
    - componentWillMount
    - render
    - componentDidMount
- prop 변화 & 업데이트 & 완료
    - componentWillReceiveProps
    - shouldComponentUpdate
        - component가 업데이트가 되었는지 판단하는 API
        - 판단 로직에서 ```false```가 리턴되면, component에 대한 lifecycle이 멈
    - componentWillUpdate
    - render
    - componentDidUpdate
- stete 변화
    - 바로 shouldComponentUpdate 실행
    - 나머진 위와 같은 실행순서
- component 제거
    - componentWillUnmount

## localStorage
- html5부터 지원되는 저장 공간
- cookie와 비슷함
    - 다른점은 저장용량, localStorage는 server로 전송되지 않음, localStorage는 text형태로만 저장이됨
```
localStorage.state = JSON.stringify(object); // 저장할 때
JSON.parse(localStorage.state); // 꺼내서 사용할 때
```



---
## 참고링크
- [React Docs](https://reactjs.org/docs/hello-world.html)
- [더북 리액트를 다루는 기술](https://thebook.io/006946/)
- [누구든지 하는 리액트 by.velopert(김민준)](https://react-anyone.vlpt.us)
- [누구든지 하는 리액트 by.velopert(김민준) inflearn 강의](https://www.inflearn.com/course/react-velopert/)

---
## 기타 참고 링크
- [react-router quick start](https://reacttraining.com/react-router/web/guides/quick-start)