# Inside Javascript

##  Chapter06 객체지향 프로그래밍

### 함수형 프로그래밍 개념

- 함수 조합으로 작업을 수행한다
- 작업 수행 동안 데이터의 상태는 변경되지 않는다
- 함수만 변경된다
- 순수 함수 pure function 은 외부에 영향을 미치지 않는 함수이다
- 고계 함수 higher-order function 은 함수를  값으로 활용하여 인자나 반환값으로 설정하는 함수이다
- 자바스크립트에서 함수는 일급 객체로 취급되어 함수 인자나 반환값으로 사용 가능하다

### 예시

```js
const arr = [1, 2, 3, 4]
const sum = (x, y) => {
    return x + y
}
const mul = (x, y) => {
    return x * y
}

function reduce(func, arr, memo){
    let accum = memo
    for(let i = 0; i < arr.length; i++){
        accum = func(accum, arr[i])
    }
    
    return accum
}

console.log(reduce(sum, arr, 0))
console.log(reduce(mul, arr, 1))
```

