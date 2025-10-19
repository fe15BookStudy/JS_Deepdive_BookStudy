# 22. this

## this 키워드

**자신이 속한 객체를 가리키는 식별자를 참소하는 것**

this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수이다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.

this는 자바스크립트 엔진에 의해 암묵적으로 생성되며, 코드 어디서든 참조할 수 있다.

this를 지역변수처럼 사용할 수 있지만 this가 가리키는 값, 즉 this 방인딩은 함수 호출 방식에 의해 동적으로 결정된다.

- 바인딩이란 식별자와 값을 연결하는 과정. this바인딩은 this와 this가 가리킬 객체를 바인딩하는 것.

```js
const circle = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  },
};
console.log(circle.getDiameter());
```

⬇️

```js
function Circle(radius) {
  this.radius = radius;
}
Circle.prototype.getDiameter = function () {
  return 2 * this.radius;
};
const circle = new Circle(5);
console.log(circle.getDiameter());
```

this는 메서드를 호출한 객체, circle을 가리킨다.

## 함수 호출 방식과 this 바인딩

this 바인딩은 함수 호출 방식, 즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다.

1. 일반 함수 호출

2. 메서드 호출

3. 생성자 함수 호출

4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출

### 1. 일반 함수 호출

기본적으로 this에는 전역 객체가 바인딩된다.

```js
function foo() {
  console.log("foo's this: ", this); // window
  function bar() {
    console.log("bar's this: ", this); // window
  }
  bar();
}
foo();
```

일반 함수로 호출하면 함수 내부의 this에는 전역 객체가 바인딩 된다.
(전역함수는 물론, 중첩함수나 콜백함수도 일반함수로 호출하면 this에는 전역 객체가 바인딩 된다.)

### 2. 메서드 호출

메서드 내부의 this에는 메서드를 호출한 객체, 즉 메서드를 호출할 때 메서드 이름 앞의 마침표(.) 연산자 앞에 기술한 객체가 바인딩된다. 주의할 것은 메서드 내부의 this는 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩 된다는 것이다.

```js
const person = {
  name: "Lee",
  getName() {
    return this.name;
  },
};
console.log(person.getName()); // Lee
```

getName 메서드는 person객체의 메서드로 정의되어있다.
getName 프로퍼티가 가리키는 함수 객체는 person 객체에 포함된 것이 아니라 독립적으로 존재하는 별도의 객체이다.

```js
const anotherPerson = {
  name: "Kim",
};

anotherPerson.getName = person.getName;
console.log(anotherPerson.getName()); // Kim

const getName = person.getName;

console.log(getName());
```

메서드 내부의 this는 프로퍼티로 메서드를 가리키고 있는 객체와는 관계가 없고 메서드를 호출한 객체에 바인딩 된다.

```js
function Person(name) {
  this.name = name;
}

Person.prototype.getName = function () {
  return this.name;
};

const me = new Person("Lee");

// getName 메서드를 호출한 객체는 me 다.
console.log(me.getName()); // 1.Lee

Person.prototype.name = "Kim";

// getName 메서드를 호출한 객체는 Person.prototype이다.
console.log(Person.prototype.getName()); // 2. Kim
```

1.Lee 의 경우 getName 메서드를 호출한 객체는 me다. 따라서 getName 메서드 내부의 this는 me를 가리키며 this.name은 'Lee'다.

2.Kim 의 경우 getName 메서드를 호출한 객체는 Person.prototype 이다. Person.prototype도 객체이므로 직접 메서드를 호출할 수 있다. 따라서 getName 메서드 내부의 this는 Person.prototype을 가리키며 this.name은 'Kim'이다.

### 3. 생성자 함수 호출

생성자함수 내부의 this에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩된다.

```js
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20
```

### 4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출

apply, call, bind 메서드는 Function.prototypoe의 메서드이다.  
이 메서드는 모든 함수가 상속받아 사용할 수 있다.

```js
function getThisBinding() {
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

console.log(getThisBinding()); // window
console.log(getThisBinding.apply(thisArg)); // {a: 1}
console.log(getThisBinding.call(thisArg)); // {a: 1}
```

apply와 call 메서드의 기능은 함수를 호출하는 것이다. 함수를 호출하면서 첫번째 인수로 전달한 특정 객체를 호출한 함수의 this에 바인딩한다.

```js
function getThisBinding() {
  return this;
}

const thisArg = { a: 1 };

console.log(getThisBinding.bind(thisArg)); // getThisBinding
console.log(getThisBinding.bind(thisArg)()); // {a: 1}
```

bind 메서드는 apply와 call 메서드와 달리 함수를 호출하지 않는다. 다만 첫 번째 인수로 전달한 값으로 this 바인딩이 교체된 함수를 새롭게 생성해 반환한다.

bind 메서드는 메서드의 this와 메서드 내부의 중첩함수 또는 콜백함수의 this가 불일치하는 문제를 해결하기 위해 사용된다.
