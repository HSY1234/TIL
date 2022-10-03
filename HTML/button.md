# Button

웹상에서 버튼은 5가지 종류가 있다.

- `<input type=" ">` 태그의 타입
  - button: 버튼 태그와 같다(그냥 버튼)
  - submit: form정보를 서버로 전송
  - reset: input 요소에 입력한 모든 정보를 초기화
  - image: img + submit 두 태그의 조합이라고 생각하면 된다. (이중 submit 조심)
- 그냥 `<button><button/>` 태그 : 자체 기능은 없고, 스크립트 함수와 연결해 사용

## image button

- image + submit

```html
<input type="image" src="img" path” alt="대체텍스트" [속성="속성값"]" />
```
