## 잔디 심기

github 잔디심기를 할때 local과 github email이 다를 경우 잔디가 안심어진다 ㅎㅎ  
github-> settings-> email에서 내 이메일과 local의 `git config --list`로 user.email이 일치하는 지 확인 후 다르다면  
`git config user.email "내 이메일 주소"`로 내 local 이메일을 github과 일치시켜준다.

## git에서 파일 추적

2022/07/29  
팀원들과 git 컨벤션을 정하고 test를 하다가 발생한 문제  
develop branch를 main branch에 merge하려 했는데 충돌 발생

- develop branch  
  원래 있던 a파일을 이름을 a2로 변경
- main branch  
  원래 있던 a파일을 삭제(revert로)

원래 의도: 없는 파일을 추가한 develop브랜치를 main branch에 병합하니까 a2파일이 main에 자동으로 병합되면서 추가될것이다!, 그런데 충돌 발생!

발생 이유: a파일의 이름을 바꿔도 git은 같은 파일로 인식하고 추적함(아마 hash코드 같은걸로?)  
즉 main 브랜치는 a파일을 삭제, develop 브랜치는 a파일을 유지한다고 생각(설사 이름을 바꿨다고 해도)해서 충돌 발생!
