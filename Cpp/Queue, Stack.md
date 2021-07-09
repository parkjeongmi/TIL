# 1) Queue

* 선입선출 (First In First Out)
  * front 원소와 back 원소에 접근 가능

* 헤더

  ```c++
  #include <queue>
  ```

* 선언

  ```c++
  queue<int>q;
  //<queue 원소의 type> name;
  ```

* 함수

  | 기본 함수     | 설명                               | 사용                         |
  | ------------- | ---------------------------------- | ---------------------------- |
  | push(element) | 큐에 원소를 추가(맨 뒤)            | q.push(1)                    |
  | pop()         | 큐에 있는 원소 삭제(맨 앞)         | q.pop()                      |
  | front()       | 큐 맨 앞 원소 반환                 | int a = q.front()            |
  | back()        | 큐 맨 뒤 원소 반환                 | int b = q.back()             |
  | empty()       | 비어있으면 true, 아니면 false 반환 | while(!q.empty())            |
  | size()        | 사이즈 반환                        | for(int i=0; i<q.size();i++) |

* 예시 : 프로그래머스 - 기능개발

  ```c++
  #include<queue>
  #include<queue>
  #include<vector>
  using namespace std;
  
  vector<int>solution(vector<int>progresses, vector<int>speeds){
    vector<int> answer;
    queue<int> rest;
    for(int i=0; i<progresses.size(); i++){
      int re = 100-progresses[i];
      if (re%speeds[i]!=0) re += speeds[i]; //예외처리(테스트케이스 11)
  		rest.push(re/speeds[i]);    
    }
    
    while(!rest.empty()){
      int count = 1;
      int now = rest.front();
      rest.pop();
      while(rest.size()>=1){
        if (rest.front<=now){
          rest.pop();
          count++;
        }
        else break;
      }
      answer.push_back(count); //answer는 vector이기 때문에 push_back 사용
    }
    return answer;
  }
  ```



# 1-2) priority_queue

* 헤더

  ```c++
  #include <queue>
  ```

* 선언

  ```c++
  priority_queue<int> pq;
  //<type> 변수명 : 선언한 자료형 변수들을 내림차순에 따라 정렬
  
  priority)queue<int, container, 비교함수>pq;
  //<type, container, 비교함수> 변수명 : 비교함수에 따라 정렬
  ```

* 함수

  | 기본 함수 | 설명                     | 사용             |
  | --------- | ------------------------ | ---------------- |
  | top()     | 맨 앞에 있는 원소를 반환 | int s = pq.top() |

* 예시 : 프로그래머스 - 프린터

  ```c++
  #include <string>
  #include <vector>
  #include <queue>
  using namespace std;
  
  int solution(vector<int> priorities, int location){
    int answer = 0;
    queue<pair<int,int>> que //pair 클래스를 통해 두 객체를 하나로 객체로 묶음 
    priority_queue<int> que2; //priority_queue선언
    for(int i=0; i<priorities.size(); i++){
      que.push(make_pair(i,priorities[i])); //pair를 만들어주는 make_pair함수
      que2.push(priorities[i]);
    }
    while(!que.empty()){
      int f = que.front().first;
      int s = que.front().second;
      if (s==que2.top()){
        if (f==location){
          return answer+1;
        }
        else{
          answer++;
          que.pop();
          que2.pop();
        }
      }
      else{
        que.push(que.front());
        que.pop();
      }
    }
    return answer;
  }
  ```

* 예시 : 오름차순

  ```c++
  #include <iostream>
  #include <queue>
  using namespace std;
  
  int main(void){
    priority_queue<int,vector<int>,greater<int>>pq; //비교함수에 greater<int>를 넣어줌
    pq.push(5);
    pq.push(1);
    pq.push(7);
    for(int i=0; i<3; i++){
      cout << pq.top() << '';
      pq.pop();
    }
  }
  //1 5 7
  ```

  



# 2) Stack

* 선입후출 (First In Last Out)

* 헤더

  ```c++
  #include <stack>
  ```

* 선언

  ```c++
  stack<int> s;
  //stack<type> name;
  
  stack<int> s2({1,2,3,4,5});
  s2.top() //5가 나옴
  ```

  