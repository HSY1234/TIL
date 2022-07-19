# babel

- `Babel is a JavaScript compiler.`
- 소스를 소스로 바꿔주는 transcompiler
- 최신 ES 문법으로 바꿔주기위한 모듈

## 설치

`npm i @babel/core @babel/cli @babel/node @bable/preset-env -D`

## 원리

1. 파싱(Parsing) : 코드를 읽고 추상 구문 트리(AST)로 변환하는 단계
2. 변환(Transforming) : 추상 구문 트리를 변경
3. 출력(Printing) : 변경된 결과물을 출력

## 플러그인

바벨 플러그인이란 바벨이 어떤 코드를 어떻게 변환할지 규칙을 담당한다.  
직접 만들어 쓸수도 있고, 보통은 만들어진 플러그인을 사용한다.  
https://babeljs.io/docs/en/plugins

## 설정

`babel.config.json` 파일을 생성해 설정값을 세팅한다.

## preset

플러그인을 매번 세팅하는건 매우 번거롭기 때문에, 플러그인들을 목적에 따라 세트로 묶어서 많이 사용한다.  
이를 프리셋(preset)이라한다. 프리셋 역시 직접 설정하거나, 바벨에서 제공하는 프리셋을 쓸 수 있다.  
대표적으로 ES6+로 변환하는 `preset-env`가 있다.

## preset 예시

`babel.config.json` 파일

```json
{
  "presets": ["@babel/preset-env"]
}
```

ES6이후 자바스크립트의 모든 기능을 컴파일할 수 있도록 설정하겠다.
