# Queue 특성

- 선입 선출 구조 FIFO

## 선형큐

- 1차원 배열을 이용한 큐

- 큐의 크기 => 배열 크기

- front. rear => 첫 번재 원소의 인덱스, 저장된 마지막 원소의 인덱스

  ```python
  from collections import deque
  
  q = deque()
  q.append(2)
  q.append(3)
  
  while q:
      print(q.popleft())
  ```

## 원형큐

- 초기 공백 상태 => front = rear = 0
- index 순환
  - front, rear 위치가 배열 마지막 인덱스인 n-1을 가리킨 후 그 다음에는 논리적 순환을 이루어 배열 처음 인덱스인 0으로 이동해야 한다
  - mod 나머지 연산자를 사용한다

## 연결 큐

- 단순 연결 리스트를 이용한 큐
- 큐의 원소: 단순 연결 리스트 노드
- 큐의 원소 순서: 노드의 연결 순서, 링크로 연결되어 있음
- front: 첫 번째 노드를 가리키는 링크
- rear: 마지막 노드를 가리키는 링크

## 우선순위 큐

- 배열을 이용한 우선순위 큐
- 리스트를 이용한 우선순위 큐

## 큐의 활용

- 버퍼
  - 데이터를 한 곳에서 다른 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리 영역
  - 버퍼링 => 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작을 의미한다

## BFS

- 넓이 우선 탐색

- 탐색 시작점의 인접한 정점들을 먼저 모두 차례로 방문한 후에 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식

  ```python
  lst = [1, 2, 1, 3, 2, 4, 2, 5, 4, 6, 5, 6, 6, 7, 3, 7]
  graph = [[] for _ in range(8)]
  n = 7
  e = 8
  for i in range(e):
      graph[lst[i * 2]].append(lst[i * 2 + 1])
      graph[lst[i * 2 + 1]].append(lst[i * 2])
  
  
  def bfs(start, graph):
      visited = [0] * (n+1)
      visited[start] = 1
      queue = [start]
      while queue:
          v = queue.pop(0)
          for i in graph[v]:
              if not visited[i]:
                  queue.append(i)
                  visited[i] = visited[v] + 1
      print(visited)
  ```
  
  