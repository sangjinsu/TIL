# 백트래킹 알고리즘

- 해를 찾는 도중에 막히면, 해가 아니면 다시 돌아가서 해를 찾는 기법이다

- 최적화 문제와 결정 문제를 해결할 수 있다
  - 결정 문제: 문제의 조건을 만족하는 해가 존재하는지의 여부를 yes 또는 no 가 답하는 문제
    - 미로 찾기
    - n-Queen 문제
    - Map coloring
    - 부분 집합의 합 문제 

- 백트래킹과 DFS 차이
  - 출발 경로가 해결로 이어지지 않을 것 같으면 그 경로를 포기함으로 시도 횟수를 줄인다(가지 치기)
  - 깊이 우선 탐색이 모든 경로를 추적하는데 비해 백트래킹이 불필요한 경로를 조기에 차단한다
  - 백트래킹 알고리즘을 적용하면 일반적으로 경우의 수가 줄어들지만 최악의 경우에 지수 함수 시간을 요구한다

- 백트래킹 기법
  - 어던 노드의 유망성을 점검한 후에 유망하지 않다고 결정되면 노드의 부모로 돌아가는 backtracking 다음 자식 노드로 감
  - 가지치기 => 유망하지 않은 노드가 포함되는 경로를 더 이상 고려하지 않는다
    1. 상태 공간 트리의 깊이 우선 탐색을 한다
    2. 각 노드가 유망한지 확인한다
    3. 유망하지 않으면 부모 노드로 돌아가 검색을 진행한다

- 부분집합 구하기

  ```python
  a = [20, 31, 78]
  t = [0] * 3
  
  
  def powerset(k):
      if k == 3:
          print(t)
      else:
          t[k] = True
          powerset(k + 1)
          t[k] = False
          powerset(k + 1)
  
  
  def powerset2(k):
      if k == 3:
          print(t)
          for i in range(3):
              if t[i]:
                  print(a[i], end=' ')
          print()
      else:
          t[k] = True
          powerset2(k + 1)
          t[k] = False
          powerset2(k + 1)
  
  
  def powerset3(k):
      if k == 3:
          for i in range(3):
              if t[i]:
                  print(a[i], end=' ')
          print()
      else:
          for i in range(2):
              t[k] = i
              powerset3(k + 1)
  
  ```

- 순열 구하기

  ```python
  visited = [False] * 3
  
  
  def per(k):
      if k == 3:
          for i in t:
              print(a[i], end=' ')
          print()
      else:
          for i in range(3):
              if not visited[i]:
                  t[k] = i
                  visited[i] = True
                  per(k + 1)
                  visited[i] = False
  ```

  

