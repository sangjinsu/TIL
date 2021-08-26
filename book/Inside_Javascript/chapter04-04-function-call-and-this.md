# Inside Javascript

##  Chapter04 함수와 프로토타입 체이닝

### 함수 호출과 this

- #### arguments 객체

  - 함수 인자보다 적게 함수 호출시 값이 넘겨지지 않은 인자는 `undefined`값이 할당된다
  - 인자 개수가 많은 경우는  에러가 발생하지 않고 초과된 인수는 무시된다
  - `arguments` 는 유사 배열 객체이다
    - 함수 인자는 배열 형태이다
    - `length` 프로퍼티는 넘겨진 인자의 개수이다
    - `callee` 프로퍼티는 현재 실행 중인 함수의 참조값이다
    - <u>**유사 배열 객체이므로 배열 메서드 사용시 에러가 발생한다!!**</u>

- #### 호출 패턴과 this 바인딩

  - `arguments`객체와 `this` 인자가 함수 내부로 암묵적으로 전달된다

  - ##### 객체 메서드 호출할 때 this 바인딩

    - **<u>메서드에서 사용된 `this`는 자신을 호출한 객체에 바인딩된다</u>**

- #### 함수 호출할 때 this 바인딩

  - 함수 호출하면 함수 내부 코드에서 사용된 `this` 는 전역 객체에 바인딩 된다

  - 브라우저는 window 전역 객체, node.js 는 global 전역 객체에 바인딩 된다

  - **<u>함수 호출에서의 `this` 바인딩은 내부 함수 inner function 호출시에도 적용된다</u>**

  - 내부 함수 호출 패턴을 자바스크립트는 정의하지 않는다

  - 내부 함수의 `this` 는 전역 객체에 바인딩 된다

    ```js
    var value = 100
    var myObject = {
        value: 1,
        func1: function(){
            this.value += 1
            console.log(this.value) // 2
            
            func2 = function(){
                this.value += 1
                console.log(this) // window
                console.log(this.value)// 101
                
                func3 = function(){
                    this.value += 1
                    console.log(this) // window
                    console.log(this.value) // 102
                }
                
                func3()
            }
            
            func2()
        }
    }
    myObject.func1()
    ```
  
  - 부모 함수의 this를 내부 함수가 접근 가능한 다른 변수에 저장하는 방법이 있다

    ```js
    var value = 100
    var myObject = {
        value: 1,
        func1: function(){
            var that = this
            this.value += 1
            console.log(this.value) // 2
            
            func2 = function(){
                that.value += 1
                console.log(that) // {value: 3, func1: ƒ}
                console.log(that.value)// 3
                
                func3 = function(){
                    that.value += 1
                    console.log(that) // {value: 4, func1: ƒ}
                    console.log(that.value) // 4
                }
                
                func3()
            }
            
            func2()
        }
    }
    myObject.func1()
    ```
  
