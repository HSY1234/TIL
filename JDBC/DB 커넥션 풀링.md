# 커넥션 풀

이전까지 드라이버 로딩을 해놓고, JDBC를 DB에 연결할때 매번 DB 커넥션을 새로 생성하고, SQL문 실행후 결과값을 받은 다음 close를 하였다.

DB에 연결을 생성하는 행위는 리소스, 시간을 많이 쓰는 행위이다. 특히 한 서비스인데 sql문을 여러번 요청해야 하면 한 서비스에도 연결하고 끊고를 여러번 반복해야 한다.

해결방법이 없을까? => 필요할때마다 연결하지 말고 미리 연결하면 어때?  
필요할때마다 빌려주고(저장해둘 공간이 필요), 완전 close를 하는게 아니고 다시 반납(재사용)을 할수 있다면? => Pool 개념 (close는 한다 다만 지우는게 아니고 반납개념)

## 커넥션 풀에 필요한 개념

WAS에는 메모리 공간이 있다.  
이중 Heap 영역은 자바와 Servlet을 관리하고 있다.  
그 외에도 별도로 어떠한 객체를 모아서 관리하는 Pool이라는 공간이 따로 있다.

ex) 클라이언트가 100명이 들어오면 프로세스가 100개 도는게 아니고, 쓰레드가 100개 돌고 이런 쓰레드를 관리하는 쓰레드 풀이 있다.

Dao에서 호출할때마다 DB에 연결을 매번 하는것이 아닌, Dao와 상관없이 TomCat이 처음 서버를 띄울때 DB와 미리 연결해둔다. 즉 DB와 미리 연결해둘수 있는 객체를 담아둔다. 이를 DB 커넥션 풀이라고 한다.

## JNDI

JNDI(Java Naming and Directory Interface) 는 디렉터리 서비스에서 제공하는 데이터 및 객체를 발견(discover)하고 참고(lookup) 하기 위한 자바 API다.

쉽게 말해 자바의 어떤 객체를 특정 디렉토리와 이름으로 관리를 할수있게 해준다.어떤 파일이 어떤 경로에 있고 파일명으로 바로 찾을 수 있게 해주는 api이다.

javax.naming 패키지에 있다.

JNDI는 일반적으로 다음의 용도로 쓰인다:

- 자바 애플리케이션을 외부 디렉터리 서비스에 연결 (예: 주소 데이터베이스 또는 LDAP 서버)
- 자바 애플릿이 호스팅 웹 컨테이너가 제공하는 구성 정보를 참고

간단히 요약하자면 우리가 연결하고 싶은 데이터베이스의 DB Pool을 미리 Naming 시켜주는 방법 중 하나이다. 우리가 저장해놓은 WAS 의 데이터베이스 정보에 JNDI를 설정해 놓으면 웹 애플리케이션은 JNDI만 호출하면 간단해진다.

그럼 왜 사용하게 되는걸까? 우리는 보통 JDBC를 설정해서 개발을 한다. 하지만 웹 애플리케이션을 운영서버로 만들경우 얘기가 달라진다. 그 이유는

개발을 한 사람과 실제 서비스를 운영하는 Admin은 다른 경우가 많기 때문에 소스 레벨에서 설정되어 있는 것보다 WAS에서 설정되어 있는 것을 선호한다.
또한 WAS에 여러 개의 웹 애플리케이션을 올려서 사용하기 때문에 WAS에서 한 번에 설정해 주는 것이 자원낭비를 줄일 수 있습니다.
또한 장애가 나거나 성능이 정상적이지 못하면 다른 한 서버가 대신 일을 해줄 수 있습니다.
정리하자면 운영, 관리, 최적화 문제 대처에 다양한 이점이 있기 때문에 JNDI를 사용한다.

모든것에는 접근할때는 protocol이 앞에 있어야한다.(`http:// 주소`, `file:C`), 그런데 브라우저는 http를 생략해도 자동으로 붙여주고, 윈도우 탐색기는 file을 생략한다.

자바에서는 앞에 `java:`이 붙어야한다. 특히 톰캣에서는 `java:comp/env`를 root context처럼 사용한다.(윈도우는 C드라이브를 root로 하듯), jdbc는 `jdbc/이름`으로 커넥션 풀을 관리할수있다.

## 커넥션 풀의 구현 방법

DB 커넥션 풀을 사용하면 서버가 실행될때 미리 DB랑 연결해놓은 객체를 풀에 담아놓고, JNDI를 이용하여 사용이 가능하다.

모든것에는 접근할때는 protocol이 앞에 있어야한다.(`http:// 주소`, `file:C`), 그런데 브라우저는 http를 생략해도 자동으로 붙여주고, 윈도우 탐색기는 file을 생략한다.

