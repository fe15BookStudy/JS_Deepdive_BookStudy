# 10장 객체 리터럴

## 10.1 객체란?

- 객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키(key)와 값(value)으로 구성된다. 객체는 프로퍼티와 메서드로 구성된다.
  - 프로퍼티: 객체의 상태를 나타내는 값
  - 메서드: 프로퍼티를 참조하고 조작할 수 있는 동작

```jsx
var counter = {
  num: 0,
  increase: function () {
    this.num++;
  },
};
```

- 구성
  - 객체: counter
  - 프로퍼티 : num : 0
  - 프로퍼티 키 : num
  - 프로퍼티 값: 0
  - 메서드 : increas: function() { this.num++; }
- JS에서 사용할 수 있는 모든 값은 프로퍼티 값이 될 수 있다.(함수도 프로퍼티 값으로 사용 가능! → 이 경우 일반 함수와 구분하기 위해 메서드라 부른다.)
- JS는 객체 기반의 프로그래밍 언어이다. 함수, 배열, 정규 표현식 등 모두 객체다.

## 10.2 객체 리터럴에 의한 객체 생성

- JS는 프로토타입 기반 객체지향 언어로서 클래스 기반 객체지향 언어와는 달리 다양한 객체 생성 방법을 지원한다.
  - 객체 리터럴
  - Object 생성자 함수
  - 생성자 함수
  - Object.create 메서드
  - 클래스(ES6)
- 객체 생성 방법 중에서 가장 일반적이고 간단한 방법은 객체 리터를을 사용하는 방법이다.
- 코드 블록의 닫는 중괄호 뒤에는 세미콜론을 붙이지 않지만 객체 리터럴은 값으로 평가되는 표현식이라 닫는 중괄호 뒤에 세미콜론을 붙인다.

```jsx
var person = {
  name: "Lee",
  sayHello: function () {
    console.log("Hello! My name is ${this.name}.");
  },
};

console.log(person); // {name: 'Lee', sayHello: ƒ}
```

## 10.3 프로퍼티

- 객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.
  - 프로퍼티 키: 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
  - 프로퍼티 값: JS에서 사용할 수 있는 모든 값
- 프로퍼티를 나열할 때는 쉼표(,)로 구분한다.
- 프로퍼티 키는 프로퍼티 값에 접근할 수 있는 이름으로서 식별자 역할을 한다.
- 문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 이때 프로퍼티 키로 사용할 표현식을 대괄호로 묶어야 한다.

  ```jsx
  var obj = {};
  var key = "hello";

  // ES5: 프로퍼티 키 동적 생성
  obj[key] = "world";
  // ES6: 계산된 프로퍼티 이름
  // var obj = { [key] : 'world' };

  console.log(obj); // {hello: 'world'}
  ```

- 프로퍼티 키에 문자열이나 심벌 값 외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다. 예를 들어, 프로퍼티 키로 숫자 리터럴을 사용하면 따옴표는 붙지 않지만 내부적으로는 문자열로 변환된다.

```jsx
var foo = {
  0: 1,
  1: 2,
  2: 3,
};

console.log(foo); // {0: 1, 1: 2, 2: 3}
```

- 이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다. 이때 에러가 발생하진 않는다.

```jsx
var foo = {
  name: "Lee",
  name: "Kim",
};

console.log(foo); // {name: 'Kim'}
```

## 10.4 메서드

- JS의 함수는 객체(일급 객체)다. 따라서 함수는 값으로 취급할 수 있기 때문에 프로퍼티 값으로 사용할 수 있다. 이때 일반 함수와 구분하기 위해 메서드(method)라 부른다. 즉, 메서드는 객체에 묶여 있는 함수를 의미한다.

```jsx
var circle = {
  radius: 5,

  // 원의 지름
  getDiameter: function () {
    // 메서드
    return 2 * this.radius; // this는 circle을 가리킨다.
  },
};

console.log(circle.getDiameter()); // 10
```

- 여기서 this는 객체 자신 (위에선 circle 객체)을 가리키는 참조변수다.

## 10.5 프로퍼티 접근

- 프로퍼티에 접근하는 방법은 다음과 같이 두 가지다.
  - 마침표 프로퍼티 접근 연산자(.)를 사용하는 **마침표 표기법**
  - 대괄호 프로퍼티 접근 연산자([…])를 사용하는 **대괄호 표기법**
- 대괄호 표기법을 사용하는 경우 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 한다.

```jsx
var person = {
  name: "Lee",
  "last-name": "Park",
};

console.log(person.name); // Lee
console.log(person["last-name"]); // Park
console.log(person["name"]); // Lee
```

- 프로퍼티 키가 숫자로 이뤄진 문자열인 경우 따옴표를 생략할 수 있다.

```jsx
var person = {
  name: "Lee",
  "last-name": "Park",
  1: 10,
};

console.log(person.name); // Lee
console.log(person["last-name"]); // Park
console.log(person["name"]); // Lee

person[1]; // 10
person["1"]; // 10
```

## 10.6 프로퍼티 값 갱신

- 이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.

```jsx
var person = {
  name: "Lee",
};

person.name = "Kim";

console.log(person.name); // Kim
```

## 10.7 프로퍼티 동적 생성

- 존재하지 않는 프로퍼티 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.

```jsx
var person = {
  name: "Lee",
};

person.age = 20;

console.log(person.age); // 20
```

## 10.8 프로퍼티 삭제

- delete 연산자는 객체의 프로퍼티를 삭제한다. 이때 delete 연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다.

```jsx
var person = {
  name: "Lee",
};

person.age = 20;

console.log(person); // {name: 'Lee', age: 20}

delete person.age;

console.log(person); // {name: 'Lee'}
```

## 10.9 ES6에서 추가된 객체 리터럴의 확장 기능

- ES6에서는 다음과 같이 더욱 간편하고 표현력 있는 개체 리터럴의 확장 기능을 제공한다.

### 10.9.1 프로퍼티 축약 표현

- ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티 키를 생략할 수 있다. 이때 프로퍼티 키는 변수 이름으로 자동 생성된다.

```jsx
// ES6
let x = 1,
  y = 2;

// 프로퍼티 축약 표현
const obj = { x, y };

console.log(obj); // {x: 1, y: 2}
```
