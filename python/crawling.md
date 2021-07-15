# Python 크롤링

```bash
python -m pip install [패키지명] # 패키지 install
```

```python
import requests
from bs4 import BeautifulSoup

url = 'https://finance.naver.com/sise/'

response = requests.get(url).text

# html에서 '#KOSPI_now'
data = BeautifulSoup(response, features='html.parser')
kospi = data.select_one('#KOSPI_now')

print(kospi.text)

```

```python
import requests
from bs4 import BeautifulSoup

url = 'https://finance.naver.com/marketindex/'

response = requests.get(url).text

data = BeautifulSoup(response, features='html.parser')

dollar = data.select_one(
    '#exchangeList > li.on > a.head.usd > div > span.value').text

print(f'달러 환율은 {dollar}입니다.')

```

## 기타 URL

네이버 주가 정보

`https://m.stock.naver.com/api/stocks/marketValue/KOSPI?page=1&pageSize=20`

이름에 따른 나이 정보

`https://agify.io/`

