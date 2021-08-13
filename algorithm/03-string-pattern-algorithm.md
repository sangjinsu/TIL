# String Pattern 알고리즘

- brute force
- rabin-karp 
- kmp
- boyer-moore

## brute force

```python
def brute_force(p: str, s: str) -> int:
    i = 0
    j = 0
    lenP = len(p)
    lenS = len(s)
    while i < lenS and j < lenP:
        if s[i] != p[i]:
            i = i - j
            j = -
   	if j == M:
        return i - M
   	return -
```



## rabin-karp

- 해쉬 값 사용

- 시간 복잡도: O(n)

- 만약 충돌이 발생한다면 문자 값들이 모두 맞는지 확인하는 작업이 필요하다

- 충돌은 해쉬값이 중복해서 나타나는 경우이다

  ```python
  def hash_str(s):
      k = 2 * (len(s) - 1)
      v = 0
      for c in s:
          v += ord(c) * k
          k //= 2
      return v
  
  
  def ravin_karp(pattern, string):
      hash_p = hash_str(pattern)
  
      hash_v = hash_str(string[:len(pattern)])
      for i in range(1, len(string) - len(pattern) + 1):
          print(hash_p, hash_v)
          if hash_p == hash_v:
              print(i)
              break
          hash_v = 2 * (hash_v - ord(string[i - 1]) * (len(pattern) - 1) * 2) + ord(string[i + len(pattern)])
  
  
  ravin_karp('dc', 'abdddddc')
  ```

  

## kmp

- 접두사와 접미사 사용

- 접두사와 접미사가 같은 구간을 나타내는 테이블 필요

- 시간 복잡도: O(M + N)

- [다른 예시](https://www.geeksforgeeks.org/python-program-for-kmp-algorithm-for-pattern-searching-2/)

  ```python
  def make_table(pattern):
      table = [0] * len(pattern)
      j = 0
      for i in range(1, len(pattern)):
          while j > 0 and pattern[i] != pattern[j]:
              j = table[j - 1]
          if pattern[i] == pattern[j]:
              j += 1
              table[i] = j
      return table
  
  
  def kmp(pattern, string):
      table = make_table(pattern) 
      j = 0
      for i in range(len(string)):
          while j > 0 and string[i] != pattern[j]:
              j = table[j - 1]
          if string[i] == pattern[j]:
              if j == len(pattern) - 1:
                  print(i - len(pattern) + 1)
                  j = table[j]
              else:
                  j += 1
  ```

  ```python
  def make_table(p: str) -> list[int]:
      lenP = len(p)
      table = [0] * lenP
      j = 0
      i = 1
      while i < lenP:
          if p[i] == p[j]:
              j += 1
              table[i] = j
              i += 1
          else:
              if j > 0:
                  j = table[j - 1]
              else:
                  i += 1
      return table
  
  
  def kmp(p: str, s: str):
      table = make_table(p)
      j = 0
      i = 0
      lenS = len(s)
      lenP = len(p)
      while i < len(s):
          if s[i] == p[j]:
              if j == lenP - 1:
                  print(i - lenP + 1)
                  j = table[j]
              else:
                  j += 1
              i += 1
          else:
              if j > 0:
                  j = table[j - 1]
              else:
                  i += 1
  
  
  kmp('abacaba', 'absdedabacaba')
  
  ```

  

## [Boyer Moore](https://www.geeksforgeeks.org/boyer-moore-algorithm-for-pattern-searching/)

- 가장 많은 소프트웨어에서 사용한다
- 패턴 오른쪽 끝을 확인한다
- 문자가 패턴 내에 존재하지 않는 경우 이동거리는 최대 패턴 길이이다 

```python
def make_skip_table(s: str) -> dict[str]:
    d = dict()
    for i in range(len(s)):
        d[s[i]] = len(s) - i - 1
    print(d)
    return d


def boyer_moore(p: str, s):
    lenP = len(p)
    lenS = len(s)

    t = make_skip_table(p)

    start = 0
    while start <= lenS - lenP:
        j = lenP - 1

        while j >= 0 and p[j] == s[start + j]:
            j -= 1

        if j == -1:
            print(start)
            start += lenP - t.get(s[start + lenP]) if start + lenP < lenS else 1
        else:
            start += max(1, t.get(s[start + j], lenP + 1))



boyer_moore('rithm', 'a pattern matching algorithm')

```

