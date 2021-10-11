# Chapter07 JSP의 내장 객체

# 내부객체

**학습목표**

- 이번 장에서는 JSP의 내부객체를 공부한다.
- 내부객체별 주요기능과 메소드를 이해한다.

**내부 객체란?** 

jsp 페이지를 작성할 때 특별한 기능을 제공하는 JSP 컨테이너가 제공하는 특별한 객체(변수)를 말합니다.

- JSP 페이지를 작성할 때 특별한 기능을 제공하는 JSP컨테이너가 제공하는 특별한 객체
- JSP에서 선언하지 않고 사용할 수 있는 객체
- 스크립트 요소에서 내부 객체와 동일한 변수명으로 선언할 수 없다.
- 사용되는 범주에 따라 4가지 형태로 분류
    
    1) JSP 페이지 입출력 관련 내부 객체
    
    2) JSP 페이지 외부 환경 정보 제공 내부 객체
    
    3) JSP 페이지 서블릿 관련 내부 객체
    
    4) JSP 페이지 예외 관련 기본객체
    

- **Tip. 내부 객체**
    
    내부 객체의 정확한 명칭은  JSP 규약에서는 implicit object입니다. 국내의 출판된 서적에서는 내장객체, 내부 객체, JSP의 기본 객체 등 조금씩 다르게 번역을 하여 표현을 하고 있습니다.
    

내부객체의 9가지 종류

![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled.png)

jsp 페이지의 내부 객체

```
**내부 객체      type                                     설명**
-----------------------------------------------------------------------------------
request        javax.servlet.http.HttpServletRequest    파라미터를 포함한 요청을 담고 있는 객체
-----------------------------------------------------------------------------------
response       javax.servlet.http.HttpServletResponse   요청에 대한 응답을 담고 있는 객체
-----------------------------------------------------------------------------------
out            javax.servlet.jsp.JspWriter              페이지 내용을 담고 있는 출력 스트림 객체
-----------------------------------------------------------------------------------
session        javax.servlet.http.HttpSession           세션 정보를 담고 있는 객체
-----------------------------------------------------------------------------------
application    javax.servlet.ServletContext             어플리케이션 Context의 모든 페이지가 공유할 데이터를 담고 있는 객체
-----------------------------------------------------------------------------------
pageContext    javax.servlet.PageContext                페이지 실행에 필요한 Context 정보를 담고 있는 객체
-----------------------------------------------------------------------------------
page           javax.servlet.jsp.HttpJspPage            jsp페이지의 서블릿 객체
-----------------------------------------------------------------------------------
config         javax.servlet.ServletConfig              jsp페이지의 서블릿 설정 데이터 초기화 정보 객체
-----------------------------------------------------------------------------------
exctption      java.lang.Throwable                      jsp페이지의 서블릿 실행 시 처리하지 못한 예외 객체
```

**①request, session, application, pageContext**

request, session, application, pageContext내부 객체는 임의 속성 값(attribute)을 저장 하고 읽을 수 있는 메소드를 제공하고 있습니다.

속성값을 저장하고 읽을 수 있는 기능은 jsp페이지들 또는 서블릿 간에 정보를 주고받을 수 있도록 해 줍니다.

- 내부 객체의 속성을 저장하고 읽어내는 공통 메서드

```
**메소드                           설명**
setAttribute(key,value)         주어진 key(이름 등)에 속성값을 연결합니다.
-----------------------------------------------------------------------------------
getAttributeNames()             모든 속성의 이름을 얻어냅니다.
-----------------------------------------------------------------------------------
getAttribute(key)               주어진 key에 연결된 속성값을 얻어냅니다.
-----------------------------------------------------------------------------------
removeAttribute(key)            주어진 key에 연결된 속성값을 제거합니다.
-----------------------------------------------------------------------------------
```

