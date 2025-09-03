# 10. 객체 리터럴

### 객체

- 자바스크립트는 객체 기반의 프로그래밍 언어이며, 자바스크립트를 구성하는 거의 모든 것이 객체다. 원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등)은 모두 객체다.

- 원시 타입은 단 하나의 값만 나타내지만 객체 타입(object/reference type)은 다양한 타입의 값(원시 값 또는 다른 객체)을 하나의 단위로 구성한 복합적인 자료구조(data structure)다.

<br>

객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 **`키(key)`** 와 **`값(value)`** 으로 구성된다.

함수도 프로퍼티 값이 될 수 있는데, 프로퍼티 값이 함수일 경우 이를 **`메서드(method)`** 라 부른다.

프로퍼티와 메서드의 역할은 다음과 같다.

<br>

- `프로퍼티`: 객체의 상태를 나타내는 값(data)

- `메서드`: 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작(behavior)

이처럼 객체는 객체의 상태를 나타내는 값(프로퍼티)과 프로퍼티를 참조하고 조작할 수 있는 동작(메서드)을 모두 포함할 수 있기 때문에 상태와 동작을 하나의 단위로 구조화할 수 있어 유용하다.

<br>

### 객체 리터럴에 의한 객체 생성

객체 생성 방법 중에서 가장 일반적이고 간단한 방법은 객체 리터럴을 사용하는 방법이다. 앞서 살펴보았듯이 `'리터럴'` 은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용하여 값을 생성하는 표기법을 말한다.

객체 리터럴은 중괄호({ ... }) 내에 0개 이상의 프로퍼티를 정의한다. 변수에 할당되는 시점에 자바스크립트
엔진은 객체 리터럴을 해석해 객체를 생성한다.

```JavaScript
var person = {
name: 'Lee",
sayHello: function() {
}
console.log("Hello! My name is ${this.name});
};
console.log(typeof person); // object
console.log(person); // {name: "Lee", sayHello: f}
```

만약 중괄호 내에 프로퍼티를 정의하지 않으면 빈 객체가 생성된다.

```JavaScript
var empty = {}; // 빈 객체
console.log(typeof empty); // object
```

앞서 코드 블록의 닫는 중괄호 뒤에는 세미
콜론을 붙이지 않기로 했다. 그러나 객체 리터럴은 값으로 평가되는 표현식이다. 따라서 객체 리터럴의 닫는 중괄호 뒤에는 세미콜론을 붙인다.

<br>

### 프로퍼티

**객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.**

```JavaScript
var person = {
// 프로퍼티 키는 name, 프로퍼티 값은 'Lee'
name:
Lee.
//프로퍼티 키는 age, 프로퍼티 값은 20
age: 20
};
```

프로퍼티를 나열할 때는 쉼표(,)로 구분한다. 일반적으로 마지막 프로퍼티 뒤에는 쉼표를 사용하지 않으나
사용해도 좋다.

- 프로퍼티 키가 식별자 네이밍 규칙을 따르는지 여부에 따라 사용법에 차이가 있다.

  규칙을 준수하는 경우: 따옴표('...' 또는 "...")를 생략할 수 있다.

```JavaScript
var person = {
  firstName: 'Ung-mo', // 식별자 규칙을 따르므로 따옴표 생략 가능
  age: 20 // 숫자도 마찬가지
};
console.log(person); // { firstName: 'Ung-mo', age: 20 }
```

- 규칙을 준수하지 않는 경우: 반드시 따옴표를 사용해야 합니다. 따옴표를 생략하면 자바스크립트 엔진이 연산자로 해석하여 `SyntaxError`가 발생할 수 있다. 예시: `'last-name': 'Lee'`

가급적 식별자 네이밍 규칙을 준수하는 프로퍼티 키를 사용하는 것이 좋다.

```JavaScript
var person = {
  'last-name': 'Lee', // 하이픈(-)은 식별자 규칙을 위반하므로 따옴표 필수
  '1st-place': 'Gold' // 숫자로 시작하는 키도 따옴표 필수
};
console.log(person); // { 'last-name': 'Lee', '1st-place': 'Gold' }
```

- 동적 생성: 문자열 또는 문자열로 평가될 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수 있다. 이때 키로 사용할 표현식을 대괄호(`[...]`)로 묶어야 한다.

```JavaScript
var obj = {};
var key = 'name';
var value = 'John';

// 동적으로 프로퍼티 키 생성
obj[key] = value; // obj['name'] = 'John'과 동일

console.log(obj); // { name: 'John' }
```

타입 변환: 문자열이나 심벌 값 외의 값을 프로퍼티 키로 사용하면 해당 값은 암묵적으로 문자열로 타입 변환된다.

```JavaScript
var foo = {
 0: 'number', // 숫자 0은 문자열 '0'으로 변환
 true: 'boolean', // 불리언 true는 문자열 'true'로 변환
 null: 'null' // null은 문자열 'null'로 변환
};
console.log(foo); // { '0': 'number', 'true': 'boolean', 'null': 'null' }
```

예약어: `var`, `function`과 같은 자바스크립트 예약어도 프로퍼티 키로 사용할 수 있지만 예상치 못한 오류를 일으킬 수 있으므로 권장하지 않는다.

