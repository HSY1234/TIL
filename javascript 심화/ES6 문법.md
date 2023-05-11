# let과 const

`let`과 `const`는 `var`과 달리 `undefined`를 할당하지 않은 채로 초기화를 마치며, 이후 특정 값을 할당하기 전까지는 해당 변수에 접근할수가 없다.  
그에 비해 `var`는 생성과 동시에 LE에서 `undefined`로 변수를 초기화 한다. undefined 자체는 값이다.

자바스크립트의 스코프 범위는 원래 함수 단위라서 for문 같은 경우 var는 scope가 적용되지 않는다.

```js
var sum = 0;
for (var i = 1; i <= 5; i++) {
  sum = sum + i;
}

console.log(sum); //15
console.log(i); //6
```

# 화살표 함수

`function` 키워드를 생략하고 `=>` 로 대체  
콜백 함수의 문법을 간결화, 콜백함수 안에 들어가는 함수는 스코프가 다르다. 스코프와 this가 달라진다.  
화살표 함수의 this는 익명함수의 this가 전역객체를 가리키는것과 달리, 화살표함수의 상위 속성의 this를 화살표 함수 내의 this가 가리키게 된다.

```js
//ES5
var sum = function (a, b) {
  return a + b;
};
//ES6
var sum = (a, b) => {
  return a + b;
};
sum(a, b);
```

# 향상된 객체 리터럴

객체 속성을 메서드로 사용할 때 `fucntion` 생략 가능

```js
var dictionary = {
  //ES5
  lookup: function(){
    console.log("hello");
  }
  //ES6
  lookup() {
    console.log("hello");
  }
}
```

객체의 속성 명과 값 명이 동일할 때 축약가능

```js
var figures = 10;
var dictionary = {
  //ES5
  figures: figures,
  //ES6
  figures,
};
```

# Modules

- 자바스크립트는 원래 모듈이 없었다.
- 자바스크립트는 원래 파일을 나눈다고 해서 스코프가 달라지지 않았다.
- ES6에 모듈 로더 라이브러리 기능을 js언어 자체에서 지원하기 시작했다.
- 모듈은 호출되기 전까지는 코드 실행과 동작을 하지 않는 특징이 있음

```js
//lib/math.js
export function sum(x, y) {
  return x + y;
}
export var pi = 3.141593;

//main.js
import { sum } from "libs/math.js";
sum(1, 2);
```

Vue.js에서 마주칠 `default` export
`default` 키워드는 한개의 파일에서 하나밖에 export가 되지 않는다.

# Object Spread Operator

`...`을 사용하면 된다.

```js
let josh = {
  field: "web",
  language: "js",
};

let developer = {
  nation: "korea",
  ...josh,
  //field: 'web'
  //language: 'js'
  //으로 변환
};
```

# 템플릿 리터럴(Template Literal)

문자열 생성시 따옴표가 아닌 `` 백틱(`)  ``으로 감싸준다.

1. 줄바꿈

```js
var str_01 = `
Hello!
    World!
             JavaScript!
happy Birthday!`;

var str_01 = "Hello! \n\t World! \n\t\t\t JavaScript! \n happy Birthday!";
```

위처럼 줄바꿈등을 이스케이프 시퀀스를 사용하지 않고 사용가능

2. 표현식 삽입(Expression interpolation)
   변수나 연산을 `${}` 사이에 삽입할수 있게 되었다.

- 변수

```js
var name = `hong`;
var age = 30;
var month = 12;

console.log(name + "는 " + age * month + "달을 살았습니다."); // 불편함
console.log(`${name}는 ${age * month}달을 살았습니다.`); // 쉽게 변형
```

- 연산

```js
console.log(`${5 + 10} 입니다`); // 15입니다.
```

# 구조 분해 문법 (Destructuring)

```js
var arr = [1, 2, 3, 4];
var obj = {
  a: 10,
  b: 20,
  c: 30,
};
```

```js
var { a, b, c } = obj;
```

원래 이런식으로 매번 변수를 할당해줘야한다.

```js
var josh = {
  language: "javascript",
  position: "front-end",
  area: "pangyo",
  hobby: "singing",
  age: "102",
};

var language = josh.language;
var position = josh.position;
var area = josh.area;
var hobby = josh.hobby;
var age = josh.age;
```

구조 분해 문법 적용시

```js
var josh = {
  language: "javascript",
  position: "front-end",
  area: "pangyo",
  hobby: "singing",
  age: "102",
};

var { language, position, area, hobby, age } = josh;
console.log(language); // javascript
console.log(position); // front-end
console.log(area); // pangyo
console.log(hobby); // singing
console.log(age); // 102
```