메소드의 파라미터 값으로 value는 Object타입 → 객체의 모든 타입을 저장 가능하고 
key는 String타입의 객체 형태를 가지고 있습니다.

- **Tip. getParameter() 메소드 매개변수**
    
    getParameter() 메소드의 매개변소들은 요청한 페이지의 form 안에 있는 요소들의 name 값입니다. 예를 들어 <input name="id">의 값을 반환하기 위해서 getParameter() 메소드의 매개변수는 id가 됩니다.
    

- request1.html 예제
    
    ```html
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=EUC-KR"/>
    </head>
    <body>
    <h1>Request Example1</h1>
    <FORM METHOD="POST" ACTION="request.jsp">
     성명 : <INPUT TYPE="text" NAME="name"><br/>
     학번 : <INPUT TYPE="text" NAME="studentNum"><br/>
     성별 : 남자 <INPUT  TYPE="radio" NAME="sex"  VALUE="man" checked>
           여자 <INPUT TYPE="radio" NAME="sex" VALUE="woman"><br/>
     전공 : <SELECT NAME="major">
    			<OPTION SELECTED VALUE="국문학과">국문학과</OPTION>
    			<OPTION VALUE="영문학과">영문학과</OPTION>
    			<OPTION VALUE="수학과">수학과</OPTION>
    			<OPTION VALUE="정치학과">정치학과</OPTION>
    			<OPTION VALUE="체육학과">체육학과</OPTION>
    		</SELECT><br>
    <INPUT TYPE="submit" value="보내기">
    </FORM>
    </body>
    </html>
    ```
    
- 결과
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%201.png)
    

- request1.jsp 예제
    
    ```java
    <h1>Request Example1</h1>
    <%@ page contentType="text/html;charset=EUC-KR"%>
    <%
    	request.setCharacterEncoding("euc-kr");
    %>
    <%
    	String name = request.getParameter("name");
    	String studentNum = request.getParameter("studentNum");
    	String gender = request.getParameter("sex");
    	String major = request.getParameter("major");
    
    	if(gender.equals("man")){
    	gender = "남자";
    	}else{
    		gender= "여자";
    	}
    %>
    <body>
    성명 : <%=name%><p>
    학번 : <%=studentNum%><p>
    성별 : <%=gender%><p>
    학과 : <%=major%>
    </body>
    ```
    
- 결과
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%202.png)
    

 

