# Inside Javascript

##  Chapter04 함수와 프로토타입 체이닝

### 함수 객체

- 함수는 일급 객체이다

- 프로퍼티를 가질 수 있다. 그리고 [[code]] 내부 프로퍼티에 함수 코드가 저장된다

  #### 일급 객체 First 

  - 리터럴에 의해 생성할 수 있다
  - 변수나 배열 요소, 객체 프로퍼티 등에 할당할 수 있다
  - 함수 인자로 전달할 수 있다
  - 함수 리턴값으로 리턴할 수 있다
  - 동적으로 프로퍼티를 생성 및 할당할 수 있다

  #### 함수 객체의 기본 프로퍼티

  ![image-20210817174911453](C:/Users/sangjs/AppData/Roaming/Typora/typora-user-images/image-20210817174911453.png)

  - name : 함수 이름, 익명 함수는 빈 문자열이다

  - coller : 자신을 호출한 함수 

  - arguments : 함수 호출시 전달된 인자값을 나타낸다. 호출된 상태가 아니므로 `null` 이다

  - `__proto__` : 모든 자바스크립트 객체는 자신의 프로토 타입을 가리키는 [[Prototype]] 내부 프로퍼티를 가진다.

  - **함수 객체의 부모 역할을 하는 포로토 타입 객체는 Function.prototype 객체이고 역시 함수 객체이다**

  - **Function.prototype 함수 객체의 부모는 Object.prototype 객체이다**

    ##### length 프로퍼티

    - 모든 함수가 가지는 표준 프로퍼티이다
    - 인자의 개수이다

    #### prototype 프로퍼티

    - 내부 `__proto__`, [[Prototype]] 과 다르다

    - 모든 객체 내부 프로퍼티인 `__proto__` 는 객체 자신의 부모 역할을 하는 프로토타입 객체를 가리킨다

    - prototype 프로퍼티는 이 함수가 생성자로 사용될 때 이 함수를 통해 생성된 객체의 부모 역할을 하는 프로토타입 객체를 가리킨다

    - **prototype 프로퍼티는 함수 생성시 만들어지고 constructor 프로퍼티 하나만 있는 객체를 가리킨다**

    - 함수 객체와 프로토타입 객체는 동시에 생성되어 각각 prototype, constructor라는 프로퍼티로 서로 참조한다

      ![image-20210817195320647](C:/Users/sangjs/AppData/Roaming/Typora/typora-user-images/image-20210817195320647.png)

      ![image-20210817195340994](C:/Users/sangjs/AppData/Roaming/Typora/typora-user-images/image-20210817195340994.png)

      - 프로토타입 객체 네이밍 -> 함수 prototype 프로퍼티가 가리키는 프로토타입 객체는 일반적으로 네이밍하지 않고 연결된 함수 prototype 값을 사용한다.
      - add() 함수 프로토타입 객체는 add.prototype이다

