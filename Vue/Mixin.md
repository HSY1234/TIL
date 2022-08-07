# Mixin

## Mixin이란?

믹스인(Mixins)은 여러 컴포넌트 간에 공통으로 사용하고 있는 로직, 기능들을 재사용하는 방법입니다. 믹스인에 정의할 수 있는 재사용 로직은 data, methods, created 등과 같은 컴포넌트 옵션입니다.

## 코드 형식

```js
//.js 파일
var HelloMixins = {
  // 컴포넌트 옵션 (data, methods, created 등)
};

//. Vue 파일에서
new Vue({
  mixins: [HelloMixins],
});
```

## 사용예시

반복되는 모달창을 예시로 모든 모달창마다 일일히 코딩하는것도 가능하지만, 재반복되는 코드이다.

프로젝트에서는 보통 mixins 폴더를 따로 생성해 거기에 .js 파일들을 저장한다.(파일 이름은 명확하게)

```js
var DialogMixin = {
  data() {
    return {
      dialog: false,
    };
  },
  methods: {
    showDialog() {
      this.dialog = true;
    },
    closeDialog() {
      this.dialog = false;
    },
  },
};
```

을 다른 vue Component에 주입한다.

```js
//LoginForm.vue
<script>
import { DialogMixin } from './mixins.js';

export default {
  // ..
  mixins: [ DialogMixin ]
  methods: {
    submitForm() {
      axios.post('login', {
        id: this.id,
        pw: this.pw
      })
      .then(() => this.closeDialog())// closeDialog 사용함
      .catch((error) => new Error(error));
    }
  }
}
</script>
```