- **Tip. URL와 URI의 차이점**
    
    **URL(Uniform Resource Locator)**은 인터넷에서 접근 가능한 자원의 주소를 일관되게 표현할 수 있는 형식을 말하고 **URI(Uniform Resource Identifier)**는 존재하는 자원을 식별하기 위한 일반적인 식별자를 규정하는 것입니다.
    예를 들어 [http://jspstudy.co.kr./jspstudy/board/List.jsp?table=qnaboard](http://jspstudy.co.kr./jspstudy/board/List.jsp?table=qnaboard에서)에서 URL은 [http://jspstudy.co.kr/jspstudy/board/List.jsp?table=qnaboard가](http://jspstudy.co.kr/jspstudy/board/List.jsp?table=qnaboard가) 되고 URI는 /jspstudy/board/List.jsp?table=qnaboard가 됩니다. URI는 요청된 URL에서 http, 호스트명, port번호(80)뺀 것이라고 생각합니다.
    

- requset 내부 객체의 요청 파라미터 메소드

```
메소드                              설명
String getMethod()                 요청에 사용된 용청 방식(GET,POST,PUT)을 반환합니다.
-----------------------------------------------------------------------------------
String getRequestURI()             요청에 사용된 URL로부터 URI을 반환합니다.
-----------------------------------------------------------------------------------
String getQueryString()            요청에 사용된 Query문장을 반환합니다.
-----------------------------------------------------------------------------------
String getRemoteHost()             클라이언트의 호스트 이름을 반환합니다.
-----------------------------------------------------------------------------------
String getRemoteAddr()             사용 중인 프로토콜을 반환합니다.
-----------------------------------------------------------------------------------
String getProtocol()               사용 중인 프로토콜을 반환합니다.
-----------------------------------------------------------------------------------
String getServerName()             서버의 도메인 이름을 반환합니다.
-----------------------------------------------------------------------------------
int getServerPort()                서버의 주소를 반환합니다.
-----------------------------------------------------------------------------------
String getHeader(name)             HTTP요청 헤더에 지정된 name의 값을 반환합니다.
-----------------------------------------------------------------------------------
```

- request2 예제 - 웹 브라우저와 웹 서버의 정보 반환
    
    ```java
    <%@ page language="java" contentType="text/html; charset=EUC-KR"
        pageEncoding="EUC-KR"%>
    
    <%
    
    	String protocol = request.getProtocol();
    	String serverName = request.getServerName();
    	int serverProt = request.getServerPort();
    	String remoteAddr = request.getRemoteAddr();
    	String remoteHost = request.getRemoteHost();
    	String method  = request.getMethod();
    	StringBuffer requsetURL = request.getRequestURL();
    	String requestURI = request.getRequestURI();
    	String useBrowser = request.getHeader("User-Agnet");
    	String fileType = request.getHeader("Accept");
    %>
    
    <h1>Request Example2</h1>
    프로토콜 : <%=protocol%><p/>
    서버의 이름 : <%=serverName%><p/>
    서버의 포트 번호 : <%=serverProt%><p/>
    사용자 컴퓨터의 주소 : <%=remoteAddr%><p/>
    사용자 컴퓨터의 이름 : <%=remoteHost%><p/>
    사용 method : <%=method%><p/>
    요청 경로(URL) : <%=requsetURL%><p/>
    요청 경로(URI) : <%=requestURI%><p/>
    현재 사용하는 브라우저 : <%=useBrowser%><p/>
    브라우저가 지원하는 file의 type : <%=fileType%><p/>
    ```
    
- 결과
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%203.png)
    

- **Tip. 루프백 주소**
    
    루프백 주소(0:0:0:0:0:0:0:1 또는 ::1)는 루프백 인터페이스를 식별하는 데 사용되며 노드가 자신에게 패킷을 보낼 수 있도록 합니다. 이 주소는 IPv4 루프백 주소 127.0.0.1과 루프백 주소가 지정된 패킷은 링크에서 전송되거나 라우터에 의해 전달되면 안 됩니다. 필자의 컴퓨터에는 사용자 컴퓨터의 주소가 0:0:0:0:0:0:0:1로 표기되었지만 127.0.0.1로 표기되어 나올 수도 있습니다.
    

- **※주의**
    
    브라우저가 지원하는 파일 타입은 브라우저에서 직접적으로 볼 수 있는 파일이거나 또는 실행 프로그램을 호출할 수 있는 파일입니다. 만약 컴퓨터에 MS Office가 설치되어 있으면 Excel, Powerpoint, Word 지원이 가능합니다. 만약 MS Office가 설치된 분은 브라우저가 지원하는 파일타입으로 ms-excel, ms-powerpoint, ms-word가 나오므로 유의하시기 바랍니다.
    

■**response**

response 내부 객체는 요청을 시도한 클라이언트로 전송할 응답을 나타내는 데이터의 묶음입니다.
JSP컨테이너는 요청된 HTTP 메시지를 통해 HttpServletResponse 객체 타입으로 사용되고 response객체명으로 사용합니다.

- response 내부객체의 메소드

```java
메소드                            설명
void setHeader(name,value)        응답에 포함될 Header를 설정합니다.   
void setContentType(type)         출력되는 페이지의 contentType을 설정합니다.
String getCharcterEncoding()      응답페이지의 문자 인코딩 Type을 반환합니다.
void sendRedirect(url)            지정된 URL로 요청을 재전송합니다.
```

