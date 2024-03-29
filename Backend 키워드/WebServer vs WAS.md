출처 : https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html

## Static pages VS Dynamic Pages

![](img/static-vs-dynamic.png)

- Static Pages

  - Web Server는 파일 경로 이름을 받아 경로와 일치하는 file contents를 반환한다.
  - 항상 동일한 페이지를 반환한다.
  - Ex) image, html, css, javascript 파일과 같이 컴퓨터에 저장되어 있는 파일들
  - 사실 언제나 똑같은 페이지는 아니다, 현재 날짜와 시간을 표현, 랜덤함수, 혹은 프론트에서 서버로 직접 요청할수도 있다(전부 자바스크립트의 기능)
  - 결국 정적 웹의 기준은 서버가 보내는 HTML,CSS,JS, 동영상, 이미지 파일들이 언제나 동일한가? 이다.
  - 즉 서버에서 매번 가공해서 보내주는게 아니고, 프로그래머가 짠 그대로 언제나 똑같이 받으면 정적 웹
  - 주로 변하지 않고 거의 고정적인 페이지에 많이 쓴다. ex) 회사소개, 음식메뉴, 댓글없는 블로그

- Dynamic Pages
  - 인자의 내용에 맞게 동적인 contents를 반환한다.
  - 즉, 웹 서버에 의해서 실행되는 프로그램을 통해서 만들어진 결과물 \* Servlet: WAS 위에서 돌아가는 Java Program
  - 개발자는 Servlet에 doGet()을 구현한다.
  - 예를들어 DB내용에 따라 페이지 내용이 바뀌어야할 경우, 서버에서 DB에서 데이터를 불러온 다음, 이 데이터를 가지고 페이지를 만들어서 유저에게 보내면, DB 상태에 따라 페이지에 다른 내용이 들어가게 만들어진다.
  - 같은 페이지라도 사용자마다 다른 결과의 웹 페이지를 서버에 요청하고 받게 된다.
  - 우리가 보는 대부분의 웹 페이지는 동적 웹페이지

## 무조건 정적웹 보다 동적 웹이 좋은가?

NO! 예를 들어 블로그를 글을 동적웹으로 만들었다고 생각해보자, 작성자, 제목, 내용, 작성일, 댓글 등의 정보가 DB에 따로 저장되고, 호출때마다 동적으로 반영되어 제공이 된다. 그런데 같은 글을 보여줄때마다 서버가 계산을 하는건 나중에가면 큰 손해다. 차라리 통채로 HTML 파일로 저장해놓는게 서버에게 유리, 즉 이런 경우 정적 블로그로 운영하는게 유리하다.  
github 블로그는 정적 웹이다.

# Web Server와 WAS 차이

![](img/webserver-vs-was1.png)

## Web Server

- Web Server의 개념
  - 소프트웨어와 하드웨어로 구분된다.
  - 하드웨어
    - Web 서버가 설치되어 있는 컴퓨터
  - 소프트웨어
    - 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 정적인 컨텐츠(.html .jpeg .css 등)를 제공하는 컴퓨터 프로그램
- Web Server의 기능
  - HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저 또는 웹 크롤러)의 요청을 서비스 하는 기능을 담당한다.
  - 요청에 따라 아래의 두 가지 기능 중 적절하게 선택하여 수행한다.
  - 기능 1)
    - 정적인 컨텐츠 제공
    - WAS를 거치지 않고 바로 자원을 제공한다.
  - 기능 2)
    - 동적인 컨텐츠 제공을 위한 요청 전달
    - 클라이언트의 요청(Request)을 WAS에 보내고, WAS가 처리한 결과를 클라이언트에게 전달(응답, Response)한다.
    - 클라이언트는 일반적으로 웹 브라우저를 의미한다.
- Web Server의 예
  - Ex) Apache Server, Nginx, IIS(Windows 전용 Web 서버) 등

## WAS(Web Application Server)

- WAS의 개념
  - DB 조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server
  - HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)이다.
  - “웹 컨테이너(Web Container)” 혹은 “서블릿 컨테이너(Servlet Container)”라고도 불린다.
    - Container란 JSP, Servlet을 실행시킬 수 있는 소프트웨어를 말한다.
    - 즉, WAS는 JSP, Servlet 구동 환경을 제공한다.
