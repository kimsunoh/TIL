# Redux-Saga
- 사이드 이펙트를 관리하기 위해 만들어짐
- action creator & reducer는 `순수`해야 하는데 사이드 이펙트는 어떻게 처리해야 하는가?에 대한 고민에서 시작됨
- 어플리케이션에서 필요한 사이드 이펙트를 별도의 쓰레드로 분리해서 관리할 수 있고, 스레드를 액션을 이용해 시작,중지,취소시킬 수 있다

## Saga
> ... 요약해보면 Saga는 어떤 시스템에서 장기(Long lived) 트랜직션과 그 실패 처리를 어떻게 관리할지에 대한 방법이다. ...
- 각 작업을 어떻게 관리할지에 대해 관심을 갖고 있다
- 실제 서비스 로직들은 모두 saga 내부에서 처리하며, 그 결과를 다시 action으로 dispatch 한다
    - 그 외의 모든 것들은 순수함수로 side-effect 없이 구현할 수 있다

---
## 참고링크
- [Redux-Saga: Beginner tutorial](https://redux-saga.js.org)
- [Redux-Saga: Beginner tutorial (kr version)](https://mskims.github.io/redux-saga-in-korean/)
- [Redux-Saga: 사이드 이펙트 관리](https://meetup.toast.com/posts/136)
- [redux-saga로 비동기처리와 분투하다. (번역본)](https://github.com/reactkr/learn-react-in-korean/blob/master/translated/deal-with-async-process-by-redux-saga.md)
- [왜 리덕스 사가(Redux-saga) 인가?](https://gracefullight.github.io/2017/12/06/Why-redux-saga/) **