# 전역 컴포넌트

```js
// Vue.component('컴포넌트 이름', 컴포넌트 내용);
Vue.component("app-header", {
  template: "<h1>Header</h1>",
});
```

# 지역 컴포넌트

```js
 <div id="app">
    <app-header></app-header>
    <app-footer></app-footer>
  </div>

  <div id="app2">
    <app-header></app-header>
    <app-footer></app-footer>

// 지역 컴포넌트
new Vue({
  el: "#app",
  components: {
    // '컴포넌트 이름': 컴포넌트 내용,
    // '키':'value',
    "app-footer": {
      template: "<footer>footer</footer>",
    },
  },
});

new Vue({
  el: "#app2",
  components: {
    "app-footer": {
      template: "<footer>footer</footer>",
    },
  },
});
```
