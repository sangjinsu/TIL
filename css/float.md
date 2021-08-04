# Float

- 텍스트를 둘러싸는 레이아웃을 위해 도입

- normal flow에서 빠져 텍스트 및 인라인 요소에 감싸짐

  | 속성값 | 설명                   |
  | ------ | ---------------------- |
  | none   | 기본값                 |
  | left   | 요소를 외쪽으로 띄움   |
  | right  | 요소를 오른쪽으로 띄움 |

```css
      .clearfix::after {
        content: "";
        display: block;
        clear: both;
      }
```

```html
    <div class="clearfix">
      <div class="box1 left">div</div>
    </div>
```

- clearfix - 가상의 요소를 생성하여 float으로 인한 겹침을 방지한다. float된 요소의 부모 요소에 적용한다.
- clear 속성은 부동 및 비부동 요소 모두에 적용이 된다.

