# Polymorphism

* 다형성은 부모의 타입으로 다양한 형태의 자식 객체를 생성, 참조 할 수 있는 것



## 1. 다형성이란

* 부모 클래스 타입으로 자식 클래스의 객체를 만들어주는 것

```java
//참조 데이터 타입 변수 선언 시
//부모클래스명 변수명 = new 자식클래스명();

Student student = new Student();
Person student = new Student(); // 가능해짐
```



## 2. 동적 바인딩

* **컴파일 할 때 호출되는 메소드**와 **실행할 때 호출되는 메소드**가 유동적으로 적용되는 것



* 부모 클래스 타입으로 자식 클래스의 객체를 만들고 오버라이딩 메소드를 실행하면
* **실제 생성된객체의 메소드**가 실행됨

* 즉, 동적 바인딩은 코드를 실행할 때 **참조 데이터 타입이 아닌 객체 타입의 메소드를 실행**하는 것

```java
//참조 데이터 타입 Person, 객체 생성 Student
//student는 Person 객체의 멤버들만 볼 수 있음
//참조 변수 student는 Student의 멤버인 department, study()는 사용할 수 없음
Person student = new Student();

//참조 데이터 타입 Student, 객체 생성 Student
//student는 Student 뿐만 아니라 부모 클래스인 Person 객체의 멤버들까지 모두 볼 수 있음
Student student = new Student();
```

### 객체의 캐스팅 (Casting)

```java
Person student = new Student();
//참조를 Student로 바꿔주면, Student만 가지고 있는 study()메소드 사용 가능
student.study(); // Error
((Student)student).study(); //OK

Student s2 = (Student)student;
s2.study();

Person teacher = new Teacher();
((Teacher)teacher).teach(); //OK

Teacter t2 = (Teacher)teacher;
t2.teach();
```

### instanceof 연산을 통한 객체 판별

A instanceof B

* A가 B의 자식이거나 같은 class 타입이면 true
* A가 B의 부모이면 false
* A의 참조 데이터 타입과 B의 부모가 동일하면 false
* 부모/자식 관계에 속하지 않는 것끼리 instanceof 하면 컴파일 에러



## 3. 인터페이스

* 인터페이스는 구현되지 않은 메소드로 구성되어 있음



* 인터페이스의 선언

```java
public interface 인터페이스명{ //인터페이스 선언
  public final static Data_Type 상수명 = 상수의 값; //상수 선언
  public Return_Type 메소드명(파라미터1, 파라미터2); //추상 메소드 선언
}

//인터페이스 내부에 선언하는 변수는 무조건 public final static
//인터페이스 내부에 선언하는 메소드는 몸체가 없는 추상 메소드

public interface Flyable{}
public interface Movable{}

public void calculateAverage();
public boolean checkSocialNumber();
```

* 인터페이스의 구현 = 인터페이스는 하위 클래스에 구현을 강제하는 기능이 있음

```java
public class 클래스명 implements 인터페이스명{
  //인터페이스에 선언된 메소드 구현
}

public interface Flayble{
  public void fly();
}
public class Airplane implements Flayble{
  public void fly(){
    //fly() 메소드 내용 구현
  }
}


//다수의 인터페이스 구현 가능 (콤마로 연결)
public class SubClass extend SuperClass implements InterfaceOne, Interfacetwo{
  
}
```



## 4. 내부, 익명 클래스

* 내부 클래스
  * 클래스 안에 선언된 클래스로, 특정 클래스 내에서만 주로 사용되는 클래스를 내부 클래스로 선언함

```java
public class OuterClass{
  class InnerClasS{}
}
```

* 익명 클래스
  * 클래스의 이름이 정의되어 있지 않고, 클래스의 선언과 생성을 동시에 하기 때문에 일회용 클래스

```java
public class OuterClass{
  public Printable doSomething(){
    Printable printlmpl = new Printable(){
      public void print(){
        System.out.println(name);
      }
    };
  }
}
```

* 인터페이스를 이용한 콜백 구현

```java
public class Sum{
  interface OnMaxNumListner{
    void onMaxNumber(int number);
  }
  
  //콜백함수를 등록
  void setOnMaxNumListner(OnMaxNumListner lisner){
    this.listner = listner;
  }
}

public static void main(String[] args){
  //OnMaxNumListner를 구현한 익명클래스
  OnMaxNumListner listner = new OnMaxNumListner(){
    @Override
    public void onMaxNumber(int number){
      System.out.println(number);
    }
  }
}
```