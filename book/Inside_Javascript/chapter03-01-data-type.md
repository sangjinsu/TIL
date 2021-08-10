# Inside Javascript

##  Chapter03 자바스크립트 데이터 타입과 연산자

### 자바스크립트 데이터 타입

- 기본 타입
  - Number
  - String
  - Boolean
  - [undefined](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/undefined)
  - [null](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/null)
  - Symbol

- 참조 타입
  - Object
    - Array
    - Function
    - 정규표현식

---



### 기본 타입

- `typeof` : 타입 확인

- 약타입 언어

  #### Number

  - **자바스크립트는 모든 숫자를 64비트 부동 소수점 형태로 저장한다**

  - 정수 부분만 얻기 위해서는 `Math.floor()` 을 사용한다

  #### String

  - 문자열은 immuatable 이다
  
  #### Boolean
  
  - true, false
  
  #### *<u>null과 undefined !!</u>* 
  
  - 모두 값이 비어있다는 것을 의미한다
  
  - 값이 할당되지 않은 값은 `undefined`이다
  
  - <u>**`undefined`는 타입이자 값을 나타낸다**</u>
  
  - `null` 은 개발자가 명시적으로 값이 비어있음을 의미한다
  
  - ```javascript
    typeof null // object
    // null 타입 변수인지 확인 할 때는 === 를 사용한다
    null === null // true
    ```
  
  - [`null`과 `undefined` 차이](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/null#difference_between_null_and_undefined)

---



### 참조 타입  - 객체

- 배열, 함수, 정규표현식 등

  #### 객체 생성

  ```javascript
  const person = new Object()
  
  person.name = 'jinsu' 
  person.age = 27
  person.gender = 'male'
  ```
  
  ```javascript
  const person = {
  	name: 'jinsu',
      age: 27,
      gender: 'male'
  }
  ```
  
  #### 객체 프로퍼티 읽기 / 쓰기 / 갱신
  
  ```javascript
  person.age // 27, 객체에 프로퍼티가 없는 경우 undefined
  person['age'] // 27
  
  person.height = 177.7 // 새로운 프로퍼티 동적 생성 후 값 할당
  person['full-name'] = 'jinsu sang'
  
  person.full-name // NaN, Not a Number, 수치 연산에서 정상적인 값을 얻지 못할 때 발생
  person['full-name'] // 'jinsu sang'
  ```
  
  #### for-in 문
  
  ```javascript
  for (const key in person) {
    if (Object.hasOwnProperty.call(person, key)) {
      console.log(key, person[key])
    }
  }
  ```
  
  #### 객체 프로퍼티 삭제
  
  ```javascript
  delete person['full-name'] // 프로퍼티만 삭제
  ```

---

### 참조 타입 특성

- 객체의 모든 연산은 실제 값이 아닌 참조값으로 처리된다

  #### 객체 비교
  
  ```javascript
  let objA = {value: 100}
  let objB = {value: 100}
  let objC = objB
  
  console.log(objA === objB) // false
  console.log(objA == objB)  // false
  console.log(objB === objC) // true 참조값이 같아야 true 이다
  console.log(objB == objC)  // true
  ```
  
  #### 참조에 의한 함수 호출 방식
  
  - 기본 타입  => call by value
  - 참조 타입 => call by reference
  
  - 함수 인자로 참조 타입이 사용될 경우 참조 타입의 값은 변경되므로 주의한다 
