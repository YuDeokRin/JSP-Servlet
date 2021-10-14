# Chapter13 파일업로드

■파일 선택 페이지 예제 

```java
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
</head>
<body>
<form name = "frmName" method="post" enctype="multipart/form-data" action="viewPage.jsp">
	user<br/>
	<input name ="user"><br/>
	title<br/>
	<input type = "file" name="uploadFile"><br/>
	<input type = "submit" value="UPLOAD"><br/>
</form>
</body>
</html>
```

- 결과
    
    ![Untitled](Chapter13%20%E1%84%91%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%A5%E1%86%B8%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20e3eedcf34ecb4d6b9c3987ce437e5d67/Untitled.png)
    
    ![Untitled](Chapter13%20%E1%84%91%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%A5%E1%86%B8%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20e3eedcf34ecb4d6b9c3987ce437e5d67/Untitled%201.png)
    

■**MultipartRequest의 생성자**

```
Method Summary
------------------------------------------------------------------------------------------
java.lang.String | getContextType(java.lang.String name) -업로드 된 파일의 컨텐트 타입을 반환
                 | 하고 업로드된 파일이 없으면 null을 반환합니다.
------------------------------------------------------------------------------------------
java.io.file     | getFile(java.String name) - 서버 상에 업로드된 파일의 객체를 반환하고 업로드
                 | 된 파일이 없으면 null을 반환합니다.
------------------------------------------------------------------------------------------
java.util.Enumeration | getFileNames() - 폼 요소 중 input 태그 속성이 file로 된 파라미터의 
                      | 이름들을 반환하고 업로드된 파일이 없으면 비어있는 Enumeration 객체를 반환
	                    | 합니다.
------------------------------------------------------------------------------------------
java.lang.String | getFilesystemName(java.lang.String name) - 사용자가 지정해서 서버에 실제로
                 | 업로드된 파일명을 반환합니다.
------------------------------------------------------------------------------------------
java.lang.String | getOriginFileName(java.lang.String name) - 사용자가 지정해서 서버에 업로드
                 | 된 파일명을 반환하고 이때의 파일명은 파일 중복을 고려한 파일명 변경 전의 이름을
                 | 반환합니다.
------------------------------------------------------------------------------------------
java.lang.String | getParameter(java.lang.String name) - 스트링으로 주어진 이름에 대한 값을
                 | 반환하고 값 없이 파라미터가 전송되었거나 해당되는 이름의 파라미터가 전송이 
                 | 안 되었을 경우 null값을 반환합니다.
------------------------------------------------------------------------------------------
java.util.Enumeration | getParameterNames() - 모든 파라미터의 이름을 Enumeration 객체로 
                      | 반환합니다.
------------------------------------------------------------------------------------------
java.lang.String[]    | getParameterValues(java.lang.String name) - 주어진 이름에 대한 값을
                      | 스트링 배열로 반환하고 파라미터가 전송되지 않을 때는 null값을 
                      | 합니다.
------------------------------------------------------------------------------------------
```