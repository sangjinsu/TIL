 

# Inside Javascript

## Chapter05 실행 컨텍스트와 클로저

### 클로저

```js
function outer(){
    const x = 10
    const inner = function(){
        console.log(x)
    }
    return inner
}
const inner = outer()
inner()
```

- inner() 의 스코프 체인은 outer 실행 컨텍스트가 사라졌지만  outer 변수 객체를 참조한다

  [전역 객체, outer, inner]

- 자바스크립트에서 구현한 클로저이다

- ***<u>이미 생명 주기가 끝난 외부 함수의 변수를 참조하는 함수를 클로저라고 한다</u>***

- outer 에서 선언된 `x` 변수를 참조하는 inner 가 클로저이며 `x`를 자유 변수라고 한다 

- > 자유 함수에 엮어있는 함수

- 대부분의 클로저에서는 스코프 체인에서 뒤쪽에 있는 객체에 접근하므로 성능을 저하시키고 메모리 부담이 많아진다. 그러므로 클로저를 사용할 때는 경험이 많이 필요하다 

### 클로저 활용

- 클로저는 성능과 자원 면ㄴ에서 손해가 발생할 수도 있으므로 무차별적으로 사용해서는 안된다

  #### 특정 함수에 사용자가 정의한 객체의 메서드 연결하기

  ```js
  function HelloFunc(){
      this.greeting = "hello"
  }
  
  HelloFunc.prototype.call = function(func){
      func ? func(this.greeting) : this.func(this.greeting)
  }
  const userFunc = function(greeting){
      console.log(greeting)
  }
  
  let obj = new HelloFunc()
  obj.func = userFunc
  obj.call() // hello
  ```

  ```js
  function saySomething(obj, methodName, name){
      return function(greeting){
          return obj[methodName](greeting, name)
      }
  }
  
  function newObj(obj, name){
      obj.func = saySomething(this, 'who', name)
      return obj
  }
  newObj.prototype.who = function(greeting, name){
      console.log(`${greeting} ${name || 'everyone'}`)
  }
  
  const obj1 = new newObj(obj, 'jinsu')
  obj1.call() // hello jinsu
  ```

  - obj1.call() 에서 실행되는 것은 실질적으로 newObj.prototype.who() 이다 
  - 실행 순서를 눈여겨 살펴보자 ~~ㅠㅠ 

  #### 함수의 캡슐화

  - 생략 - 164쪽

  #### setTimeout() 에 지정되는 함수의 사용자 정의

  ```js
  function callLater(obj, a, b){
      return (function(){
          obj.sum = a + b
          console.log(obj.sum)
      })
  }
  
  const sumObj = {
      sum : 0
  }
  const func = callLater(sumObj, 5, 6)
  setTimeout(func, 5000)
  ```

### 클로저 주의사항

	#### 클로저의 프로퍼티값이 쓰기 가능하므로 그 값이 여러 번 호출로 항상 변할 수 있음에 유의해야 한다

```js
function outer(num){
    return function(x) {
        num += x
        console.log(num)
    }
}

exam = outer(40)
exam(5) // 45
exam(-3) // 42
```

#### 한 클로저가 여러 함수 객체의 스코프 체인에 들어가 있는 경우도 있다

```js
function func(){
    let x = 1
    return {
        func1(){
            console.log(++x)
        },
        func2(){
            console.log(-x)
        }
    }
}
const exam = func()
exam.func1() // 2
exam.func2() // -2
```

#### 클로저를 루프 안아세 사용할 때 주의해야 한다

```js
function count(time){
    for(var i = 0; i <= time; i++){
        setTimeout(function() {
            console.log(i)
        }, i * 1000)
    }
}

count(3)
```

- setTimeout 함수 인자로 들어가는 함수는 자유 변수 i를 참조한다.
- 하지만 setTimeout 실행되는 함수는 i가 이미 4가 되므로 모두 4를 출력한다
  - 반복문의 i 가 `let` 으로 설정되어 있는 겨우 정상적으로 출력이 된다
  - ***<u>`let` 의 유효 범위 규칙</u>***
    - `let` 으로 선언된 변수는 변수가 선언된 블록 내에서만 유효하다
    - `var`는 함수 블록 이외의 블록은 무시하고 선언된다 

```js
function count(time){
    for(var i = 0; i <= time; i++){
        (function(current){
            setTimeout(function() {
            	console.log(current)
        	}, i * 1000)
        })(i)

    }
}

count(3)
```



