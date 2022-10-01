# Head의 요소

- `<head>` tag는 브라우저에게 HTML문서의 머리 부분임을 인식.
- `<title>`, `<meta>`, `<style>`, `<script>`, `<link>`, `<base>` tag를 포함 가능.

## title

- `<title>` tag는 문서의 제목을 의미, 브라우저의 제목 표시줄에 tag 내용이 나타남.
- `<title>` tag 이외의 다른 tag로 표현한 정보는 화면에 출력 X.
- `<title>` 요소는 모든 HTML / XHTML 문서에서 요구됩니다.

`<title>` 요소:

- 브라우저 툴바의 제목을 정의
- 즐겨 찾기에 추가 될 때 페이지 제목을 제공합니다
- 검색 엔진의 검색 결과에서 페이지의 제목을 표시합니다

## base

`<base>` 태그는 페이지의 모든 상대적인 URL에 대한 기본 URL/대상을 지정합니다

## meta

메타 데이터를 표현하기 위해 사용하는 태그
제공된 정보는 브라우저나 검색 엔진, 다른 웹 서비스에서 사용하게 된다.

특히 HTML5에서는 `<meta>` 요소를 통해 웹 페이지에서 사용자가 볼 수 있는 영역인 뷰포트(viewport)를 제어할 수 있도록 name 속성에 viewport 속성값을 제공하고 있습니다.

- 문서의 작성자, 날짜, 키워드등 브라우저의 본문에 나타나지 않는 일반 정보를 나타냄.
- name과 content 속성을 이용하여 다양한 정보를 나타냄.
- http-equiv 속성을 이용하여 인코딩 설정 및 문서 이동, 새로 고침이 가능.
- charset 속성을 이용하여 문서의 인코딩 정보를 설정.

```html
<!-- 검색엔진에 검색 -->
<meta name="keyword" content="HTML, meta, tag, element, reference" />
<!-- 페이지 설명 -->
<meta name="description" content="HTML meta tag page" />
<!-- 저자 -->
<meta name="author" content="hong" />
<!-- 5초후 리다이렉트 -->
<meta http-equiv="refresh" content="5; url=http://www.google.com" />
<!-- 모든 장치에서 viewport -->
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<!-- char-set 지정 -->
<meta charset="UTF-8" />
<!-- 익스플로러 호환성 지정 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
```

## meta의 http-equiv

http-equiv 속성은 content 속성에 명시된 값에 대한 HTTP 헤더를 제공합니다.
http-equiv 속성은 HTTP 응답 헤더를 시뮬레이션할 때 사용할 수 있습니다.
만약 http-equiv 속성이 명시되어 있다면, 반드시 content 속성도 함께 명시되어야만 합니다.

- content-type: 해당 문서의 문자 인코딩 방식을 명시함.
- default-style: 우선적으로 적용할 스타일시트를 명시함. content 속성값은 동일한 문서에 존재하는 link 요소의 title 속성값과 일치하거나, 동일한 문서에 존재하는 style 요소의 title 속성값과 일치해야만 합니다.
- refresh: 해당 문서를 새로고침(refresh)할 시간 간격을 명시함.
- X-UA-Compatible: 구버전 IE 호환성

```html
<meta http-equiv="content-type|default-style|refresh" />

<meta http-equiv="content-type" content="text/html; charset=UTF-8" />
<meta http-equiv="default-style" content="preferred stylesheet" />
<meta http-equiv="refresh" content="30" />
```

## link

`<link>` 태그는 현재 문서와 외부 자원 사이의 관계를 정의한다

## style

- `<style>` 태그는 HTML 문서에 대한 스타일 정보를 정의하는 데 사용됩니다
- `<style>` 요소 안에 HTML 요소들이 브라우저에 렌더링되는 방법들을 지정합니다

## script

`<script>` 태그 JavaScript와 같은 클라이언트 측 스크립트를 정의하는 데 사용된다.
