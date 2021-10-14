# EL /JSTL

`${RESULT}`

`<%=loginName%>`   ->      `${loginName}`



[필수] 상단에 넣기

```html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```



* c : url

  * `<form action=*"/exercise/login"* method=*"post"*>`
  * `  <form action="<c:url value = /login"/>", method="post">`

* c : if

  ```html
  if(type.equals("error")){
      //사용자가 원인을 알 필요가 없는 오류 발생에 대한 처리
  %>
    	<font color="red">오류가 발생했습니다</font>
  <%
  	}else if(type.equals("loginFail")){
      //로그인 실패시에 메세지 처리( 해당하는 사용자 정보가 없음)
  %>
    	<font color='green'>회원이 아닙니다. 다시 시도하세요.<br/>
    	<a href='/exercise/loginForm.html'>로그인</a></font>
  <%
  	}else if(type.equals("writeSuccess")){
      //게시글 등록이 성공하였을 경우 메세지 처리
  %>
    	<font color='green'>등록되었습니다. <br/><br/>
    	<a href='/exercise/freeboardList'>게시글 목록보기</a></font>
  <%
  	}
  %>
  ```

  

* c : choose

* c : foreach

  ```html
  for(int i=0; i<list.size(); i++) {
  			    FreeBoardEntity entity = list.get(i);
  		
  		      <tr>
  		      <td><%= entity.getBnum()%></td>
  		      <td><%= entity.getContent()%></td>
  		      <td><%= entity.getWriteDate()%></td>
  		      <td><%= entity.getMid()%></td></tr>
  	
  			}// for문 종료
  ```

  ```html
  <c:forEach items="${FreeBoardEntity} }" var="entity">
  					<tr>
  				      <td><%= entity.getBnum()%></td>
  				      <td><%= entity.getContent()%></td>
  				      <td><%= entity.getWriteDate()%></td>
  				      <td><%= entity.getMid()%></td></tr>
  				</c:forEach>
  ```

  



## 복습

* Client -> Server
  * GET : query
  * Post : form

* Session : Client로 구성된 저장 장소
  * redirect : 응답을 받은 클라이언트에게 요청을 다시 요청.  : 비효율적
  * forward : 클라이언트는 요청 1회. 하지만 refresh 할 경우 데이터가 다시 넘어가니 redirect로 보내야 함

* 멱등성

  * GET : 조회 -> 다시해도 문제 없음

  * POST : 생성 + 처리
  * PUT : 업데이트
  * DELETE : 삭제

* JDBC : Java와 database와 통신

  1. Connection

  2. Statement ->

  3. Result Set

  4. Result Set 닫기

  5. Statement 닫기

  6. commit (Connection 닫기 전) -> try `JdbcUtil.commit(conn);`

  7. rollback (Connection 닫기 전) -> catch `JdbcUtil.rollback(conn);`

  8. Connection 닫기 -> finally `JdbcUtil.close(conn);`

  -> 한 단위가 트랜잭션!!!!



## 기타

SSR

* Client -> Server   /  Server---HTML ---> Client
* 즉, HTML이 완성될 때까지 안보내줌. 로드가 오래 걸림 (못기다리고 새로고침 ~ 또 로드)
* 지금은 HTML을 만들 때 JSP를 사용하고 있음!

CSR (=최대한 빨리 뼈대를 보여줌) ex) React

* HTML 뼈대만 받아와서 대강 그림 / 나중에 세부사항 바꿈
* 즉, 골격을 먼저 보고 / 세부사항은 기다림



Exception

* Checked Exception (only java)
  * 컴파일러가 잡아줌 -> 처리하지 않으면
  * Exception을 상속받음
  * throws를 하든지, try catch로 잡는다
* Unchecked Exception
  * 컴파일러가 안 잡아줌
  * RuntimeException을 상속받음

+예외 상황이 발생하면 꼭 Exception을 throw해야하고

throw한 Exception은 꼭 처리해야 함



## 설치

Intellij Community(설치완료) -> Intellij Ultimate (30)

Postman (설치완료)

VS Code > Open Option 추가하기

