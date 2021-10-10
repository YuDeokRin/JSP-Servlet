# Chapter06 JSP의 지시자와 태그

## 지시자(Directive)

지시자는 클라이언트의 요청에 jsp 페이지가 실행이 될 때 필요한 정보를 JSP 컨테이너에게 알리는 역할을 합니다. 그 역할은 jsp 페이지에 "이렇게 처리를 하시오"라는 지시를 내리는 것입니다.  지시자는 태그 안에서 @ 로 시작하며 다음과 같은 3가지 종류가 있습니다. 

- **Tip. taglib 지시자**
    
    taglib 지시자는 JSP 기능을 확장할 때 사용하는 사용자 정의 태그의 집합을 의미합니다. 한마디로 JSP 태그(액션 태그)가 지원 하지 못하는 부분을 사용자가 직접 작성하여 그 태그를 불러다 사용하겠다는 것입니다.                                                                                                                                    
    
    **<%taglib URI="URI" prefix="tagPrefix"%>**
    

**1) page 지시자**

jsp 페이지에 지원되는 속성들을 정의하는 것들입니다. JSP 지시자는 jsp페이지에서 JSP컨테이너에게 해당 페이지를 어떻게 처리할 것인가에 대한 페이지 정보를 알려주는데 사용되는 것입니다.

