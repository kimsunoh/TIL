# Redux
- facebook 에서 flux architecture를 관리하기 위해 만든 라이브러리
- React 어플리케이션에서 stete 관리를 할 때 사용되는 라이브러리

## FLUX
- Action -> Dispatcher -> Store -> View
- facebook의 알람 bug를 해결하기 위해 ```시스템을 예측 가능하게 만들어서 문제점을 없애기 위해``` 만들어진 패턴
    - 기존의 데이터 흐름에서 View 가 model을 업데이트해야 할 일이 종종 발생했고, dependency 때문에 model이 다른 model을 업데이트해야할 때도 있었다
    - 데이터의 상태에 접근하는 방법이 다양하고 파악하기 어려워서 DEBUG 자체가 어려워지기 시작했다
- unidirectional data flow
    - 데이터는 단방향으로만 흐르고, 새로운 데이터를 넣으면 처음부터 흐름이 다시 시작된다

### 각 순서별 특징과 역할

#### Action (Action creator)
- 모든 변경사항과 사용자와의 상호작용이 거쳐가야 하는 액션의 생성을 담당한다
- 어플리케이션의 상태를 변경하거나 뷰를 업데이트하고 싶다면 액션을 생성해야만 한다
- type과 payload를 포함한 액션을 생성한다
    - type: 시스템에 정의된 액션들 중의 하나 (e.g. MESSAGE_CREATE)
    - 메세지를 포멧에 맞게 변환시켜준다
- 가능한 액션들을 파악하기 쉽다
    - 프로젝트의 행동 생성자 파일을 보면 시스템에서 제공하는 API가 지원하는 *모든 상태변경*을 바로 확인할 수 있다

#### Dispatcher
- 기본적으로 callback이 등록되어 있는 곳
- 액션을 보낼 필요가 있는 모든 store를 가지고 있고, 액션 생성자로부터 action이 넘어오면 여러 store에 action을 보낸다
    - a.k.a 전화교환대 (등록된 모든 전화들을 알고있고, 원하는 수신자로 전화를 연결해주는 역할)
- store에 action을 넘기는 처리는 동기적으로 실행된다
    - 만약, store들 사이엥 dependency가 있어서 하나를 다른 것보다 먼저 업데이트 해야한다면, waitFor()를 사용해서 dispatcher가 적절하게 처리하도록 조절할 수 있다
- action 타입과는 관계없이 등록된 모든 스토어로 action을 보낸다
    - store가 직접 모든 action을 받은 뒤 처리할지 말지 결정한다. 특정 action만 subscribe하지 않는다 

#### Store
- 애플리케이션 내의 모든 상태와 그와 관련된 로직을 가지고 있다
- 모든 상태 변경은 반드시 store에 의해서 결정되어야만 하며, 상태 변경을 위한 요청을 store에 직접 보낼 순 없다
- 무조건 action 생성자/dispatcher 파이프라인을 거쳐서 action을 보내야만 한다
    - store에는 설정자(setter)가 존재하지 않으므로, 상태 변경을 요청하기 위해서는 *반드시* 모든 정해진 절차를 따라야만 한다
- 내부에서 switch statement를 사용해서 처리할 action과 무시할 action을 결정하게 된다
- 상태 변경을 완료하고 나면, 변경 이벤트 (change event)를 내보낸다
    - event: controller view에 상태가 변경됬다는 것을 알려주는 역할

#### The controller view 와 View
- view: 상태를 가져오고 유저에게 보여주고 입력받을 화면을 렌더링하는 역할을 맡는다
    - 받은 데이터를 처리해서 보여지는 포맷(HTML)로 어떻게 바꾸는지 알고 있다
 - controller view: store와 view 사이에서, 상태가 변경되었을 때 store가 알려준 변경 사실을 자신의 하위에 있는 모든 view에게 넘겨준다

### data flow
- 준비과정 이후 데이터 흐름
1. view: action creator에게 action을 준비하라고 말한다
2. action creator: action 포맷에 맞게 만들어서 dispatcher에게 넘긴다
3. dispatcher: action을 들어온 순서에 따라 store로 보낸다
4. store: 모든 action을 받고 필요한 action만 골라서 상태를 변경하고, 작업이 완료되면 자신을 subscribe하고 있는 controller view 에게 event를 알린다
5. controller view: store에게 변경된 상태를 요청하고, 응답을 받으면 자신 하위의 모든 view에게 새로운 상태에 맞게 렌더링하도록 변경상태를 알린다


---
## 참고링크
- [Redux:배경지식|MVC,FLUX](https://www.youtube.com/watch?v=LRUQfJLuPA8)
- [Flux로의 카툰 안내서](http://bestalign.github.io/2015/10/06/cartoon-guide-to-flux/)