```JavaScript
var keywords = {
    var: 'variable',
  function: 'method'
};
console.log(keywords); // { var: 'variable', function: 'method' }
```

키 중복: 동일한 이름의 프로퍼티 키를 중복으로 선언하면 나중에 선언된 프로퍼티가 이전에 선언된 프로퍼티를 덮어쓴다. 이때 에러는 발생하지 않는다.

```JavaScript
var user = {
  name: 'Lee', // 첫 번째 name 프로퍼티
  age: 30,
  name: 'Kim'  // 두 번째 name 프로퍼티가 첫 번째를 덮어씀
};
console.log(user); // { name: 'Kim', age: 30 }
```

### 메서드

자바스크립트에서 객체의 프로퍼티 값이 함수일 경우 이 함수를 메서드라고 부른다. 메서드는 객체에 묶여 있는 함수를 의미한다. 메서드 내부에서 사용되는 this 키워드는 메서드가 속한 객체 자신을 가리킨다.

예시:

```JavaScript
var circle = {
  radius: 5,
  getDiameter: function () {
    return 2 * this.radius; // 'this'는 circle 객체를 참조
  }
};
console.log(circle.getDiameter()); // 10
```

#### 프로퍼티 접근

객체의 프로퍼티에 접근하는 방법에는 마침표 표기법과 대괄호 표기법 두 가지가 있다.

- 마침표 표기법 (.): 프로퍼티 키가 식별자 네이밍 규칙을 준수하는 경우에만 사용 가능합니다.

`예시: person.age`

- 대괄호 표기법 ([...]): 프로퍼티 키가 문자열인 경우 사용하며 키를 따옴표로 묶어 표현한다. 동적으로 프로퍼티에 접근하거나 키가 식별자 네이밍 규칙을 따르지 않는 경우에 유용하다.

`예시: person['last-name']`

두 방법 모두 연산자 왼쪽에 객체로 평가되는 표현식을 사용하고 마침표 오른쪽 또는 대괄호 내부에 프로퍼티 키를 지정한다.

### 프로퍼티 값 갱신

이미 존재하는 객체 프로퍼티에 새로운 값을 할당하면 해당 프로퍼티의 값이 갱신된다.

```JavaScript
var person = { name: 'Lee' };
person.name = 'Kim'; // 'name' 프로퍼티의 값을 'Kim'으로 갱신
console.log(person); // { name: 'Kim' }
```

### 프로퍼티 동적 생성

객체에 존재하지 않는 프로퍼티에 값을 할당하면 새로운 프로퍼티가 동적으로 생성되고 해당 값이 할당된다.

```JavaScript
var person = { name: 'Lee' };
person.age = 20; // 'age' 프로퍼티가 없으므로 새로 생성
console.log(person); // { name: 'Lee', age: 20 }
```

### 프로퍼티 삭제

`delete` 연산자는 객체의 프로퍼티를 삭제한다. 연산자의 피연산자로는 프로퍼티에 접근하는 표현식이 와야 한다. 존재하지 않는 프로퍼티를 삭제하려 해도 에러가 발생하지 않는다.

```JavaScript
var person = { name: 'Lee', age: 20 };
delete person.age; // 'age' 프로퍼티 삭제
delete person.address; // 'address' 프로퍼티는 없으므로 무시됨
console.log(person); // { name: 'Lee' }
```

## ES6에서 추가된 객체 리터럴의 확장 기능

ES6는 객체 리터럴을 더 간결하게 표현하는 기능을 제공한다.
<br>

### 프로퍼티 축약 표현

- 프로퍼티 값으로 사용하는 변수의 이름과 프로퍼티 키의 이름이 같을 때 프로퍼티 키를 생략할 수 있다.

  - ES5: var obj = { x: x, y: y };

  - ES6: const obj = { x, y };

```JavaScript

let x = 1, y = 2;
const obj = { x, y };
console.log(obj); // { x: 1, y: 2 }
```

### 계산된 프로퍼티 이름

- 객체 리터럴 내에서 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수 있다. 이때 표현식은 대괄호([])로 묶어야 한다.

  - ES5: 객체 리터럴 외부에서 obj[표현식] = 값 형태로 사용해야 했다.

  - ES6: 객체 리터럴 내부에서 [표현식]: 값 형태로 바로 사용 가능하다.

```JavaScript

// ES6 예시
const prefix = 'prop';
let i = 0;
const obj = {
  [`${prefix}-${++i}`]: i, // 'prop-1': 1
  [`${prefix}-${++i}`]: i, // 'prop-2': 2
};
console.log(obj); // { 'prop-1': 1, 'prop-2': 2 }
```

### 메서드 축약 표현

- 메서드를 정의할 때 function 키워드를 생략하는 간결한 문법을 제공한다.

  - S5: sayHi: function() { ... }

  - ES6: sayHi() { ... }

```JavaScript

// ES6 예시
const obj = {
  name: 'Lee',
  sayHi() {
    console.log(`Hi! ${this.name}`);
  }
};
obj.sayHi(); // Hi! Lee
```
