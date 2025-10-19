# 모던 자바스크립트 Deep Dive

## 25장 클래스

## 클래스 정의

클래스는 class 키워드를 사용하여 정의하면 일반적으로 파스칼 케이스를 사용한다.

```js
class Person {}
```

일반적이지는 않지만 함수와 마찬가지로 표현식으로 클래스를 정의할 수 있다.

```js
const Person = class {};

const Person = class MyClass {}; // 함수와 마찬가지로 이름을 가질 수도 있다.
```

클래스를 표현식으로 정의할 수 있다는 것은 일급객체라는 것을 의미한다.
조 ㅁ더 자세히 말하자면 클래스는 함수다. 클래스 몸체에는 0개 이상의 메서드만 정의할 수 있따. 클래스 몸체에서 정의할 수 있는 메서드는 constructor, 프로토타입 메섣, 정적 메서드 이다.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  // 프로토타입 메서드
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }

  // 정적 메서드
  static sayHello() {
    console.log("Hello!");
  }
}

const me = new Person("Lee");

console.log(me.name);
me.sayHi();
Person.sayHello();
```

### 클래스 호이스팅

```js
class Person {}
console.log(typeof Perosn); // function
```

클래스는 함수로 평가된다. 클래스 선언문으로 정의한 클래스는 함수 선언문과 같이 소스코드 평가 과정에 평가되어 함수 객체를 생성한다.

클래스 선언문은 마치 호이스팅이 발생하지 않는 것처럼 보이나 그렇지 않다

```js
const Person = "` ";
{
  console.log(Person); // 호이스팅이 발생하지 않는다면 ''이 출력되어야한다.
  // 오류

  class Person {}
}
```

클래스 선언문도 변수 선언, 함수 정의와 마찬가지로 호이스팅이 발생한다. 클래스는 let, const 키워드로 선언한 변수처럼 호이스팅된다. 따라서 클래스 선언문 이전에 일시적 사각지대에 빠지기 때문에 호이스팅이 발생하지 않는 것처럼 동작한다.

## 인스턴스 생성

클래스는 생성자 함수이며 new 연산자와 함께 호출되어 인스턴스를 생성한다.

```js
class Person {}

// 인스턴스 생성
const me = new Person();
console.log(me); // Person()
```

## 메서드

클래스 몸체에는 0개 이상의 메서드만 선언할 수 있다.

### constructor

constructor는 인스턴스를 생성하고 초기화하기 위한 특수한 메서드다.

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}
```

- constructor는 클래스내에 최대 한개만 존재할 수 있다.
- constructor는 생략할 수 있다.
- constructor를 생략하면 빈 constructor가 암묵적으로 정의된다.
- constructor 내부에서 return 문을 반드시 생략해야 한다.

```js
class Person1 {
  constructor() {}
  constructor() {}
  // 오류
}
class Person2{}

class Person3{
  // constructor를 생략하면 빈 constructor를 생성 => constructor() {}
}
const me= new Person3();
console.log(me) // Person3

```

1. 프로퍼티가 추가되어 초기화된 인스턴스를 생성하려면 constructor 내부에서 this에 인스턴스 프로퍼티를 추가한다.

2. 클래스 외부에서 인스턴스 프로퍼티의 초기값을 전달하려면 다음과 같이 constructor에 매개변수를 선언하고 초기값을 전달한다.

```js
class Person1 {
  constructor() {
    this.name = "Lee";
    this.address = "Seoul";
  }
}
const me = new Person1();
console.log(me); // Person1{name : "Lee", address : "Seoul";}

class Person2 {
  constructor(name, address) {
    this.name = name;
    this.address = address;
  }
}
const me = new Person2("Lee", "Seoul");
console.log(me); // Person2{name : "Lee", address : "Seoul";}
```

### 프로토타입 메서드

생성자 함수를 사용하여 인스턴스를 생성하는 경우 프로토타입 메서드를 생성하기 위해서는 다음과 같이 명시적으로 프로토타입에 메서드를 추가해야한다.

```js
function Person(name) {
  this.name;
}
Person.prototype.sayHi = function () {
  console.log(`Hi! My name is ${this.name}`);
};

const me = new Person("Lee");
me.sayHi(); // Hi! My name is Lee
```

클래스 몸체에서 정의한 메서드는 prototype 프로퍼티에 메서드를 추가하지 않아도 기본적으로 프로토타입 메서드가 된다.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  // 프로토타입 메서드
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }
}
const me = new Person("Lee");
me.sayHi(); // Hi! My name is Lee
```

### 정적 메서드

생성자 함수의 경우 정적 매서드를 생성하기 위해서는 다음과 같이 명시적으로 생성자 함수에 메서드를 추가해야한다.

```js
function Person(name) {
  this.name = name;
}

