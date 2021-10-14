# Chpater12 세션(session)과 쿠키(cookie)

## 세션이란?

■**세션 사용 목적 및 이해** 

- 상태가 없는 프로토콜인 HTTP에서 상태에 대한 보전을 위해서 사용
- 온라인 쇼핑몰에서 사용하는 장바구니에 사용되는 기술
- 사용자의 브라우저와 서버 간의 논리적인 연결
- 서버가 자신에게 접속한 클라이언트의 정보를 갖고 있는 상태

## 쿠키란?

■쿠키 사용 목적 및 이해

- 상태가 없는 프로토콜을 위해 상태를 지속시키기 위한 방법
- 세션과는 달리 클라이언트 자신들에게 그 정보를 저장
- 쿠키를 읽어서 새로운 클라이언트인지 이전에 요청을 했던 클라이언트인지를 판단
- 클라이언트에 대한 정보가 과자 부스러기처럼 남는다고 해서 쿠키라 불림

**세션**은 서버 측에 정보를 남겨두는 것

**쿠키**는 클라이언트 측에 정보를남기는 것

## 쿠키 사용방법

- 쿠키 생성(꼬리표 만들기)

```java
Cookie myCookie = new Cookie("CookieName", "What a Delicious Cookie it is!");
```

Cookie 클래스의 생성자는 스트링 타입의 인자 두 개를 받는 형식을 가지고 있습니다.

CookieName은 생성되어지는 쿠키에 대한 이름을 나타내고, What a Delicious Cookie it is!은 이 쿠키의 값을 말하는 것입니다.

- 쿠키 셋팅(꼬리표에 정보기록하기)

```java
myCookie.setValue("Wow!");
```

쿠키 생성 시 이름에 대응하는 값을 새롭게 지정할 때 사용합니다.

즉, myCookie라는 이름을 가진 쿠키를 생성할 때의 값을 새롭게 지정하기 위해서 사용됩니다.

이 메소드가 수행되면 초기에 생성된 쿠키의 값은 이 메소드에 지정한 스트링 타입의 인자로 변경됩니다.

- 쿠키 전달(꼬리표 붙이기)

```java
response.addCookie(myCookie);
```

응답객체, 즉, response 객체에 지정한 쿠키를 전달합니다. 이렇게 함으로써 클라이언트에 크기가 저장됩니다.

- 쿠키 읽기(꼬리표 읽기)

```java
request.getCookies();
```

클라이언트의 요청과 함께 전달되어져 온  response.addCookie(String cookieName)으로 클라이언트에 저장된 쿠키를 읽습니다. 이 메소드는 클라이언트에 저장된 쿠키를 모두 읽어 옵니다. 반환형은 Cookie[] 타입으로 반환합니다.

- 쿠키 수명주기

```java
cooke.setMaxAge(int expiry);
```

expiry는 초 단위로 쿠키의 초대 수명을 설정합니다. 

처음 쿠키가 생성된 뒤로 여기서 설정 한 초만큼만 쿠키는 유효하게 됩니다. 이 시간을 벗어난 쿠키는 사용기간이 만료된 쿠키로 분류됩니다.

예를들면 쿠키의 생성을 일주일로 설정하기 위해서는 cookie.setMaxAge(7*24*60*60);로 설정합니다. 이는 7:7일, 24:24시간(하루), 60:60분(1시간), 60:60초(1분)라는 뜻입니다.

■**쿠키생성 과정에 대한 절차** 

①쿠키를 생성합니다.

②쿠키에 필요한 설정을 합니다. 예를 들면 쿠키의 유효시간(즉 쿠키의 유통기한을 말하는 것입니다.) 쿠키에 대한 설명 등을 적용하고, 도메인, 패스, 보안, 새로운 값 설정

③클라이언트에 생성된 쿠키를 전송합니다.

```java
쿠키생성                :  Cookie myCookie = new Cookie(String, String)
생성된 쿠키에 대한 설정  :  myCookie.setValue(String)
설정이 완료된 쿠키 전송  :  response.addCookie(myCookie)
```

**■쿠키를 사용하는 절차**

①클라이언트의 요청에서 쿠키를 얻습니다.

