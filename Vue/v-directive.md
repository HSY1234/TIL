# v-derctive 모음

## v-html

html 태그를 그대로 뿌려야할때 사용한다.

## v-bind

tag의 속성에 변수값을 설정할수있다.

```js
<a href="a.html"></a>
<a v-bind:href="url"></a>//url에 해당 값이 저장됨
<a :href="url"></a> //v-bind 생략가능
```
