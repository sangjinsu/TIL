# 문자열

- 문자 나열
- immutable, ordered, iterable

### 문자열 Slicing

- `s[start:stop:step]`

### 문자열 조회 및 탐색

- `find(문자열)` : 문자열 첫 번째 위치를 반환 없으면 -1을 반환
- `index(문자열)`: 문자열 첫번째 위치를 반환 없으면 오류 발생

### 문자열 변경

- `replace(old, new [, count])` -  바꿀 대상에서 새로운 글자로 바꿔서 **<u>복사본</u>**을 반환, count 지정시 해당 개수만큼 변환
- `strip([chars])` - 특정 문자들 지정시 양쪽, 왼쪽 오른쪽 제거 (strip, lstrip, rstrip), 문자열을 지정하지 않으면 공백을 제거, chars 인자는 접두사나 접미사가 아니라 모든 값 조합이 제거
- `split([chars])` - 문자열을 특정한 단위로 나눠 리스트로 반환, chars 미지정시 공백으로 나눔

- `'seperator'.join([iterable])` - iterable 컨테이너 요소들을 serperator로 합쳐 문자열 반환
- `capitalize`, `upper`, `lower`, 
- `swapcase` - 대소문자 서로 변경
- `title` -  `'` 나 공백 다음 첫 문자를 대문자로 변경

### 문자열 관련 검증 메소드

- `isalpha` - 알파벳 문자 여부, 단수한 알파벳이 아닌 유니코드상 letter로 한국어도 포함한다
- `isupper` - 대문자 검증
- `islower` - 소문자 검증
- `istitle` - 타이틀 형식 여부
- `isdecimal`,  `isdigit`, `isnumeric`  