# Python API 심화

## 날씨 API

```python
import requests

def fetch_seoul_weather_status():
    # seoul
    url = 'https://www.metaweather.com/api/location/1132599/'
    resp = requests.get(url).json()

    consolidated_weather = resp.get('consolidated_weather')

    today_weather = consolidated_weather[0]
    today_weather_abbr = today_weather.get('weather_state_abbr')
    today_max_temp = round(today_weather.get('max_temp'), 1)
    today_min_temp = round(today_weather.get('min_temp'), 1)

    weather_state = dict(
        lr='약한 비',
        sn='눈',
        sl='진눈깨비',
        h='싸래기눈',
        t='뇌우',
        hr='폭우',
        s='소나기',
        hc='구름 많음',
        lc='구름 조금',
        c='맑음'
    )

    return f'오늘 서울 예상 최고 기온는 {today_max_temp}도, 최저 기온은 {today_min_temp}도이며 날씨는 {weather_state.get(today_weather_abbr)} 입니다.'

```

## PAPAGO API and 명언 API

```python
import requests

def fetch_quote():
    fetch_quote_url = 'https://favqs.com/api/qotd'
    resp_quote = requests.get(fetch_quote_url).json()
    quote = resp_quote.get('quote').get('body')

    PAPAGO_CLIENT_ID = 'YOUR_ID'
    PAPAGO_CLIENT_SECRET = 'YOUR_SECRET'

    headers = {
        'X-Naver-Client-Id': PAPAGO_CLIENT_ID,
        'X-Naver-Client-Secret': PAPAGO_CLIENT_SECRET
    }

    data = {
        'source': 'en',
        'target': 'ko',
        'text': quote
    }

    URL = f'https://openapi.naver.com/v1/papago/n2mt'

    translation = requests.post(URL, headers=headers, data=data).json()
    translated_quote = translation.get(
        'message').get('result').get('translatedText')

    return translated_quote

```

## Telegram API

```python
import requests


TOKEN = 'YOUR_TOKEN'
BASE_URL = f'https://api.telegram.org/bot{TOKEN}'

get_updates_url = BASE_URL + '/getUpdates'
resp_update = requests.get(get_updates_url).json()

result = resp_update.get('result')
message = result[0].get('message')
chat = message.get('chat')
chat_id = chat.get('id')

text = quote.fetch_quote()

send_message_url = BASE_URL + f'/sendMessage?chat_id={chat_id}&text={text}'
resp_send_message = requests.get(send_message_url).json()

if resp_send_message.get('ok') == True:
    print('메시지 전송 성공')
else:
    print('메시지 전송 실패')
```

