# 백트래킹

- 여러 가지 선택지들이 존재하는 상황에서 한가지를 선택한다.
- 선택이 이루어지면 새로운 선택지들의 집합이 생성된다.
- 이런 선택을 반복하면서 최종 상태에 도달한다.

### 백트래킹과 깊이 우선 탐색 차이

- 가지치기 

  어떤 노드에서 출발하는 경로가 해결책으로 이어지지 않으면 그 경로를 포기한다

- 백트래킹 알고리즘을 적용하면 일반적으로 경우의 수가 감소하지만 최악의 경우에는 지수함수 시간을 요구하므로 처리가 불가능하다

#### 합이 10인 부분 집합

```python
lst = [1, 2, 3, 4, 5, 6, 7, 8, 9]
visited = [False] * 9


def recursion(cnt, value):
    if cnt == 9:
        if value == 10:
            for i in range(len(visited)):
                if visited[i]:
                    print(lst[i], end=' ')
            print()
        return

    if value > 10:
        return

    visited[cnt] = True
    recursion(cnt + 1,  value + lst[cnt])
    visited[cnt] = False
    recursion(cnt + 1, value)


recursion(0, 0)

```

