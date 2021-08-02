# Selector 심화

## 결합자 Combinators

- 자손 결합자

  - selectorA 하위의 모든 selectorB  요소

    ```css
    div span {
        color: red;
    }
    ```

- 자식 결합자

  - selectorA 바로 아래의 selectorB 요소

    ```css
    div > span {
        color: red;
    }
    ```

- 일반 형제 결합자

  - selectorA의 형제 요소 중 뒤에 일치하는 selectorB요소를 모두 선택

    ```css
    p ~ span {
        color: red;
    }
    ```

    

- 인접 형제 결합자

  - selectorA의 형제 요소 중 바로 뒤에 위치하는 selectorB 요소 선택

    ```css
    p + span {
        color: red;
    }
    ```

    

  

