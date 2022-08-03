## Vuex의 헬퍼 함수

Vuex 기술 요소들을 컴포넌트에서 더 편하게 쓸수 있도록 도와주는 API  
주로 ES6의 spread operator과 함께 사용된다.  
Store에 있는 4가지 속성을 간편하게 코딩할수 있도록 도와준다.

- state => mapState
- getters => mapGetters
- mutations => mapMutations
- actions => mapActions

```js
import { mapState } from "vuex";
import { mapGetters } from "vuex";
import { mapMutations } from "vuex";
import { mapActions } from "vuex";

export default {
  computed() {...mapState(['num']), ...mapGetters(['countedNum'])},
  methods: {...mapMutations(['clickBtn']), ...mapActions(['asyncClickBtn'])}
}
```

## mapState

```js
// App.vue
import { mapState } from "vuex";

computed(){
  ...mapState(['num'])
  // num() {return this.$store.num; }
}

//store
state: {
  num: 10
}

// 실제 호출
{{this.num}}
//{{this.$store.state.num}}
```

## 헬퍼의 유연성

```js
...mapMutations([
  'clickBtn',// 'clickBtn:clickBtn
  'addNumber'// addNumber(인자)
])

...mapMutations({
  popupMsg: 'clickbtn'// 컴포넌트에서 쓸 메서드 명: Store의 뮤테이션 명
})

```