②쿠키는 이름, 값의 쌍으로 되어 있습니다. ①의 단계에서 얻어온 쿠키들에서 쿠키이름을 가져옵니다.

③받아온 쿠키이름을 통해서 해당 쿠키에 설정된 값을 추출합니다.

```java
요청에 포함된 쿠키 가져오기 : Cookie[] cookies = request.getCookies()
쿠키 이름을 읽기           : Cookies[i].getName()
얻어진 이름을 통해 정보 사용 : cookies[i].getValue()
```

### Cookie 사용 예제

**01.쿠키를 생성하는 페이지를 작성하고 저장합니다.**

```java
<%@ page contentType="text/html; charset=EUC-KR" %>
<html>
<head>
	<title>Cook Cookie</title>
</head>
<%
	String cookieName = "myCookie";
	Cookie cookie =  new Cookie(cookieName, "Apple");
	cookie.setMaxAge(60); // One minute
	cookie.setValue("Melone");
	response.addCookie(cookie);
%>
<body>
<h1>Example Cookie</h1>
쿠키를 만듭니다.<br/>
쿠키 내용은 <a href="tasteCookie.jsp">여기로</a>!!!
</body>
</html>
```

**02.생성한 쿠키를 이용하는 페이지를 작성하고 저장합니다.**

```java
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Taste Cookie</title>
</head>
<body>
	<h1>Example Cookie</h1>
<%
	Cookie[] cookies = request.getCookies();
	if(cookies!=null){
		for(int i = 0; i<cookies.length; ++i){
			if(cookies[i].getName().equals("myCookie")){
%>
			cookie Name : <%=cookies[i].getName()%><br/>
			cookie Value : <%=cookies[i].getValue()%><br/>	
<% 			
			}
		}
	}
%>
</body>
</html>
```

- 결과
    
    ![Untitled](Chpater12%20%E1%84%89%E1%85%A6%E1%84%89%E1%85%A7%E1%86%AB(session)%E1%84%80%E1%85%AA%20%E1%84%8F%E1%85%AE%E1%84%8F%E1%85%B5(cookie)%2008a21495800e43ce9787c3515010b472/Untitled.png)
    

## 세션 인터페이스

javax.servlet.http 패키지의 HttpSession  인터페이스를 통해서 세션을 사용할 수 있습니다.

쿠키는 클라이언트에 저장이 되어 서버가 쿠키 정보를 읽어서 사용하는 경우였습니다. 하지만, 클라이언트에 저장된 쿠키를 열어볼 수 가 있기 때문에 중요한 정보를 쿠키에 저장할 경우 보안에 문제가 될 우려가 있습니다.

**※Tip.**

서버와 관련되 정보를 노출시키지 않기 위해서 쿠키를 사용하는 것보다 HttpSession 인터페이스를 이용한 세션의 상태관리가 더욱 효율적입니다.

- **Tip. void**
    
    메소드는 함수로 생각합니다. y=f(x)라는 함수표현을 떠올려보세요. f()에 어떤 값 x 넣어서 내부적으로 처리한 결과가 y입니다. 여기서 f가 함수, 메소드입니다. 자바에서는 메소드는 반환형을 가지는데 이 반환형은 메소드 내부에서 처리된 결과에 대한 데이터형(int, char, boolean, 그리고 객체형)을 말합니다. 예를 들면 request.getParameter()에서 getParameter()는 메소드입니다.
    
    이 메소드는 반환형이 String인데, getParameter() 메소드 내부에서 처리된 결과는 String 이기 떄문에 이 메소드의 변환형을 String이라고 하는 것입니다. 하지만 void라는 반환형을 가진 메소드는 수행결과로 반환해 주는 것이 없기 때문에 다른 어떤 것으로도 받을 수가 없습니다.
    

**■Session 객체의 메소드들**

