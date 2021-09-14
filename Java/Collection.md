# Collection

* 객체를 담을 수 있는 신축성 있는 주머니

| -    | 배열                                         | 컬렉션                                            |
| ---- | -------------------------------------------- | ------------------------------------------------- |
| 장점 | 모든 데이터 저장 가능. 사용이 편리함.        | 자동으로 크기를 조절. 명시적인 이름의 메소드 사용 |
| 단점 | 처음에 지정한 크기에서 공간의 크기 변경 불가 | 사용 방법이 다소 복잡                             |

* 컬렉션 프레임워크
  * 데이터 군을 저장하는 클래스들을 표준화한 설계
  * 다수의 데이터를 쉽게 처리할 수 있는 방법을 제공하는 클래스들로 구성
  * 기본 골격
    * 컬렉션을 다루는데 필요한 기능을 가진 3개의 인터페이스 정의 (Set, List, Map)
    * Colelction<E> : 인스턴스 단위의 데이터 저장 기능 제공
    * Map<K, V> : key-value 구조의 인스턴스 저장 기능 제공

## 1. ArrayList <E>

* 데이터를 순차적으로 처리
* ArrayList에 데이터를 추가하는 순서대로 인덱스 번호가 매겨짐
* 데이터 중복을 허용

| 주요 메소드명              | 설명                                  |
| -------------------------- | ------------------------------------- |
| add(Object obj)            | ArrayList에 객체를 하나 추가          |
| get(int index)             | index번에 있는 객체를 반환            |
| remove(int index)          | index번에 있는 객체를 삭제            |
| set(int index, Object obj) | index번에 있는 객체를 obj로 변경      |
| size()                     | ArrayList에 저장된 객체의 개수를 반환 |
| clear()                    | ArrayList의 모든 객체를 삭제          |

```java
//객체 생성
//ArrayList<데이터 타입> 변수명 = new ArrayList<>();
ArrayList<Integer>numbers = new ArrayList<>();
ArrayList<String> fruits = new ArrayList<>();
List<Student> students = new ArrayList<>();

//데이터 추가
//list.add(데이터 값);
numbers.add(100);

//데이터 가져오기
//list.get(인덱스_번호);
int number = numbers.get(0); //인덱스 0 위치에 있는 100
int numSize = numbers.size(); //number 데이터 개수 3

//for문 이용해 ArrayList 데이터 접근
//for(int inx=0; inx<list.size(); inx++){System.out.println(list.get(inx));}
for (int inx=0; inx<fruits.size(); inx++){System.out.println(fruits.get(inx));}

//for-each문 이용해 ArrayList 데이터 접근
//for (데이터타입 변수명 : list){ ... }
for (String fruit : fruits){System.out.println(fruit);}
```



## 2. HashMap<K,V>

* 저장되는 순서가 유지되지 않음
* key의 중복을 허용하지 않음
* key를 이용해 각 value를 구별할 수 있음

| 주요 메소드명                 | 설명                                |
| ----------------------------- | ----------------------------------- |
| put(object key, Object value) | HashMap에 value 객체 하나 추가      |
| get(Object key)               | Key 객체로 저장되어 있는 value 반환 |
| remove(Object key)            | Key 객체로 저장되어 있는 value 제거 |
| keySet()                      | key로만 구성되어 있는 컬렉션 반환   |
| size()                        | HashMap에 저장된 객체의 개수 반환   |
| clear()                       | HashMap의 모든 객체 삭제            |

```java
//객체 생성
//HashMap<키_데이터 타입, 값_데이터타입> 변수명 = new HashMap<>();
HashMap<String, Integer> map1 = new HashMap<>();
HashMap<Integer, Movie> map2 = new HashMap<>();

//데이터 추가
//map.put(키_값, 데이터_값);
map1.put("Production_cost", 1000);
map2.put(20, new Movie("헝거게임", "게리로스"));

//데이터 가져오기
//데이터_타입 변수명 = map.get(키_값);
int production_cost = map1.get("Production_cost");
Movie movie = map2.get(20);
int priceSize = map1.size(); //map1의 데이터 개수는 1

//for-each문 이용해 HashMap 데이터 접근
//for(키_데이터타입 변수명 : map.keySet()){ System.out.println(map.get(변수명));}
for (String key : map1.keySet()){
  System.out.println(map1.get(key));
}

//데이터 내용 교체
//map.put(이미_존재하는_키_값, 데이터 값);
map1.put("Production_cost", 100);

//데이터 삭제
//map.remove(키_값);
map1.remove("Production_cost");

```



## 3. 제네릭스

* 클랙스 내부에 사용할 데이터 타입을 외부에서 지정
* 클래스를 정의할 때 데이터의 타입을 확정하지 않고, 객체를 생성할 때 지정
* 구현의 편의성과 자료형의 안정성 보장 위해 사용

```java
//타입 매개변수는 하나의 대문자 (주로 'T')
//객체 생성시에 <> 안에 매개변수 타입을 선언, 컴파일러에게 사용 타입 전달
Class FruitBox<T>{
  T item;
  public void store(T item){
    this.item = item;
  }
  public T pullOut{
    return item;
    )
}
```

* 제네릭스의 와일드 카드

  * '?'문자로 표시하며 임의의 자료형으로 지정할 수 있도록 해줌

  ```java
  public static void printAll(List<?> list){
    for(object e : list){
      System.out.println(e);
    }
  }
  ```

* 클래스 상속 계층 구조의 와일드 카드

  * super와 extends 예약어를 사용하여 상속 구조상의 경계 지정
  * <?extends T> : T 또는 T의 자손 타입을 의미
  * extends 다음에 나오는 클래스와 그 자식 클래스들이 제네릭 자료형으로 가능

