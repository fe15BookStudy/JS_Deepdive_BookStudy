## 25.1 클래스는 무엇인가?
- 클래스는 함수이다.
→ 클래스 선언 시 내부적으로 생성자 함수가 만들어진다.
- class 키워드를 사용하며, 이름은 보통 파스칼 케이스(MyClass)로 쓴다.
- 클래스도 값처럼 표현식으로 정의 가능하다.

| 구분        | 생성자 함수                              | 클래스 (`class`)                    |
| ---------- | -----------------------------------------| ---------------------------------- |
| **호출 방식**  | `new` 없이 호출 가능                   | 반드시 `new`로 호출해야 함          |
| **상속 문법**  | `prototype`을 수동으로 연결            | `extends`, `super` 키워드 제공      |
| **호이스팅**   | 함수 호이스팅 발생 (선언 전 호출 가능)  | TDZ 존재 — 선언 전에 호출 불가        |
| **엄격 모드**  | 명시하지 않으면 비엄격 모드             | 항상 암묵적으로 strict mode          |
| **메서드 속성** | enumerable: true (열거 가능)          | enumerable: false (열거 불가능)     |

```javascript
const Person = class MyClass {};
```
- 클래스는 리터럴, 변수, 매개변수, 반환값 등으로 사용 가능하다.

## 25.2 클래스 정의
- 클래스는 class 키워드로 정의.
- 내부에 생성자(constructor), 프로토타입 메서드, 정적(static) 메서드 정의 가능.
- 클래스 표현식으로도 정의 가능.
```javascript
class Person {
  constructor(name) { this.name = name; }
  sayHi() { console.log(`Hi ${this.name}`); } // 프로토타입 메서드
  static sayHello() { console.log("Hello!"); } // 정적 메서드
}
```
## 25.3 클래스 호이스팅
- 클래스도 호이스팅이 발생한다.
단, let, const처럼 **TDZ(일시적 사각지대)** 에 묶인다.
→ 선언 이전에 접근하면 ReferenceError 발생.
- 클래스 선언은 런타임 이전에 평가되지만 **초기화 전까지는 접근 불가.**

## 25.4 인스턴스 생성
- 클래스는 반드시 new 연산자와 함께 호출해야 한다.
→ 일반 함수처럼 호출 시 TypeError 발생.
- 클래스 표현식에서 이름은 내부에서만 유효하다.
- 인스턴스는 클래스의 설계도를 바탕으로 만들어진 객체이다.

## 25.5 클래스의 메서드
클래스 내부에는 3종류 메서드만 정의 가능:
1. constructor
2. 프로토타입 메서드
3. 정적(static) 메서드

🔹 constructor (생성자)

- 인스턴스를 생성하고 필드를 초기화하기 위한 특수 메서드.
- 클래스 내에 단 하나만 존재 가능 (SyntaxError otherwise)
- return문이 없어도 자동으로 this가 반환됨.
- 명시적으로 객체를 반환하면 this가 무시되고 그 객체가 반환됨.
```javascript
class Person {
  constructor(name) {
    this.name = name;
    return {}; // this 무시
  }
}
new Person('Lee'); // {}
```
🔹 프로토타입 메서드
- 클래스 내부에서 정의된 일반 메서드 → prototype에 저장됨.
- 모든 인스턴스가 공유한다.
```javascript
class Person {
  sayHi() { console.log(`Hi ${this.name}`); }
}
```
🔹 정적(static) 메서드
- static 키워드로 정의.
- 클래스 이름으로 호출하며, 인스턴스에서 호출 불가.
```javascript
class Person {
  static sayHello() { console.log('Hello!'); }
}
Person.sayHello();
```
- 프로토타입 메서드와 달리 this가 인스턴스가 아닌 클래스 자체를 가리킴.
- 주로 유틸리티 함수, 헬퍼 함수 정의용으로 사용.

### 정적 메서드 vs 프로토타입 메서드
| 구분     | 프로토타입 메서드   | 정적 메서드           |
| ------ | ----------- | ---------------- |
| 호출 대상  | 인스턴스        | 클래스              |
| `this` | 인스턴스        | 클래스 자체           |
| 목적     | 인스턴스 데이터 조작 | 클래스 레벨의 공통 기능 제공 |




