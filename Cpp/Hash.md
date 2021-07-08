# Hash

* 중복을 허용하지 않는 자료 구조

| 종류               | 라이브러리 내부 구현 |
| ------------------ | -------------------- |
| std::unordered_map | Hash table           |
| std::map           | binary search tree   |



## 1) unordered_map

* 헤더

  ```c++
  #include<unordered_map>
  ```

* 선언

  ```c++
  std::unordered_map<string, int>d;
  //<key의 type, value의 type> name;
  
  cout << d["leo"] << endl; 
  //존재하지 않는 value는 기본 값 -> 0혹은 " "
  
  d["leo"]=3; //"leo" key에 대한 value 업데이트
  cout << d["leo"] << endl;
  ```

* 순회

  ```c++
  for(auto&i:d)
    cout << i.first << "-" << i.second << endl;
  
  //auto를 통해 i의 type은 컴파일러가 추론한 => 여기에서는 순서쌍인 pair
  //i.first = key , i.second = value
  ```

* 예시 : 프로그래머스 - 완주하지 못한 선수

  ```c++
  #include <string>
  #include <vector>
  #include <unordered_map>
  
  using namespace std;
  
  string solution(vector<string> participant, vector<string> completion) {
      string answer = "";
      std::unordered_map<string, int>d;
      for (auto&i : participant) d[i]++;
      for (auto&i : completion) d[i]--;
      for (auto&i : d){
          if (i.second!=0) answer = i.first;
      }
      return answer;
  }
  ```

* 예시 : 프로그래머스 - 위장

  ```c++
  #include <vector>
  #include <unordered_map>
  #include <string>
  using namespace std;
   
  int solution1(vector<vector<string>>clothes){
      int answer = 1;
      unordered_map <string, int> m;
      for (auto clo : clothes){
          m[clo[1]] += 1;
      }
      for (auto n : m ){
          answer *= (n.second+1);
      }
      return answer-1;
  }
  ```

  

## 2) Map

* 헤더

  ```c++
  #include <map>
  ```

* 선언

  ```c++
  std::map<string, int> d;
  //<key의 type, value의 type> name
  
  d.insert({"Cam", 300}); //"Cam" key에 대한 value 300 업데이트
  
  if (d.find("Cam") != d.end()){
    cout << "find" << endl;
  }
  else {
    cout << "not find" << endl;
  }
  //데이터를 끝까지 찾지 못했을 경우, iterator는 map.end()를 반환
  
  map<string, int, greater>d;
  //내림차순의 경우 'greater'를 추가
  ```

* 순회

  * 인덱스 기반

    ```c++
    for (auto iter=d.begin(); iter!=d.end(); i++){
      cout << iter->first << " " << iter->second << endl;
    }
    cout << endl;
    ```

  * 범위 기반

    ```c++
    d.erase(d.begin()+2); //특정 위치의 요소 삭제
    
    d.erase("Cam"); //key 값 기준으로 요소 삭제
    
    d.erase(d.begin(),d.end()); //erase 함수로 모든 요소 삭제
    
    d.clear(); //clear 함수로 모든 요소 삭제
    ```

* 예시 : 프로그래머스 위장

  ```c++
  #include <string>
  #include <vector>
  #include <map>
  
  using namespace std;
  
  int solution(vector<vector<string>> clothes) {
      int answer = 1;
      map<string,int> m;
      for(auto clo : clothes){
          m[clo[1]]+=1;
      }
      for(auto iter=m.begin();iter!=m.end();iter++){
          answer*=iter->second+1;
      }
      return answer-1;
  }
  ```

  