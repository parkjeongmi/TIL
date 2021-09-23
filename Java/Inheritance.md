# Inheritance / 상속

## 1. 상속이란

* 상위 개념의 특징을 하위 개념이 물려 받는 것

-> 각 클래스에 공통적으로 반복되는 부분을 묶어서 독립된 클래스로 만든 후, 각 클래스가 그 클래스를 상속 받도록 함

```java
public class 자식클래스명 extends 부모클래스명{}

public class Student extends Person{}
public class Teacher extends Person{}
```



* 상속에서의 생성자
  * 생성자는 객체 생성 시, 자신의 클래스에 대한 객체만 생성함
  * 자식 클래스에서는 부모의 필드나 멤버 메소드를 사용해야 하기 때문에 부모의 생성자를 호출하여 부모의 객체를 만들어 주어야 함

```java
//자식 클래스 생성자의 첫 번째 줄에 super 키웓를 이용하여 부모의 생성자를 호출
//명시적으로 부모의 생성자를 호출하지 않는 경우, 자동으로 super(); 추가

public class Person{
  public Person(){} // 기본 생성자가 없는 경우 에러 발생
  public Person(String name, String phoneNumber){
    this.name = name;
    this.phoneNumber = phoneNumber;
  }
}

public class Student extends Person{
  public Student(String department){
    super(); //자동으로 추가
    this.department = department;
  }
  
public Student(String name, String phoneNumber){
  super(name, phoneNumber);
}
}
```

```java
//super 키워드를 이용하여 생성자를 명시적으로 호출하는 경우, 
//반드시 생성자의 첫 번째 줄에 기술되어야 함
//또한, super()와 this()를 같이 호출하지 못함

public class Student extends Person{
  public Student(String name, String phoneNumber){
    super(name, phoneNumber);
    this(name, phonNumber, null); //Error : super()와 this() 같이 사용 불가
  }
  
  public Student(String name, String phoneNumber, String department){
    this.department = department;
    super(name, phoneNumber) // Error : 반드시 첫 번째 줄 기술
  }
}
```



## 2. 오버라이딩

* 부모롤부터 상속 받은 메소드의 내용을 다시 정의하는 것



* 메소드 오버라이딩이란
  * 부모 클래스의 메소드의 내용을 자식 클래스에서 다시 정의하는 것

* 메소드 오버라이딩의 조건
  * 메소드 이름이 같아야 함
  * 메소드 파라미터 개수와 데이터 타입이 같아야 함
  * 메소드의 리턴 타입이 같아야 함
  * 접근제어자는 부모이 것과 같거나 더 넓은 범위여야 함
* 메소드 오버라이딩 할 수 없는 경우
  * 부모 클래스의 메소드 접근 제어자가 private으로 선언되어 있는 경우
  * 부모 클래스의 메소드가 final 키워드로 선언되어 있는 경우
    * final을 붙인 메소드는 나를 오버라이딩 할 수 없다는 의미



## 3. Object Class

* 모든 클래스의 부모 클래스
* 최상위 클래스
* Extends 키워드를 사용하지 않은 클래스는 자동으로 extends Object를 추가
* toString()과 같은 유용한 메소드 제공



## 4. 추상 클래스

* 추상 클래스란

  * body가 없는 메소드를 포함한 클래스
  * Abstract 클래스일 경우 클래스의 선언부에 abstract 키워드를 사용

  ```java
  public abstract class Example{	
  }
  ```

* 추상 메소드란

  * 메소드의 몸체({})가 없는 메소드를 추상 메소드로 지칭
  * 몸체 없는 메소드의 선언부에 abstract 키워드를 사용

  ```java
  public abstract void sayHOwareyou(); //선언 후 세미콜론
  ```

  

* 추상클래스의 특징
  * 미완성 클래스
  * 자체적으로 객체 생성 불가 -> 반드시 상속 통하여 객체 생성
  * 객체 생성은 안되나, 참조 변수 타입으로는 가능 ex) Appliance app = new Radio(); // Appliance는 추상 클래스
* 추상클래스의 장점
  * 일관된 인터페이스 제공
  * 꼭 필요한 기능 강제함