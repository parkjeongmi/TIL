# 변경에 유연한 웹 페이지 개발

## 1. 유연한 프로그램 개발

Servlet (비즈니스로직) --(forward)--> JSP (화면)



Request.setAttribute() : 임시로 저장할 때 = 화면에서 쓰려고 전달해줄 때 (대부분의 경우)

Session.setAttribute() : 계속 저장하고 싶을 때 (로그인 같은 특별한 경우)

* PRG = POST Redirect GET
* /order POST -> 주문(insert) -> 포워드 -> "주문완료되었습니다"
* /order POST -> 주문(insert) -> 리다이렉트(GET/loginSuccess.jsp) -> GET "주문완료되었습니다"



* RequestDispatcher 사용 순서

  * RequestDispatcher 객체 획득

    `RequestDispatcher rd = request.getRequestDispatcher("/result.jsp");`

  * View(JSP)에서 필요한 정보를 request 영역에 저장

    `request.setAttribute(“data", “resultData”);`

  * request와 response를 argument로 하여 모든 제어를 전달

    `rd.forward( request, response );`

## 2. MVC 적용한 구조적 프로그래밍

Servlet(logic) -> JSP(view)

Controller(Servlet-흐름제어) -> Model -> View(JSP)



## 3. DAO Pattern 적용한 유연한 프로그래밍

* 문제
  * 매번 새로운 연결을 맺는게 비효율적
  * 커넥션의 개수를 제한하지 않으면 장애가 발생할 수 있음

=> "Pool"

1. 미리 커넥션을 일정 개수 만들어 놓고, 필요할 때 꺼내서 씀

2. 다 사용하면 다시 반납

* 장점
  * 새로운 연결을 맺는 비용을 줄일 수 있음
  * 최초에 만드니깐 시간 단축
  * 개수를 제한할 수 있음



* DB와 연결해서 작업하는 (쿼리를 날리는) 역할 = DAO(Data Access Object)

## Appendix

* 리다이렉트
  * 요청을 다시 보낸다 (클라이언트가)
  * Servlet <---redirect-- -> chrome
  * JSP <--> chrome
  * Chrome -> Servlet ---forward---> JSP -> Chrome



* 화면 응답 : redirect vs forward
  * redirect : 필요할 떄 쓴다 (PRG, Post 같은 것들이 중복되지 않게 방지)
  * forward : 대부분의 경우
* 임시 저장소
  * session : 필요할 때만 쓴다 (로그인)
  * request : view에 전달할 떄 쓴다
* Servlet의 짐을 조금 덜어주자 = MVC 패턴 = Biz(Service)라는 클래스를 만들어서 역할을 나눔



* MVC 패턴
  * Controller = Servlet : 흐름통제 (요청을 받아서 비즈니스 로직을 실행시키고 화면에 데이터 전달)
  * View = JSP : 화면을 보여준다 (HTML)
  * Model= Biz, Dao : 비즈니스 로직
    * Biz : 트랜잭션 관리 (커넥션 연결하고, 커밋, 롤백, 연결 끊기)
    * Dao : 데이터 접근 (statement 날리고, )

