# font-family

- 속성은 선택된 요소에 우선 순위가 지정된 font family 이름과 generic family 이름을 지정할 수 있게 해줍니다
- 하나 이상의 글꼴을 나열할 때는 쉼표를 사용한다
- 글꼴 이름에 공간이 들어가는 경우 `" "` 를 사용한다
- family-name, generic-family 순으로 설정한다
- [MDN](https://developer.mozilla.org/ko/docs/Web/CSS/font-family)

# word-wrap & word-break

- [`word-wrap`](https://www.w3schools.com/cssref/css3_pr_word-wrap.asp) : 속성을 사용하면 긴 문자열을 끊고 다음 줄에 넣을 수 있습니다.

  | 속성값     | 설명                                                         |
  | ---------- | ------------------------------------------------------------ |
  | normal     | 허용되는 구분점에서만 단어를 구분합니다.                     |
  | break-word | 끊을 수 없는 단어를 끊을 수 있습니다.                        |
  | initial    | 이 속성을 기본값으로 설정합니다. [Read about *initial*](https://www.w3schools.com/cssref/css_initial.asp) |
  | inherit    | 상위 요소에서 이 속성을 상속합니다. [Read about *inherit*](https://www.w3schools.com/cssref/css_inherit.asp) |

- [`word-break`](https://www.w3schools.com/cssref/css3_pr_word-break.asp): 속성은 행의 끝에 도달할 때 단어가 구분되는 방법을 지정합니다.

  | 속성값     | 설명                                                         |
  | ---------- | ------------------------------------------------------------ |
  | normal     | 기본값입니다. 기본 줄 바꿈 규칙을 사용합니다.                |
  | break-all  | 오버플로우를 방지하기 위해 임의의 문자에서 단어가 끊어질 수 있습니다. |
  | keep-all   | 중국어/일본어/한국어(CJK) 텍스트에는 단어 구분 기호를 사용하면 안 됩니다. CJK가 아닌 텍스트 동작이 "일반" 값과 동일합니다. |
  | break-word | 오버플로를 방지하기 위해 임의 지점에서 단어가 끊어질 수 있습니다. |
  | initial    | 이 속성을 기본값으로 설정합니다. [Read about *initial*](https://www.w3schools.com/cssref/css_initial.asp) |
  | inherit    | 상위 요소에서 이 속성을 상속합니다. [Read about *inherit*](https://www.w3schools.com/cssref/css_inherit.asp) |

  

