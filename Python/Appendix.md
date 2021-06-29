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

  ```python
  d = deque([v,i for i, v in enumerate(list)])
  #deque([(2, 0), (1, 1), (3, 2), (2, 3)])
  ```



* List Comprehension

  리스트를 쉽게 생성하기 위한 방법

  ```python
  list = [x*2 for x in range(11)]
  #[0,2,4,6,8,10,12,14,16,18,20]
  ```

  ```python
  list = [1,2,3,4,5]
  
  index = [0 * i for i in range(len(list))]
  #index = [0,0,0,0,0] -> list의 길이만큼 0 생성
  ```
  
  
* 집합 set 

  중복을 허용하지 않는 자료 구조

  ```python
  s = {1,3,5,3,}
  set(s) // {1,3,5}
  ```

  * 원소 추가
    * 하나일 경우 : s.add(4)
    * 여러개일 경우 : s.update([4,5])
  * 원소 제거 (item으로 직접)
    * 없으면 오류 발생 : s.remove(4)
    * 없어도 오류 미발생 : s.discard(4)
  * 연산
    * 합집합 : c = a|b , c = a.union(b)
    * 교집합 : c = a&b, c= a.intersection(b)
    * 차집합 : c = a-b, c = a.difference(b)
    * 대칭차집합 : c = a^b, c = a.symmetric_difference(b)
