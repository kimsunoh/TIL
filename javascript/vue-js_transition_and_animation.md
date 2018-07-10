# 진입/진출 그리고 리스트 트랜지션
- Vue는 transition wrapper 컴포넌트를 제공함
	- transision : 트랜지션, 컴포넌트로 싸여진 엘리먼트가 삽입되거나 제거될 때 일어남
- 특정 상황에서 엘레먼트 또는 컴포넌트에 대한 진입/진출 트랜지션을 추가 할 수 있음 
<details><summary> 특정상황</summary><p>
- v-if 사용\
- v-show 사용\
- 동적 컴포넌트\
- 컴포넌트 루트 노드
</p>
</details>

## 단일 엘리먼트/컴포넌트 트랜지션
### 트랜지션 클래스
- 각 클래스에는 트랜지션 이름이 접두어로 붙는다
	- v- 접두어 : 이름 없이 <transition> 엘리먼트를 사용할 때의 기본 값
	- 이름을 사용하면 {name}-enter 로 사용 된다

#### 트랜지션 각각의 상태
![트랜지션 각각의 상태](https://kr.vuejs.org/images/transition.png)
이미지 출처: [Vue.js 가이드](https://kr.vuejs.org/v2/guide/transitions.html#트랜지션-클래스)

| 클래스명 | 상태 | 시점 |
| --- | --- | --- |
| v-enter | enter 시작 상태 | 엘리먼트가 삽입되기 전에 적용되고\한 프레임 후에 제거됨 |
| v-enter-active | enter 활성 및 종료 상태 | 엘리먼트가 삽입되기 전에 적용됨\트랜지션/애니메이션이 완료되면 제거됨 |
| v-enter-to\*2.1.8이상 버전에서 지원*| enter 종료 상태 | 엘리먼트가 DOM에 추가 된 후 (v-enter가 제거되는 것과 동시에) 프레임을 적용하고, 트랜지션/애니메이션이 끝날 때 프레임이 제거됨 |
| v-leave | leave를 위한 시작 상태 | 진출 트랜지션이 트리거 될 때 적용되고, 한 프레임 후에 제거됨 |
| v-leave-active | leave 활성 및 종료 상태 | 진출 트랜지션이 트리거되면 적용되고, 트랜지션/애니메이션이 완료되면 제거됨 |
| v-leave-to\*2.1.8이상 버전에서 지원*| leave 상태의 끝에서 실행 | leave 트랜지션이 트리거되고 (동시에 v-leave가 제거됨), 트랜지션/애니메이션이 끝날 때 프레임이 제거됨 |

### 사용자 지정 트랜지션 클래스
- 기존의 class 명을 오버라이드 하여 사용자 지정 방식으로 사용하는 것
- '-class'를 이용해 트랜지션 클래스의 내용을 수정 하는 것
- e.g.
```html
...
<transition
    name="custom-classes-transition"
    enter-active-class="animated tada"
    leave-active-class="animated bounceOutRight"
> <!-- --> </trasition>
...
```

### JavaScript 훅
- 속성에서 javaScript 훅을 설정할 수 있다.
	- javaScript 이벤트 메시지를 가로채서 다른 작업을 설정할 수 있다.
- javaScript 전용 트랜지션을 사용하는 경우 enter,leave 훅에서 **done 콜백이 필요하다**
	- 콜백을 하지 않으면 트랜지션 완료가 동기적으로 호출되어 처리된다

## 최초 렌더링시 트랜지션
- 초기 렌더에 트랜지션을 적용하고 싶다면 trasision에 appear 속성을 추가해서 사용한다
- 사용자 정의 css 클래스를 지정할 수 있다
```html
<transition 
	appear
	appear-class="custom-appear-class"
	> 
	<!-- --> 
</trasition>
```

## 엘리먼트간 트랜지션
- v-if/v-else 를 사용하여 원본 엘리먼트간에 트랜지션을 할 수 있다