Person.sayHi = function () {
  console.log(`Hi!`);
};
// 정적 메서드 호출
Person.sayHi(); // HI!
```

클래스에서는 메서드에 static 키워드를 붙이면 정적 메서드가 된다.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  // 정적 메서드
  static sayHello() {
    console.log("Hi!");
  }
}
```

- 정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있다.
- 정적 메서드는 인스턴스로 호출할 수 없다.

인스턴스로 호출할 수 없는 이유는정적 메서드가 바인딩된 클래스는 인스턴스의 프로토타입 체인상에 존재하지 않기때문이다. (프로토타입 메서드는 인스턴스의 프로토타입에 존재함)

인스터스의 프로토타입 체인 상에는 클래스가 존재하지 않기 때문에 인스턴스로 클래스의 메서드를 상속받을 수 없다.

```js
Person.sayHi(); // Hi!

const me = new Person("Lee");
me.sayHi(); // 에러
```

### 정적메서드와 프로토타입 메서드의 차이

1. 정적메서드와 프로토타입 메서드는 자신이 속해 있는 프로토타입 체인이 다르다.
2. 정적 메서드는 클래스로 호출하고 프로토타입 메서드는 인스턴스로 호출된다.
3. 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있다.

### 클래스에서 정의한 메서드의 특징

1. function 키워드를 생략한 메서드 축약 표현을 사용한다.
2. 객체 리터럴과는 다르게 클래스에 메서드를 정의할 때는 콤마가 필요없다.
3. 암묵적으로 strict mode가 실행된다.
4. for..in 문이나 Object.keys 메서드 등으로 열거할 수 없다. 프로퍼티 어트리뷰트 [[Enumrable]]의 값이 false다.
5. 내부 메서드[[Constructor]]를 갖지 않는 non-constructor다. 따라서 new 연산자와 함께 호출할 수 없다.

## 클래스의 인스턴스 생성 과정

new 연산자와 함께 클래스를 호출하면 생성자 함수에 마찬가지로 클래스의 내부 메서드 [[Constructor]]가 호출된다. 클래스는 new 연산자 없이 호출할 수 없다.

1. 인스턴스 생성과 this 바인딩

   - new 연산자와 함께 클래스를 호출하면 constructor의 내부 코드가 실행되기에 앞서 암묵적으로 빈 객체가 생성된다. 그리고 암묵적으로 생성된 빈 객체, 즉 인스턴스는 this에 바인딩된다.

2. 인스턴스 초기화

   - constructor의 내부 코드가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다. 즉, thisdp 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티 값을 초기화한다.

3. 인스턴스 반환
   - 클래스의 모드 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

## 프로퍼티

### 인스턴스 프로퍼티

인스턴스 프로피티는 constructor 내부에서 정의해야 한다.

```js
class Person {
  constructor(name) {
    this.name = name; // name 프로퍼티는 public
  }
}
const me = new Person("Lee");

console.log(me); // Person {name:'Lee'}
console.log(me.name); // Lee
```

constructor 내부에서 this에 추가한 프로퍼티는 언제나 클래스가 생성한 인스턴스의 프로퍼티가 된다. ES6에서는 다른 객체지향 언어처럼 private, public, protected 키워드와 같은 접근 제한자를 지원하지 않아 언제나 public이다.

### 접근자 프로퍼티

접근자 프로퍼티는 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수, getter와 setter 함수로 구성되어 있다.

- getter는 인스턴스 프로퍼티에 접근할 때마다 프로퍼티 값을 조작하거나 별도의 행위가 필요할 때 사용한다. 메서드 이름 앞에 get키워드를 사용해 정의한다.
- setter는 인스턴스 프로퍼티에 할당할 때마다 프로퍼티 값을 조작하거나 별도의 행위가 필요할 때 사용한다. 메서드 이름 앞에 set키워드를 사용해 정의한다.

```js
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(" ");
  }
}

const me = new Person("Ungmo", "Lee");
console.log(`${me.firstName} ${me.lastName}`); //Hyunwook Yoo

me.fullName = "Hyunwook Yoo"; // setter 사용

console.log(me);

console.log(me.fullName); // getter 사용
```

### 클래스 필드 정의 제안

자바스크립트의 클래스 몸체에는 메서드만 선언할 수 있다. 따라서 클래스 몸체에 자바와 유사하게 클래스 필드를 선언하면 문법에러가 발생한다.

