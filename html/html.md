# HTML

- Hyper Text Markup Language

# HTML 기본 구조

- html 최상위 요소: HTML 문서 최상위 요소로 문서의 root를 의미한다.

- head: 해당 문서 정보를 담으며 브라우저에 나타나지 않는다. 외부 파일을 가져올 때 사용한다.

- body: 브라우저 화면에 나타나는 정보를 실제로 표현한다.

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>
    </head>
    <body></body>
  </html>
  ```

- DOM 트리 Document Object Model
  - 구조화된 표형을 제공한다.
  - web page의 객체 지향 표현

### element

- 태그는 컨텐츠를 앞뒤로 감싸는 역할을 함
- 내용이 없는 태그: br, hr, img, input, link, meta
- element는 중접되어 사용될 수 있음

### attribute

- 속성을 통해 태그에 부가적인 정보를 설정
- 이름과 값이 한 쌍으로 존재
- 태그와 상관없이 사용 가능한 속성 HTML Global Attribute 들도 있음
- HTML Global Attribute: id, class, hidden, lang, style, tabindex, title

### sementic tag

- HTML5에서 의미론적 요소를 담은 태그
  - header: 문서 전체나 섹션 헤더
  - nav: 내비게이션
  - aside: 사이드에 위차한 공간, 메인 콘텐츠와 관련이 적음
  - section: 일반적인 구분, 컨텐츠 그룹 표현
  - article: 문서, 페이지, 사이트 안에서 독립적으로 구분되는 영역
  - footer: 문서 전체나 섹션의 푸터

- 의미있는 정보 그룹을 태그로 표현
- non-sementic element는 `div`, `span` 등이 있다
- 의미가 명확해져 가독성을 톺이고 유지보수를 쉽게 한다.
- 검색 엔진 최적화 SEO 를 위해 메타 태그, 시멘틱 태그 등을 통한 마크업을 효과적으로 할 필요가 있다
- 그룹 컨텐츠 : p, hr, ol, ul, pre, blockquote, div

- 텍스트 관련 element : a, b(단순 굵게) vs strong(강조), i vs em, span, br, img

### table

- tr, td, th
- thread, tbody, tfoot
- caption
- 셀 병합 속성: colsapn, rowspan
- scope 속성
- col, colgroup

### form

- 데이터를 서버에 제공
- action, method

### input

- label : 서식 입력 요소 캡션
- name, placeholder, required, autofocus