- WAS의 역할
  - WAS = Web Server + Web Container
  - Web Server 기능들을 구조적으로 분리하여 처리하고자하는 목적으로 제시되었다.
    - 분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용된다.
    - 주로 DB 서버와 같이 수행된다.
  - 현재는 WAS가 가지고 있는 Web Server도 정적인 컨텐츠를 처리하는 데 있어서 성능상 큰 차이가 없다.
- WAS의 주요 기능
  1. 프로그램 실행 환경과 DB 접속 기능 제공
  2. 여러 개의 트랜잭션(논리적인 작업 단위) 관리 기능
  3. 업무를 처리하는 비즈니스 로직 수행
- WAS의 예
  - Ex) Tomcat, JBoss, Jeus, Web Sphere 등

# Web Server 와 WAS를 구분하는 이유

![](img/webserver-vs-was2.png)

- Web Server가 필요한 이유?

  - 클라이언트(웹 브라우저)에 이미지 파일(정적 컨텐츠)을 보내는 과정을 생각해보자.
    - 이미지 파일과 같은 정적인 파일들은 웹 문서(HTML 문서)가 클라이언트로 보내질 때 함께 가는 것이 아니다.
    - 클라이언트는 HTML 문서를 먼저 받고 그에 맞게 필요한 이미지 파일들을 다시 서버로 요청하면 그때서야 이미지 파일을 받아온다.
    - Web Server를 통해 정적인 파일들을 Application Server까지 가지 않고 앞단에서 빠르게 보내줄 수 있다.
  - 따라서 Web Server에서는 정적 컨텐츠만 처리하도록 기능을 분배하여 서버의 부담을 줄일 수 있다.

- WAS가 필요한 이유?
  - 웹 페이지는 정적 컨텐츠와 동적 컨텐츠가 모두 존재한다.
    - 사용자의 요청에 맞게 적절한 동적 컨텐츠를 만들어서 제공해야 한다.
    - 이때, Web Server만을 이용한다면 사용자가 원하는 요청에 대한 결과값을 모두 미리 만들어 놓고 서비스를 해야 한다.
    - 하지만 이렇게 수행하기에는 자원이 절대적으로 부족하다.
  - 따라서 WAS를 통해 요청에 맞는 데이터를 DB에서 가져와서 비즈니스 로직에 맞게 그때 그때 결과를 만들어서 제공함으로써 자원을 효율적으로 사용할 수 있다.
- 그렇다면 WAS가 Web Server의 기능도 모두 수행하면 되지 않을까?
  1. 기능을 분리하여 서버 부하 방지
  - WAS는 DB 조회나 다양한 로직을 처리하느라 바쁘기 때문에 단순한 정적 컨텐츠는 Web Server에서 빠르게 클라이언트에 제공하는 것이 좋다.
  - WAS는 기본적으로 동적 컨텐츠를 제공하기 위해 존재하는 서버이다.
  - 만약 정적 컨텐츠 요청까지 WAS가 처리한다면 정적 데이터 처리로 인해 부하가 커지게 되고, 동적 컨텐츠의 처리가 지연됨에 따라 수행 속도가 느려진다.
  - 즉, 이로 인해 페이지 노출 시간이 늘어나게 될 것이다.
  2. 물리적으로 분리하여 보안 강화
  - SSL에 대한 암복호화 처리에 Web Server를 사용
  3. 여러 대의 WAS를 연결 가능
  - Load Balancing을 위해서 Web Server를 사용
  - fail over(장애 극복), fail back 처리에 유리
  - 특히 대용량 웹 어플리케이션의 경우(여러 개의 서버 사용) Web Server와 WAS를 분리하여 무중단 운영을 위한 장애 극복에 쉽게 대응할 수 있다.
  - 예를 들어, 앞 단의 Web Server에서 오류가 발생한 WAS를 이용하지 못하도록 한 후 WAS를 재시작함으로써 사용자는 오류를 느끼지 못하고 이용할 수 있다.
  4. 여러 웹 어플리케이션 서비스 가능
  - 예를 들어, 하나의 서버에서 PHP Application과 Java Application을 함께 사용하는 경우
  5. 기타
  - 접근 허용 IP 관리, 2대 이상의 서버에서의 세션 관리 등도 Web Server에서 처리하면 효율적이다.
