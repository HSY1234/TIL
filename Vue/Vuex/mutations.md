## 왜 state를 직접 변경하지 않고 mutations를 사용할까?

여러개의 컴포넌트에서 state 값을 변경하는 경우 어느 컴포넌트에서 해당 state를 변경했는지 추적하기가 어렵다.

특정 시점에 어떤 컴포넌트가 state를 접근하여 변경한 건지 확인하기 어렵기 때문

따라서 뷰의 반응성을 거스르지 않게 명시적으로 상태 변화를 수행하게 mutations를 따로 만들었다.

그렇게 때문에 mutations시 devtool로 체크가 가능해진다.(devtools가 mutations 시점에 호출되는 이유)
