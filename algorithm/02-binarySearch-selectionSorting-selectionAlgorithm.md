# 이진 검색, 선택 정렬, 셀렉션 알고리즘

## 이진 검색

- 정렬된 자료 가운데를 키로 하여 검색하고 대소 비교를 하며 범위를 줄이고 다시 검색하는 방식이다

- 시간 복잡도 : O(logn) 

  ```python
  def binary_search(lst, item):
      start, end = 0, len(lst) -1
      while start <= end:
          middle = (start + end) // 2
          if lst[middle] == item:
              return middle
         	elif lst[middle] > item:
              end = middle - 1
          else:
              start = middle + 1
      return -1
  ```

  ```python
  def binary_search(lst, item, start, end):
      if start > end:
          return -1
      
      middle = (start + end) // 2
      if lst[middle] == item:
          return middle
     	elif lst[middle] > item:
     		return binary_search(lst, item, start, middle - 1)
      else:
          return binary_search(lst, item, middle + 1, end)
          
  ```



## 선택 정렬

- 주어진 자료들 중 가장 작은 값을 차례대로 앞으로 옮기는 방식

- 시간 복잡도: O(n2)

  ```python
  def selection_sort(lst):
      for i in range(len(lst) - 1):
          min_idx = i
          for j in range(i + 1, len(lst)):
              if lst[min_idx] < lst[j]:
                  min_idx = j
          lst[min_idx], lst[j] = lst[j], lst[min_idx]
  ```

  

## 셀렉션 알고리즘

- k번째로 작은 원소를 찾는 알고리즘

  ```python
  def selection(lst, k):
      for i in range(k):
          min_idx = i
          for j in range(i + 1, len(lst)):
              if lst[min_idx] < lst[j]:
                  min_dix = j
          lst[min_idx], lst[j] = lst[j], lst[min_idx]
      return lst[k - 1]
  ```

  