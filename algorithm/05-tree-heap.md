# 트리

- 비선형 구조
- 원소들 간에 1:n 관계를 가지는 자료구조
- 원소들 간에 계층 관계를 가지는 계층형 자료구조
- 한 개 이상의 노드로 이루어진 유한 집합이며 다음 조건을 만족한다
  - 최상위 노드는 루트이다
  - 나머지 노드들은 n개의 분리 집합으로 분리될 수 있다
  - 분리 집합은 다시 하나의 트리가 되며 서브트리라고 한다

- 노드 - 트리 원소
- 간선 - 노드를 연결하는 선, 부모 노드와 자식 노드를 연결
- 형제 노드 - 같은 부모 노드의 자식 노드들
- 조상 노드 - 간선을 따라 루트 노드까지 이르는 경로의 모든 노드들
- 차수 
  - 노드의 차수 - 노드에 연결된 자식 노드의 수
  - 트리의 차수 - 트리에 있는 노드 차수 중에서 가장 큰 값
  - 단말 노드 - 차수가 0인 노드

- 높이
  - 노드 높이 - 루트에서 노드에 이르는 간선 수, 노드의 레벨
  - 트리 높이 - 트리에 있는 노드의 높이 중 가장 큰 값

---

## 이진 트리

- 모든 노드들이 2개의 서브트리를 갖는 특별한 형태의 트리
- 각 노드가 자식 노드를 최대 2개 까지만 가질 수 있는 트리
- 높이 h, 최소 노드 개수 h +1, 최대 개수 2^(h+1)-1

---

## 포화 이진 트리

- 모든 레벨에 노드가 포화상태로 차 있는 이진 트리
- 루트를 1 또는 0으로 하여 2^(h+1)-1 까지 정해진 위치에 대한 노드 번호를 가진다

---

## 완전 이진 트리

- 높이가 h이고 노드 수가 n개일 때, 포화 이진 트리 노드 번호는 1번부터 n번 까지 빈자리가 없는 이진 트리이 다

---

## 편향 이진 트리

- 높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진 트리

---

## 순회

- 트리의 각 노드를 중복되지 않게 전부 방문하는 것
- 트리는 비 선형 구조로 선후 연결 관계를 알 수 없다

- 3가지 기본적인 순회 방법

  - 전위 순회 preorder traversal : VLR
    - 부모 노드 방문 후, 자식 노드를 좌, 우 순서로 방문한다

  - 중위 순회 inorder traversal : LVR
    - 왼쪽, 부모, 오른쪽 노드 순으로 방문한다

  - 후위 순회 postorder traversal : LRV
    - 자식 노드를 좌우 순서로 방문한 후, 부모 노드로 방문한다 

### 전위 순회

1. 현재 노드를 방문하여 처리한다
2. 현재 노드의 왼쪽 서브트리로 이동한다
3. 현재 노드의 오른쪽 서브트리로 이동한다

### 중위 순회

1. 현재 노드의 왼쪽 서브트리로 이동한다
2. 현재 노드를 방문하여 처리한다
3. 현재 노드의 오른쪽 서브트리로 이동한다

### 후위 순회

1. 현재 노드의 서브트리로 이동한다
2. 현재 노드의 오른쪽 서브트리로 이동한다
3. 현재 노드를 방문하여 처리한다

---

## 이진트리의 표현 - 배열

- 노드 번호가 i  인 노드의 부모 노드 번호 => [i/2]
- 노드 번호가 i 인 노드의 왼쪽 자식 노드 번호 => 2 * i
- 노드 번호가 i 인 노드의 오른쪽 자식 노드 번호 => 2 * i + 1
- 레벨 n 의 노드 번호 시작 번호는 2^n

## 이진트리의 표현 - 연결 리스트

- 배열 표현시 단점
  - 편향 이진 트리인 경우 사용하지 않는 배열 원소에 대한 메모리 낭비 발생
  - 트리 중간에 새로우 노드를 삽입하거나 삭제하는 경우 배열 크기 변경이 어렵다

- 연결 자료구조를 이용한 이진 트리 표현
  - `left data right` 

---

## 이진 탐색 트리

- 탐색 작업을 효율적으로 하기 위한 자료구조
- 모든 원소는 서로 다른 유일한 키를 갖는다
- 중위 순회시 오름차순으로 정렬된 값을 얻을 수 있다
- 탐색, 삽입, 삭제 시간은 트리 높이만큼 시간이 걸린다
- 시간 복잡도: O(log n) 최악의 경우 O(n)

---

## Heap

- 완전 이진 트리에 있는 노드 중에서 키값이 가장 큰 노드나 키 값이 가장 작은 노드를 찾기 위해서 만든 자료구조
- 최대 힙: 키 값이 가장 큰 노드를 찾기 위한 완전 이진 트리
- 최소 힙: 키 값이 가장 작은 노드를 찾기 위한 완전 이진 트리

- 우선순위 큐, 힙 정렬에 힙이 사용된다