- #### 생성자 함수를 호출할 때 this 바인딩

  - **기존 함수에 new 연산자를 붙여서 호출하면 해당 함수를 생성자 함수로 동작한다**

  - 특정 함수가 생성자 함수로 정의되어 있으면 첫 문자를 대문자로 쓰기를 권장한다

    - ##### 생성자 함수 동작 방식, new 연산자로 생성자 호출

      1. 빈 객체 생성 및 this 바인딩
         1. 생성자 함수 코드가 실행되기 전 빈 객체 생성
         2. 빈 객체에 this 로 바인딩
         3. 생성자 함수 코드 내부에서 사용된 this는 빈 객체를 가리킨다
         4. 사실상 빈 객체가 아니라 자신의 부모인 프로토타입 객체와 연결되어 있고 부모 메서드를 사용할 수 있다
         5. **<u>생성자 함수가 생성한 객체는 자신을 생성한 생성자 함수의 property 프로퍼티가 가리키는 개체를 자신의 프로토타입 객체로 설정한다</u>**

      2. this를 통한 프로퍼티 생성
         1. 함수 코드 내부에서  this를 사용해서 생성된 빈 객체에 동적으로 프로퍼티나 메서드를 생성할 수 있다

      3. 생성된 객체 리턴

         1. 리턴문 동작 방식은 경우에 따라 다르다

            - 리턴문이 없는 경우 this로 바인딩된 새로 생성한 객체가 리턴된다
              - 명시적으로 this를 리턴해도 결과가 같다
              - 생성자 함수가 아닌 일반 함수를 호출할 때 리턴값이 명시되어 있지 않으면 undefined 가 리턴된다

            - 리턴 값이 새로 생성한 this가 아닌 다른 객체를 반환하는 경우 생성자 함수를 호출했다고 하더라도  this가 아닌 해당 객체가 리턴된다

    - ```js
      var Person = function(name) {
          this.name = name
      }
      var p1 = new Person('jinsu')
      ```

      1. Person()함수가 생성자로 호출되면 빈 객체가 생성
      2. 빈 객체는 Person() 성성자 함수의 prototype 프로퍼티가 가리키는 객체 Person.prototype 객체를 [[Prototype]] 링크로 연결해서 자신의 프로토 타입으로 설정한다
      3. 생성된 객체는 생성자 함수 코드에서 사용되는 this로 바인딩 된다.
      4. this가 가리키는 빈 객체에 name이라는 동적 프로퍼티를 생성한다
      5. 리턴값이 특별히 없으므로 this로 바인딩한 객체가 생성자 함수의 리턴값으로 반환되어 p1 변수에 저장된다

- #### 객체 리터럴 방식과 생성자 함수를 통한 객체 생성 방식의 차이

  - 객체 리터럴 방식으로 생성된 객체는 같은 행태의 객체를 재생성할 수 없다

  - 프로로타입 객체인 `__prototype__` 이 다르다

    - 객체 리터럴 방식은 자신의 프로토타입 객체가 Object.prototype 이다
    - 생성자 함수 방식은 생성자 함수의 prototype 프로퍼티이다

    - **<u>자바스크립트 객체 생성 규칙에서 자바스크립트 객체는 자신을 생성한 생성자 함수의 prototype 프로퍼티가 가리키는 객체를 자신의 프로토타입 객체로 설정한다는 것이다</u>**

- #### 생성자 함수를 new를 붙이지 않고 호출할 경우

  - 일반 함수와 생성자 함수의 차이는 없다

  - 생성자 함수를 `new`없이 호출하거나 일반 함수에  `new` 를 사용해 호출할 때 오류가 발생할 수 있다

  - 일반 함수 호출은 this가 window 전역 객체에 바인딩된다

  - 생성자 함수 호출은 this가 새로 생성된 빈 객체에 바인딩 된다

  - 생성자 함수 호출에 `new` 가 없는 경우 `this`는 window 전역 객체에 바인딩된다. 리턴값은 `undefined` 이다 

    - 해당 상황을 피하기 위한 패턴

      ```js
      function A(arg){
          if (!(this instanceof A)) return new A(arg)
          this.value = arg ? arg : 0
      }
      ```

- #### call과  apply 메서드를 이용한 명시적인 this 바인딩

  - Function.prototype 객체의 메서드이다

  - apply(), call() => 함수가 호출하며 this를 특정 객체에 바인딩할 뿐 역시 함수 호출이다

    - 첫번째 인자인 객체에 this로 명시적으로 바인딩된다

    - 두번재 argArray 인자는 함수를 호출할 때 넘길 인자들의 배열을 가리킨다

      ```js
      function Person(name, age){
          this.name = name
          this.age = age 
      }
      
      let p1 = {}
      Person.apply(p1, ['jinsu', 27])
      Person.call(p1, 'jinsu', 27)
      ```

    - **<u>유사 배열 객체에서 배열 매서드를 사용하도록 할 수 있다</u>**

      - arguments 객체에서 마치 배열 메서드가 있는 것처럼 처리한다
      - `slice()`는 인자가 없는 경우 전체 배열을 복사한다
      - args 의 `__prototype__` 은 Array.prototype 인 반면, arguments는 Object.prototype이다

      ```js
      function func() {
          const args = Array.prototype.slice.apply.(arguments)
      }
      ```

      

    