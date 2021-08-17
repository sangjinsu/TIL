# Inside Javascript

##  Chapter04 함수와 프로토타입 체이닝

### 함수 형태

	#### 콜백 함수

- 함수를 등록하고 이벤트 발생이나 특정 시점에 호출되는 함수이다
- 대표적인 콜백함수는 이벤트 핸들러 처리이다

#### 즉시 실행 함수 immediaete functions

- 최초 한 번 실행만이 필요한 초기화 코드 부분등에 사용된다

#### 내부 함수 inner functions

- 클로저 생성, 부모 함수 코드에서 외부 접근을 막고 독립적인 함수를 구현하는 용도 등으로 사용된다

- 내부 함수는 부모 함수의 변수에 접근이 가능하다 -> 스코프 체이닝

- 내부 함수는 일반적으로 부모 함수 내부에서만 호출된다

- 클로저 예시

  ```js
  function closure(){
      const a = 100
      const child = function(){
          console.log(a)
      }
      return child
  }
  ```

#### 함수를 리턴하는 함수

```js
const func = function(){
    console.log('hello')
    return function(){
        console.log('bye')
    }
}
```



