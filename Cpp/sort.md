# sort

## 헤더파일

```c++
#include <algorithm>
```

```c++
sort(a,b) //a는 시작점의 주소, b는 마지막 주소 +1
```

* 예시

  ```c++
  #include <iostream>
  #include algorithm>
  
  using namespace std;
  
  int main(void){
    int a[10] = {9,3,5,4,1,10,8,6,7,2};
    sort(a, a+10);
    for (int i=0; i<10; i++){
      cout << a[i] << ' ';
    }
  }
  ```



## compare() 함수

* Compare() 함수를 sort()의 세 번째 인자 값으로 넣으면, 해당 함수의 반환 값에 맞게 정렬이 동작

  ```c++
  #include <iostream>
  #include <algorithm>
  using namespace std;
  
  bool compare(int a, int b){
    return a>b;
  }
  
  int main(void){
    int a[10] = {9,3,5,4,1}
    sort(a, a+10, compare);
    for(int i=0;i<10;i++){
      cout << a[i] << ' ';
    }
  }
  ```

* 특정한 변수 기준으로 정렬

  ```c++
  #include <iosteram>
  #include <algorithm>
  using namespace std;
  
  class Student{
    public :
    string name;
    int score;
    Student(string name, int score){
      this-> name = name;
      this-> score = score;
    }
    bool operator < (Student &student){
      return this->score < student.score;
    }
    
  };
  
  bool compare(int a, int b){
    return a>b;
  }
  
  int main(void){
    Student students[] = {
      Student("나동빈", 90);
      Student("나동반", 80);
      Student("나동번", 70);
    };
    sort(students, students+3);
    for(int i=0; i<5; i++){
      cout << students[i].name << ' ';
    }
  }
  ```

  