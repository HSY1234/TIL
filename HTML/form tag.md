# Form 태그란

- 웹페이지에서 데이터를 전송하는데 사용되는 HTML의 태그이다.
- 전송 대상은 보통은 서버이지만, 웹페이지가 데이터를 사용하기 위해 사용될때도 있다.
- 사용자로부터 데이터를 입력 받아 서버에서 처리하기 위한 용도로 사용.
- 사용자의 요청에 따라 서버는 HTML form을 전달(회원가입양식, 검색 양식 등).
- 사용자는 HTML form에 적절한 데이터를 입력한 후 서버로 전송. 이를 submit이라 함.
- 서버는 사용자의 요청을 분석한 후 데이터를 등록하거나, 원하는 데이터를 조회하여 결과를 다시 반환.

## form 태그 주의사항

- `<form></form>` 사이에 다른 `<form></form>` 삽입 불가
- `<form>`의 이름 속성은 한 페이지에서 중복 사용 불가
- `<form>` 태그는 css로 폰트가 적용이 안되므로 따로 적용해주어야한다.
- 사용자가 입력하기 위한 control 요소들은 모두 `<form>` tag 하위에 위치해야 서버로 전송됨.
- 각 control 요소마다 텍스트 입력, 버튼 클릭 등 다양한 형식으로 입력을 받는다.

## form tag의 속성

- action : 입력데이터의 전달 위치를 지정합니다. form을 전송할 서버 쪽의 script 파일을 지정전송되는 서버 url 또는 html 링크 ex) `action="/action_page.php" `-php, `"/bw/singleparam"`-servlet
- method : 입력 데이터의 전달 방식을 선택합니다. ex) GET, POST
- name : form의 이름, 서버로 제출된 폼 데이터, 한 문서안에 여러 form 태그가 있을경우 구분자로 사용

# input tag

- form 태그 안에 입력양식 태그은 input 태그로 data를 받을수 있다.
- 일반적으로 input 태그는 form 안에 있어야 하지만, Ajax기술의 활성화로 규칙을 안지키는 경우가 늘고 있다.

## input tag의 type 속성

```html
<input type="button" />
```

- button: 버튼
- checkbox : 체크박스
- file : 파일
- hidden : 보이지 않음
- image: 이미지
- password: 패스워드
- radio : 라디오 버튼
- reset: 초기화 버튼
- submit: 제출 버튼
- text: 글자 입려 양식
- 그외에도 매우 많다.

## submit VS button

기능적으로는 동일, 기본적으로 button에

## label tag

label 태그는 input 태그를 설명하는데 사용합니다.

- label 태그는 어떤 태그를 설명해주고 있는지 표시해야합니다.
- label의 `for` 속성과 input의 `id` 속성이 일치해야합니다.
- label 태그를 클릭하면 자동으로 해당하는 input 태그에 초점이 맞춰진다.

# textarea tag

# select tag

# fieldset

# legend
