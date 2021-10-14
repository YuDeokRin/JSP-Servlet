# Chapter11 JDBC로 데이터베이스 연동

**JDBC**

- JDBC 인터페이스 : 프로그래머에게 쉬운 데이터베이스와 연동되는 프로그램을 작성할 수 있게 하는 도구
- JDBC드라이버 : JDBC 인터페이스를 구현하여 실제로 DBMS를 작동시켜서 질의를 던지고 결과를 받음

![Untitled](https://user-images.githubusercontent.com/56623911/137312521-c6c9d99e-e656-4ece-831d-a893f59f4638.png)


**JDBC Driver Type**

![Untitled 1](https://user-images.githubusercontent.com/56623911/137312532-7a2119b2-1578-4fad-af0b-980323c5440d.png)


■**Type 1:  JDBC-ODBC 브릿지 + ODBC 드라이버(JDBC-ODBC Brdge Plus ODBC Driver)**

JDK에서 제공하는 드라이버로서 JDBC 뿐만 아니라 ODBC를 같이 이용하여 데이터베이스에 접근하는 방법이다.  데이터베이스와 연결되었다면 모든 문제는 ODBC에 달려있게 되는 것입니다. 이 방법의 이점으로는 기존에 존재하는 ODBC에 연결할 수 있다는 것이고, 약점이라면 ODBC라는 통신을 한 번 더 이용하기 때문에 속도가 JDBC 드라이버를 이용했을 때 보다 느리다는 것입니다.

■**Type 2: 네이티브-API 부분적인 자바드라이버(Native-API Partly-Java Diver)**

이 방식은 로컬에 설치된 원시 라이브러리를 이용해 데이터베이스와 연결된다는 것입니다. 원시라이브러리는 거의 'C'로 작성되어 있습니다. 즉 어플리케이션이 데이터베이스에 JDBC로 요청을 하면이 요청을 원시 라이브러리의 메소드 호출로 변환하여 요청을 하는 것입니다.

■**Type 3: JDBC-NET 순수 자바 드라이버(JDBC-Net Pure Java Driver)**

이 방식은 타입2와 거의 비슷한 방식입니다. 단지 차이점이라고는 타입2가 로컬에 원시 라이브러리가 있어서 이 원시 라이브러리를 이용한다는 것이고, 타입3은 원시 라이브러리가 원격 서버에 있어서 원격 서버에서  원시 라이브러리를 이용한다는 것입니다. 그러므로 원시 라이브러리의 호출이 로컬에서 이루어지는 것이 아니라 원격 서버에서 이루어지므로 인터넷에 연결되어져 있다면 어디서든지 원시 라이브러리를 이용하여 연결되어질 수 있다는 이점이 있습니다.

■**Type 4: 네이티브-프로토콜 순수 자바 드라이버(Naive-Protocol Java Driver)**

이 방식은 그동안 설명했던 방식과 차이점을 가지고 있는데, 가장 중요한 차이점은 바로 순수 자바로 만들어졌다는 것입니다. 순수 자바로 만들어졌으므로 ODBC나 원시 라이브러리를 이용하지 않고 곧바로 데이터베이스에 연결되어진다는 이점이 있습니다. 거의 모든 벤더에서 JDBC를 위한 드라이버를 만들어 놓고 있으며, 그동안 끝까지 드라이버를 만들지 않고 있었던 MS-SQL에서도 현재 베타2까지 내놓은 상태입니다.

JDBC를 통한 Oracle과 연동 테스트

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.*;

public class DriverTest {
	public static void main(String[] args) {
		Connection con;
		
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver").newInstance();
			con=DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "scott","TIGER");
			System.out.println("Success");
		}
		catch(SQLException ex) { System.out.println("SQLException" + ex);
		
		}
		catch(Exception ex) { System.out.println("Exception:" + ex);
		
		}
	}
}
```

- 결과
    
![Untitled 2](https://user-images.githubusercontent.com/56623911/137312543-e12815cc-3b50-4e44-a3cb-b14da942a02c.png)
 
    
- **Tip.JDBC API**
    
    데이터베이스 연결 , 질의 전송, 결과 처리 등의 과정들이 데이터베이스 연동 프로그램시 많이 사용되는 과정들입니다. 이때 쓰이는 인터페이스들은 JDBC API에 존재합니다.
    

## **JDBC API**

- Driver : 모든 드라이버 클래스들이 구현해야 하는 인터페이스
- DriverManager : 드라이버를 로드하고 데이터베이스에 연결
- Connection : 특정 데이터베이스와 연결
- Statement: SQL문을 실행해 작성된 결과를 반환
- PreparedStatement : 사전에 컴파일 된 SQL문을 실행
- ResultSet : SQL문에 대한 결과를 얻어냄

JDBC 프로그래밍 단계 

```
① JDBC 드라이버의 인스턴스 생성
class.forName("Driver_Name");

---------------------------------------------------------------------------------

② JDBC 드라이버 인스턴스를 통해 DBMS에 대한 연결 생성
Connection con = DriverManager.getConnection("DBURL","Account ID", "Account PW");

---------------------------------------------------------------------------------

③ Statement 생성
Statement stmt = conn.createStatement();

---------------------------------------------------------------------------------

④ 질의문 실행/ResultSet으로 결과 받음
ResultSet rs = stmt.executeQuery("select * from ..");

---------------------------------------------------------------------------------

⑤ ResultSet 해지
rs.close();

---------------------------------------------------------------------------------

⑥ Statement해지
stmt.close();
---------------------------------------------------------------------------------

⑦데이터베이스와 연결 해지
conn.close();
---------------------------------------------------------------------------------

```

![Untitled 3](https://user-images.githubusercontent.com/56623911/137312556-52600bc8-686c-4930-87d7-e53dbbedd7aa.png)
