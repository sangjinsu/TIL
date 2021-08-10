# 리스트

## 버블정렬

- 인접한 두 개의 원소를 비교하여 자리를 계속 교환하는 방식

- 시간 복잡도: O(n2)

  ```python
  def bubble_sort(lst):
      nums = lst[:]
      check = True
      for i in range(len(nums) - 1, 0, -1):
          if not check:
              break
          check = False
          for j in range(i):
              if nums[j] > nums[j + 1]:
                  nums[j], nums[j + 1] = nums[j + 1], nums[j]
                  check = True
      return nums
  ```

  

## 카운팅 정렬

- 항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개식 있는지 세는 작업을 함

- 선형 시간에 정렬하는 알고리즘

  ### 제한 사항

  - 정수 데이터에만 활용 가능
  - 집합 내의 가장 큰 정수를 알아야 공간을 할당한다

- 시간 복잡도: O(n + k) n은 리스트 길이, k는 정수의 최대값 

  ```python
  def counting_sort(lst):
      nums = lst[:]
  
      max_num = 0
      for num in nums:
          if max_num < num:
              max_num = num
  
      counts = [0] * (max_num + 1)
      for num in nums:
          counts[num] += 1
  
      for i in range(1, len(counts)):
          counts[i] = counts[i - 1] + counts[i]
  
      new_lst = [-1] * len(nums)
      for num in nums:
          new_lst[counts[num] - 1] = num
          counts[num] -= 1
  
      return new_lst
  
  ```

## 완전 탐색

- 모든 경우의 수를 나열해보고 확인학는 기법
- Brute-force 라고도 불린다
- 모든 경우의 수를 테스트하고 최종 해법을 도출한다.
- 일반적으로 경우의 수가 상대적으로 작을 때 유용

## 탐욕 알고리즘

- 최적해를 구하는데 사용되는 근시안적인 방법

- -최적의 해를 찾는 방식

  동작 과정

  1. 해 선택 - 현재 상태에서 부분 문제의 최적 해를 구한 뒤, 이를 부분해 집합에 추가한다
  2. 실행 가능성 검사 - 새로운 부분해 집합이 실행 가능한지를 확인한다. 문제 제약 조건을 위반하는지 확인한다
  3. 해 검사 - 부분해 집합이 문제의 해가 되는지 확인한다.