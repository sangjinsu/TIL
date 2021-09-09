# Inside Javascript

##  Chapter06 객체지향 프로그래밍

### 캡슐화

- 정보 은닉

  ```js
  const Person = function(arg){
      const name = arg ? arg : 'jinsu'
      
      return {
          getName(){
              return name
          },
          setName(arg){
              name = arg
          }
      }
  }
  
  const me = Person()
  console.log(me.name, me.getName()) // undefined jinsu
  ```

  - private 멤버가 객체나 배열인 경우 사용자가 쉽게 변경하는 문제가 발생한다 
  - 이 문제를 해결하기 위해서는 함수를 반환하는 방법이 접근을 불가능하게 하기 때문에 좋다

  ```js
  const Person = function(arg){
      const name = arg ? arg : 'jinsu'
      
      const Func = function(){}
      Func.prototype = {
          getName(){
              return name
          },
          setName(arg){
              name = arg
          }
      }
      
      return Func
  }()
  
  const me = Person()
  console.log(me.name, me.getName()) 
  // TypeError: Cannot read property 'name' of undefined
  ```

