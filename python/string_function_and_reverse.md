# 문자열 함수와 뒤집기

## 뒤집기

```python
word = 'apple'
print(word[::-1])
# elppa
```

## [함수](https://wikidocs.net/13#_19)

### 문자열 바꾸기

```python
word = 'elephant'
word.replace('e', '')
# lphant - 전체 바꾸기
word.replace()

word = 'elephant'
word.replace('e', '', 1)
# lephant - 바꿀 횟수 정하기
```

### 문자열 나누기

```python
words = 'This is my book'
print(words.split())
print(words.split(' '))
# 괄호 안에 특정값이 없는 경우 공백을 기준으로 문자열을 나눈다.
print(words.split('i'))
# ['Th', 's ', 's my book']
```

