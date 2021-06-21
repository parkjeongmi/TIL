# Hash

* Key-Value 쌍으로 데이터를 저장할 때
* 원소를 넣거나 삭제할 일이 많을 때 사용



## Dictionary

* 기본 활용

  ```python
  dict = {'name' : 'jamie', 'age' : 24}
  
  dict.keys()
  #name, age
  
  dict.values()
  #jamie, 24
  
  dict['job'] = 'student'
  #student 원소를 job이 key인 곳에 추가
  
  del dict['job']
  #job이 key인 것 삭제
  
  dict.pop('jobs', 'no')
  #'jobs'가 key인 것 삭제, 'jobs'가 없다면 'no' 리턴 (get함수와 동일한 원리)
  ```

* 반복문을 이용한 Dictionary 활용

  ````python
  #items를 이용해 key, value 쌍에 순서대로 접근
  for key, value in dict.items() :
    print(key, value)
    
  #key 값에 순서대로 접근  
  for key in dict.keys() :
    print(key)
  ````

* Dictionary 안의 원소 확인

  ```python
  dict = {'name', :'jamie', 'age' : 24}
  student = {'gildong', 'donggil', 'dongdong'}
  
  for value in dict.values() :
    if value in student :
      print(value)
     	#jamie
  ```

* Get 함수

  ```python
  get(key, x)
  #key가 존재하면 value 반환, 없으면 x 반환
  
  dict = {'name', : 'jamie', 'age' : 24}
  dict.get('jobs', 'no')
  #'no' 반환
  ```

  