setHeader(name, value) 메소드는 HTTP 응답 Header 설정을 위한 메소드입니다.
브라우저가 캐시에 저장하여 사용하지 않고 매번 새로운 요청을 통해 서버로부터 전송받도록 적절한 Header 설정을 예제을 통해서 알아보기 

- response예제
    
    01.응답을 보내는 jsp페이지를 작성하고 저장합니다.
    
    ```java
    <h1>Respose Example1</h1>
    <%
    	response.sendRedirect("response1_1.jsp");
    %>
    ```
    
    02.요청에 따라 서버에서 문서를 찾아 보내는 jsp 페이지를 작성하고 저장합니다.
    
    ```java
    <%@ page language="java" contentType="text/html; charset=EUC-KR"
        pageEncoding="EUC-KR"%>
    <%
    	response.setHeader("Pragma","no-cache");
    	if(request.getProtocol().equals("HTTP/1.1")){
    		response.setHeader("Cache-Control", "no-store");
    	}
    %>
    <html>
    <body>
    	<h1>Response Example</h1>
    	http://localhost/myapp/ch07/response1.jsp가<p>
    	http://localhost/myapp/ch07/response1_1.jsp로 변경이 되었습니다.
    </body>
    </html>
    ```
    
- 결과
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%204.png)
    

- **Tip. Paragma와 Cache-Control**
    
    Pragma와 Cache-Control은 브라우저나 프록시 서버로 하여금 요청 시에 cache된 문서 처리를 위한 헤더입니다. HTTP 1.0에서는 Pragma이고 HTTP 1.1에서는 Cache-Control 헤더에 value값을 지정할 수 있습니다.
    

■**out**

out객체는 jsp 페이지의 결과를 클라이언트에 전송해 주는 출력 스트림을 나타내며 jsp페이지가 클라이언트에게 보내는 모든 정보는 out객체를 통해서 전답됩니다.

- out내부 객체의 메소드

```java
메소드                   설명
boolean isAutoFlush()    출력버퍼가 다 채워져 자동으로 flush 했을 경우는 true반환, 그렇지 않는 경우는 false 바
int getBufferSize()      출력 버퍼의 전체 크리를 바이트 단위로 반한합니다.     
int getRemaining()       출력 버퍼의 남은 양을 바이트 단위로 반환합니다.
void clearBuffer()       현재 출력 버퍼에 저장된 내용을 취소합니다.
String pringln(string)   String을 브라우저에 출력합니다
void flush()             현재 출력 버퍼의 내요을 flush하여 클라이언트로 전송합니다.
void close()             출력의 버퍼의 내용을 flush하고 스트림을 닫습니다.
```

- **out 예제**
    
    01.페이지의 buffer 상태를 출력하는 jsp페이지를 작업하고 저장합니다. 
    
    ```java
    <%@ page language="java" contentType="text/html; charset=EUC-KR"
        pageEncoding="EUC-KR" buffer="5kb"%>
    
    <% 
    	int totalBuffer = out.getBufferSize();
    	int remainBuffer = out.getRemaining();
    	int useBuffer = totalBuffer - remainBuffer;
    %>
    
    <h1>Out Example1</h1>
    <b>현재 페이지의 Buffer 상태</b><p/>
    출력 buffer의 전체 크기 : <%=totalBuffer%>byte<p/>
    남은 Buffer의 크기 : <%=remainBuffer%>byte<p/>
    현재 Buffer의 사용량 : <%=useBuffer%>byte<p/>
    ```
    
- 결과
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%205.png)
    

- **Tip. 버퍼(buffer)란?**
    
    동작 속도가 크게 다른 두 장치 간의 인터페이스가 서로의 속도차를 조정하기 위해 이용되는 일시적인 기억 영역을 말합니다. 버퍼는 각 장치나 프로세스가 상대방에 의해 정체되지 않고 잘 동작할 수 있도록 해주며 효율적인 버퍼를 만들기 위해서는 버퍼의 크기를 상황에 맞게 잘 설계하고, 데이터를 버퍼로 집어넣거나 뺴내기 쉽도록 개발하는 것이 중요합니다.
    