```js
class Person {
  name = "Lee";
}
const me = new Person("Lee");
```

하지만 위 예제를 최신 브라우저 또는 최신 Node.js에서 실행하면 문법 에러가 발생하지 않고 정상 작동한다.

클래스 몸체에서 클래스 필드를 정의하는 경우 this에 클래스 필드를 바인딩해서는 안된다. this는 클래스의 constructor와 메서드 내에서만 유효하다.

```js
class Person {
  this.name = "Lee"; // 문법에러
}
```

클래스 필드를 참조하는 경우 자바와 같은 클래스 기반 객체지향 언어에서는 this를 생략할 수 있으나 자바스크립트에서는 this를 반드시 사용해야 한다.

```js
class Person {
  name = "Lee";
  constructor() {
    console.log(name); // 문법에러
  }
}
```

클래스 필드에 초기값을 할당하지 않으면 undefined를 갖는다.

```js
class Person {
  name;
}
const me = new Person();
console.log(me); // Person {name: undefined}
```

인스턴스를 생성할 때 외부의 초기값으로 클래스 필드를 초기화해야 할 필요가 있다면 constructor에 클래스 필드를 초기화해야 한다.

```js
class Person {
  name;
  constructor(name) {
    this.name = name;
  }
}
const me = new Person();
console.log(me); // Person {name: 'Lee'}
```

이처럼 인스턴스를 생성할 때 클래스 필드를 초기화할 필요가 있다면 constructor 밖에서 클래스 필드를 정의할 필요가 없다.

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}
const me = new Person();
console.log(me); // Person {name: 'Lee'}
```

함수는 일급객체이므로 함수를 클래스 필드에 할당할 수 있다. 따라서 클래스 필드를 통해 메서드를 정의할 수도 있다. 이처럼 클래스 필드에 함수를 할당하는 경우, 이 함수는 프토토 타입 메서드가 아닌 인스턴스 메서드가 된다. 따라서 클래스 필드에 함수를 할당하는 것은 권장하지 않는다.

### private 필드 정의 제안

자바스크립트에서는 private, public, protected 키워드와 같은 접근 제한자를 지원하지 않는다. 따라서 인스턴스 프로퍼티는 인스턴스를 통해 클래스 외부에서 언제나 참조할 수 있다. 즉 언제나 public이다.

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}

const me = new Person("Lee");
console.log(me.name);
```

클래스 필드 정의 제안을 사용하더라도 클래스 필드는 기본적으로 public하기 때문에 외부에 그대로 노출된다.

```js
class Person {
  name = "Lee";
}

const me = new Person("Lee");
console.log(me.name);
```

현재 private 필드를 정의할 수 있는 새로운 표준 사양이 제안되어 있다.
private 필드의 선두에는 #을 붙여준다. private 필드를 참조할 때도 #을 붙어주어야 한다.

```js
class Person {
  #name = "";

  constructor(name) {
    this.#name = name;
  }
}

const me = new Person("Lee");
console.log(me.#name); // 에러 : 참조할 수 없다.
```

public 필드는 어디서든 참조할 수 있지만 private 필드는 클래스 내부에서만 참조할 수 있다.
|접근 가능성|public|private|
|---|---|---|
|클래스 내부|O|O|
|자식 클래스 내부|O|X|
|클래스 인스턴스를 통한 접근|O|X|

이터럼 클래스 외부에서 private 필드에 직접 접근할 수 있는 방법은 없다. 다만 접근자 프로퍼티를 통해서 간접적으로 접근하는 방법은 유효하다.

```js
class Person {
  #name = "";

  constructor(name) {
    this.#name = name;
  }
  get name() {
    return this.#name;
  }
}

const me = new Person("Lee");
console.log(me.#name); // Lee
```

private 필드는 반드시 클래스 몸체에 정의해야 한다. constructor에서 정의하면 에러가 발생한다.

### static 필드 정의 제안

```js
class MyMath {
  //static public 필드 정의
  static PI = 22 / 7;

  static #num = 10;

  static increment() {
    return ++MyMath.#num;
  }
}

console.log(MyMath.PI); // 3.1428....
console.log(MyMath.increment()); // 11
```

## 상속에 의한 클래스 확장

### 클래스 상속과 생성자 함수 상속

프로토타입 기반 상속은 프로토타입 체인을 통해 다른 객체의 자산을 상속받는 개념이지만 **상속에의한 클래스 확장은 기존 클래스를 상속받아 새로운 클래스를 확장하여 정의하는 것**이다.

