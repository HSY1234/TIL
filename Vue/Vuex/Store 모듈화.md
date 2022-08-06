## 기본 Store 폴더

src 폴더에 store 폴더 생성후 index.js로 관리

```js
//index.js
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

export const store = new Vuex.Store({
  state: {},
  getters: {},
  mutations: {},
  actions: {},
});
```

```js
//main.js
import { store } from "./store/index.js";

new Vue({
  render: (h) => h(App),
  router,
  store,
}).$mount("#app");
```

## 스토어의 분리
