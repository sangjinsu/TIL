# Inside Javascript

##  Chapter03 자바스크립트 데이터 타입과 연산자

### 프로토타입

- **자바스크립트의 모든 객체는 부모 객체(프로토타입 객체)와 연결되어 있다**
- **모든 객체는 자신의 프로토타입을 가리키는 [[Prototype]]라는 숨겨진 프로퍼티를 가진다**
- ECMAScript 명세서에는 [[Prototype]] 이라고 명시하지만 chome dptjsms `__proto__` 이다
- 객체 리터럴 방식으로 생성된 개체는 Object.prototype 객체이다
- Object.property 개체에 있는 다양한 메서드를 사용할 수 있다 

