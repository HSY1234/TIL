## 설치

`npm init`

## package.json

Node.js는 `package.json` 파일을 기반으로 프로젝트에서 프로젝트 정보와 의존성을 기록하고 관리한다.  
프로젝트에 패키지를 추가로 설치할 때마다 패키지 정보가 자동으로 입력되기도 하고, package.json에 입력된 내용을 토대로 프로젝트 개발 환경을 구축할수 있다.

## scripts

콘솔에서 프로젝트 명령어를 추가할수 있다.

```
"scripts":{
  "dev": "nodemon"
}
```

`npm run dev`라고 명령어를 입력할 경우 nodemon이 실행된다.
