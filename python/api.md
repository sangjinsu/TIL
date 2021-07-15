# Python API 사용

## 나이 예측

```python
import requests

# name = input('영문 이름 입력: ')

names = ['tak', 'tony', 'eric', 'musk']

# url = f'https://api.agify.io?name={name}&country_id=KR'
url = 'https://api.agify.io?'

for name in names:
    url += f'name[]={name}&'

responses = requests.get(url).json()
# json() -> dict 형식으로 변환
# 결과 2개 이상인 경우 [ dict ... ] 구조

for response in responses:
    age = response.get('age')
    name = response.get('name')
    print(name, age)

```

## 나라 예측

```python
import requests

name = 'michael'
url = f'https://api.nationalize.io?name={name}'
response = requests.get(url).json()
country_expect = response.get('country')

countries = list()
for country in country_expect:
    countries.append(country.get('country_id'))

result = f'확률이 가장 높은 국가는 {countries[0]} 입니다.'
print(result)
```

## 도전 API

`https://m.stock.naver.com/api/stocks/marketValue/KOSPI?page=1&pageSize=20`