**②session, application, pageContext 내부 객체**

■**session**

내부 객체는 클라리언트 요청에 대한 context정보의 세션과 관련된 정보(데이터)를 저장하고 관리하는 객체입니다.

- **Tip.세션관리란?**
    
    세션을 관리한다는 의미는 웹 브라우저에서 서버가 클라이언트 정보를 저장하고, 요청을 시도한 특정 클라이언트를 다른 클라이언트와 구별하여, 각각의 클라이언트에 대한 정보를 지속적으로 관리하는 상태라고 생각합니다.
    

- session 내부 객체의 메소드

```java
**메소드                                설명**
String getId()                        해당 세션의 세션 ID를 반환합니다.
long getCreationTime()                세션의 생성된 시간을 반환합니다.
long getLastAccessedTime()            클라이언트 요청이 마지막으로 시도된 시간을 반환합니다.
void setMaxinactiveInterval(time)     세선을 유지할 시간을 초단위로 설정합니다.
int getMaxinactiveInterval()          String을 브라우저에 출력합니다.
boolean isNew()                       클라이언트 세션 ID를 할당하지 않은 경우 true 값을 반환합니다. 
void invalidate()                     해당 세션을 종료 시킵니다.
```

- **session예제**
    
    01비밀번호와 아이디를 입력받을 html페이지를 작성하고 저장합니다.
    
    ```java
    <h1>Session Example1</h1>
    <form method="post" action="session1.jsp">
    	아이디 : <input name ="id"><p/>
    	비밀번호 : <input type="password" name="pwd"><p/>
    	<input type="submit" value="로그인">
    </form>
    ```
    
    02.session 개체의 연결을 설정하는 jsp페이지를 작성하고 저장합니다.
    
    ```java
    <%@ page language="java" contentType="text/html; charset=EUC-KR"
        pageEncoding="EUC-KR" session="true" %>
       
    <%
    	request.setCharacterEncoding("EUC-KR");
    	
    	String id = request.getParameter("id");
    	String pwd = request.getParameter("pwd");
    	
    	session.setAttribute("idkey",id);
    	session.setMaxInactiveInterval(60*5);
    %>
    
    <h1>Session Example</h1>
    <form method="post" action="session1_1.jsp">
    	1.가장 좋아하는 계절은?<br/>
    	<input type="radio" name="season" value="봄">봄
    	<input type="radio" name="season" value="여름">여름
    	<input type="radio" name="season" value="가을">가을
    	<input type="radio" name="season" value="겨울">겨울<p/>
    	
    	2.가장 좋아하는 과일은?<br/>
    	<input type="radio" name="fruit" value="watermelon">수박
    	<input type="radio" name="fruit" value="melon">멜론
    	<input type="radio" name="fruit" value="apple">사과
    	<input type="radio" name="fruit" value="orange">오렌지<p/>
    	<input type="submit" value="결과보기">
    	
    </form>
    ```
    
    03요청한 값들을 반환하는 jsp페이지를 작성하고 저장합니다.
    
    ```java
    <%@ page contentType="text/html;charset=EUC-KR"%>
    <%
    	request.setCharacterEncoding("euc-kr");
    %>
    <h1>Session Example1</h1>
    <%
    	String season = request.getParameter("season");
    	String fruit = request.getParameter("fruit");
        String id = (String)session.getAttribute("idKey");    
    	String sessionId = session.getId();
    	int intervalTime = session.getMaxInactiveInterval();
     
    	if(id != null){
    %>
    <b><%=id%></b>님이 좋아하시는 계절과 과일은<p>  
    <b><%=season%></b>과 <b><%=fruit%></b> 입니다.<p>
    세션 ID : <%=sessionId%><p>
    세션 유지 시간 : <%=intervalTime%>초<p>
    <%
    	 session.invalidate();
    	}else{
             out.println("세션의 시간이 경과를 하였거나 다른 이유로 연결을 할 수가 없습니다.");
        }
    %>
    ```
    
