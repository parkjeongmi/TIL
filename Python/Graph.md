# Graph



## BFS

* 너비우선탐색

* Queue를 사용해서 들어온 순서대로 나간다.

  ```python
  from collections import deque
  
  def bfs(graph, start_node) :
    visit = []
    queue = deque(start_node)
    while queue :
      node = queue.popleft()
      if node not in visit :
        visit.append(node)
        queue.extend(graph[node])
    return visit
  ```

  

## DFS

* 깊이 우선 탐색

* Stack을 사용해서 가까운 것부터 나간다.

  ```python
  def dfs(graph, start_node, visit = []) :
    visit = visit + [start_node]
    for node in graph[start_node] :
      if node not in visit :
        visit = dfs(graph, node, visit)
    return visit
  ```

  

## Minimum Spanning Tree

* 전체 요소들을 연결할 때 사용
* 간선이 적으면 Kruskal, 많으면 Prim

#### Kruskal Algorithm

1. 간선들을 정렬
2. 간선이 잇는 두 정점의 root를 찾음
3. 다르다면 하나의 root를 바꾸어 연결

#### Prim Algorithm

1. 임의의 정점을 선택
2. 해당 정점에서 갈 수 있는 간선을 minheap에 넣음
3. 최솟값을 뽑아 해당 정점을 방문 안했다면 선택

#### Dijkstra Algorithm

1. 최단 거리 배열을 무한대로 초기화. (방문여부 배열은 False로 초기화)
2. 출발 노드는 방문했다고 체크한 후 heap에 넣음
3. 아직 방문하지 않은 노드중, 최단 거리 테이블 값이 가장 작은 노드 선택
4. 저장된 최단거리 값과 현재노드에 가중치를 더한 거리 값 중 작은 값으로 update