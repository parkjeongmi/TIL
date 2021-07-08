# map

* 각 노드가 key와 value 쌍으로 이루어진 트리
* 중복을 허용하지 않음
* first, second가 있는 pair 객체로 저장됨 (first-key, second-value 형태)



## 헤더 파일 & 선언

```c++
#include <map>
map<string,int>m; //map<key type, value type>이름;
```



## map 정렬

* map은 key를 기준으로 오름차순 정렬

* 내림차순으로 정렬하고 싶은 경우 아래 이용

  ```c++
  map<int, int, greater>map1;
  ```

  

## map에서 데이터 search

* Iterator 사용

* 데이터 끝까지 찾지 못했을 경우, iterator는 map.end()를 반환

  ```c++
  if(m.find("Alice") != m.end()){
    cout << "find" << endl;
  }
  else{
    cout << "not find" << endl;
  }
  ```



## map에 데이터 삽입

* map은 중복을 허용하지 않음

* insert를 수행할 때, key가 중복되면 insert 수행되지 않음

  ```c++
  m.insert({"Cam", 300});
  ```



## 반복문 데이터 접근(first, second)

1. 인덱스 기반

   * Iterator 활용하여 begin()부터 end() 까지 찾음

   ```c++
   for(auto iter=m.begin(); iter!= m.end(); i++){
     cout << iter->first << " " << iter->second << endl;
   }
   cout << endl;
   ```

2. 범위 기반

   * map에서 데이터를 삭제하기 위해 활용할 함수는 erase와 clear

   ```c++
   //특정 위치의 요소 삭제
   m.erase(m.begin()+2);
   
   //key 값을 기준으로 요소 삭제
   m.erase("Alice");
   
   //erase 함수로 모든 요소 삭제
   m.erase(m.begin(), m.end());
   
   //clear 함수로 모든 요소 삭제
   m.clear();
   ```

   