- 결과
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%206.png)
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%207.png)
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%208.png)
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%209.png)
    

- **Tip. Session VS Cookie?**
    
    http 프로토콜은 상태가 없는, 즉 이전에 무엇을 했고, 지금 무엇을 했는지에 대한 정보가 없는 특징을 가지고 있습니다. 이러한 점을 보완하기 위해서  Session과 Cookie가 나왔습니다.
    Session은 **서버**가 자신에게 접속한 클라이언트의 정보를 갖고 있는상태를 말하고 그 반대로 쿠키는 세션과는 달리 서버에 클라리언트의 정보를 담아두지 않고 **클라이언트 자신들**에게 그 정보를 저장합니다.
    

■**application**

application 객체는 서블릿 또는 어플리케이션 외부 환경 정보(Context)를 나타내는 객체입니다.

서버의 정보와 자원 그리고 이벤트 로그 같은 정보를 제공합니다.

- application 내부 객체의 메소드

```java
**메소드                       설명**
----------------------------------------------------------------------
String getServerInfo         서블릿 컨테이너의 이름과 버전을 반환합니다.
----------------------------------------------------------------------
String getMimeType(fileName) 지정한 파일의 MIME 타입을 반환합니다.
----------------------------------------------------------------------
String getRealPath(url)      URL를 로컬 파일 시스템으로 변경하여 반환합니다.
----------------------------------------------------------------------
void log(message)            로그 파일에 message를 기록합니다.
```

- **application  예제**
    
    01서블릿과 어플리케이션 정보를 출력하는 jsp페이를 작성하고 저장합니다.
    
    ```java
    <%@ page language="java" contentType="text/html; charset=EUC-KR"
        pageEncoding="EUC-KR"%>
    <%
    	String serverInfo = application.getServerInfo();
    	String mimeType = application.getMimeType("request1.html");
    	
    	String realPath = application.getRealPath("/");
    	application.log("application 내부 객체 로그 테스트");
    	
    	
    %>
    
    <h1>Application Example1</h1>
    서블릿 컨테이너의 이름과 버젼 : <%=serverInfo%><p/>
    RequestExample.html의 MIME Type : <%=mimeType%><p/>
    로컬 파일 시스템 경로 : <%=realPath%>
    ```
    
- 결과
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%2010.png)
    

■**pageContext**

pageContext 내부 객체는 현재 JSP페이지의 Context를 나타내면 pageContext 객체를 통해서 다른 객체를 통해서 다른 내부 객체에 접근할 수 가 있습니다.

PageContext 내부 객체의 메소드 

```java
**메소드                               설명**
ServletRequest getRequest()         페이지 요청 정보를 담고 있는 개체를 반환합니다.
ServletResponse getResponse()       페이지 요청에 대한 응답 객체를 반환합니다.
String getRealPath(url)             URL를 로컬 파일 시스템으로 변경하여 반환합니다.
JspWriter getOut()                  페이지 요청에 대한 응답 출력 스트림을 반환합니다.
HttpSession getSession()            요청한 클라이언트의 세션 정보를 담고 있는 객체를 반환합니다.
ServletContex getServletContext()   페이지에 대한 서블릿 실행 환경 정보를 담고 있는 객체를 반환합니다.
Object getPage()                    페이지의 서블릿 객체를 반환합니다.
ServletConfig getServletConfig()    페이지의 서블릿 초기 정보의 설정 정보를 담고 있는 객체를 반환합니다.
Exception getException()            페이지 실행 중에 발생되는 에러 페이지에 대한 예외 객체를 반환합니다.
```

