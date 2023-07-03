# Web Architecture

![](img/Web%20Architecture%20Concept.png)

client에서 데이터를 요청(request)를 할때 넘겨주는 데이터를 parameter라고 한다.
parameter가 반드시 있어야 하지는 않지만, 대부분 있다.

client가 서버에 접속을 할때 http 프로토콜을 사용하며, 이를 도와주는 역할을 하는게 web server이다. web server는 http server라고도 불리기도 하며, 클라이언트의 요청(request)과 응답(response)을 처리해준다.

그러면 Web server는 접속과 응답만 처리해주기 때문에 실제로 Data를 처리하는 역할을 누가 해줘야한다.

이런 역할을 담당하는것이 Application Server이다. Application Server에서 Programming Laguage를 돌릴수 있다. (JAVA, ASP, PHP 등). Application Server는 클라이언트 요청에 대한 로직을 처리했다.

예전에는 Web Server와 Application Server가 분리를 시켜놨었다. 둘다 처리하는게 부담이 많이 되어서, 그러나 요즘은 같이 가지고 있다. 이를 WAS라고 한다.

WAS의 종류에는 WebLogic, WebSphere, Jeus, Tomcat 등이 있다.

JAVA를 쓴다면 JDBC를 통해 DB와 WAS가 연동이 가능하다.

Application Server 실행 순서

1. data get
2. Logic  
   2-1. Bussiness Logic (Service)
   2-2. DB Logic (Dao)
3. 응답(HTML로 보내줘야지)

DTO, VO의 차이점

3. DTO(데이터를 보내주는 역할)
4. VO(Value Object)

Application에서 도는 JAVA + Web 을 Servlet이라고 한다.
Servlet이 너무 어려워서 JSP가 등장했다.
