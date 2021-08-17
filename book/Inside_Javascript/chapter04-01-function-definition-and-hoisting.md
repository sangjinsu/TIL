# Inside Javascript

##  Chapter04 함수와 프로토타입 체이닝

### 함수 정의

- function statement

- function expression

- Function()

  #### 함수 선언문

  - 함수도 일반 객체로 취급한다

    ```js
    function add(a, b){
        return a + b
    }
    ```

  #### 함수 표현식

  - 함수는 일급 객체로 하나의 값으로 취급한다

    ```js
    const add = function(a, b){
        return a + b
    }
    
    const plus = add
    ```

  - add, plus 함수 변수는 같은 익명 함수를 참조한다

  - 이름이 없는 함수 형태는 익명 함수이다

  - 익명 함수 반대는 기명 함수이다

    ```js
    const add = function sum(a, b){
        return a + b
    }
    
    sum(7, 6) // error 발생
    
    // 재귀 함수에서의 활용
    const factorial_recursive = function factorial(n){
        if(n <= 1){
            return 1
        }
        return factorial(n-1) * n
    }
    ```

  #### 함수 선언문과 표현식에서의 세미콜론

  ```js
  const func = function() {
      return 42
  }  // 세미콜론 미사용                                          (function() {
      console.log('function called')
  })();
  ```

  - TypeError 발생 - 42() 으로 실행되어 버린다
  - 함수 표현식 방식에서는 세미콜론을 권고하기도 한다

  #### Function()

  - 생성자 함수로 함수를 생성한다

    ```js
    const add = new Function('x', 'y', 'return x+y')
    ```

  #### 함수 호이스팅

  - Function Hoisting
  - **세 방식 모두 같은 기능의 함수를 생성하지만 내부 동작이 다르다**
  - 함수 선언문 방식은 유효 범위가 전범위이기 때문에 코드 구조를 망칠 가능성이 있다.(함수 호이스팅) 함수 표현식 사용을 더글라스 크락포드는 권고한다
  - 함수 호이스팅은 자바스크립트 변수 생성(instatation)과 초기화(initialization) 작업의 분리가 원인이다