자바에서는 앞에 `java:`이 붙어야한다. 특히 톰캣에서는 `java:comp/env`를 root context처럼 사용한다.(윈도우는 C드라이브를 root로 하듯), jdbc는 `jdbc/이름`으로 커넥션 풀을 관리할수있다.

## 바꾸기 전

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DBUtil {

	private final String driverName = "com.mysql.cj.jdbc.Driver";
	private final String url = "jdbc:mysql://127.0.0.1:3306/DB이름?serverTimezone=UTC";
	private final String user = "root";//id
	private final String pass = "1234";//비밀번호

	private static DBUtil instance = new DBUtil();

	private DBUtil() {
		try {
			Class.forName(driverName);
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
	}

	public static DBUtil getInstance() {
		return instance;
	}

	public Connection getConnection() throws SQLException {
		return DriverManager.getConnection(url, user, pass);
	}

	public void close(AutoCloseable... closeables) {
		for (AutoCloseable c : closeables) {
			if (c != null) {
				try {
					c.close();
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		}
	}
}

```

Dao 구현

```java
public void registerArticle(GuestBookDto guestBookDto) throws SQLException {
		Connection conn = null;
		PreparedStatement pstmt = null;
		try {
			conn = dbUtil.getConnection();
			StringBuilder registerArticle = new StringBuilder();
			registerArticle.append("insert into guestbook (userid, subject, content, regtime) \n");
			registerArticle.append("values (?, ?, ?, now())");
			pstmt = conn.prepareStatement(registerArticle.toString());
			pstmt.setString(1, guestBookDto.getUserId());
			pstmt.setString(2, guestBookDto.getSubject());
			pstmt.setString(3, guestBookDto.getContent());
			pstmt.executeUpdate();
		} finally {
			dbUtil.close(pstmt, conn);
		}
	}

```

## 커넥션 풀 적용

```java
import java.sql.Connection;
import java.sql.SQLException;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.naming.NamingException;
import javax.sql.DataSource;

public class DBUtil {
	private static DBUtil instance = new DBUtil();

	private DBUtil() {}// 싱글톤 필요없어짐

	public static DBUtil getInstance() {
		return instance;
	}

	public Connection getConnection() throws SQLException {
		try {
			Context context = new InitialContext();// 메모리 접근할 컨텍스트 객체
			Context rootContext = (Context) context.lookup("java:comp/env");// 루트 컨텍스트 찾기 자바의 객체를 다 찾아주므로 Object리턴이라 형변환 필요
			DataSource dataSource = (DataSource) rootContext.lookup("jdbc/hello");//루트 컨텍스트에서 찾는다, 내가 context.xml에 'jdbc/이름' 으로 지정한것과 똑같이 하면됨
			return dataSource.getConnection();
      // 결국 호출할때마다 이제 Context로 dataSource에 접근해서 dataSource가 주는 getConnection만 받아오면된다!
		} catch (NamingException e) {
			e.printStackTrace();
		}
		return null;
	}

	public void close(AutoCloseable... closeables) {
		for (AutoCloseable c : closeables) {
			if (c != null) {
				try {
					c.close();
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		}
	}
}
```

잘보면 DB 정보가 없어졌다.  
어디다 설정했는가? => WebContent 폴더 => META-INF의 context.xml 파일

context.xml 파일 설정

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Context>
	<Resource name="jdbc/hello" auth="Container" type="javax.sql.DataSource"
			maxTotal="100" maxIdle="30" maxWaitMillis="10000"
			username="root" password="1234" driverClassName="com.mysql.cj.jdbc.Driver"
			url="jdbc:mysql://localhost:3306/이름?serverTimezone=UTC&amp;useUniCode=yes&amp;characterEncoding=UTF-8"/>
    <WatchedResource>WEB-INF/web.xml</WatchedResource>
</Context>
```

Dao에서는 따로 코드 변경할 필요 X  
커넥션풀을 하면 close가 더 중요해지는데, close를 해주지 않으면 반납이 안된다!!

## 톰캣이 어떻게 돌아가는가?

1. 톰캣이 실행될때 Servers 프로젝트의 server.xml을 읽어온다.
2. server.xml에서 `<Context docBase= "" path=""...>` 태그가 있는데 프로젝트의 문서들을 읽어들임
3. 이것에 의해 톰캣은 해당 프로젝트를 실행할때 META-INF 폴더의 문서들을 읽음
4. 여기 있는 JDBC 풀 설정을 읽어들인다.
5. 이걸 다 읽으면 web.xml로 넘어가 다른 설정들을 읽어들인다.(즉 설정을 읽는데도 순서가 있다.)
