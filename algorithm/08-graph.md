# 그래프

- 연결 관계 표현
- 종류
  - 무향 그래프
  - 유향 그래프
  - 가중치 그래프
  - 사이클 없는 방향 그래프

- 완전 그래프 

   모든 정점들에 대해 가능한 모든 간선들을 가진 그래프

## 그래프 표현

- 인접 행렬 - 2차원 배열
  - 두 정점을 연결하는 간선의 유무를 행렬로 표현
  - 행 번호와 열 번호는 그래프 정점에 대응
  - 무향 그래프 - i 번째 행의 합, i번째 열의 합 = v 의 차수
  - 유향 그래프 - 행 i의 합 = V의 진출 차수, 열 i의 합 = v의 진입 차수 
- 인접 리스트
- 간선의 배열
  - 시작 정점, 끝 정점을 배열에 연속적으로 저장한다

## 깊이 우선 탐색

가장 마지막에 만났던 갈림길의 점점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입 선출 구조의 스택 사용

### 스택

- 선형 구조
- 후입 선출
- push, pop, isEmpty, peek

## 넓이 우선 탐색

인접한 정점들에 대해 탐색을 한 후, 차례로 다시 너비우선탐색을 진행해야 하므로, 선입선출 형태의 자료구조인 큐를 활용합니다.

### 큐

- 선입 선출
- enqueue, dequeue, createqueue
- isEmpty, isFull

## 서로소 집합들

- 서로소 도는 상호배타 집합들은 서로 중복 포함된 원소가 없는 집합들이다
- 교집합이 없다
- 집합에 속한 한 특정 멤버를 통해 각 집합들을 구분한다
- 이를 대표자라고 한다

### 상호 배타 집합을 표현하는 방법

- 연결 리스트
- 트리

### 서로 배타 집합 연산

- Make-Set(x)
- Find-Set(x)
- Union(x, y)

### 연산 효율을 높이는 방법

- Rank 를 이용한 Union
  - 각 노드는 자신을 루트로 하는 subtree의 높이를 rank 라는 이름으로 저장한다
  - 두 집합을 합칠 때 rank가 낮은 집합을 rank가 높은 집합에 붙인다
- Path Compression
  - find-set 을 행하는 과정에서 만나는 모든 노드들이 직접 root 를 가리키도록 포인터를 바꾸어 준다

```python
# 서로소 집합

# 특정 원소가 속한 집합 찾기
# def find_parent(parent, x):
#     if parent[x] != x:
#         return find_parent(parent, parent[x])
#     return x
# 경로 압축 기법
def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


# 두 원소가 속한 집합 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b


# 노드 개수와 간선 개수 입력
v, e = map(int, input().split())
parent = [0] * (v + 1)

for i in range(1, v + 1):
    parent[i] = i

for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)

print('각 원소가 속한 집합: ', end='')
for i in range(1, v + 1):
    print(find_parent(parent, i), end=' ')
print()

print('부모 테이블: ', end=' ')
for i in range(1, v + 1):
    print(parent[i], end=' ')

```

### cycle 판별

```python
cycle = False

for i in range(e):
    a, b = map(int, input().split())
    if find_parent(parent, a) == find_parent(parent, b):
        cycle = True
        break
    else:
        union_parent(parent, a, b)
```

## 최소 신장 트리

- 그래프에서 최소 비용 문제
  1. 모든 정점을 연결하는 간선들의 가중치의 합이 최소가 되는 트리
  2. 두 정점 사이의 최소 비용의 경로 찾기 

- 신장 트리
  - n 개의 정점으로 이루어진 무방향 그래프에서 n개의 정점과 n-1개의 간성으로 이루어진 트리

- 최소 신장 트리

  - 무방향 가중치 그래프에서 신장 트리를 구성하는 간선들의 가중치 합이 최소인 신장 트리

    

### Prim 알고리즘

- 하나의 정점에서 연결된 간선들 중에 하나씩 선택하면서 MST 를 만들어 가는 방식
  1. 임의 정점을 하나 선택해서 시작
  2. 선택한 장점과 인접하는 정점들 중의 최소 비용의 간선이 존재하는 정점을 선택
  3. 모든 정점이 선택될 때까지 1번과 2번 과정을 반복한다 

-  서로소인 2개의 집합 정보를 유지
  - 트리 정점들(tree, vertices) - MST 를 만들기 위해 선택된 정점들
  - 비트리 정점들(nontree vertices) - 선택되지 않은 정점들

### 크루스갈 알고리즘

- 간선을 하나씩 선택해서 MST를 찾는 알고리즘

  1. 최초, 모든 간선을 가중치에 따라 오름차순으로 정렬
  2. 가중치가 가장 낮은 간선부터 선택하면서 트리를 증가시킨다
     - 사이클이 존재하면 다음으로 가중치가 낮은 간선을 선택한다

  3. n-1 개의 간선이 선택될 때까지 2) 반복 

```python
def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


# 두 원소가 속한 집합 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b


# 노드 개수와 간선 개수 입력
v, e = map(int, input().split())
parent = [0] * (v + 1)

edges = []
result = 0

for i in range(1, v + 1):
    parent[i] = i

for _ in range(e):
    a, b, cost = map(int, input().split())
    edges.append((cost, a, b))

edges.sort()

for edge in edges:
    cost, a, b = edge
    if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost

print(result)

```

## 다익스트라 알고리즘

```python
import heapq
import math

n, m = map(int, input().split())
start = int(input())

graph = [[] for _ in range(n + 1)]
distance = [math.inf] * (n + 1)

for _ in range(m):
    a, b, c = map(int, input().split())
    graph[a].append((b, c))

print(graph)


def dijkstra(start):
    q = []
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q:
        print(q, distance)
        # start 지점 으로부터의 거리와 현재 위치
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue
        for i in graph[now]:
            cost = dist + i[1]
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))


dijkstra(start)

for i in range(1, n + 1):
    if distance[i] == math.inf:
        print('cant')
    else:
        print(distance[i])

```

