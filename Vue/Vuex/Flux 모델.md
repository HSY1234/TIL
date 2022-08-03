# Flux란?

- MVC 패턴의 복잡한 데이터 흐름 문제를 해결하는 개발 패턴 -Unidirectional data flow(단방향)
- 무조건 데이터가 단방향이라 문제를 방지하고 발생한 문제를 추적하기가 쉽다.

  Action => Distpatcher => Model => View

1. action: 화면에서 발생하는 이벤트 또는 사용자의 입력
2. dispatcher: 데이터를 변경하는 방법, 메서드
3. model: 화면에 표시할 데이터
4. view: 사용자에게 비춰지는 화면

# MVC 패턴의 문제점

- 기능 추가 및 변경에 따라 생기는 무제점을 예측할 수가 없음.
- 앱이 복잡해지면서 생기는 업데이트 루프
