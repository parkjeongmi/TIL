# 웹에서 Database 이용하기

## JDBC

* Java를 이용하여 Database에 있는 값을 활용하기 위한 API
* 연결 순서
  * 드라이버 등록
  * DBMS 연결
  * Statement 생성
  * SQL 생성
  * 결과 받기
  * 연결 닫기

## DBMS

* DML에서의 Transaction 처리

  ```java
  conn.setAutoCommit(false);
  conn.commit();
  conn.rollback();
  ```

  

## PreparedStatement

* SQL 데이터의 동적인 적용

  * 데이터 사용 부분은 ?로 처리

   `String sql = “SELECT EMP_NO FROM TBL_EMPLOYEE WHERE EMP_NO = ?”;`

  * 객체 생성 시, 미완성된 SQL 구문 등록

  `PreparedStatement stmt = conn.prepareStatement( sql );`

  * ?로 처리한 부분에 값을 대입 : ?의 순번을 사용하여 위치 지정

  `stmt.setString( 1, “T10”);`

  * 이미 SQL 문장이 PreparedStatement에 등록되어 있기 때문에 바로 실행

  `stmt.executeQuery();`

## Entity

* Entity = 테이블 데이터(테이블과 1:1 맵핑)
* DTO = Data Transfer Object (C에서 struct) 기능은 없고 데이터 전달만을 위한 객체



## Servlet에서 DB 사용







## Appendix

* Transaction 과 Lock

  * 트랜잭션 = 가장 최소의 업무 단위

  * 배치 프로그램

    * 새로운 데이터를 입력 받고
    * 기존 데이터를 읽어와서
    * 변경된 것은 수정, 없어진 것은 삭제, 생긴 것은 생성

    ```java
    입력받기
    {
      읽어온다 -> 여기서부터 Lock
      비교
     	수정
      삭제
      생성
    } commit / rollback
    ```

    

* 정리

  * http : 프로토콜

  * Localhost: 도메인 (=127.0.0.1)

  * 8080 : 포트

  * /부터 경로

    * ServletExercise_chap3 : context path = 프로젝트 이름(default)
    * loginFail.jsp : WebContent 하위 경로 ex) Servlet/Exervice_chap3/test/test3/test.html

    

    * `http://localhost:8080/ServletExercise-chap3/login `
    * /login : servlet 맵핑(@WebServlet(urlPattern = "/login")) -> 확장자가 없음



* 정리2
  * `<form> `태그의 action ="" ["method"(일반적으로 POST)]
  * `<a>` 태그의 href = "" [GET]
  * `js`ㅇㅔ서 Location.href = "/login" [GET]