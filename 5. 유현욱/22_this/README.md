# 모던 자바스크립트 Deep Dive

## 22장 this

## this 키워드

동작을 나타내는 메서드는 자신이 속한 객체의 상태, 즉 프로퍼티를 참조하고 변경할 수 있어야 한다. 이때 메서드가 자신이 속한 객체의 프로퍼티를 참조하려면 먼저 **자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다.**

객체 리터럴 방식으로 생성한 객체의 경우 메서드 내부에서 메서드 자신이 속한 객체를 가리키는 식별자를 재귀적으로 참조할 수 있다.

```js
const circle = {
  radius: 5,
  getDiameter() {
    return 2 * circle.radius;
  },
};
console.log(circle.getDiameter());
```

getDiameter 메서드가 호출되는 시점에는 이미 객체 리터럴이 평가가 완료되어서 circle 식별자를 참조할 수 있다.

```js
function Circle(radius) {
  ???.radius=radius;
}
Circle.prototype.getDiameter=function(){
  return 2*???.radius;
};
const circle = new Circle(5);
```

생성자 함수 내부에서는 프로퍼티 또는 메서드를 추가하기 위해 자신이 생성할 인스턴스를 참조할 수 있어야 한다. 하지만 생성자 함수에 의한 객체 생성 방식은 먼저 생성자 함수를 정의한 이후 new연산자와 함께 생성자 함수를 호출하는 단계가 추가적으로 필요하다.

정의하는 시점에는 아직 인스턴스를 생성하기 이전이므로 생성할 인스턴스를 가리키는 식별자를 알수가 없다. 따라서 자바스크립트는 this라는 특수한 식별자를 제공한다.

this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.

위에서 살펴본 객체 리터럴과 생성자 함수의 예제를 this를 사용하면

```js
const circle = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  },
};
console.log(circle.getDiameter());
/* ------------------------------------------*/
function Circle(radius) {
  this.radius = radius;
}
Circle.prototype.getDiameter = function () {
  return 2 * this.radius;
};
const circle = new Circle(5);
console.log(circle.getDiameter());
```

## 함수 호출 방식과 this 바인딩

this 바인딩은 함수 호출 방식, 즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다.

### 일반 함수 호출

```js
var value = 1;

const obj = {
  value: 100,
  foo() {
    console.log("foo's this: ", this); //{value: 100, foo: f}
    console.log("foo's this.value: ", this.value); // 100
    function bar() {
      console.log("bar's this: ", this); // window
      console.log("bar's this.value: ", this.value); // 1
    }

    // 메서드 내에서 정의한 중첩함수도 일반 함수로 호출되면 중첩 함수 내부의 this에는 전역 객체가 바인딩된다.
    bar();
  },
};
obj.foo();
```

모든 함수(중첩함수, 콜백 함수 포함)가 일반 함수로 호출된다면 콜백 함수 내부의 this에도 전역 객체가 바인딩된다. 어떠한 함수라도 일반 함수로 호출되면 this에 전역객체가 바인딩된다.

### 메서드 호출

메서드 내부의 this에는 메서드를 호출한 객체, 즉 메서드를 호출할 때 메서드 이름 앞의 마침표(.) 연산자 앞에 기술한 객체가 바인딩된다. 주의할 것은 메서드 내부의 this는 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩 된다는 것이다.

```js
const person = {
  name: "Lee",
  getName() {
    return this.name;
  },
};
console.log(person.getName()); // Lee

const anotherPerson = {
  name: "Kim",
};

anotherPerson.getName = person.getName;
console.log(anotherPerson.getName()); // Kim

const getName = person.getName;

console.log(getName());
```

따라서 메서드 내부의 this는 프로퍼티로 메서드를 가리키고 있는 객체와는 관계가 없고 메서드를 호출한 객체에 바인딩 된다.

### 생성자 함수 호출

### Function.prototype.apply/call/bind 메서드에 의한 간접 호출