```
메소드 이름                           설명
Object getAttribute(String name)    | name이란 이름에 해당되는 속성값을 Object 타입으로
																	  | 반환합니다. 해당되는 이름이 없을 경우에는 null을 반환합니다.
------------------------------------------------------------------------------------------------------------------
Enumeration getAttributeNames()     | 속성의 이름들을 Enumeration 타입으로 반환합니다.
------------------------------------------------------------------------------------------------------------------
long getCreationTime()              | 1970년 1월 1일 지정을 기준으로 하여 현재 세션이 생성된
                                    | 시간까지 지난 시간을 계산하여 밀리세컨드로 반환합니다.
------------------------------------------------------------------------------------------------------------------
String getId()                      | 세션에 할당된 유일한 식별(ID)를 String 타입으로 반환합니다.
------------------------------------------------------------------------------------------------------------------
int getMaxinactiveInterval()        | 현재 생성된 세션을 유지하기 위해 설정된 최대 시간을
                                    | 정수형으로 반환합니다.
------------------------------------------------------------------------------------------------------------------
void invalidate()                   | 현재 생성된 세션을 무효화시킵니다.
------------------------------------------------------------------------------------------------------------------
void removeAttribute(java.lang.String name)  | name으로 지정한 속성의 값을 지웁니다.
------------------------------------------------------------------------------------------------------------------
void setAttribute(java.lang.String name, java, lang.Object Value) |  name으로 지정한 이름에 value 값을 할당합니다.
------------------------------------------------------------------------------------------------------------------
void setMaxinactiveInterval(int interval) | 세션의 최대 유지시간을 초 단위로 설정합니다.
```

- **세션 생성**

```java
session.setAttribute("mySeesion", "session value");
```

mySession 이란 이름을 가진 세션에 Session value란 값을 설정합니다. 이렇게해서 mySession이 라는 이름을 가진 세션 객체가 생성이 됩니다.

- 세션의 유지시간 설정

```java
session.setMaxInactiveInterval(60*5) ;// 세션 유지시간을 5분으로 설정
```

생성 된 세션의 유지시간을 설정합니다. 세션은 기본적으로 유지시간은 30분입니다. 

사용자 접속 후 세션이 생성되었을 때 이후에 아무런 동작이 없는 동안 세션을 유지하는 최대 시간을 설정하는 부분입니다. 만약 사용자 5분 동안 아무런 동작이 없는 경우, 세션의 최대 지속시간은 5분으로 되었기 때문에 세션은 자동으로 종료가 됩니다.

- 세션 속성 삭제

```java
session removeAttribute("mySession");
```

mySession이란 이름을 가진 세션에 부여된 값을 삭제합니다.

- 세션 삭제

```java
session.invalidate();
```

생성된 세션을 삭제합니다.

- **Tip.기본 세션 시간**
    
    톰켓에서 세션은 기본적으로 30분으로 설정이 되어 있습니다. 즉 세션유지 기간은 30분입니다. 기본값으로 설정된 세션을 사용했을 때, 브라우저로부터 아무런 요청이 없다면, 그리고 이 아무런 요청이 없는 시간이 30분 이상이 되면, 이 브라우저에 연결된 세션은 해체가 됩니다.
    
    세션을 통해 로그인 서비스를 구현했을 때, 로그인 후 30분간 아무런 요청이 없게 되면, 톰캣은 이 브라우저와의 세션을 해제해 버리게 됩니다. 30분 경과 후 로그인 정보가 사라지게 되는 것입니다.
    

**■세션 이용 예제**

01.생성을 생성하는 페이지를 작성하고 저장합니다.

```java
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>세션사용예제(세션생성)</title>
</head>
<body>
<%
	String id = "rorod";
	String pwd = "1234";
	
	session.setAttribute("idkey", id);
	session.setAttribute("pwdkey", pwd);
%>
세션이 생성되었습니다.<br/>
<a href="viewSessionInfo.jsp">세션정보를 확인 하는페이지로 이동</a>
</body>
</html>
```

02.세션에 할당된 이름과 값을 확인하기 위한 jsp페이지를 작성하고 저장합니다.

```java
<%@ page contentType="text/html; charset=euc-kr" %>
<%@ page import="java.util.*" %>
<html>
<head><title>세션사용예제(세션확인)</title></head>
<body>
<%
	Enumeration en = session.getAttributeNames();
	while(en.hasMoreElements()){
		String name = (String)en.nextElement();
		String value = (String)session.getAttribute(name);
		out.println("session name : " + name + "<br>");
		out.println("seesion value " + value + "<br>");
	}
%>
</body>
</html>
```

