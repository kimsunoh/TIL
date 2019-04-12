# Hook
- 16.8 버전 이상에서부터 사용할 수 있는 새로운 기능
- useState, useEffect, ... 

## useState
```react
const [count, setCount] = useState(0);
```
- 컴포넌트 내부에서 호출하면 로컬 state를 추가한다
- func의 return은 \[current state, state를 업데이트 할 수 있는 함수\]이다 
    - state update func는 class 내부에서 this.setState를 호출한것과 같은 작업을 한다
    - 함수는 state를 new value로 덮어쓴다. old와 new를 merge하지 않는다
- useState의 arg로는 state의 initial 값을 준다

## useEffect


---
## 참고링크
- [hooks intro](https://reactjs.org/docs/hooks-intro.html)