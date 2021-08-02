# Box Model

- 모든 HTML 요소는 box 형태이다
- content, padding, border, margin
  - content - 실제 내용
  - padding - 테두리 안족의 내부 여백, 요소에 적용된 배경색 이미지는 padding까지 적용
  - border - 테두리 영역
  - margin - 테두리 바깥의 외부 여백, 배경색을 지정할 수 없다

```css
/* 상하좌우 */
.margin-1 {
    margin: 10vw
}
/* 상하 좌우 */
.margin-2 {
    margin: 10vw, 10vw 
}
/* 상 좌우 하 */
.margin-3 {
    margin: 10vw, 10vw, 10vw
}
/* 상 우 하 좌 시계 방향 */
.margin-4 {
    margin: 10vw, 10vw, 10vw, 10vw
}
```

## box-sizing

- content-box : content 기준, padding 제외

- border-box : border 까지의 너비를 100px 보는 것을 원할 때 사용

## 마진 상쇄 margin collapsing

- box A의 top 과 box B의 bottom에 적용된 각각의 margin이 둘 중에서 큰 마진 값으로 결합 되는 현상

  