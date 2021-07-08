# Vector

## 핵심

| 종류         | 함수               | 설명                                      |
| ------------ | ------------------ | ----------------------------------------- |
| 추가 및 삭제 | push_back(element) | 벡터 제일 뒤에 원소 추가                  |
|              | pop_back()         | 벡터 제일 뒤에 원소 삭제                  |
| 조회         | [i]                | i번째 원소 반환                           |
|              | at(i)              | i번째 원소 반환                           |
|              | front()            | 첫번째 원소 반환                          |
|              | back()             | 마지막 원소 반환                          |
| 기타         | empty()            | 벡터가 비어있으면 true, 아니면 false 반환 |
|              | size()             | 벡터 원소들의 수 반환                     |



## 헤더파일 & 선언

```c++
#include <vector>
```

```c++
//vector <자료형> 벡터명;
vector <int> v1;
vector <char> v2;
vector <string> v3;
```

```c++
//int
vector <int> v1;
vector <int> v2(10);

vector <int> v3(7,5);
vector <int> v4{0,1,2,3};
vector <int> v5(v2);

//char
vector <char> v1;
vector <char> v2{'a','b','c'};
vector <char> v3(10);

//string
vector <string> v1{"ab", "xyx"};
vector <string> v1 = {"ab", "xyx"};
```



## 멤버함수

* v.size()

  v의 원소의 개수를 반환

* v.empty()

  v가 비어있으면 true(1), 비어있지 않으면 false(0) 반환

* v.front()

  v의 첫번째 원소 반환

* v.back()

  v의 마지막 원소 반환

* v.at(i) 

  v의 i번째 원소 // v[i]와 같음

* v.clear()

  v의 모든 원소 제거

* **v.push_back(5)**

  **v의 맨 뒤에 원소 '5'를 추가**

* **v.pop_back()**

  **v의 맨 뒤에 원소 꺼내기**

* v.insert(i,5)

  v의 i번째 위치에서 원소 '5'를 추가

* v.erase(i)

  v의 i번째 원소 삭제 (v의 size가 1만큼 줄어듬)

* v1.swap(v2)

  v1과 v2를 swap

### iterator

* v.begin()

  beginning iterator를 반환

* v.end()

  end iterator를 반환





## 기타

### sort

* sort(arr,arr+n);
* sort(v.begin(),v.end());
* sort(v.begin(),v.end(),compare); //사용자 정의 함수 사용
* sort(v.begin(), v.end(), greater<자료형>()); //내림차순
* sort(v.begin(),v.end(),less<자료형>());