### 1. 메서드 정의 방식
클래스 내부에 메서드를 정의하면 자동으로 prototype 메서드가 된다.
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }
}
```
- Person.prototype.sayHi로 저장된다.
- 모든 인스턴스는 이 메서드를 공유한다.
프로토타입 체인 관계는 다음과 같다:
```javascript
me → Person.prototype → Object.prototype
```

### 2. 정적 메서드(static method)
- 메서드에 static 키워드를 붙이면 **클래스 자체에 바인딩**된다.
- 즉, 인스턴스가 아니라 **클래스로 직접 호출**해야 한다.

```javascript
class Person {
  static sayHi() {
    console.log('Hi!');
  }
}
Person.sayHi(); // ✅ Hi!
new Person().sayHi(); // ❌ TypeError
```
정적 메서드는 클래스 함수 객체의 프로퍼티로 저장된다.
(프로토타입이 아니라 클래스 자신에 속함)

### 3. 정적 메서드 vs 프로토 타입 메서드
| 구분           | 정적 메서드    | 프로토타입 메서드      |
| ------------ | --------- | -------------- |
| 소속           | 클래스 자체    | 클래스의 prototype |
| 호출 방식        | 클래스명으로 호출 | 인스턴스로 호출       |
| this         | 클래스 자신    | 인스턴스           |
| 인스턴스 프로퍼티 접근 | 불가능       | 가능             |
```javascript
class Square {
  static area(w, h) { return w * h; } // 정적
  area() { return this.width * this.height; } // 프로토타입
}
```
> 정적 메서드는 공통 동작(유틸리티 함수)에 적합하고, 프로토 타입 메서드는 개별 인스턴스 동작에 적합하다.

### 4. 클래스 메서드의 특징
1. function 키워드 생략
→ 축약 메서드 형태로 정의함.
2. 암묵적 strict mode 적용.
3. 열거 불가 ([[Enumerable]]: false).
4. non-constructor
→ 메서드 자체로는 new 사용 불가.

### 5. 내장 객체의 정적 메서드 예시
| 내장 객체   | 정적 메서드 예시                  |
| ------- | -------------------------- |
| Math    | `Math.max()`, `Math.min()` |
| Number  | `Number.isNaN()`           |
| JSON    | `JSON.stringify()`         |
| Object  | `Object.is()`              |
| Reflect | `Reflect.has()`            |
→ 유틸리티 함수처럼 클래스(또는 네임스페이스) 단위로 묶어두는 개념.

## 25.6 클래스의 인스턴스 생성 과정
인스턴스는 new 연산자와 함께 클래스를 호출하면 생성된다.

1️⃣ 빈 객체 생성

- new 연산자가 호출되면 암묵적으로 빈 객체 생성.
- 이 객체는 Person.prototype을 프로토타입으로 설정.

2️⃣ this 바인딩
- constructor 내부의 this가 이 새 객체를 참조하게 됨.

3️⃣ 프로퍼티 추가 및 초기화
- constructor 내부에서 this.name = name 식으로 프로퍼티 초기화.

4️⃣ 인스턴스 반환
- constructor가 반환하지 않으면, this가 암묵적으로 반환됨.
```javascript
class Person {
  constructor(name) {
    console.log(this); // Person {}
    this.name = name;
  }
}
const me = new Person('Lee');
```

## 25.7 프로퍼티
### 25.7.1 인스턴스 프로퍼티
- 반드시 constructor 내부에서 정의해야 한다.
- 클래스 몸체(class body)에는 직접 정의 불가능 (이후 class field 문법에서 가능).
```javascript
class Person {
  constructor(name) {
    this.name = name; // 인스턴스 프로퍼티
  }
}
```
- 인스턴스 프로퍼티는 항상 public.
(자바나 C#의 private, public, protected 같은 키워드는 지원하지 않음)

### 25.7.2 접근자 프로퍼티 (getter / setter)
접근자 프로퍼티는 값을 직접 저장하지 않고,
다른 프로퍼티 값을 간접적으로 읽거나 쓸 때 사용한다.
```javascript
class Person {
  constructor(first, last) {
    this.firstName = first;
    this.lastNa나 접근 가능하고 외부에서는 완전히 차단된다.
```javascript
class Person {
  #name = 'Lee';
  get name() { return this.#name; }
}
const me = new Person();
console.log(me.name); // Lee
console.log(me.#name); // ❌ SyntaxError
```
> private 필드는 반드시 클래스 몸체에 선언해야 하며,
> constructor 내부에서 정의하면 문법 오류가 발생한다.

### 25.7.5 static 필드 정의 제안
- static 키워드로 클래스 레벨의 프로퍼티를 정의할 수 있다.
- 인스턴스가 아닌 클래스 자체에 바인딩된다.
```javascript
class MyMath {
  static PI = 3.141592;
  static #count = 0; // private static
  static increment() { return ++MyMath.#count; }
}
console.log(MyMath.PI); // 3.141592
console.log(MyMath.increment()); // 1
```

### 1. 클래스 필드의 개념
- 클래스 필드(field) 는 클래스의 프로퍼티(멤버 변수) 를 정의하는 문법이다.
- 기존에는 클래스 내부에 메서드만 선언할 수 있었고, 프로퍼티는 반드시 constructor 안에서 정의해야 했다.
- ES2022(또는 Chrome 72+, Node.js 12+)부터 클래스 몸체(class body) 안에서도 직접 필드를 정의할 수 있게 되었다.
```javascript
class Person {
  name = 'Lee'; // 클래스 필드 정의
}
const me = new Person();
console.log(me.name); // 'Lee'
```
> → 클래스 필드는 인스턴스의 프로퍼티로 생성된다.

### 2. 클래스 필드의 초기화와 this
- 클래스 필드를 정의할 때는 this를 사용할 수 없다.
  - 클래스 필드는 constructor 실행 전 단계에서 평가되기 때문.
- 따라서 클래스 몸체 내부에서 this.name = ... 형태는 사용할 수 없고,
 그건 constructor 안에서만 가능하다.
 ```javascript
 class Person {
  this.name = 'Lee'; //❌ SyntaxError
 }  
 ```

 ### 3. 클래스 필드의 초기값
 - 필드에 값을 할당하지 않으면 undefined로 초기화된다.

 ```javascript
 class Person {
  name; // undefined
}
const me = new Person();
console.log(me.name); // undefined
```

### 4. 클래스 필드와 함수 할당
- 클래스 필드에 함수(화살표 함수 포함)를 할당할 수 있다.
- 이런 함수는 프로토 타입 메서드가 아니라, 인스턴스의 메서드로 만들어진다.
```javascript
class Person {
  name = 'Lee';
  getName = function() { return this.name; }; // 인스턴스 메서드
  arrowGetName = () => this.name; // 화살표 함수도 가능
}
```

### 5. 클래스 필드와 화살표 함수
- 화살표 함수를 클래스 필드에 할당하면,
해당 함수의 this는 항상 인스턴스를 가리킨다.
```javascript
class App {
  constructor() {
    this.button = document.querySelector('.btn');
    this.count = 0;
    this.button.onclick = this.increase; // this 고정
  }
  increase = () => {
    this.button.textContent = ++this.count;
  };
}
```
> 이 방법은 이벤트 핸들러의 this 문제를 해결할 때 자주 사용된다.

### 6. 클래스 필드의 공개 범위 (public / private)
(1) 기본값: public
- 모든 클래스 필드는 기본적으로 public이다.
- 즉, 외부에서도 자유롭게 접근 가능.
```javascript
class Person {
  name = 'Lee';
}
console.log(new Person().name); // Lee
```
(2) private 필드
- #을 붙여 정의한다.
- 클래스 내부에서만 접근 가능하며, 외부에서 접근 시 SyntaxError 발생.
```javascript
class Person {
  #name = 'Lee';
  getName() { return this.#name; }
}
const me = new Person();
console.log(me.getName()); // Lee
console.log(me.#name); // ❌ SyntaxError
```
> private 필드는 반드시 클래스 몸체 안에서 정의해야 한다.
> constructor 내부에서 직접 정의하면 에러가 난다.

### 7. private 필드의 접근자 메서드
- 외부 접근이 불가능하므로, 간접적으로 접근하기 위해 getter/setter를 사용한다.
```javascript
class Person {
  #name;
  constructor(name) { this.#name = name; }
  get name() { return this.#name.trim(); }
  set name(value) { this.#name = value; }
}
```

### 8. static 필드 (정적 필드)
- static 키워드를 붙이면 인스턴스가 아닌 클래스 자체에 속하는 프로퍼티를 정의한다.
```javascript
class MyMath {
  static PI = 3.141592;
  static #count = 0; // private static
  static increment() { return ++MyMath.#count; }
}
console.log(MyMath.PI); // 3.141592
console.log(MyMath.increment()); // 1
```
> - "인스턴스로는 접근 불가 (`myMath.PI ❌`)"
> - "클래스 이름을 통해 직접 접근해야 함"




## 25.8 클래스 상속

### 1. 상속의 기본 개념
- 자바스크립트 클래스는 다른 클래스를 extends 키워드로 확장할 수 있다.
- 부모 클래스(슈퍼클래스)의 모든 속성과 메서드를 물려받는다.
```javascript
class Animal {
  eat() { return 'eat'; }
}
class Bird extends Animal {
  fly() { return 'fly'; }
}
const bird = new Bird();
console.log(bird.eat()); // eat
console.log(bird.fly()); // fly
```

### 2. 클래스 상속의 내부 구조
상속은 프로토타입 체인을 통해 구현된다.
```javascript
Bird.prototype → Animal.prototype → Object.prototype
Bird → Animal → Function.prototype
```
> 따라서 인스턴스(bird)는 Animal의 메서드에도 접근할 수 있다.

### 3. extends 키워드
- 클래스뿐 아니라 생성자 함수를 상속받을 수도 있다. 
- extends는 super 키워드와 함께 동작한다.
```javascript
class Derived extends Base {}
```

### 4. super 키워드
super는 두 가지 역할을 한다.

1️⃣ 부모 클래스의 생성자(super constructor) 호출

2️⃣ 부모 클래스의 메서드(super method) 참조

(1) super() 호출
- 서브클래스의 constructor에서 반드시 super()를 호출해야 한다.
- 부모 클래스의 인스턴스 생성 및 this 초기화 역할을 함.
- super() 호출 전에는 this를 사용할 수 없다.
```javascript
class Base {
  constructor(a, b) { this.a = a; this.b = b; }
}
class Derived extends Base {
  constructor(a, b, c) {
    super(a, b);
    this.c = c;
  }
}
```
(2) super.method() 호출
- 부모 클래스의 prototype 메서드를 호출할 때 사용.
- 내부적으로 Object.getPrototypeOf(Derived.prototype) 을 통해 부모 prototype 참조.
```javascript
class Base { sayHi() { return 'Hi'; } }
class Derived extends Base {
  sayHi() { return `${super.sayHi()} Lee`; }
}
```
### 5. super의 동작 원리
- super는 자신이 속한 메서드의 [[HomeObject]] 내부 슬롯을 이용해 부모 프로토타입을 참조한다.
- 따라서 super는 ES6 메서드 축약 표현으로 정의된 함수 안에서만 사용 가능하다.
### 6. 동적 상속
- extends 뒤에는 클래스뿐 아니라 평가식도 가능하다.
```javascript
class Derived extends (condition ? Base1 : Base2) {}
```
> 런타임 시점의 조건에 따라 상속 대상을 바꿀 수 있음.
### 7. 상속의 개념
- 상속(Inheritance) 은 기존 클래스를 확장(extend) 하여 새로운 클래스를 만드는 메커니즘.
- 자식(서브클래스)은 부모(슈퍼클래스)의 속성과 메서드를 그대로 물려받고, 자신만의 속성을 추가할 수 있다.
- 코드 재사용과 구조적 계층 설계가 가능해짐.

### 8. 의사 클래스 상속(pseudo classical inheritance)
ES6 이전에는 함수 기반으로 상속을 흉내 냈다.
```javascript
function Animal(age, weight) {
  this.age = age;
  this.weight = weight;
}
Animal.prototype.eat = function() { return 'eat'; };
Animal.prototype.move = function() { return 'move'; };

function Bird(age, weight) {
  Animal.call(this, age, weight); // super 호출처럼 부모 생성자 실행
}
Bird.prototype = Object.create(Animal.prototype);
Bird.prototype.constructor = Bird;
Bird.prototype.fly = function() { return 'fly'; };
```
- Animal → Bird 의 프로토타입 체인 연결
- new Bird(1,5) 하면 Bird → Animal → Object 순으로 상속 구조 탐색됨

### 9. extends 키워드(ES6 상속)
```javascript
class Animal { ... }
class Bird extends Animal { ... }
```
- extends는 **부모 클래스(슈퍼클래스)**와 **자식 클래스(서브클래스)**의 상속 관계를 설정.
- 클래스 간뿐만 아니라 **함수 객체(생성자 함수)**도 상속 가능.
- 내부적으로 프로토타입 체인이 자동으로 연결된다.

```plaintext
Bird.prototype → Animal.prototype → Object.prototype
Bird → Animal → Function.prototype
```
즉,
- **인스턴스 프로토타입 체인**과
- **클래스 자체의 프로토타입 체인**이 각가 연결된다.

### 10. 서브클래스의 constructor
- 서브클래스에서 constructor를 생략하면 자동으로 아래처럼 정의된다.
```javascript
constructor(...args) { super(...args); }
```
- 즉, 부모 클래스의 constructor를 자동 호출한다.
- 직접 정의할 경우 반드시 `super()`를 호출해야 한다.
 그렇지 않으면 `ReferenceError: Must call super constructor...` 발생

 ```javascript
 class Base {}
class Derived extends Base {
  constructor() {
    super(); // ✅ 반드시 필요
    this.value = 1;
  }
}
```

### 11. super 키워드

(1) constructor 내부에서

- super()는 부모 클래스의 constructor(=super-constructor) 를 호출한다.
- 부모 인스턴스를 생성하고, 그 인스턴스를 this에 바인딩한다.
- super() 호출 전에는 this를 사용할 수 없다.
```javascript
class Base {
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
}
class Derived extends Base {
  constructor(a, b, c) {
    super(a, b); // 부모 constructor 호출
    this.c = c;
  }
}
```
(2) 메서드 내부에서

- super.method()는 부모 클래스의 prototype 메서드를 호출한다.
- 내부적으로는 Object.getPrototypeOf(Derived.prototype) 를 참조.
```javascript
class Base { sayHi() { return 'Hi'; } }
class Derived extends Base {
  sayHi() { return `${super.sayHi()} Lee`; }
}
```
→ super.sayHi() 는 Base.prototype.sayHi를 가리킴.

### 12. super 참조의 내부 동작
- super는 자신이 정의된 메서드의 [[HomeObject]] 내부 슬롯을 통해 부모 프로토타입을 찾는다.
- [[HomeObject]]는 ES6 메서드 축약 표현으로 정의된 메서드에만 존재.
- 따라서 super는 메서드 축약 표현 안에서만 사용할 수 있다.
```javascript
const base = { sayHi() { return 'Hi'; } };
const derived = {
  __proto__: base,
  sayHi() { return `${super.sayHi()} Lee`; } // OK
};
```
### 13. super의 수동 모사
- 실제로 super는 다음과 같은 코드로 동작한다.
```javascript
const _super = Object.getPrototypeOf(Derived.prototype);
_super.sayHi.call(this);
```
- 즉, 부모 프로토타입의 메서드를 찾아 현재 인스턴스의 this를 바인딩하여 실행한다.

### 14. 동적 상속
- extends에는 클래스뿐 아니라 생성자 함수 반환식도 올 수 있다.
- 즉, 어떤 조건에 따라 상속 대상을 동적으로 바꿀 수 있다.
```javascript
class Derived extends (condition ? Base1 : Base2) {}
```
### 15. super 관련 주의점

1. 서브클래스 constructor에서 super() 호출 전에는 this를 참조할 수 없다.
2. super()는 서브클래스에서만 사용 가능 (extends 없는 클래스나 일반 함수에서 사용 불가).
3. 메서드 안에서 super는 부모 클래스의 prototype 메서드를 참조한다.
→ 정적 메서드 안에서는 부모 클래스의 정적 메서드를 참조.

### 16. 상속과 프로토타입 체인 구조 요약
| 구분     | 프로토타입 체인                                                          |
| ------ | ----------------------------------------------------------------- |
| 인스턴스   | `derived → Derived.prototype → Base.prototype → Object.prototype` |
| 클래스 자체 | `Derived → Base → Function.prototype`                             |
- 따라서 자식 클래스 인스턴스는 부모 클래스의 모든 메서드에 접근 가능.
- 정적(static) 메서드 역시 상속된다.

### 17. 핵심 흐름 요약

| 단계               | 설명                           |
| ---------------- | ---------------------------- |
| ① `extends` 선언   | 부모-자식 클래스 상속 관계 설정           |
| ② `super()` 호출   | 부모 constructor 실행 및 this 초기화 |
| ③ this 활성화       | super 이후부터 this 사용 가능        |
| ④ 메서드 내 super    | 부모 prototype 메서드 호출          |
| ⑤ [[HomeObject]] | super 참조의 내부 슬롯              |
| ⑥ 프로토타입 체인 연결    | 클래스 간, 인스턴스 간 모두 자동 연결       |


### 18. 서브 클래스의 인스턴스 생성 과정
🔹 기본 개념
- 클래스 간 상속에서 서브클래스(subclass) 는 인스턴스를 직접 만들지 않고, 슈퍼클래스(superclass) 에게 인스턴스 생성을 위임한다.
- extends 키워드를 사용하면, 자바스크립트 내부적으로 두 종류의 클래스가 구분된다.
  - base 클래스: 다른 클래스를 상속받지 않은 클래스
  - derived 클래스: 다른 클래스를 상속받은 클래스 (extends 사용)

🔹 동작 순서
1. new 연산자와 함께 서브클래스를 호출하면,
2. JS 엔진은 먼저 슈퍼클래스의 constructor를 호출한다.
3. 슈퍼클래스 constructor가 빈 객체(this)를 생성하고 초기화한다.
4. 이 인스턴스가 서브클래스로 전달되어, 서브클래스의 constructor 내부에서 super()가 실행된다.
5. super() 호출 후에만 this를 사용할 수 있다. (그 전엔 아직 인스턴스가 존재하지 않음)

```javascript
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
}

class ColorRectangle extends Rectangle {
  constructor(width, height, color) {
    super(width, height); // super가 this 생성 및 초기화
    this.color = color;
  }
}
```
- super()를 호출하지 않으면 에러 발생 (ReferenceError: Must call super constructor)
- super() 호출 후 this를 사용할 수 있다.

### 19. super와 this 바인딩
- super는 슈퍼클래스의 constructor나 메서드를 참조하는 키워드이다.
- super()는 슈퍼클래스의 constructor를 호출하고, 그 결과로 생성된 인스턴스를 this에 바인딩한다.
- 따라서 서브클래스 내부에서 super()를 호출해야만 this가 활성화된다.
```javascript
class ColorRectangle extends Rectangle {
  constructor(width, height, color) {
    super(width, height); // 반드시 먼저 호출
    console.log(this); // Rectangle 인스턴스
    this.color = color;
  }
}
```

### 20. [[HomeObject]]와 super 참조
- super 키워드는 ES6 메서드 축약 표현으로 정의된 메서드 안에서만 사용 가능.
- 이 메서드는 내부 슬롯 [[HomeObject]] 를 갖는다.
- super는 이 [[HomeObject]]를 통해 자신의 “부모 클래스의 프로토타입”을 참조한다.
```javascript
const base = {
  sayHi() {
    return 'Hi';
  }
};

const derived = {
  __proto__: base,
  sayHi() {
    return `${super.sayHi()} Lee!`; // base.sayHi() 호출
  }
};
```
### 21. 상속 관계의 프로토타입 체임
클래스 상속 시 인스턴스와 클래스 자체 모두 프로토타입 체인이 연결된다.
```javascript
ColorRectangle.prototype → Rectangle.prototype → Object.prototype
ColorRectangle → Rectangle → Function.prototype
```
즉, 인스턴스의 메서드 탐색 순서:
colorRectangle → ColorRectangle.prototype → Rectangle.prototype → Object.prototype

### 22. 표준 빌트인 생성자 함수 확장 (Array 예제)
🔹 기본 Array 상속
```javascript
class MyArray extends Array {
  uniq() {
    return this.filter((v, i, self) => self.indexOf(v) === i);
  }
  average() {
    return this.reduce((a, b) => a + b, 0) / this.length;
  }
}
```
- MyArray는 Array를 상속하므로, 배열 관련 내장 메서드(map, filter, reduce) 사용 가능.
- 인스턴스는 Array.prototype의 메서드뿐 아니라 MyArray.prototype의 메서드도 쓸 수 있다.
```javascript
const myArray = new MyArray(1, 1, 2, 3);
console.log(myArray.uniq()); // MyArray [1, 2, 3]
console.log(myArray.average()); // 1.75
```
### 23. Symbol.species와 메서드 체이닝 문제
-Array의 map, filter 등은 새로운 배열 인스턴스를 반환한다.
- 기본적으로 반환 타입은 파생 클래스(MyArray) 가 아니라 Array이다.
- 따라서 메서드 체이닝 시, MyArray에만 있는 메서드를 이어서 쓸 수 없음.
```javascript
myArray.uniq() instanceof MyArray; // false
myArray.uniq() instanceof Array;   // true
myArray.uniq().average(); // ❌ TypeError
```
🔹 해결: Symbol.species
```javascript
class MyArray extends Array {
  static get [Symbol.species]() { return Array; }
}
```
- 이렇게 하면 filter, map 같은 메서드가 Array 인스턴스를 반환하도록 제어할 수 있다.
- 반대로 Symbol.species를 MyArray로 두면 MyArray 인스턴스를 유지할 수도 있다.
