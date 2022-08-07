## JS의 module과 발전과정

우선, js는 브라우져에서 사용되도록 개발되었다. script 태그 안에 코드나 코드의 위치를 넣어두면 코드가 실행된다. import나 require의 개념이 없기 때문에 어떤 스크립트를 불러와서 사용하려면 일반적으로 전역변수에 배당해야 한다. 이러면 전역변수가 겹치는 두 라이브러리를 쓰기 번잡해진다.

초기 스크립트는 크기도 작고 기능도 단순했기 때문에 자바스크립트는 긴 세월 동안 모듈 관련 표준 문법 없이 성장할 수 있었다.

하지만 스크립트의 크기가 점차 커지고 기능도 복잡해지자 자바스크립트 커뮤니티는 특별한 라이브러리를 만들어 필요한 모듈을 언제든지 불러올 수 있게 해준다거나 코드를 모듈 단위로 구성해 주는 방법을 만드는 등 다양한 시도를 하게 된다.

## 모듈 생성

스크립트 파일이 곧 모듈이 된다.

## export

`export` 지시자를 변수나 함수 앞에 붙이면 외부 모듈에서 해당 변수나 함수에 접근할 수 있습니다.  
`export`는 최상위 항목이어야 합니다. 함수 내부에서는 사용 불가

```js
export const name = "square";

export function draw(ctx, length, x, y, color) {
  ctx.fillStyle = color;
  ctx.fillRect(x, y, length, length);

  return {
    length: length,
    x: x,
    y: y,
    color: color,
  };
}

//하나하나 export 붙이지 않고 여러개를 한번에 파일 마지막에 하는게 편하다.
export { name, draw, reportArea, reportPerimeter };
// 별칭도 가능
export { sayHi as hi, sayBye as bye };
```

## import

`import` 지시자를 사용하면 외부 모듈의 기능을 가져올 수 있습니다(모듈 가져오기).

```js
import { name, draw, reportArea, reportPerimeter } from "./modules/square.js";
import { sayHi as hi, sayBye as bye } from "./say.js"; // 별칭도 가능
```

## 모듈의 핵심기능

1. 엄격 모드(strict)로 실행  
   선언되지 않은 변수등을 모듈에 새로 할당할수 없음.

2. 모듈의 레벨 스코프
   모듈은 자신만의 스코프가 있습니다. 따라서 모듈 내부에서 정의한 변수나 함수는 다른 스크립트에서 접근할 수 없습니다.

3. 모듈의 this값은 `undefiend`
   일반적으로 일반스크립트의 this는 전역객체인것과 대조됨

## export default

모듈은 크게 두 종류로 나뉩니다.

1. 복수의 함수가 있는 라이브러리 형태의 모듈
2. 개체 하나만 선언되어있는 모듈

대개는 두 번째 방식으로 모듈을 만드는 걸 선호하기 때문에 함수, 클래스, 변수 등의 개체는 전용 모듈 안에 구현됩니다.

그런데 이렇게 모듈을 만들다 보면 자연스레 파일 개수가 많아질 수밖에 없습니다. 그렇더라도 모듈 이름을 잘 지어주고, 폴더에 파일을 잘 나눠 프로젝트를 구성하면 코드 탐색이 어렵지 않으므로 이는 전혀 문제가 되지 않습니다.

모듈은 export default라는 특별한 문법을 지원합니다. export default를 사용하면 **'해당 모듈엔 개체가 하나만 있다’** 는 사실을 명확히 나타낼 수 있습니다.

내보내고자 하는 개체 앞에 export default를 붙여봅시다.

이때 default를 붙여서 모듈을 내보내면 중괄호 {} 없이 모듈을 가져올 수 있습니다.

```js
export default class User {
  constructor(name) {
    this.name = name;
  }
}
```

```js
import { User } from "./user.js"; // 원래는 export한 이름으로 {} 사이에 받아와야한다.
import Userrr from "./user.js"; // {User}가 아닌 Userrr로 클래스를 가져왔습니다. 어차피 받을게 default로 하나 뿐이니까 이름을 내맘대로 해도 된다!!!

new User("John");
```

|      named export       |         default export          |
| :---------------------: | :-----------------------------: |
| export class User {...} | export default class User {...} |
| import {User} from ...  |      import User from ...       |
