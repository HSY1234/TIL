# Spinner

## 스피너란?

페이지 로딩이 일어날때 사용자에게 프로그램이 다운되거나 죽은것이 아닌, 진행중임을 알려줄수 있는것

## 원리

`<spinner loading="true">` 인 동안 해당 컴포넌트가 그냥 창위에 떠있다.(로딩 중이 아니더라도)  
즉, 로딩중일때 loading 값을 true로 설정하게 코딩해주면 된다. 여기서 loading은 props로 받은 값이다.

개발자가 고민해야하는 부분은 스피너를 언제 실행하고, 언제 끄는지이다.

```js
<template>
  <div class="css 클래스 이름" v-if="loading">
    <div>
    </div>
    <div>
    </div>
    <div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    loading: {
      type: Boolean,
      required: true,
    },
  },
}
</script>

```

## vue에서 스피너 구현

컴포넌트에 Spinner.vue를 제작한다음

```js
//Sponner.vue
<template>
  <div class="css 클래스 이름" v-if="loading">
    <div>
    </div>
    <div>
    </div>
    <div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    loading: {
      type: Boolean,
      required: true,
    },
  },
}
</script>

```

App.vue에 컴포넌트를 임포트후 `<spinner :loading="true"><spinner>`를 추가한다.

스피너는 emit props를 쓰는 방법도 있지만 보통 이벤트 버스를 사용한다.

이벤트 버스는 빈 이벤트 객체를 만들어서 컴포넌트간의 데이터를 전달하는 것을 말한다.

보통 src 폴더 밑에 utils 폴더에 bus.js를 만들어 준다. (이벤트 객체 생성)

```js
//bus.js
import Vue from "vue";

export default new Vue();
```

사용하려는 페이지에서 bus 모듈을 import한 다음  
`created()` 안에 둔다

```js
created(){
  bus.$emit('start:spinner');
  //action 같은 시간 걸리는것
  bus.$emit('end:spiiner');
}
```

App.vue에도 bus를 임포트 한후에,

App.vue의 `created()`, `beforeDestroy()`에 추가

```js
data() {
  return{
    loadingStatus: false,
  };
}

methods:{
  startSpinner(){
    this.loadingStatus = true;
  },
  endSpinner(){
    this.loadingStatus = false;
  }
}

created(){
  bus.$on('start:spinner',this.startSpinner);
  bus.$on('end:spinner', this.endSpinner);
}

beforeDestroy(){// 객체 삭제용
  bus.$off('start:spinner',this.startSpinner);
  bus.$off('end:spinner', this.endSpinner);
}

```

여기까지하면 제대로 안될것이다. 스피너가 돌아가는코드와 꺼지는 코드 사이에 비동기 Action이 들어감으로, 비동기가 완료가 되기전에 스피너는 동기 코드로 꺼지게 된다.  
이걸 막기위해 Actions의 함수가 성공하고 then에서 return으로 response값을 전달하면, 해당액션을 호출한 함수에서 then으로 반환된 response(Promise객체)에 then을 붙여 비동기로 스피너 호출이 가능해진다. (Promise 체이닝)

```js
created(){
  bus.$emit('start:spinner');
  this.$store.dispatch('ACTION_FUNCTION')// 해당 액션 함수가 response를 반환하게 해주자
    .then(()=>{
      console.log('성공!!');
      bus.$emit('end:spiiner');
    })
    .catch((error)=>{// 에러 핸들링도 해줘
      console.log(error);
      bus.$emit('end:spiiner');
    })
  // bus.$emit('end:spiiner'); 이제 필요없음
}
```
