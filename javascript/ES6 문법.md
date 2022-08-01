# let과 const

`let`과 `const`는 `var`과 달리 `undefined`를 할당하지 않은 채로 초기화를 마치며, 이후 특정 값을 할당하기 전까지는 해당 변수에 접근할수가 없다.  
그에 비해 `var`는 생성과 동시에 LE에서 `undefined`로 변수를 초기화 한다. undefined 자체는 값이다.

자바스크립트의 스코프 범위는 원래 함수 단위라서 for문 같은 경우 var는 scope가 적용되지 않는다.
