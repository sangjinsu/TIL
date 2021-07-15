# File Write

2021 . 07 . 15

```
읽기 모드: r, 쓰기모드 w, 추가모드 a, 텍스트 모드 t, 바이너리 모드 b
```

## 파일 읽기

```python
f = open('./resource/it_news.txt', 'rt', encoding='UTF-8')

print(f.encoding, f.name, f.mode)

cts = f.read()
print(cts)

f.close()
```

### with, close 생략

```python
with open('./resource/it_news.txt', 'rt', encoding='UTF-8') as f:
    c = f.read()
    print(c)
    print(iter(c))
    print(list(c))
```

### read() 활용

```python
with open('./resource/it_news.txt', 'rt', encoding='UTF-8') as f:
    c = f.read(20) # 20바이트만 읽음
    print(c)
    c = f.read(20)
    print(c)
```

### readline() 한 줄 읽기

```python
with open('./resource/it_news.txt', 'rt', encoding='UTF-8') as f:
    cts = f.readlines()
    print(cts)
    print()
    for c in cts:
        print(c, end='')
```

---

## 파일 쓰기

```python
with open('./resource/contents1.txt', 'w') as f:
    f.write('I maybe love python\n')

with open('./resource/contents1.txt', 'a') as f:
    f.write('I maybe love python 2\n')

# writelines 리스트 -> 파일
with open('./resource/contents2.txt', 'w') as f:
    li = ['Fried Chicken\n', 'Coffee\n', 'Ramen\n']
    f.writelines(li)
```

### print 활용

```python
with open('./resource/contents3.txt', 'w') as f:
    print('Text Write', file=f)
    print('Text Write', file=f)
    print('Text Write', file=f)
```



---



## CSV 파일 읽기

`import csv`

```python
with open('./resource/test1.csv', 'r') as f:
    reader = csv.reader(f)

    # 헤더 생략
    next(reader)

    for c in reader:
        print(c)
```

### delimiter 

```python
with open('./resource/test2.csv', 'r') as f:
    reader = csv.reader(f, delimiter='|')

    for c in reader:
        print(c)
```

### dict 형식으로 읽기

```python
with open('./resource/test1.csv', 'r') as f:
    reader = csv.DictReader(f)

    for c in reader:
        for k, v in c.items():
            print(k, v)
        print('===============')
```

## CSV 파일 쓰기

`w = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]`

```python
with open('./resource/write1.csv', 'w', encoding='UTF-8', newline='') as f:
    wt = csv.writer(f)

    for value in w:
        wt.writerow(value)
```

### dict 형식으로 쓰기

```python
with open('./resource/write2.csv', 'w', encoding='UTF-8', newline='') as f:
    fields = ['first', 'second', 'third']
    wt = csv.DictWriter(f, fieldnames=fields)
    wt.writeheader()

    for v in w:
        d = dict(
            first=v[0],
            second=v[1],
            third=v[2]
        )

        wt.writerow(d)
```

