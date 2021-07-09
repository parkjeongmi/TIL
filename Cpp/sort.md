# Sort

* 헤더

```c++
#include <algorithm>
```

* 선언

```c++
sort(start, end) //[start, end) 범위의 인자를 오름차순으로 정렬
sort(start, end, compare) //compare 기준으로 정렬
sort(start, end, greater<자료형>()) //[start, end) 범위의 인자를 내림차순으로 정렬
```

* 예시(내림차순) : 프로그래머스 H-Index

  ```c++
  #include <algorithm>
  #include <string>
  #include <vector>
  
  using namespace std;
  
  int solution(vector<int> citations){
    int answer = 0;
    sort(citations.begin(), citations.end(), greater<int>()); //greater<int>()
    if(!citations[0]) return 0;
    for(int i=0; i<citations.size(); i++){
      if(citations[i]>i) answer++;
      else break;
    }
    return answer;
  }
  ```



## + sort(start, end, compare)

* compare() 함수를 sort()의 세 번째 인자 값으로 넣으면, 해당 함수의 반환 값에 맞게 정렬이 동작

* 예시

  ```c++
  #include <iostream>
  #include <algorithm>
  using namespace std;
  
  bool compare(int a, int b){
    return a>b;
  }
  
  int main(void){
    int a[10] = {9,3,5,4,1}
    sort(a, a+10, compare); //위의 compare에 따라 정렬함
    for(int i=0;i<10;i++){
      cout << a[i] << ' ';
    }
  }
  ```

* 예시 : 프로그래머스 - 가장 큰 수

  ```c++
  #include <string>
  #include <vector>
  #include <algorithm>
  using namespace std;
  
  bool compare(int a, int b){
    string first = to_string(a) + to_string(b);
    string second = to_string(b) + to_string(a);
    return first > second;
  }
  string solution(vector<int> numbers){
    string answer = "";
    sort(numbers.begin(), numbers.end(), compare);
    for(auto&i:numbers){
      answer+=to_string(i);
    }
    return answer[0]=='0' ? "0" : answer; // a ? b : c -> a이면 b이고, 아니면 c
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

  

## + Appendix

* string::substr(시작인덱스, 문자열 길이)

  ```c++
  s1 = s.substr(2,3) //2번 인덱스부터 문자열 3개
  ```

* string::substr(시작인덱스)

  ```c++
  s2 = s.substr(1) //1번 인덱스부터 문자열 끝까지
  ```

* 예시

  ```c++
  if (phone_book[i] == phone_book[i+1].substr(0, phone_book[i].size()))
  //1) phone_book의 i번째 원소와
  //2) i+1번째 원소를 0부터 phone_book[i]의 사이즈만큼의 길이로 자른 것
  //1)과 2)가 같다면!
  ```

  

