# Inside Javascript

##  Chapter03 자바스크립트 데이터 타입과 연산자

## 배열

### 배열의 요소 생성

- 동적으로 배열 원소를 추가할 수 있다

- 어떤 인덱스 위치에나 값을 동적으로 추가할 수 있다

- 배열 크기는 인덱스에서 가장 큰 값을 기준으로 설정한다

  ```javascript
  const empty = []
  empty[0] = 1
  empty[3] = 5
  console.log(empty, empty.length, empty[1])
  // [ 1, <2 empty items>, 5 ] 4 undefined
  ```

### length 프로퍼티

- 배열에서 가장 큰 인덱스에 1을 더한 값이다

- 명시적 할당이 가능하다

- length 프로퍼티를 벗어나는 값은 삭제된다

  ```javascript
  const arr = [1, 2, 3]
  arr.length = 5
  console.log(arr, arr[3])
  // [ 1, 2, 3, <2 empty items> ] undefined
  arr.length = 1
  console.log(arr, arr[2])
  // [ 1 ] undefined
  ```

### 배열 표준 메서드와 length 프로퍼티

- 배열 메서드에 영향을 주므로 주의해서 사용한다

```javascript
const arr = [1, 2, 3]

arr.push(4)
arr.length = 5
arr.push(6)

console.log(arr)
// [ 1, 2, 3, 4, <1 empty item>, 6 ]
```

### 배열과 객체 차이점

- 배열은 length 프로퍼티가 있으나 객체는 없다
- 배열의 타입은 객체이다
- **배열 -> Array.property -> Object.property 순으로 상속한다.**
- 배열은 Object.prototype의 표준 메서드를 사용할 수 있다

### 배열 프로퍼티 동적 생성

- **length 프로퍼티는 배열 원소의 가장 큰 인덱스가 변경되었을 경우에만 변경된다**

  ```javascript
  const arr = [1, 2, 3]
  
  console.log(arr.length) // 3
  arr.name = 'array'
  arr.emotion = 'happy'
  console.log(arr.length) // 3
  
  arr.push(4)
  console.log(arr.length) // 4
  
  console.dir(arr)
  // [ 1, 2, 3, 4, name: 'array', emotion: 'happy' ]
  ```

### 프로퍼티 열거

- `for in` 만 요소뿐만 아니라 다른 프로퍼티도 출력한다

  ```javascript
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i])
  }
  // 1
  // 2
  // 3
  // 4
  arr.forEach((x) => {
    console.log(x)
  })
  // 1
  // 2
  // 3
  // 4
  for (const key in arr) {
    console.log(arr[key])
  }
  // 1
  // 2
  // 3
  // 4
  // array
  // happy
  
  for (const item of arr) {
    console.log(item)
  }
  // 1
  // 2
  // 3
  // 4
  ```

### 배열 요소 삭제

- `delete` 를 사용하여 요소를 삭제한다

- 요소를 `undefined`로 변경할 뿐 요소 자체를 삭제하지 않는다

- `length` 프로퍼티는 그대로이다

- `splice(start, deleteCount, item)` 배열 메서드를 사용해 요소를 완적히 삭제한다. 삭제한 요소를 배열 형태로 반환한다

  ```javascript
  const arr = [1, 2, 3]
  delete arr[0]
  console.log(arr)
  // [ <1 empty item>, 2, 3 ]
  
  arr[0] = 1
  
  arr.splice(1, 1)
  console.log(arr)
  // [ 1, 3 ]
  
  arr.splice(1, 1, 4, 5)
  console.log(arr)
  // [ 1, 4, 5 ]
  
  arr.splice(1, 0, ...[10, 11, 12])
  console.log(arr)
  //[ 1, 10, 11, 12, 4, 5 ]
  
  ```

### Array() 생성 함수

- 호출 인자가 1개이고 숫자인 경우 호출 인자를 length로 가지는 배열을 생성한다

- 그외에는 호출된 요소를 갖는 배열을 생성한다

  ```javascript
  const arr = new Array(5)
  console.log(arr, arr.length)
  // [ <5 empty items> ] 5
  
  const arr2 = new Array(1, 2, 3, 4, 5)
  console.log(arr2)
  // [ 1, 2, 3, 4, 5 ]
  ```

### array-like objects

- length 프로퍼티를 가진 배열을 `array-like objects` 유사 객체 배열이라 부른다

- `apply()` 메서드를 사용하면 객체여도 표준 배열 메서드를 사용할 수 있다

  ```javascript
  const obj = {
    name: 'jinsu',
    age: 27,
    length: 1,
  }
  
  Array.prototype.push.apply(obj, ['hello'])
  console.log(obj)
  // { '1': 'hello', name: 'jinsu', age: 27, length: 2 }
  ```

- `length` 프로퍼티가 키값으로 되어 `'hello'` 가 추가되어면서 length 가 1 증가하였다
- 만약 `length` 프로퍼티가 없으면 값이 1인  `length` 프로퍼티를 생성하고 0이 키가 되어 만들어진다