③**page, config  내부 객체**

**■page**

page 객체는 jsp페이지 그 자체를 나타내는 객체입니다. 그래서 jsp 페이지 내에서 page객체는 this 키워드로 자기 자신을 참조할 수 있습니다. 그리고 page객체는 javax.servlet.jsp.HttpJspPage 클래스 타입으로 제공되는 JSP 내부 객체입니다.

- **page예제**
    
    01페지의 info 속성값을 반환하는 jsp페이지를 작성하고 저장합니다.
    
    ```java
    <%@ page info = "JSPStudy.co.kr"
    	contentType="text/html; charset=EUC-kR"%>
    	
    <%
    
    	String pageInfo = this.getServletInfo();
    %>
    
    <h1>Page Example</h1>
    현재 페이지의 info값 : <%=pageInfo%>
    ```
    
- 결과
    
    ![Untitled](Chapter07%20JSP%E1%84%8B%E1%85%B4%20%E1%84%82%E1%85%A2%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%205ce5fc9d597341b79a00518c25ad86c5/Untitled%2011.png)
    

**■config**

config 객체는 javax.servlet.ServletConfig 클래스 타입의 내부 객체입니다.

ServletConfig는 Servlet에게 Servlet을 초기화하는 동안 참조해야 할 정보를 전해 주는 역할을 합니다. 다시 설명하면 서블릿이 초기화될 때 참조해야 할 다른 여러 정보를 가지고 있다가 전해 준다고 생각합니다.

config 내부 객체의 메소드

```java
**메소드                                설명
-----------------------------------------------------------------------------------------**
Enumeration getInitParameterNames()   서블릿 설정 파일에 지정된 초기 파라미터 이름을 반환합니다.
**-----------------------------------------------------------------------------------------**
String getInitParameter(name)         지정한 name의 초기 파라미터 이름을 반환합니다.
**-----------------------------------------------------------------------------------------**
String getServletName()               서블릿의 이름을 반환합니다.
**-----------------------------------------------------------------------------------------**
ServletContex getServletContext()     실행하는 서블릿 ServletContext를 반환합니다.
**-----------------------------------------------------------------------------------------**
```

**④exception 내부 객체**

exception 내부 객체는 프로그래머가 jsp 페이지에서 발생한 예외를 처리하는 페이지를 지정한 경우 에러 페이지에 전달되는 예외 객체입니다. page 지시자의 isErrorPage 속성을 "true"로 지정한 jps 페이지에서만 사용 가능한 내부 객체입니다. 그리고 exception 객체는 java.lang.Throwable 클래스 타입으로 제공되는 JSP 내부 객체입니다.

exception 내부 객체의 메소드 

```java
**메소드                설명
--------------------------------------------------**
String getMessage()   에레 메시지를 반환합니다
**--------------------------------------------------**
String toString()     에러 실체의 클래스명과 에러 메시지를 반환합니다.
**--------------------------------------------------**
```

- exception 예제
    
    01.예외 처리를 설정한 jsp 페이지를 작성하고 저장합니다.
    
    ```java
    <%@ page contentType="text/html;charset=EUC-KR"
             errorPage="exception2.jsp"
    %>
    <%
      int one  = 1;
      int zero = 0;
    %>
    <h1>Exception Example1</h1>
    one / zero = <%=one/zero%><p>
    ```
    
    02.예외를 처리하는 jsp페이를 코딩하고 저장합니다.
    
    ```java
    <%@ page contentType="text/html;charset=EUC-KR"
             isErrorPage="true"
    %>
    <%
       String message = exception.getMessage();
       String objectMessage = exception.toString();
    %>
    <h1>Exception Example1</h1>
    에러 메세지 : <b><%=message%></b><p>
    에러 실체의 클래스명과 에러 메세지  : <b><%=objectMessage%></b><p>
    ```
    
- 결과