예를 들어, 동물을 추상화한 Animal 클래스와 새와 사자를 추상화한 Bird, Lion 클래스를 각각 정의한다고 생각해보자. 새와 사자는 동물에 속하므로 동물의 속성을 갖는다. 하지만 새와 사자는 자신만의 고유한 속성도 갖는다. 이때 Animal 클래스는 동물의 속성을 표현하고 Bird, Lion 클래스는 상속을 통해 Animal 클래스의 속성을 그대로 사용하면서 자신만의 고유한 속성만 추가하여 확장할 수 있다.

```js
class Animal {
  constructor(age, weight) {
    this.age = age;
    this.weight = weight;
  }

  eat() {
    return "eat";
  }

  move() {
    return "move";
  }
}

class Bird extends Animal {
  fly() {
    return "fly";
  }
}
const bird = new Bird();
console.log(bird);
console.log(bird instanceof Bird);
console.log(bird instanceof Animal);
console.log(bird.eat());
console.log(bird.move());
console.log(bird.fly());
```

클래스는 상속을 통해 다른 클래스르 확장할 수 있는 문법인 extends 키워드가 기본적으로 제공된다. extends 키워드를 사용한 클래스 확장은 간편하고 직관적이다.

### extends 키워드

상속을 통해 클래스를 확장하려면 extends 키워드를 사용하여 상속받을 클래스를 정의한다.

```js
class Base {}

class Derived extends Base {}
```

상속을 통해 확장된 클래스를 서브 클래스라 부르고, 서브클래스에게 상속된 클래스를 수퍼클래스라 부른다. 서브클래스를 파생 클래스 또는 자식 클래스, 수퍼클래스를 베이스 클래스 또는 부모 클래스라고 부른다.

수퍼클래스와 서브클래스는 인스턴스의 프로토타입 체인뿐 아니라 클래스 간의 프로토타입 체인도 생성한다. 이를 통해 프로토타입 메서드, 정적 메서드 모두 상속이 가능하다.

### 동적 상속

extends 키워드는 클래스뿐만 아니라 생성자 함수를 상속받아 클래스를 확장할 수도 있다. 단 extends 키워드 앞에는 반드시 클래스가 와야한다.

```js
function Base(a) {
  this.a = a;
}

class Derived extends Base {}
const derived = new Derived(1);

console.log(derived); // Derived {a: 1}
```

extends 키워드 다음에는 클래스뿐만 아니라 [[constructor]] 내부 메서드를 갖는 함수 객체로 평가될 수 있는 모든 표현식을 사용할 수 있다. 이를 통해 동적으로 상속받을 대상을 결정할 수 있다.

```js
function Base1() {}

class Base2 {}

let condition = true;

class Derived extends (condition ? Base1 : Base2) {}

const derived = new Derived();

console.log(derived);
console.log(derived instanceof Base1); // true
console.log(derived instanceof Base2); // false
```

### 서브클래스의 constructor

constructor는 생략되면 암묵적으로 정의가 된다.

서브클래스에서 constructor를 생략하면 클래스에 다음과 같은 constructor가 암묵적으로 정의된다. args는 new 연산자와 함께 클래스를 호출할 때 전달한 인수의 리스트다

```js
constructor(...args){super(...args);}
```

다음 예제를 보면 수퍼클래스와 서브클래스 모두 constructor를 생략했다.

```js
class Base {}

class Derived extends Base {}
```

그러면 암묵적으로 constructor가 정의된다

```js
class Base {
  constructor() {}
}

class Derived extends Base {
  constructor(...args) {
    super(...args);
  }
}

const derived = new Derived();
console.log(derived); // Derived {}
```

### super 키워드

super 키워드는 함수처럼 호출할 수도 있고 this와 같이 식별자처럼 참조할 수 있는 특수한 키워드다.

- super를 호출하면 수퍼클래스의 constructor를 호출한다
- super를 참조하면 수퍼클래스의 메서드를 호출할 수 있다.

#### super 호출

super를 호출하면 수퍼클래스의 constructor를 호출한다.

```js
class Base {
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
}
class Derived extends Base {
  // 암묵적으로 consturctor가 정의된다.
  // constructor(...args) {super(...args);}
}

const derived = new Derived(1, 2);
console.log(derived); // Derived { a: 1, b: 2 }
```

다음 예제와 같이 서브클래스에서 추가한 프로퍼티를 갖는 인스턴스를 생성한다면 constructor를 생략할 수 없다.

```js
class Base {
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
}
class Derived extends Base {
  constructor(a, b, c) {
    super(a, b);
    this.c = c;
  }
}

const derived = new Derived(1, 2, 3);
console.log(derived); // Derived { a: 1, b: 2 }
```

