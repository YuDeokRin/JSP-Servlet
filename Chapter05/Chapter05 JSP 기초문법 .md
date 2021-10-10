# Chapter05 JSP 기초문법

# JSP 기초 문법

**JSP의 스크립트(Script)**

스크립트의 요소란 JSP프로그래밍에서 사용되는 문법의 표현 형태를 말합니다.

JSP에서는  동적인 페이지를 생성하기 위해서 다양한 형태를 제공하여 각각 필요한 곳에 적절히 사용할 수 있도록 하고 있습니다. 

■JPS의 스크립트 요소 4가지

①선언문(Declaration)

②스크립트릿(Scriptlet)

③표현식(Expression)

④주석(Comment)

### ①**선언문(Declaration)**

JSP 프로그램의 스크립트 요소 중 선언문(Declaration)은 JSP에서 사용될 변수나 메소드를 선언할 수 있는 영역의 요소를 의미합니다.

jsp페이지 내에서 변수 및 메소드를 선언을 하고 선언된 변수나 메소드를 이용하여 필요한 동적인 HTML코드를 생성하는데 사용하는 것입니다.

선언문에서 선언된 변수는 멤버 변수(member variable)이다.

- 선언문 문법

```
<%! 
		멤버변수 및 메소드를 선언하는 영역
%>
```

1) 멤버변수 선언

- 예제
    
    ```java
    <%@ page contentType="text/html;charset=EUC-KR"%>
    
    <h1>Declaration Example1</h1>
    
    <%
    
    String name = team + " Fighting!!!";
    
    %>
    
    <%!
    
    String team = "Korea";
    
    %>
    
    출력되는 결과는? <%=name%>
    ```
    

2) 메소드(method)선언

- 예제
    
    ```java
    <%@ page contentType="text/html;charset=EUC-KR"%>
    <h1>Declaration Example2</h1>
    <%!
          int one;
          int two = 1;
          public int plusMethod(){
           return one + two;
          }
          String msg;
          int three;
    %>
    
    one와 two 합은 ? <%=plusMethod()%><p>
    String msg의 값은? <%=msg%><p>
    int three의 값은 ? <%=three%>
    ```
    

### ②스트립트릿

스트립트릿(Scriptlet)요소는 가장일반적으로 많이 사용되는 스크립트 요소로 jsp  페이지가 서블릿으로 변환되고 요청될 때 _jspService (Tomcat 기준으로 설명) 메소드 안에 선언이 되는 요소입니다. 그리고 스크립트릿은 선언문과 달리 선언된 변수는 지역 변수로 선언이 되고 메소드 선언은 할수 없습니다.(만약 선언을 하게 되면 메소드 안에 메소드를 선언한 것이기 때문에 만들 수가 없습니다.)

- 스트립트릿의 문법

```
<%
	이곳에 필요한 자바코드를 삽입합니다.(지역 변수 선언, for, while, if 등...)
%>
```

### ③표현식

표현식(Expression)은 말그대로 동적인 jsp페이지를 브라우저로 표현을 하기 위한 요소입니다.

표현식은 변수를 출력하거나 메소드의 결과 값을 브라우저에 출력할 수 있습니다.

- 표현식문법

```
<%=변수 혹은 메소드%>
```

1)표현식의 활용

- 표현식 요소 예제
    
    ```java
    <%@ page contentType="text/html;charset=EUC-KR"%>
     <h1>Expression Example1</h1>
    <%!
    	String name[] = {"Java","JSP","Android","Struts"};
    %>
    <table border="1" width="200">
    <% for (int i=0;i<name.length;i++){%>
    <tr><td><%=i%></td>
    <td><%=name[i]%></td>
    </tr>
    <%}%>
    </table>
    ```