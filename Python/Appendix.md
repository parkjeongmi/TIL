## Appendix

* enumerate

  인덱스 번호와 컬렉션의 원소를 tuple 형태로 반환

  ```python
  list(enumerate(['a', 'b', 'c']))
  #[(0, 'a'), (1, 'b'), (2, 'c')]
  ```

  반복문 사용 시 몇 번째 반복문인지 확인하기 위해 사용

  ```python
  list = ['a', 'b', 'c']
  for i in enumerate(list) : print(i)
  #(0,a)
  #(1,b)
  #(2,c)
  ```

  시작 인덱스를 변경할 경우는 start 인자를 사용

  ```python
  for i, v in enumerate(['a', 'b,', 'c'], start = 1) :
    print(i, v)
  #1, 'a'
  #2, 'b'
  #3, 'c'
  ```

  

  deque과 연계한 enumerate 사용 (프로그래머스/프린터 문제)

  ```py
  d = deque([v,i for i, v in enumerate(list)])
  #deque([(2, 0), (1, 1), (3, 2), (2, 3)])
  ```

  

