# Redux
- facebook 에서 flux architecture를 관리하기 위해 만든 라이브러리
    - `flux`의 구현체
- `React` 어플리케이션에서 stete 관리를 할 때 사용되는 라이브러리

## 3가지 원칙
- Single Source of Truth
    - 어플리케이션의 state를 위해 단 한개의 `store`를 사용한다
        - flux에서는 여러개의 `store`를 사용하지만, redux는 단 하나를 사용한다. 주요차이점
- State is Read-Only
    - state는 읽기 전용이다
    - 변경을 위해선 무조건 `action`이 `dispatch` 되어야한다
- Change are made with pure Functions
    - `action` 객체를 처리하는 함수를 `reducer`라 한다
    - `reducer`는 정보를 받아서 상태를 어떻게 업데이트 할 지 정의한다
    - `reducer`는 순수함수*로 작성되어야 한다

# Flux! then Redux
- hot reloading & time travel debugging

## Flux를 바꿔야 하는 이유. Redux의 필요성
1. `store` 코드는 애플리케이션 상태를 삭제하지 않고는 reloading이 불가능하다
    - `Flux` store: `상태 변환을 위한 로직`, `현재 어플리케이션 상태`를 포함한다
        - 두가지를 같이 가지고 있어서, `로직`을 위해 store객체를 reloading하면 저장되어있던 기존의 상태(데이터)를 잃어버리게 된다
    - `Redux` 
        - 두 기능을 분리해서 각각의 객체로 갖음
        - 로직이 변화되서 reloading 되도, 상태 정보는 갖고 있을 수 있다
2. 애플리케이션의 상태는 매 `action`마다 재기록 된다
    - `time travel debugging`을 위해서는 상태 객체의 모든 버전을 기록해두면서 각각의 버전이 완전히 독립된 객체가 될 필요가 있다 (수정이 되면 안되므로)
    - `Redux`
        - `action`이 `store`로 전달되었을 때 기존의 애플리케이션 상태를 수정하는 대신, 그 상태를 복사한 뒤 복사본을 수정하면 된다

