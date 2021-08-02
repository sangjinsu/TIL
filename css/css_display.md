# CSS Display

- 모든 요소는 박스 모델이고 display에 따라 배치가 달라진다

- `display: block` 
  - 줄 바꿈이 발생
  - 화면 크기 전체의 가로 폭을 차지
  - 블록 레벨 요소 안에 인라인 레벨 요소가 들어감
  - div, ul, ol, li, p, hr, form

- `display: inline `
  - 줄 바끔이 일어나지 않음
  - content 너비 만큼 가로 폭을 차지함
  - width, height, margin-top, margin-bottom을 지정할 수 없다
  - 상하 여백은 line-height로 지정
  - span, a, img, input, label, b, em, i, strong

- `display: inline-block`
  - block과 inline 레벨 요소 특징을 가짐
  - inline 처럼 한 줄 표시 가능
  - block 처럼 width, height, margin 속성을 모두 지정할 수 있음

- `display: none`
  - 공간이 사라짐
  - 화면에 표시하지 않음
  - `visibility: hidden` - 공간은 차지하나 표시되지 않음

## 수평 정렬

- 왼쪽으로 -> `margin-right:auto;` `text-align:left;`
- 오른쪽으로 -> `margin-left:auto;` `text-align:right;`
- 가운데로 -> `margin-right:auto;` `margin-left:auto;` `text-align:center;`



