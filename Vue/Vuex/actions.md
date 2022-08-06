## 왜 비동기 처리 로직은 actions에서 선언해야할까?

- 언제 어느 컴포넌트에서 해당 state를 호출하고, 변경했는지 확인하기가 어려움  
  ex) 예를 들어 여러개의 컴포넌트에서 mutations를 시간차로 호출할 경우, state 값의 변화를 추적하기 어렵기 때문에 mutations 속성에는 동기 처리 로직만 넣어야 한다.

## actions 함수

actions에 있는 함수 호출법

```js
this.$store.dispatch("함수 이름");
```

해당 store의 함수정의

```js
actions:{
getReview(context, id) {
      const API_URL = `${REST_API}/review/${id}`;
      axios({
        url: API_URL,
        method: "GET",
        headers: {
          "access-token": localStorage.getItem("access-token"),
        },
      })
        .then((res) => {
          context.commit("GET_REVIEW", res.data);// 뮤테이션 호출!
        })
        .catch((err) => {
          console.log(err);
        });
    },


getReview({ commit }, id) {// ES6 구조분해 문법(Destructuring)
      const API_URL = `${REST_API}/review/${id}`; // 백엔드 참고
      axios({
        url: API_URL,
        method: "GET",
        headers: {
          "access-token": localStorage.getItem("access-token"),
        },
      })
        .then((res) => {
          commit("GET_REVIEW", res.data);// 뮤테이션 호출!
        })
        .catch((err) => {
          console.log(err);
        });
    },
}
```

actions 속성은 모두 context라는 인자를 처음에 무조건 받는다. 그리고 context의 commit API를 반드시 호출하게 되어있다.

인자 값으로 첫번째를 `context`로 받거나`{commit}` 객체 형식으로 받을수 있고(ES6 구조 분해 문법으로 받는다), commit함수를 통해 mutation을 호출할수 있다.

예시) 구조분해 문법이 실제로 적용된것을 확인해보자

```js
actions: {
  fetchData(context) {
    context.commit('addProducts');
  }
}
```

여기서 구조 분해 문법을 적용해보면

```js
var context = {
  commit: (actionName) => console.log(actionName + " has been committed!!"),
};
```

이렇게 된다.

적용되는 과정을 살펴보자. 이렇게 되어있다고 생각해보면

```js
var context = {
  commit: (actionName) => console.log(actionName + " has been committed!!"),
};
```

다음과 같이 된다고 볼수 있다.

```js
var { commit } = context;
commit("addProducts");
```
