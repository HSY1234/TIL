## 상위 view에서 component에 필요한 데이터를 호출해서 Store에 반영했다고 할때

1. 컴포넌트에서 store를 직접 접근한다
2. 상위 view에서 store 데이터를 뽑아다 component에 직접 props 해준다.

어느게 더 좋은 방법인가?

예시) UserView => UserProfile 이라고 가정한다.

- UserProfile에서 computed로 스토어 state 직접 접근

  - Vuex을 쓰는 훨씬 방식에 직관적임
  - 쉽다

- UserView에서 props로 직접 UserProfile에 전달
  - 컴포넌트의 데이터 흐름을 명시적으로 표현 가능
  - 조금 복잡

틀린건 없다. 상황에 맞춰 쓸것
