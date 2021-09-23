# Exception / 예외처리

* Exception 객체를 처리하는 것

---

## 1. 예외처리란

* 예외가 발생할 경우
  1. 예외 상황 발생
  2. 에러와 관련된 정보를 가지고 있는 Exception 객체가 생성
  3. Exception 객체가 소멸되지 않으면 프로그램은 비정상적으로 종료

```java
//catch(예외_상황 객체_이름){실행할 구문};

try{
  int result = 10/0;
} catch (ArithmeticException e){
  System.out.println("0으로 나눌 수 없습니다.");
}
System.out.println("예외가 발생하였는가?");
```

* 예외 클래스의 분류

  * Checked Exception : 컴파일 시에 예외 처리를 해 주었는지 체크하는 Exception ex) IOexception

  * Unchecked Exception : 프로그램 실행 중에 발생하는 Exception ex) ArithmaticException

    | 종류                          | 설명                                                         |
    | ----------------------------- | ------------------------------------------------------------ |
    | ArithmeticException           | 산술 연산 중 0으로 나누었을 때 발생                          |
    | NullPointerException          | 참조 데이터형 변수의 값이 null인데 객체에 접근하려고 하는 경우 발생 |
    | ArrayIndexOutOfBoundException | 배열의 범위를 벗어난 인덱스에 접근하려고 할 때 발생          |
    | ClassCatException             | 객체의 형 변환 시, 잘못된 클래스로 변환하려고 할 때 발생     |

## 2. 예외 처리 방법

```java
try{
  //Exception이 발생할 가능성이 있는 구문
} catch(Exception_클래스_타입 변수명){
  //Exception이 발생했을 경우 수행해야 하는 문장
}

//오류가 두 개인 경우는 or로 잡는다
//catch(ArithmeticException e1 | Exception e2)
```

## 2. try ~ catch ~finally

* try 블록 안 코드의 Exception 발생 유무와 상관 없이 반드시 수행해야 하는 문장

* catch 블록이 모두 끝난 후 finally 블록을 작성

  ```java
  try{
    //Exception이 발생할 가능성이 있는 구문
  } catch(Exception_클래스_타입 변수명){
    //Exception이 발생했을 경우 수행해야 하는 문장
  } finally{
  	//반드시 수행해야 하는 문장
  }
  
  try{
    int result = number1 / number2;
  } catch (ArithmeticException e){
   	System.out.println("에러 발생");
  } finally{
    System.out.println("반드시 수행");
  }
  ```

---

## 3. throws

* 호출한 상위 메소드로 발생한 Exception을 던지는 것
* 여러 개의 에러를 모아서 처리하려고 사용

```java
public Return_Type 메소드명 (파라미터)
  throws Exception_Type1, Exception_Type2{
  //메소드 내용
}

public void print() throws Exception{...}
public String getMessage()
  throws IOException, ArithmeticException{...}
```

```java
//상위 메소드로 Exception 던지기
public class ThrowsEX{
  public static void main(String[] args){
    Throws ex = new ThrowsEx();
    
    try{
      // 3) methodA로 인해 예외가 발생
      ex.methodA();
    } catch (Exception e){
      // 4) 아래 출력
      System.out.println("error");
    }
  }
  public void methodA throws Exception{
    // 2) methodB로 인해 예외가 발생하는 구문이지만 Exception을 throw함
    methodB();
  }
  
  public void methodB throws Exception{
    // 1) 예외가 발생하는 구문이지만 Exception을 throw함
    System.out.println(10/0);
  }
}
```

* 강제로 Exception 발생시키기

  ```java
  throw new Exception("Exception 발생 메시지");
  throw Exception_객체
  ```

  ```java
  public static void main(String[] args){
    int age = 10;
  
    try{
      if(age<19){
        throw new Exception("입장 불가!");
      }
      else{
        System.out.println("입장하세요");
      }
    } catch (Exception e){
      System.out.println(e.getMessage());
      //입장 불가! 가 출력된다.
    }
  }
  ```

## 4. 사용자 정의 예외

* 기존에 정의된 예외 클래스를 '상속'받아 새로운 예외 클래스를 정의

```java
Class AgeInputException extends Exception{
  public AgeInputException(){
    super("유효하지 않은 나이가 입력되었습니다.");
  }
}

//사용자 정의 예외 클래스의 처리
// 1) 예외상황이 메서드 내에서 처리되지 않으면, 메서드를 호출한 영역으로 예외의 처리가 넘어간다.
try{
  int age = readAge();
  System.out.println(age);
} catch(AgeInputException e){
  System.out.println(e.getMessage());
}

// 2) 예외가 readAge 메서드 내에서 처리되지 않고 넘어감을 명시
public static void readAge throws AgeInputException{
  Scanner sc = new Scanner(System.in);
  int age = scanner.nextInt();
  if (age<0){
    AgeInputException e = new AgeInputException() throw e; //예외상황 발생지점! 예외를 던진다.
  }
}
```
