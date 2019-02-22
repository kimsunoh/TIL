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
## 참고문헌
- [React Docs](https://reactjs.org/docs/hello-world.html)
- [더북 리액트를 다루는 기술](https://thebook.io/006946/)
- [누구든지 하는 리액트 by.velopert(김민준)](https://react-anyone.vlpt.us)
- [누구든지 하는 리액트 by.velopert(김민준) inflearn 강의](https://www.inflearn.com/course/react-velopert/)