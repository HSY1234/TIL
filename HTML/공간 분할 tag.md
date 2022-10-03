## div

- **block** 형식으로 공간을 분할합니다.
- div는 줄바꿈이 일어난다. 즉 한줄 내려간다.
- div는 사각형 단위의 박스로 영역을 지정한다.
- div는 width, height 설정 가능
- div 박스의 margin은 4방향에 전부 적용되고, 위아래가 div일 경우 여백이 두배가 되는게 아니라 겹쳐진다.
- **block 요소인 div태그 내부에 inline 요소를 넣을수 있다**
- div는 다른 block 태그를 포함할수있지만, p같은 tag는 div 포함 불가(div 태그의 목적이 공간 분할이기 때문)

## span

- **inline** 형식으로 공간을 분할합니다.
- span은 줄바꿈 없이 옆줄에 붙게 된다.
- span는 줄 단위로 공간을 차지합니다.
- span은 width, height 설정 불가능(줄 단위)
- span의 margin은 양방향에만 있고 겹쳐지지 않는다.
- **inline 요소인 span태그 내부에 block 요소를 넣을수 없다!** (높이 개념이 없으므로)

## display 속성 block VS inline

| block 형식 태그 | inline 형식 태그 |
| :-------------: | :--------------: |
|       div       |       span       |
|      h1~h6      |        a         |
|        p        |      input       |
|      목록       |     글자형식     |
|     테이블      |                  |
|      form       |                  |

이미지와 멀티미디어 태그는 inline-block 이다.

## 차이점

- div와 span을 여러 개를 만들어 나란히 나열하였을 때, div는 자동 줄 바꿈이 일어나면서 세로로, span은 줄 바꿈이 일어나지 않고 가로로 나열.
- 동일한 문장을 감쌌을 때, div는 박스 형태로 영역이 설정되고 그 안에 정렬됩니다. 하지만 span 은 줄 단위로 영역이 설정되기 때문에 박스 형태가 아닌 텍스트가 노출되는 영역만 포함.
- div의 margin은 4방향 모두 적용이 되며, span의 margin은 양옆으로만 적용