super를 사용할 때 주의할 사항은 다음과 같다.

1. 서브클래스에서 constructor를 생략하지 않은 경우 서브클래스의 constructor에서는 반드시 super를 호출해야 한다.
2. 서브클래스의 constructor에서 super를 호출하기전에 this를 참조할 수 없다.
3. super는 반드시 서브클래스의 constructor에서만 호출한다. 서브클래스가 아닌 클래스의 constructor나 함수에서 super를 호출하면 에러가 발생한다.

#### super 참조

메서드내에서 super를 참조하면 수퍼클래스의 메서드를 호출할 수 있다.

서브클래스의 프로토타입 메서드 내에서 super.sayHi는 수퍼클래스의 프로토타입 메서드 sayHi를 가리킨다.

```js
class Base {
  constructor(name) {
    this.name = name;
  }

  sayHi() {
    return `Hi! ${this.name}`;
  }
}
class Derived extends Base {
  sayHi() {
    return `${super.sayHi()}, how are you doing?`;
  }
}

const derived = new Derived("Lee");
console.log(derived.sayHi());
```

서브클래스의 정적 메서드 내에서 super.sayHi는 수퍼클래스의 정적 메서드 sayHi를 가리킨다.

```js
class Base {
  static sayHi() {
    return `Hi!`;
  }
}
class Derived extends Base {
  static sayHi() {
    return `${super.sayHi()}, how are you doing?`;
  }
}

console.log(Derived.sayHi());
```

### 상속 클래스의 인스턴스 생성 과정

상속 관계에 있는 두 클래스가 어떻게 협력하며 인스턴스를 생성하는지 살펴보자.

```js
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }

  toString() {
    return `width = ${this.width}, height = ${this.height}`;
  }
}

class ColorRectangle extends Rectangle {
  constructor(width, height, color) {
    super(width, height);
    this.color = color;
  }

  toString() {
    return super.toString() + `, color = ${this.color}`;
  }
}

const colorRectangle = new ColorRectangle(2, 4, "red");
console.log(colorRectangle);

console.log(colorRectangle.getArea());
console.log(colorRectangle.toString());
```

1. 서브 클래스의 super 호출
   - 서브클래스는 자신이 직접 인스턴스를 생성하지 않고 수퍼클래스에게 인스턴스 생성을 위임한다. 이것이 바로 서브클래스의 constructor에서 반드시 super를 호출해야하는 이유다. 서브클래스가 new 연산자와 함께 호출되면 constructor 내부의 super 키워드가 함수처럼 호출된다. 그러면 수퍼클래스의 constructor가 호출된다.
2. 수퍼클래스의 인스턴스 생성과 this 바인딩
   - 수퍼클래스의 constructor 내부의 코드가 실행되기 이전에 암묵적으로 빈 객체를 생성한다. 이 빈 객체가 바로 클래스가 생성한 인스턴스다. 빈 객체는 this에 바인딩된다. 따라서 수퍼클래스의 constructor 내부의 this는 생성된 인스턴스를 가리킨다.
3. 수퍼클래스의 인스턴스 초기화
   - 수퍼클래스의 constructor가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다.
4. 서브클래스 constructor로의 복귀와 this 바인딩
   - super의 호출이 종료되고 제어 흐름이 서브클래스 constructor로 돌아온다. 이때 super가 반환한 인스턴스가 this에 바인딩된다. 서브클래스는 별도의 인스턴스를 생성하지 않고 super가 반환한 인스턴스를 this에 바인딩하여 그대로 사용한다.
5. 서브클래스의 인스턴스 확장
   - super 호출 이후, 서브클래스의 constructor에 기술되어 있는 인스턴스 초기화가 실행된다.
6. 인스턴스 반환
   - 클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

### 표준 빌트인 생성자 함수 확장

String, Number, Array 같은 표준 빌트인 객체도 [[constructor]] 내부 메서드를 갖는 생성자 함수 이므로 extends 키워드를 사용하여 확장할 수 있다.

```js
class MyArray extends Array {
  uniq() {
    return this.filter((v, i, self) => self.indexOf(v) === i);
  }

  average() {
    return this.reduce((pre, cur) => pre + cur, 0) / this.length;
  }
}
const myArray = new MyArray(1, 1, 2, 3);
console.log(myArray); // MyArray(4) [1, 1, 2, 3]

console.log(myArray.uniq()); // MyArray(3) [1, 2, 3]
console.log(myArray.average()); // 1.75
```