![Untitled](https://user-images.githubusercontent.com/56623911/136704151-fb1a441f-d6cb-403a-b65c-93f4248fb546.png)


■info 속성

info 속성은 페이지를 설명해 주는 문자열로 속성값의 내용이나 길이의 제한이 없습니다.

이 속성은 설정을 하지 않더라도 페이지의 처리 내용에는 아무런 영향을 주지는 않지만  jsp페이지의 제목을 붙이는 것과 같은 기능을 하는 속성 입니다.

```java
<%@page info="JSPStudy.co.kr"%>
```

■language 속성

language 속성은 jsp 페이지의 스트립트 요소에서 사용할 언어를 지정하는 속성입니다. 만약 이 속성을 지정하지 않으면 기본값으로 Java가 지정이 됩니다.

```java
<%@page language="java"%> 
```

- **Tip.MIME(Mutil-Purpose internet Mail Extension) 이란?**
    
    MIME[마임]은 인터넷 전자우편 프로토콜, 즉 ,SMTP를 확장하여 오디오, 비디오, 이미지, 응용 프로그램, 기타 여러 가지 종류의 데이터 파일들을 주고 받을 수 있도록 기ㄷ능이 확장된 프로토콜입니다.
    
    서버들은 어떤 웹 전송에서라도 시작부분에 MIME 헤더를 집어넣으며, 클라이언트들은 헤더가 나타내는 데이터 형식(html. gif,xml 등)에 따라 이를 브라우저에서 실행합니다.
    

■contentType 속성

contentType 속성은 jsp 페이지의 내용이 어떤 형태로 출력을  할 것인지 MIME 형식으로 브라우저에 알려주는 역할을 속성입니다. 지정할 속성 값으로는 text/html, text/plain, text/xml, text/gif등 여러 가지 값이 있으며, 기본값은 text/html의 MIME형식입니다.

contentTyep 속성은 jsp 페이지에서 사용하는 문자형식(charset)을 지정하는데 사용할 수 있습니다. charset의 기본값은 ISO-8859-1이고 한글을 지정하는 문자 형식은 EUC-KR혹은 euc-kr로 표현합니다.

```java
<%page contentType="text/html";charset="EUC-KR"%>
```

- page지시자의 예제 - info, language, contentType 속성
    
    ```java
    <%@page info="Copyright 2018 by JSPStudy.co.kr" language="java"
    contentType="text/htmlcharset=EUC-KR"%>
    <h1>Directive Example</h1>
    <%=this.getServletInfo()%>
    ```
    

■extends 속성

jsp 페이지는 JSP Container에 의해서 Servlet으로 변환이 된 후에 처리 결과를 웹 서버에 전송하여 클라이언트에게 보여주게 됩니다. 이때 extends속성은 jsp페이지가  Servlet소스로 변환되는 시점에서 자신이 상속받을 클래스를 지정할 때 사용됩니다. 하지만 JSP 컨테이너가 알아서 적절한 클래스들을 상속시켜 변환해 주므로 사용할 일은 거의 없습니다.

```java
<%@page extends="com.jspstudy.Drietive"%>
//com.jspstudy.Directive클래스를 상속을 하겠다는 의미입니다.
```

■import 속성

jsp 페이지 내에서 package 이름을 지정하지않고 다른 클래스를 가져와서 사용하는 경우, import 속성을 지정할 때 쓰입니다. import 속성은 page 지시자 중에 유일하게 중복 사용이 가능한 속성입니다.

- **Tip 세션(session)이란?**
    
    두 컴퓨터나 네트워크 장치의 논리적인 연결 상태이며 이와 상대되는 개념으로 링크(link)가 있습니다. 즉 웹상에서는 브라우저(클라이언트)와 서버가 계속 연결된 상태를  session이라고 합니다.
    

■session 속성

jsp 페이지가 HttpSession을 사용할지 여부를 지정하는 속성입니다. 이 속성 값은 true와 false로 나뉘어져 있습니다. true일 경우에는 현재의 페이지가 세션을 유지하고 존재하지 않을 경우는 새로운 세션을 생성하여 연결되며,  false일 경우에는 세션에 연결되지 않습니다. 이 속성의 기본값은 true입니다.

```java
<%@page session="false"%>
```

- **Tip. 버퍼(buffer)란?**
    
    동작 속도가 크게 다른 두 장치 간의 인터페이스가 서로의 속도차를 조정하기 위해 이용되는 일시적인 기억 영역을 말합니다. 버퍼는 각 장치나 프로세스가 상대방에 의해 정체되지 않고 잘 작동할 수 있도록 해주며 효율적인 버퍼를 만들기 위해서는, 버퍼의 크기가 상황에 맞게 잘 설계하고, 데이터를 버퍼로 집어넣거나 쉽도록 개발하는 것이 중요합니다.
    

■buffer속성

buffer속성은  jsp 페이지의 출력 크기를 킬로바이트 단위로 지정하는 속성이며 기본값은 "8KB"입니다. buffer 값을 "none"으로 지정하면 출력 버퍼를 사용하지 않고 jsp 페이지의 출력 내용을 즉시 브라우저로 전달하겠다는 의미입니다.

일반적으로 "8KB"가 대부분의 jsp 페이지에서 알맞은 버퍼의 크기입니다. 만약 jsp 페이지가 많은 양의 데이터를 출력한다면, 그에 따라 알맞게 크기를 늘려주는 것이 좋습니다.

```java
<%@page buffer="16KB"%>
<%@page buffer="none"%>
```

■autoFlush 속성

autoFlush속성은 jsp 페이지의 내용들이 브라우저에 출력되기 전에 버퍼에 다 채워질 경우 저장되어 있는 내용들을 어떻게 처리할 지를 결정하는 것입니다.

만약  autoFlush 속성값을 "true"로 설정해 놓으면 버퍼가 다 찼을 경우 자동적으로 비워지게 되어 요청한 내용을 브라우저에게 전송합니다.

기본값은 "true"이며 만약  buffer속성 값이 "none"일 경우 autoFlush속성을  "false"로 지정할 수가 없습니다. 왜냐하면 버퍼가 저장할 공간도 없고, 또 자동적으로 출력할 수 없게끔 설정되기 때문입니다.

■isThreadSafe 속성

isTHreadSafe 속성은 하나의 jsp 페이지가 동시에 여러 브라우저의 요청을 처리할 수 있는지 여부를 설정하는 것입니다.

기본값은 "true"이며 이 속성 값을 "false"로 지정해 놓으면 요청을 동시에 처리하지 않고 요청한 순서대로 처리합니다. 사용자의 내용을 처리하는데 상당이 오랜 시간이 걸릴 수 있으므로 충분히 처리 시간을 고려하여 결정을 해야 합니다.

```java
<%@page isThreadSafe="false"%> 
```

- page지시자의 예제 - import, session, buffer, autoFlush, isThreadSafe 속성
    
    ```java
    <h1>directive Example2</h1>
    <%@page contentType="text/html;charset=EUC-KR" 
       import="java.util.*"
       session="true" 
       buffer="16kb" 
       autoFlush="true" 
       isThreadSafe="true"
    %>
    <%
    	Date date = new Date();
    %>
    현재의 날짜와 시간은?<p>
    <%=date.toLocaleString()%>// <-날짜 Format을 로컬에 맞추어 현재 날짜와 시간을 가져오는 부분입니다.
    ```
    

■ trimDirectiveWhitespaces 속성

trimDirectiveWhitespaces 속성은 디렉티브나 스크립트 코드로 인하여 발생되는 줄 바꿈 공백 문자를 제거하는 기능을 하는 속성입니다.   JSP 2.1버젼부터 새롭게 추가된 속성으로 기본값은 "false"이며, trimDirectiveWhitespaces 속성값을 "true"로 설명하면 불필요한 줄바꿈 공백 문자가 제거 됩니다.

```java
<%@page trimDirectiveWhitespaces="true"%>
```

page 지시자의 예제 - trimDirectiveWhitespaces 속성

```java
<%@page contentType="text/html;charset=EUC-KR"%>
<%@page import="java.util.*"%>
<%@page session="true"%>
<%@page buffer="16kb"%>
<%@page autoFlush="true"%>
<%@page isThreadSafe="true"%>
<% Date date = new Date(); %>
<h1>trim Before</h1>
현재의 날짜와 시간은?<p>
<%=date.toLocaleString()%>
```

- 결과
    
![Untitled 1](https://user-images.githubusercontent.com/56623911/136704157-e28a19e0-a9d7-43d7-ad5d-008b8af0290c.png)

    
![Untitled 2](https://user-images.githubusercontent.com/56623911/136704162-555c0291-82f3-4e4e-978c-1a6a132627e1.png)

    

- 결과 2
    
![Untitled 3](https://user-images.githubusercontent.com/56623911/136704166-cdd4f6fd-cb3c-4695-81a1-598e1e183f04.png)


![Untitled 4](https://user-images.githubusercontent.com/56623911/136704172-09bac388-b2da-4ecc-b988-ff4786ce2f59.png)
    

■errorPage 속성

errorPage 속성은 jsp 페이지를 처리하는 도중에 페이지에서 예외가 발생할 경우 자신이 예외를 처리하지 않고  다른페이지에서 처리하도록 지정할 수 있는 속성입니다. 속성 값으로는 직접 예외를 처리할 페이지의 로컬 URL을 적어주면 됩니다.

```java
<%@page errorPage="Error.jsp"%>
```

■isErrorPage 속성

isErrorPage속성은 현재 jsp 페이지가 에러 처리를 담당하는 페이지인지 아닌지의 여부를 지정할 때 사용되는 속성입니다. 요청된 페이지가 예외를 발생하여 에러 처리를 위해서 만들어지는 에러 페이지라면 isErrorPage 속성 값을 'true'로 설정해야 합니다. 이 속성의 기본값은 'false'로, 에러를 처리하지 않는 페이지라면 설정할 필요가 없습니다.

```java
<%@page isErrorPage="true"%>
```

■pageEncoding 속성

JSP 1.2규약에 새로 추가된 속성으로 jsp 페이지 에서 사용되는 character의 인코딩을 지정할 때 사용됩니다. 기본값으로는 ISO-8859-1로 인코딩이 됩니다.

```java
<%@page pageEncoding="EUC-KR"%>
```

pageEncoding 값은 contentType 속성의 charset과 밀접한 관련이 있습니다. 만약 pageEncoding 속성이 생략이되어 있다면 contentType 속성의 charset의 값을 사용하게 됩니다.

```java
<%@page contentType="text/html";charset="EUC-KR"%>
```

그러나   jsp 페이지를 구현 할 때  EUC-KR로 구현을 하고 응답에 대한 인코딩은 UFT-8로 하고 싶다면 다음과 같이 설정을 해야 합니다.

```java
<%@page contentType="text/html"; charset="UTF-8"
				pageEncoding="EUC-KR"
%>
```

- page 지시자의 예제 - errorPage, isErrorPage 속성
    
    1.
    
    ```java
    <h1>Directive Example3</h1>
    <%@page contentType="text/html;charset=EUC-KR" 
      errorPage="error.jsp"%>
    <%
    	int one = 1;
    	int zero = 0;
    %>
    one과 zero의 사칙연산<p>
    one+zero=<%=one + zero%><p>
    one-zero=<%=one - zero%><p>
    one*zero=<%=one * zero%><p>
    one/zero=<%=one / zero%><p>
    ```
    
    ```java
    <h1>Error Page</h1>
    <%@page contentType="text/html; charset=EUC-KR"	
      isErrorPage="true"%>
    다음과 같은 예외가 발생하였습니다.<p>
    <%=exception.getMessage() %>
    ```
    
    ## include 지시자
    
    여러 jsp 페이지에서 공통적으로 포함하는 내용이 있을 때 이러한 내용을 매번 입력하지 않고 별도의 파일을 저장해 두었다가 JSP 파일에 삽입할 수 있습니다. 이때 지정한 파일에 해당 JSP파일을 삽입하도록 하는 것이  include지시자입니다.
    
    ```java
    <%@include file="로컬URL"%>
    ```
    
    include 지시자를 사용한 jsp 페이지를 컴파일하면 그 과정에서  include되는 jsp페이지의 소스내용을 그대로 포함해서 컴파일하게 됩니다. 즉, 두 개의 파일이 하나의 파일로 구성이 된다는 것입니다.
    
    두 개의 파일을 하나의 파일로 합쳐진 것과 같은 영향을 줌으로서 각각의 페이지가 따로 존재는 하지만 두 개의 페이지는 하나의 페이지처럼 프로그래밍 해야 합니다. 예를 들어 변수를 선언한다고 할 경우 각각의 페이지에 같은 이름의 변수를 선언해서 사용할 수가 없습니다. 하나의 jsp 페이지에 같은 이름의 변수를 중복해서 사용할 수 없는 것과 같습니다.

![Untitled 5](https://user-images.githubusercontent.com/56623911/136704178-1023ee11-2def-46c9-bb91-a673518c89bc.png)
    
    - **Tip. include 지시자**
        
        include 지시자는 홈페이지에서 항상 공통으로 적용되는 파일을 포함시킬 때 사용이 됩니다.
        
        예를 들어 페이지 상단에 있는 메뉴와 페이지의 밑 부분에 있는 사이트 정보, 관리자 이메일, 사이트 연락처 이런 정보들이 있는 파일은 어떠한 페이지에서도 나오는 부분이므로 JSP  파일마다 이런 부분을 포함시킨다는 것은 비효율적인 방법입니다. 이럴 때 Top.jsp(메뉴 파일)과 Bottom,jsp(사이트 정보)를 하나씩 만들어 놓고 필요한 JSP 파일에서 include를 하면 아주 효율적인 프로그래밍을 할 수가 있습니다.
        

include 지시자의 예제

```java
// 01 포함시키는 JSP페이지를 작성하고 저장
<h1>Directive Example4</h1>
<%@page contentType="text/html;charset=EUC-KR"%>
<%@include file="directiveTop.jsp"%>
include지시자의 Body 부분입니다.
<%@include file="directiveBottom.jsp"%>
```

```java
//02 첫 번째 포함되어지는 jsp페이지를 작성하고 저장합니다.
<%@page contentType="text/html;charset=EUC-KR"%>
<html>
<body>
include 지시자의 Top 부분입니다.
<hr>
```

```java
//03 두 번째 포함되어지는 jsp 페이지를 작성하고 저장합니다.
<%@page import="java.util.*"%>
<%@page contentType="text/html;charset=EUC-KR"%>
<%
	Date date = new Date();
%>
<hr>
include 지시자의 Bottom 부분입니다.<p>
<%=date.toLocaleString()%>
</body>
</html>
```

- 결과
    
![Untitled 6](https://user-images.githubusercontent.com/56623911/136704181-32402e06-c802-4487-b26f-5f105fbac79d.png)

    

- **Tip. include 지시자 vs include 액션태그**
    
     include 지시자 외에 뒤에서 배울 include 액션 태그를 통해서도 페이지 삽입이 가능합니다. 그러나 모양도 비슷하고 또 역할도 비슷하지만 기능적으로 약간의 차이가 있습니다. include 지시자는 포함시킬 파일의 내용(소스자체) 전체를 페이지에 넣어 jsp페이지가 Servlet 소스로 함께 변환이 됩니다. 이렇게 될 경우 포함된 페이지가 포함될 페이지의 변수들을 사용할 수 있다는 의미가 되지만 그러나 앞으로 설명할 include 액션 태그의 경우에는 코드를 포함시키는 것이 아니라 해당 시점에 결과를 호출하여 결과를 포함하는 방법을 취하고 있습니다.
    

## 액션태그

JSP에서 액션 태그는 스크립트 요소, 주석, 지시자와 함께 JSP 문법에 속하는 태그

액션 태그는 어떤 동작 또는 액션이 일어나는 시점에 페이지와 페이지 사이에 제어를 이동시킬 수도 있고 또 브라우저에서 자바 애플릿을 실행시킬 수도 있습니다. 

액션 태그 종류 6가지

- include
- forward
- plug-in
- useBean
- setProperty
- getProperty

■include  액션 태그

include  액션 태그는 include 지시자와 함께 다른 페이지를 현재 페이지에 포함시킬 수 있는 기능을 가지고 있습니다.
그러나 include 지시자는 단순하게 소스의 내용이 텍스트로 포함이 되지만 inlcude 액션 태그는 포함 시킬 페이지의 처리 결과를 포함시킨다는 점이 다릅니다. 

```java
<jsp:include page="로컬URL" flush="true"/>
```

include 액션 태그의 flush 속성은 포함될 페이지로 이동할 때 현재 페이지가 지금까지 출력 버퍼에 저장한 결과를 어떻게 처리할 것인가를 결정합니다. 
flush 속성 값을 true로 지정하면 포함할 페이지의 내용을 삽입하기 이전에 현재 페이지가 지금까지 버퍼에 저장한 내용을 출력하게 되는 것입니다.

![Untitled 7](https://user-images.githubusercontent.com/56623911/136704187-7a56cfdd-c7dc-46b8-ad2d-74dbaf58fd91.png)

- include 액션 태그의 예제
    
    ```html
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=EUC-KR"/>
    </head>
    <body>
    <h1>Include Tag Example1</h1>
    <FORM METHOD=POST ACTION="includeTag1.jsp">
    이름 : <INPUT TYPE="text" NAME="name"><p>
    <INPUT TYPE="submit" VALUE="보내기">
    </FORM>
    </body>
    </html>
    ```
    
    - **Tip. form태그**
        
        form태그의 method 속성에는 get 방식과 post방식 두 가지가 있습니다. get 방식은 전송할 데이터를 URL 뒤에 덧붙여서 보내어지고 용량에 제한이 있는 속성이지만, post 방식은 전송할 데이터를 환경변수(header)에 담아서 넘기고 용량에는 제한이 없는 속성입니다.
        
        참고로 get 방식이 먼저 나왔기 떄문에 form 태그에 method의 기본값으로 설정이 되어 있고, post방식이 나온 이유는 가면 갈수록 HTML에서 전송하는 데이터 용량이 많아져서 get 방식으로는 처리가 불가능해졌기 때문입니다.
        
        그리고 <input type="text" name="test">랑 <input name="test">는 동일하게 브라우저에서는 반응을 합니다. 이유는 input="text"가 디폴트(default) 지정이 되었기 때문입니다. 
        
    
    ```java
    <h1>Include Tag Example1</h1>
    <%@page contentType="text/html;charset=EUC-KR"%>
    <%
    	request.setCharacterEncoding("euc-kr"); //form으로부터 전송된 한글을 제대로 출력하기 위해서 필요한 코드입니다.
    	String name = "Korea Football"; 
    //includeTagTop1.jsp에서 name값은 includeTag1.html에서 입력 받은 값으로 처리가 된 후이기 때문에
    // 이 페이지의 name 값은 전혀 상관이 없는 값 됩니다. 
    %>
    <html>
    <body>
    <jsp:include page="includeTagTop1.jsp" />
    //include  액션 태그로 includeTagTop1.jsp를 포함시키고 있습니다. 
    //포함시킬 파일로 이동하여 처리 결과의 내용만을 가지고 다시 현재 페이지로 돌아옵니다.
    include ActionTag의 Body입니다.
    </body>
    </html>
    ```
    
    ```java
    <%@page contentType="text/html;charset=EUC-KR"%>
    <%
    	//includeTag1.html에서 입력받은 name 값을 String변수로 받아서 6라인에서 출력을 하고 있습니다.
    	String name = request.getParameter("name");
    
    %>
    include ActionTag의 Top입니다.
    <p>
    <b><%=name%> Fighting!!!</b>
    <hr>
    ```
    
    - **Tip. get&post**
        
        jsp 페이지에서는 get 방식으로 보내건 post 방식으로 보내건 상관없이 요청되는 매개변수들은 request.getParmeter("...")으로 받습니다. 그렇기 때문에 브라우저의 URL 입력란에 [http://localhost:8080/myapp/includeTag1.](http://localhost:8080/myapp/includeTag1.html)jsp?name=KOREA로 요청을 하면 HTML에서는 FORM태그의 method에 get 방식으로 요청한 것과 똑같은 결과 값이 나옵니다.
        만약 넘어가는 매개변수가 추가 된다면, name=KOREA&msg=Fighting식으로 "&"로 구분을 해서 보내면 됩니다.
        
    
    - include액션 태그의 예제 - 새로운 요청 파라미터 추가
        
        01.브라우저를 통하여 요청하는 html 페이지를 작성하고 저장합니다.
        
        ```html
        <html>
        <head>
        <meta http-equiv="Content-Type" content="text/html; charset=EUC-KR"/>
        </head>
        <body>
        <h1>include Tag Example2</h1>
        <form method="post" action="includeTag2.jsp">
        SITENAME : <input name="siteName"></p>
        <input type="submit" value="보내기">
        </form>
        </body>
        </html>
        ```
        
        02.포함시키는 jsp페이지를 작성하고 저장합니다.
        
        ```java
        <h1>Include Tag Example2</h1>
        <%@page contentType="text/html;charset=EUC-KR"%>
        <%
        	request.setCharacterEncoding("euc-kr");
        	String siteName = request.getParameter("siteName");
        %>
        <html>
        <body>
        <jsp:include page="includeTagTop2.jsp">
        <jsp:param name="siteName" value="JSPStudy.co.kr" />
        </jsp:include>
        include ActionTag의 Body입니다.<p>
        <b><%=siteName%></b>
        <hr>
        </body>
        </html>
        ```
        
        03포함되어지는 jsp 페이지를 작성하고 저장합니다.
        
        ```java
        <%@page contentType="text/html;charset=EUC-KR"%>
        <%
        	String siteName = request.getParameter("siteName");
        %>
        include ActionTag의 Top입니다.<p>
        <%=siteName%>
        <hr>
        ```
        
    
    **include 지시자 vs include 액션태그**
    
    include 지시자는 소스의 내용을 그대로 포함하지만 액션 태그 소스의 내용이 아니라 처리 결과물을 포함하게 됩니다.
    
    따라서 지시자의 경우에는 이를 '정적'으로 처리된다고 표현하며, 액션태그의 경우 '동적'으로 처리 된다고 표현을 하게됩니다. 
    
    ■ forward 액션 태그
    
    forward 액션 태그는 다른 페이지로 이동할 때 사용되는 태그.
    
    jsp 페이지 내에 forward액션 태그를 만나게 되면 forward태그가 있던 jsp 페이지의 모든 내용을 버리고서 forward태그가 지정하는 다른 페이지로 이동하게 됩니다.
    
    - **Tip. forward & include**
        
        forward 태그의 의미는 전환한다는 것이고, include태그는 포함한다는 의미입니다. 그래서 forword태그는 완전히 제어권이 넘어가고 include 태그는 출력되어 내용이 같이 포함되어서 출력이 이루어집니다.
        
    
    로컬 URL로 지정된 값은 상대경로나 절대경로를 지정할 수 있고 또 직접 입력하지 않고 동적으로도 부여할 수 있습니다.
    
    ```java
    <jsp:forward page ="로컬URL"/>
    <jsp:forward page="로컬URL"><jsp:forward>
    <jsp.forward page='<%=expression%>'/>
    ```
    
![Untitled 8](https://user-images.githubusercontent.com/56623911/136704190-8a28d9cd-1d7a-41ee-b976-2665df64ddac.png)

    - forward액션 태그의 예제
        
        01.브라우저를 통하여 요청하는 html 페이지를 작성하고 저장합니다.
        
        ```html
        <html>
        <head>
        <meta http-equiv="Content-Type" content="text/html; charset=EUC-KR"/>
        </head>
        <body>
        <h1>Forward Tag Example1</h1>
        <FORM METHOD=POST ACTION="forwardTag1_1.jsp">
        아이디 : <INPUT TYPE="text" NAME="id"><p>
        패스워드 : <INPUT TYPE="password" NAME="password"><p>
        <INPUT TYPE="submit" VALUE="보내기">
        </FORM>
        </body>
        </html>
        ```
        
        02.forward 시키는 jsp페이지를 작성하고 저장합니다.
        
        ```java
        <h1>Forward Tag Example1</h1>
        <%@page contentType="text/html;charset=EUC-KR"%>
        <%
        	request.setCharacterEncoding("euc-kr");
        %>
        <html>
        <body>
        Forward Tag의 포워딩 되기 전의 페이지입니다.
        	<jsp:forward page="forwardTag1_2.jsp" />
        </body>
        </html>
        ```
        
        03.forward되는 jsp페이지를 작성하고 저장합니다.
        
        ```java
        <h1>Forward Tag Example1</h1>
        <%@page contentType="text/html;charset=EUC-KR"%>
        <%
        	String id = request.getParameter("id");
        	String password = request.getParameter("password");
        %>
        당신의 아이디는<b><%=id%></b>이고<p>
        패스워드는 <b><%=password%></b> 입니다.
        ```
        
    - forward액션 태그의 예제 - 매개변수의 값 추가
        
        01브라우저를 통하여 요청하는 html 페이지를 작성하고 저장합니다.
        
        ```html
        <html>
        <head>
        <meta http-equiv="Content-Type" content="text/html; charset=EUC-KR"/>
        </head>
        <body>
        <h1>Forward Tag Example2</h1>
        <FORM METHOD=POST ACTION="forwardTag2_1.jsp">
        혈액형별로 성격 테스트<p>
        당신의 혈액형은?<p>
        <INPUT TYPE="radio" NAME="bloodType" VALUE="A">A형<br>
        <INPUT TYPE="radio" NAME="bloodType" VALUE="B">B형<br>
        <INPUT TYPE="radio" NAME="bloodType" VALUE="O">O형<br>
        <INPUT TYPE="radio" NAME="bloodType" VALUE="AB">AB형<br>
        <INPUT TYPE="submit" VALUE="보내기">
        </FORM>
        </body>
        </html>
        ```
        
        ```java
        <h1>Forward Tag Example2</h1>
        <%@page contentType="text/html;charset=EUC-KR"%>
        <%
         	String name = "JSPStudy";
         	String bloodType = request.getParameter("bloodType");
         %>
        <jsp:forward page='<%=bloodType + ".jsp"%>'>
         	<jsp:param name="name" value="<%=name%>"/>
        </jsp:forward>
        ```
        
        1. forward되는 jsp페이지를 코딩하고 저장 
        A형
        
        ```java
        <h1>Forward Tag Example2</h1>
        <%@ page contentType="text/html;charset=EUC-KR"%>
        <%
           String name = request.getParameter("name");
           String bloodType = request.getParameter("bloodType");
        %>
        <b><%=name%></b>님의 혈액형은
        <b><%=bloodType%></b>형이고
        성실하고 신중하며 완벽주의자입니다.
        ```
        
        3-1. AB 형
        
        ```java
        <h1>Forward Tag Example2</h1>
        <%@page contentType="text/html;charset=EUC-KR"%>
        <%
        	String name = request.getParameter("name");
        	String bloodType = request.getParameter("bloodType");
        %>
        <%=name%>님의 혈액형은
        <b><%=bloodType%></b>형이고<p>
        정확한 판단력을 가진 합리주의자입니다.
        ```
        
        3-2.B형
        
        ```java
        <h1>Forward Tag Example2</h1>
        <%@ page contentType="text/html;charset=EUC-KR"%>
        <%
           String name = request.getParameter("name");
           String bloodType = request.getParameter("bloodType");
        %>
        <b><%=name%></b>님의 혈액형은
        <b><%=bloodType%></b>형이고 
        규격을 싫어하는 자유인입니다.
        ```
        
        3-3.O형
        
        ```java
        <h1>Forward Tag Example2</h1>
        <%@ page contentType="text/html;charset=EUC-KR"%>
        <%
           String name = request.getParameter("name");
           String bloodType = request.getParameter("bloodType");
        %>
        <b><%=name%></b>님의 혈액형은
        <b><%=bloodType%></b>형이고
        강한 의지의 소유자입니다.
        ```
        

■스크립트 요소를 대체하는 액션 태그

문법적인 구조

```java
<jsp:declaration>코드</jsp:declaration>
<jsp:scriptlet>코드</jsp:scriptlet>
<jsp:expression>코드</jsp:expression>
<jsp:directive.page contentType="text/html; charset=EUC-KR" />
<jsp:directive.include file="xxx.jsp" />
```

- 스크립트 요소를 대체하는 액션태그의 예제
    
    ```java
    <jsp:directive.page contentType="text/html; charset=EUC-KR" />
    <html>
    <body>
     <h1>Script Tag Example</h1>
     <jsp:declaration>
     	public int max(int i, int j){
     		return (i>j)? i : j;
     	}
     </jsp:declaration>
     <jsp:scriptlet> 
        int i = 22; 
        int j = 23;
     </jsp:scriptlet>
     i = <jsp:expression>i</jsp:expression>와 
     j = <jsp:expression>j</jsp:expression> 중에 더 큰 숫자는?
     <b><jsp:expression>max(i,j)</jsp:expression></b>
    </body>
    </html>
    ```
    
    jsp:directive.page  :  앞의 page 지시자(<%@page)와 다르게 XML기반 구분입니다.
    
    <jsp:declaration> : XML기반 이며 <%! %> 와 같은 의미입니다. jsp 페이지에 사용하는 변수(필드)와 메소드를 선언하거나 정의할 수 있습니다.
    
     <jsp:scriptlet>  : XML 끼반 이며 <% %>와 같은 의미입니다. jsp 페이지에 사용하는 변수를 선언하거나 자바 코드를 정의 할 수 있습니다.
    
    i = <jsp:expression>i</jsp:expression> : XML기반이며 <%= %>와 같은 의미입니다. 브라우저에 출력하기 위한 자바코드를 삽입하는 데 사용됩니다.