- 즉, 자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성 을 위해 Web Server와 WAS를 분리한다.
- Web Server를 WAS 앞에 두고 필요한 WAS들을 Web Server에 플러그인 형태로 설정하면 더욱 효율적인 분산 처리가 가능하다.

# Web Service Architecture

- 다양한 구조를 가질 수 있다.
  1. Client -> Web Server -> DB
  2. Client -> WAS -> DB
  3. Client -> Web Server -> WAS -> DB
     ![](img/web-service-architecture.png)

3번 구조의 동작과정

1. Web Server는 웹 브라우저 클라이언트로부터 HTTP 요청을 받는다.
2. Web Server는 클라이언트의 요청(Request)을 WAS에 보낸다.
3. WAS는 관련된 Servlet을 메모리에 올린다.
4. WAS는 web.xml을 참조하여 해당 Servlet에 대한 Thread를 생성한다. (Thread Pool 이용)
5. HttpServletRequest와 HttpServletResponse 객체를 생성하여 Servlet에 전달한다.
   5-1. Thread는 Servlet의 service() 메서드를 호출한다.
   5-2. service() 메서드는 요청에 맞게 doGet() 또는 doPost() 메서드를 호출한다.
   5-3 protected doGet(HttpServletRequest request, HttpServletResponse response)
6. doGet() 또는 doPost() 메서드는 인자에 맞게 생성된 적절한 동적 페이지를 Response 객체에 담아 WAS에 전달한다.
7. WAS는 Response 객체를 HttpResponse 형태로 바꾸어 Web Server에 전달한다.
8. 생성된 Thread를 종료하고, HttpServletRequest와 HttpServletResponse 객체를 제거한다.

## 참고 DBMS와 MiddleWare의 개념

- DBMS(Database Management System)
  - 다수의 사용자들이 DB 내의 데이터를 접근할 수 있도록 해주는 소프트웨어
  - DBMS는 보통 Server 형태로 서비스를 제공한다.
  - Ex) MySQL, MariaDB, Oracle, PostgreSQL 등
  - Q) DBMS Server에 직접 접속해서 동작하는 Client Program의 문제점?
    - Client에 로직이 많아지고 이에 따라 Client Program의 크기가 커진다.
    - 로직이 변경될 때마다 매번 배포가 되어야 한다.
    - Client에 대부분의 로직이 포함되어 배포가 되기 때문에 보안에 취약하다.
  - A) => 이를 해결하기 위해 아래와 같은 MiddlWare가 등장했다.
- MiddleWare
  - Client - MiddleWare Server - DB Server(DBMS)
  - 동작 과정
    1. Client는 단순히 요청만 중앙에 있는 MiddleWare Server에게 보낸다.
    2. MiddleWare Server에서 대부분의 로직이 수행된다.
    3. 이때, 데이터를 조작할 일이 있으면 DBMS에 부탁한다.
    4. 로직의 결과를 Client에게 전송한다.
    5. Client는 그 결과를 화면에 보여준다.
  - 즉, 비즈니스 로직을 Client와 DBMS 사이의 MiddleWare Server에서 동작하도록 함으로써 Client는 입력과 출력만 담당하게 된다.

## 그럼 Apache Tomcat?

웹서버는 Apache, WAS서버는 Tomcat이 있는데, Tomcat 5.5 버전부터 정적 컨텐츠를 처리하는 기능이 추가되어, Tomcat이 Apache의 기능을 포함하고 있기 때문에, Apache Tomcat이라고 부르게 되었다. 그러나 Tomcat은 아파치의 기본적인 기능만 가지고 있기 때문에, 아파치와 연동하여 아파치가 가지고 있는 다양한 웹서버 기능을 이용하기 위해, 따로 두는 경우가 더 많다.
