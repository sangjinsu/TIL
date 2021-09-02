# Inside Javascript

## Chapter05 실행 컨텍스트와 클로저

### 스코프 체인

- 자바스크립트도 다른 언어와 동일하게 유효 범위가 있다 
- **<u>하지만 자바스크립트 내에서는 함수 안의  `{}` 블록과 같이 `for(){}`, `if{}` 와 같은 구문은 유효 범위가 없다</u>**
- **<u>오직 함수만이 유효 범위의 한 단위가 된다</u>**
- <u>**유효 범위를 나타내는 스코프가 [[scope]] 프로퍼티로 각 함수 객체 내에서 연결 리스트 형식으로 관리된다**</u>
- <u>**=> 스코프 체인**</u>

- <u>**각각의 함수는 [[scope]] 프로퍼티로 자신이 생성된 실행 컨텍스트의 스코프 체인을 참조한다**</u> 
- **<u>함수 실행시 실행 컨텍스트가 생성되고 실행된 함수의 [[scope]] 프로퍼티를 기반으로 새로운 스코프 체인을 만든다</u>** 

#### 전역 실행 컨텍스트의 스코프 체인

```js
const var1 = 1
const var2 = 2
console.log(var1)
console.log(var2)
```

- 변수 객체의 [[scope]] 는 변수 객체 자신이다 

  149 페이지  그림 5-8

#### 함수를 호출한 경우 생성되는 실행 컨텍스트의 스코프 체인

```js
const var1 = 1
const var2 = 2
function func() {
    const var1 = 10
    const var2 = 20
    console.log(var1)
    console.log(var2)
}
func()
console.log(var1)
console.log(var2)
```

- `func()` 함수 실행으로 새로운 컨텍스트가 만들어진다 

- >  func 컨텍스트의 스코프 체인은 실행된 함수의 [[scope]] 프로퍼티를 그대로 복사한 후 현재 생성된 변수 객체를 복사한 스코프 체인의 맨 앞에 추가한다.

- func 실행 컨텍스트의 스코프 체인은 [func 변수 객체 - 전역 객체]이다 

  150 페이지 그림 5-9

  - 각 함수 객체는 [[scope]] 프로퍼티로 현재 컨텍스트의 스코프 체인을 참조한다
  - 현재 실행되는 함수 객체의 [[scope]] 프로퍼티를 복사하고 새롭게 생성된 변수 객체를 해당 체인 맨 앞에 추가한다
  - 스코프 체인 => 현재 실행 컨텍스트의 변수 객체 + 상위 컨텍스트의 스코프 체인 

```js
const v = 'v1'
function func(){
    const v = 'v2'
    function func2(){
        return v
    }
    console.log(func2())
}
func() // v2
```

```js
const v = 'v1'
function func(){
    return v
}
function func2(f){
    const v = 'v2'
    console.log(f())
}
func2(func) // v1
```

- 스코프 체인으로 식별자 인식이 이루어진다
- 스코프 체인의 첫번째 변수 객체부터 식별자 인식은 시작한다 
- 함수 호출시 대응되는 프로퍼티를 찾을 때가까지 객체를 이동한다
- **<u>`this` 는 식별자가 아닌 키워드로 분류하므로 스코프 체인의 참조 없이 접근할 수 있다</u>**

- 현재 실행 컨텍스트에 추가하는 with 구문은 사용하지 않는다 (python global 키워드 같은 존재)

