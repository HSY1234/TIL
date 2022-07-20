# nodemon

nodemon은 node monitor의 약자로, 노드가 실행하는 파일이 속한 디렉터리를 감시하고 있다가 파일이 수정되면 자동으로 노드 애플리케이션을 재시작하는 확장 모듈이다. nodemon을 설치하면 재시작 없이 코드를 자동 반영 할수 있다

## 설치

`npm i nodemon -D`

## 설정

`nodemon.json` 파일에 설정

## 설정 예시

```json
{
  "exec": "babel-node src/server.js"
}
```

바벨을 이용해 컴파일을 먼저 한 다음 server.js 파일을 실행하겠다.

- ignore  
  특정 소스 변경시 재시작 하지 않고 무시 가능
