# Webpack
- (자바스크립트) 모듈 번들러
- 코드가 많아지면 하나의 파일로 관리하는데 한계가 있고, 여러개의 파일을 브라우저에서 로딩하는 것은 네트워크 비용이 들게되면서 관리를 퍈하게 하기위해 말들어진 툴
- 주요한 네가지 개념이 있다
    - entry, output, loader, plugins
- 터미널에서 ```webpack``` 커멘드로 빌드 할 수 있다
- webpack4의 문법이 이전 버전보다 접근이 쉬워졌 

## entry
- 의존성 그래프의 시작점
- webpack은 entry를 통해서 필요한 모듈을 로딩하고 하나의 파일로 묶는다
    - webpack에서 모든것은 모듈이다
```jsx harmony
module.export = {
	entry: {
		main: './src/index.js'
	}
}
```

## output
- 번들된 결과물을 처리할 위치를 기록하는 설정값
    - entry에 설정한 JS파일을 시작으로 의존되어 있는 모든 모듈을 하나로 묶은 후 저장할 정보
```jsx harmony
module.export = {
	output: {
		path: './dist',
		filename: 'bundle.js'
	}
}
```
- html 파일에서는 번들링된 파일 ```bundle.js```를 로딩한다
```html
<body>
    <script src="./dist/bundle.js"></script>
</body>
```

## loader
- none-JS file을 webpack이 이해하게 설정해수는 부분
- webpack은 JS 파일만 읽을 수 있으므로, 어떤 표현식을 사용한 파일인지 명시해 주는 부분

---
1.
```
$ npm install -g webpack webpack-dev-servers
```
- webpack: 브라우저 위에서 import(require)를 할 수 있게 해주고 자바스크립트 파일들을 하나로 합쳐준다
- webpack-dev-server: 별도의 서버를 구축하지 않고도 static 파일을 다루는 웹서버를 열 수 있으며 hot-loader 를 통하여 코드가 수정 될 때마다 자동으로 리로드 되게 할 수 있습니다

---
