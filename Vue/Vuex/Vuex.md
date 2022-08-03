# Vuex

복잡한 애플리케이션에서 컴포넌트의 개수가 많아지면 컴포넌트 간에 데이터 전달이 어려워진다.

- 이벤트 버스로 해결을 하려해도 이벤트를 어디서 보냈는지, 누가 받았는지 알기 힘들어짐

1. MVC 패턴에서 발생하는 구조적 오류
2. 컴포넌트간 데이터 전달 명시
3. 여러 개의 컴포넌트에서 같은 데이터를 업데이트 할 때 동기화 문제

해결가능!!!

# Vuex의 컨셉

state: 컴포넌트 간에 공유하는 데이터 data()  
view: 데이터를 표시하는 화면 templete  
action: 사용자의 입력에 따라 데이터를 변경하는 methods

# Vuex 구조
1. vue components에서 dispatch로 action호출
2. actions는 비동기 로직을 처리하고 commit으로 Mutations 호출(action은 state 변경 불가)
3. mutations에서 mutate로 state의 데이터를 변경
4. rendering

공식문서 그림 참고