## Search

### Brute Force

* 완전 탐색 알고리즘 (해가 존재할 것으로 예상되는 모든 영역 전체 탐색)

* 어떤 구조여도 모든 자료를 탐색해야 함. 따라서 자료구조마다 방법이 있음

  * 선형구조 탐색 : 순차 탐색
    * 주어진 문제를 선형 구조로 구조화
    * 구조화된 문제를 해를 구할 때까지 탐색
    * 탐색한 해를 출력 조건에 맞도록 정리
  * 비선형구조 탐색 : DFS, BFS

  

Brute Force를 이용한 풀이

```python
#프로그래머스-주식가격
def solution(prices) :
  answer = [0] * len(prices)
  for i in range(len(prices)) :
    for j in range(i+1, len(prices)) :
      if prices[i] <= prices[j] :
        answer[i] += 1
      else : 
        answer[i] += 1
        break
   return answer
```

위의 풀이가 Brute Force인 이유는, 초기에 answer = [0] * 개수로 초기화된 리스트를 만들었기 때문이다.