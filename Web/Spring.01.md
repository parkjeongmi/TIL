

# 스프링과 객체지향

## 1. 스프링이란

객체 지향 언어가 가진 강력한 특징을 살려내는 프레임 워크

* Spring Framework : 핵심 기술
* Spring Boot : 스프링을 편리하게 사용할 수 있도록 지원 / 톰캣 서버 내장



객체 지향 프로그래밍 (Object-Oriented Programing : OOP)

* 컴퓨터 프로그램을 명령어의 목록으로 보는 시각에서 벗어나 여러 개의 독립적 단위인 객체들의 모임으로 파악하고자 하는 것. 각각의 객체는 메시지를 주고 받고 데이터를 처리함

* 프로그램을 유연하고 변경이 용이하게 만든다
* OOP의 4대 특성
  * 캡슐화 : 객체의 속성과 행위를 하나로 묶음 (클래스) / 실제 구현 내용을 일부 외부에 감추어 은닉함. / 필요한 정보만 알려주면 됨
  * 상속 : 이미 존재하는 객체를 기반으로 확장된 객체를 만드는 방법 / 기존 객체에 속한 송석과 동작을 물려 받음
  * 다형성 : 같은 지시에 대해 다른 종류의 객체가 동작을 다르게 하는 것 / 어떤 구현이 실행될 지는 실행 중에 결정 됨 / 다형성을 사용하려면 상속 관계가 필요함
  * 추상화 : 객체 사용 시 그 안에 정확히 어떤 데이터가 있는지 알 필요가 없음
  * 컴포지션 : 여러 개의 부품으로 새로운 개체를 만드는 방법
  * 집합 : 여러 객체를 모아 다른 객체를 만들지만, 별도로 존재 가능
  * 연관 : 어떤 객체가 제공하는 기능을 다른 객체가 이용하는 관계

* 재사용성 : 테스트 시간 절약 / 관리 비용 절감
* 객체지향 5원칙 (SOLID)
  * 단일 책임 원칙(SRP) : 하나의 클래스는 하나의 책임 가져야 함
  * 리스코프 치환원칙(LSP) : 프로그램 객체는 프로그램의 정확성을 깨뜨리지 않으면서, 하위 타입의 인스턴스로 바꿀 수 있어야 함
  * 인터페이스 분리 원칙(ISP) : 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스보다 낫다
  * 의존관계 역전 원칙(DIP) : 프로그래머는 추상화에 의존해야지, 구체화에 의존하면 안됨
  * 개방 폐쇄 원칙(OCP) : 소프트웨어 요소는 확장에 열려 있으나 변경에는 닫혀 있어야 함



# 2. 스프링 DI 컨테이너

DI : Dependency Injection

IOC : Inversion Of Control



"Spring이 다 관리하고

우리는 Spring 한테 받아서 쓸거야""

1. Spring 한테 어떻게 등록해?
   * config 파일 위에 @Bean 달아서 리턴을 해줘
   * Class 위에 @Component 달아
2. Spring한테 어떻게 받아서 써? = 받아서 쓰려면 받는 놈도 받을 놈도 Spring에 등록되어 있어야 함
   - @Autowired를 달아줌
   - 어디에?
     - 생성자 위에 ** 
     - Setter 위에
     - 필드 위에

3. Qualifier / 이름 : 중복과 충돌을 해결한다.



-> new MemberDao(); -> 이런 걸 다 없애자 -> Spring에 등록하고 Spring한테 받자!



## 복습

* 웹 환경에서 통신하는 방법
  * HTTP -> Servlet: @WebServlet(urlPattern = "/") <- WAS가 이걸 매핑해줌 / extends HTTPServlet
  * URI(URL)
  * JSP = HTML 형식에 맞게 코드를 작성할 수 있다.
  * Servlet(Controller) -> JSP(View)
  * JDBC = Java가 DB와 통신하는 규약
  * {Connection 받아 와서 / 뭔가 수행 / 커밋 / 롤백 / Connection 반납} = 트랜잭션 = Lock 격리 수준
  * Dao Biz
  * MVC 패턴 = Servlet(Controller) -> 비즈니스. 로직을 수행하는 Biz 클래스 -> JSP(View)
  * Biz = 트랜잭션 관리 전담
  * Dao = DB와의 교류
  * Query
  * Form
  * GET POST DELETE PUT 
  * forward / redirect (멱등성 -> Post/Redirect/Get)
  * request / session (꼭 필요한 데이터만 담자)
  * JSP EL/JSTL
  * Dao의 리팩토링 -> abstract / interface



## 기타

* Reference : 인프런(김영한, 백기선) / 포프 + 토비의 스프링
* 김영한 : 스프링 핵심 원리 - 기본편