- 결과
    
    ![Untitled](Chpater12%20%E1%84%89%E1%85%A6%E1%84%89%E1%85%A7%E1%86%AB(session)%E1%84%80%E1%85%AA%20%E1%84%8F%E1%85%AE%E1%84%8F%E1%85%B5(cookie)%2008a21495800e43ce9787c3515010b472/Untitled%201.png)
    
    ![Untitled](Chpater12%20%E1%84%89%E1%85%A6%E1%84%89%E1%85%A7%E1%86%AB(session)%E1%84%80%E1%85%AA%20%E1%84%8F%E1%85%AE%E1%84%8F%E1%85%B5(cookie)%2008a21495800e43ce9787c3515010b472/Untitled%202.png)
    

## Cookie 과 Session 비교

![Untitled](Chpater12%20%E1%84%89%E1%85%A6%E1%84%89%E1%85%A7%E1%86%AB(session)%E1%84%80%E1%85%AA%20%E1%84%8F%E1%85%AE%E1%84%8F%E1%85%B5(cookie)%2008a21495800e43ce9787c3515010b472/Untitled%203.png)

![Untitled](Chpater12%20%E1%84%89%E1%85%A6%E1%84%89%E1%85%A7%E1%86%AB(session)%E1%84%80%E1%85%AA%20%E1%84%8F%E1%85%AE%E1%84%8F%E1%85%B5(cookie)%2008a21495800e43ce9787c3515010b472/Untitled%204.png)

**■각각의 클라이언트를 식별하는 ID를 알아내는 예제**

01.세션을 생성하기 위한 jsp페이지를 작성하고 저장합니다.

```java
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>세션사용예제(세션생성)</title>
</head>
<body>
<%
	String id = "rorod";
	String pwd = "1234";
	
	session.setAttribute("idkey", id);
	session.setAttribute("pwdkey", pwd);
%>
세션이 생성되었습니다.<br/>
<a href="viewCookieSessionInfo.jsp">쿠키 및 세션정보를 확인하는 페이지로 이동</a>
</body>
</html>
```

02세션에 할당된 이름과 값을 확인하기 위한 jsp 페이지를 작성하고 저장합니다.

```java
<%@ page contentType="text/html; charset=euc-kr" %>
<%@ page import="java.util.*" %>
<html>
<head><title>세션사용예제(세션확인)</title></head>
<body>
<%
	Enumeration en = session.getAttributeNames();
	while(en.hasMoreElements()){
		String name = (String)en.nextElement();
		String value = (String)session.getAttribute(name);
		out.println("session name : " + name + "<br>");
		out.println("seesion value " + value + "<br>");
	}
%>
--------------------------------------------------------<br>
<%
	Cookie[] cookies = request.getCookies();
	if(cookies!=null){
		for(int i=0; i<cookies.length;++i){
%>
				Cookie Name : <%=cookies[i].getName()%><br>
				Cookie Value : <%=cookies[i].getValue()%><br>
<%
		}
	}		
%>
</body>
</html>
```

- 결과
    
    ![Untitled](Chpater12%20%E1%84%89%E1%85%A6%E1%84%89%E1%85%A7%E1%86%AB(session)%E1%84%80%E1%85%AA%20%E1%84%8F%E1%85%AE%E1%84%8F%E1%85%B5(cookie)%2008a21495800e43ce9787c3515010b472/Untitled%205.png)
    
    ![Untitled](Chpater12%20%E1%84%89%E1%85%A6%E1%84%89%E1%85%A7%E1%86%AB(session)%E1%84%80%E1%85%AA%20%E1%84%8F%E1%85%AE%E1%84%8F%E1%85%B5(cookie)%2008a21495800e43ce9787c3515010b472/Untitled%206.png)
    

- **Tip. 쿠키의 유효성**
    
    기본적으로 쿠키는 사용자가 브라우저를 종료하는 순간 쿠키의 유효성이 없어지게 됩니다. 쿠키의 정보가 사용자의 컴퓨터에 남아있기는 하지만, 쿠키에 대한 특별한 설정(쿠키의 유효성 지속기간)이 없는 경우 브라우저가 실행되고 있는 동안만 쿠키의 정보가 유효합니다.