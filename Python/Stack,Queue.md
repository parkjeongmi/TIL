## Stack/Queue

* Stack

  선입후출 LIFO	

  ```python
  list = ['a','b','c']
  list.append('d')
  list.pop()
  #가장 늦게 넣은 d가 가장 먼저 출력됨
  ```

* Queue

  선입선출 LILO

  Deque 사용 필요 (from collections import duque)

  ```python
  list = ['a', 'b', 'c']
  list.append('d')
  list.popleft() #-> deque 필요
  #가장 먼저 넣은 a가 가장 먼저 출력됨
  ```

* Deque

  양쪽 끝에서 자료를 넣고 뺄 수 있음

  ```python
  from collections import deque
  list = deque()
  
  #오른쪽에 a push하기
  list.append('a')
  #왼쪽에 b push하기
  list.appendleft('b')
  
  #오른쪽 데이터 pop하기
  list.pop()
  #왼쪽 데이터 pop하기
  list.popleft()
  ```

  