## Redux의 장점
- [정리할 paper 링크](https://stackoverflow.com/questions/32461229/why-use-redux-over-facebook-flux/32920459#32920459) 

## 각각의 역할과 특징

### Action creators 
: 이하 AC로 표기
- 어떤 메세지를 보내고 싶은지 AC에게 알려주면 나머지 시스템이 이해할 수 있는 포맷으로 바꿔준다
- `action`의 포멧을 바꾼뒤 `action`을 돌려준다
    - `Flux`와 다른점
    - `dispatcher`로 `action`을 보내지 않는다

### Store
- 모든 상태변화를 컨트롤한다
    - 다만, 상태 변환 처리 자체는 다른 곳에 위임을 한다
- 상태변화는 `Store`로 직접 요청하는 대신 `action` 파이프라인을 따라가야 한다
- `state tree`전체를 유지하는 책임을 진다
    - `Flux`와 다른점
    - `Redux`는 단일 `Store`를 가지고 있으므로, 직접 상태변화를 작업하지 않는다
- `Flux`에서 `dispatcher`가 하던 일을 한다
- `action`이 어떤 상태 변화를 만드는지 알 필요가 있을때 `reducer`에게 묻는다

### Reducer
- `root reducer`는 애플리케이션 상태 객체의 key를 기준 삼아 상태를 조각조각 나눈다
    - 나누어진 상태 조각은 그 조각을 처맇라 줄 아는 `reducer`로 넘겨준다
- 예전 상태를 변경하지 않고, 새로운 복사본을 만든 후 복사본에 변경사항을 적용한다
    - *상태 객체는 직접 변경되지 않는다.* 대신 각각의 상태 조각이 복사 후 변경되고 새로운 상태 객체 하나로 합쳐진다
- 상태 변화 작업 흐름
    - `reducer`는 복사되고 업데이트된 상태 객체를 `root reducer`에게 넘겨준다 
    - `root reducer`는 변경된 상태들을 모아서 새 객체를 만들고 이 객체를 `store`로 보낸다 
    - `store`는 이 객체를 새로운 애플리케이션 상태로 만든다
- 트리 모양 계급구조 안에 존재한다
    - 이 구조는 컴포넌트 구조처럼 필요한 만큼의 tree level을 가질 수 있다

### the View : smart and dumb components
- smart `component`: `action` 처리를 책임진다
    - props를 통해서 dumb `component`에게 `function`을 보낸다
    - DOM 요소들을 관리하는 dumb `component`들을 관리한다
    - 자기자신의 CSS style, DOM을 가지고 있지 않다
- dumb `component`: props를 통해서 받은 `function`을 콜백으로써 단순히 호출만 한다
    - `action`에 dependency를 가지지 않는다
    - CSS style을 포함한다
        - style props를 받아 기본 style에 병합시켜 사용할 수도 있다

### the view layer binding (react-redux)
- `store`를 `view`와 연결시켜주는 준다
- `provider component`: 컴포넌트 트리를 감싸는 컴포넌트
    - `connect()`를 이용해 `root component`들이 `store`에 연결되기 쉽게 만들어준다
- `connect()`: react-redux가 제공하는 함수, `selector`를 이용해 필요한 모든 연결을 만든다 
    - `component`가 어플리케이션 상태 업데이트를 받고 싶으면 `connect()`를 이용해서 `component`를 감싸주면 된다
- `selector`: 직접 만들어야 하는 함수
    - 애플리케이션 상태 안의 어느 부분이 컴포넌트에 props로써 필요한 것인지 지정한

### the root component
- `component` 계층 구조에서 가장 위에 위치하는 `component`
- `store`를 생성하고 무슨 `reducer`를 사용할지 알려주며 `view layer binding`과 `view`를 불러온다
- 필요한 모든 `reducer`를 가지고 있다
    - `combineReducers()`를 이용해서 다수의 `reducer`를 하나로 묶는다

# The setup (준비)
1. `store`를 준비한다
    - `root component`는 `createStore()`를 이용해서 `store`를 생성하고 무슨 `reducer`를 사용할지 알려준다
2. `store`와 `component` 사이의 커뮤니케이션을 준비한다
    - `root component`는 공급 component로서 서브 `component`를 감싸고 `store`와 공급 `component`사이를 연결한다
    - 공급 `component`는 기본적으로 `component`를 업데이트하기 위한 네트워크를 생성한다
    
    

---

# FLUX
- Action -> Dispatcher -> Store -> View
- facebook의 알람 bug를 해결하기 위해 ```시스템을 예측 가능하게 만들어서 문제점을 없애기 위해``` 만들어진 패턴
    - 기존의 데이터 흐름에서 View 가 model을 업데이트해야 할 일이 종종 발생했고, dependency 때문에 model이 다른 model을 업데이트해야할 때도 있었다
    - 데이터의 상태에 접근하는 방법이 다양하고 파악하기 어려워서 DEBUG 자체가 어려워지기 시작했다
- unidirectional data flow
    - 데이터는 단방향으로만 흐르고, 새로운 데이터를 넣으면 처음부터 흐름이 다시 시작된다

## 각각의 역할과 특징

### Action (Action creator)
- 모든 변경사항과 사용자와의 상호작용이 거쳐가야 하는 액션의 생성을 담당한다
- 어플리케이션의 상태를 변경하거나 뷰를 업데이트하고 싶다면 액션을 생성해야만 한다
- type과 payload를 포함한 액션을 생성한다
    - type: 시스템에 정의된 액션들 중의 하나 (e.g. MESSAGE_CREATE)
    - 메세지를 포멧에 맞게 변환시켜준다
- 가능한 액션들을 파악하기 쉽다
    - 프로젝트의 행동 생성자 파일을 보면 시스템에서 제공하는 API가 지원하는 *모든 상태변경*을 바로 확인할 수 있다

### Dispatcher
- 기본적으로 callback이 등록되어 있는 곳
- 액션을 보낼 필요가 있는 모든 store를 가지고 있고, 액션 생성자로부터 action이 넘어오면 여러 store에 action을 보낸다
    - a.k.a 전화교환대 (등록된 모든 전화들을 알고있고, 원하는 수신자로 전화를 연결해주는 역할)
- store에 action을 넘기는 처리는 동기적으로 실행된다
    - 만약, store들 사이엥 dependency가 있어서 하나를 다른 것보다 먼저 업데이트 해야한다면, waitFor()를 사용해서 dispatcher가 적절하게 처리하도록 조절할 수 있다
- action 타입과는 관계없이 등록된 모든 스토어로 action을 보낸다
    - store가 직접 모든 action을 받은 뒤 처리할지 말지 결정한다. 특정 action만 subscribe하지 않는다 

### Store
- 애플리케이션 내의 모든 상태와 그와 관련된 로직을 가지고 있다
- 모든 상태 변경은 반드시 store에 의해서 결정되어야만 하며, 상태 변경을 위한 요청을 store에 직접 보낼 순 없다
- 무조건 action 생성자/dispatcher 파이프라인을 거쳐서 action을 보내야만 한다
    - store에는 설정자(setter)가 존재하지 않으므로, 상태 변경을 요청하기 위해서는 *반드시* 모든 정해진 절차를 따라야만 한다
- 내부에서 switch statement를 사용해서 처리할 action과 무시할 action을 결정하게 된다
- 상태 변경을 완료하고 나면, 변경 이벤트 (change event)를 내보낸다
    - event: controller view에 상태가 변경됬다는 것을 알려주는 역할

### The controller view 와 View
- view: 상태를 가져오고 유저에게 보여주고 입력받을 화면을 렌더링하는 역할을 맡는다
    - 받은 데이터를 처리해서 보여지는 포맷(HTML)로 어떻게 바꾸는지 알고 있다
 - controller view: store와 view 사이에서, 상태가 변경되었을 때 store가 알려준 변경 사실을 자신의 하위에 있는 모든 view에게 넘겨준다

## data flow
- 준비과정 이후 데이터 흐름
1. view: action creator에게 action을 준비하라고 말한다
2. action creator: action 포맷에 맞게 만들어서 dispatcher에게 넘긴다
3. dispatcher: action을 들어온 순서에 따라 store로 보낸다
4. store: 모든 action을 받고 필요한 action만 골라서 상태를 변경하고, 작업이 완료되면 자신을 subscribe하고 있는 controller view 에게 event를 알린다
5. controller view: store에게 변경된 상태를 요청하고, 응답을 받으면 자신 하위의 모든 view에게 새로운 상태에 맞게 렌더링하도록 변경상태를 알린다


---
## 용어
- 순수함수(pure function)
    - 같은 인수로 실행된 함수가 항상 같은 결과를 반환하는 함수
    - none pure function e.g. Date.now(), Math.random() 
    
---
## 참고링크
- [Redux:배경지식|MVC,FLUX](https://www.youtube.com/watch?v=LRUQfJLuPA8)
- [Flux로의 카툰 안내서](http://bestalign.github.io/2015/10/06/cartoon-guide-to-flux/)
- [Redux로의 카툰 안내서](http://bestalign.github.io/2015/10/26/cartoon-intro-to-redux/)