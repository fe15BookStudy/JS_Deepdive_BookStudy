# 22장 this

### this 키워드

### 함수 호출 방식과 this 바인딩

*** this 바인딩( this에 바인딩될 값 ) 은 함수 호출 방식, 즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다. ***

함수를 호출하는 방식은 다음과 같이 다양하다.

1. 일반 함수 호출

2. 메서드 호출

3. 생성자 함수 호출

4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출

----------

#### 일반 함수 호출

*** 기본적으로 this에는 전역 객체가 바인딩된다. ***

```JavaScript
function foo(){
  console.log("foo's this: ", this); // window
  function bar() {
    console.log("bar's this: ", this); // window
  }
  bar();
}
foo();
```

전역 함수는 물론이고 중첩 함수를 일반 함수로 호출하면 함수 내부의 this에는 전역 객체가 바인딩 된다. strict mode 가 적용된 일반 함수 내부의 this 에는 undefined가 바인딩 된다.

```JavaScript
function foo(){
  'use strict';

  console.log("foo's this: ", this); // undefined
  function bar () {
    console.log("bar's this: ", this); // undefined
  }
  bar();
}
foo( );
```

메서드 내에서 정의한 중첩 함수도 일반 함수로 호출되면 중첩 함수 내부의 this 에는 전역 객체가 바인딩된다.

```JavaScript
// var 키워드로 선언한 전역 변수 value는 전역 객체의 프로퍼티다.
var value = 1;
// const 키워드로 선언한 전역 변수 value는 전역 객체의 프로퍼티가 아니다.
// const value = 1;

const obj = {
  value: 100,
  foo() {
    console.log("foo's this: ", this); // {value: 100, foo: f}
    console.log("foo's this.value: ", this.value); // 100

    // 메서드 내에서 정의한 중첩 함수
    function bar(){
      console.log("bar's this: ", this); // window
      console.log("bar's this.value: ", this.value); // 1
    }

    // 메서드 내에서 정의한 중첩 함수도 일반 함수로 호출되면 중첩 함수 내부의 this에는
    // 전역 객체가 바인딩된다.
    bar();  // 중첩함수 일반 함수로 호출

  };
}

obj.foo();
```

콜백 함수가 일반 함수로 호출된다면 콜백 함수 내부의 this 에도 전역 개체가 바인딩된다. **어떠한 함수라도 일반 함수로 호출되면 this에 전역 객체가 바인딩된다.**

```JavaScript
var value = 1;

const obj = {
  value: 100,
  foo() {
    conosle.log("foo's this: ", this); // {value: 100, foo : f}
    // 콜백 함수 내부의 this에는 전역 객체가 바인딩된다.
    setTimeout(function () {
      console.log("callback's this: ", this); // window
      console.log("callback's this.value: ", this.value); // 1
    },100);
  }
};

obj.foo();
```

*** 이처럼 일반 함수로 호출된 모든 함수( 중첩 함수, 콜백 함수 포함 ) 내부의 this에는 전역 객체가 바인딩된다. ***

하지만 메서드 내에서 정의한 중첩 함수 또는 메서드에게 전달한 콜백 함수가 일반 함수로 호출될 때 메서드 내의 중첩 함수 또는 콜백 함수의 this가 전역 객체를 바인딩하는 것은 문제가 있다. 중첩 함수 또는 콜백 함수는 외부 함수를 돕는 헬퍼 함수의 역할을 하므로 외부 함수의 일부 로직을 대신하는 경우가 대부분이다. 하지만 외부 함수인 메서드와 중첩 함수 또는 콜백 함수의 this가 일치하지 않는다는 것은 중첩 함수 또는 콜백 함수를 헬퍼 함수로 동작하기 어렵게 만든다. 

메서드 내부의 중첩 함수나 콜백 함수의 this 바인딩을 메서드의 this 바인딩과 일치시키기 위한 방법은 다음과 같다.

```JavaScript
var value = 1;
const obj = {
  value: 100,
  foo() {
    // this 바인딩 (obj)을 변수 that에 할당한다.
    const that = this ;

    // 콜백 함수 내부에서 this 대신 that을 참조한다.
    setTimeout(function () {
      console.log(that.value); //100
    },100);
  }
};

obj.foo();
```

위 방법 이외에도 자바스크립트는 this를 명시적으로 바인딩할 수 있는 Function.prototype.apply, Function.prototype.call, Function.prototype.bind 메서드를 제공한다.

```JavaScript
var value = 1;

const obj = {
  value: 100,
  foo() {
    // 콜백 함수에 명시적으로 this를 바인딩한다.
    setTimeout(function () {
      console.log(this.value); // 100
    }.bind(this), 100);
  }
};

obj.foo();
```
관련해서 더 자세한 메서드는 22.2.4절에서 살펴본다.


또는 화살표 함수를 사용해서 this 바인딩을 일치시킬 수도 있다.

```JavaScript
var value = 1

const obj = {
  value: 100,
  foo(){
    // 화살표 함수 내부의 this는 상위 스코프의 this를 가리킨다.
    setTimeout(() => console.log(this.value), 100); //100
   }
  };

obj.foo();
```

화살표 함수에 대해서도 26.3절에서 자세히 살펴본다.

-------- 

#### 메서드 호출

메서드 내부의 this에는 메서드를 호출한 객체, 즉 메서드를 호출할 때 메서드 이름앞의 마침표(.) 연산자 앞에 기술한 객체가 바인딩된다. 주의할 것은 메서드 내부의 this는 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다는 것이다. 

```JavaScript 
const person = {
  name: 'Lee',
  getName(){
    // 메서드 내부의 this는 메서드를 호출한 객체에 바인딩된다.
    return this.name;
  }
};

// 메서드 getName을 호출한 객체는 person이다.
console.log(person.getName()); // Lee
```

위 예제의 getName 메서드는 person 객체의 메서드로 정의되었다. 메서드는 프로퍼티에 바인딩된 함수다. 즉, person 객체의 getName 프로퍼티가 가리키는 함수 객체는 person 객체에 포함된 것이 아니라 독립적으로 존재하는 별도의 객체다. getName 프로퍼티가 함수 객체를 가리키고 있을 뿐이다.

따라서 getName 프로퍼티가 가리키는 함수 객체, 즉 getName 메서드는 다른 객체의 프로퍼티에 할당하는 것으로 다른 객체의 메서드가 될 수도 있고, 일반 변수에 할당하여 일반 함수로 호출될 수도 있다.

```JavaScript 
const anotherPerson = {
  name: 'Kim'
};
// getName 메서드를 anotherPerson 객체의 메서드로 할당
anotherPerson.getName = person.getName;

// getName 메서드를 호출한 객체는 anotherPerson이다.
console.log(anotherPerson.getName()); // Kim

// getName 메서드를 변수에 할당
const getName = person.getName;

// getName 메서드를 일반 함수로 호출
console.log(getName()); // ''
// 일반 함수로 호출된 getName 함수 내부의 this.name은 브라우저 환경에서 window.name과 같다.
// 브라우저 환경에서 window.name은 브라우저 창의 이름을 나타내는 빌트인 프로퍼티이며 기본값은 ''이다.
// Node.js 환경에서 this.name은 undefined다.
```

따라서 메서드 내부의 this는 프로퍼티로 메서드를 가리키고 있는 객체와는 관계가 없고 메서드를 호출한 객체에 바인딩된다.

프로토타입 메서드 내부에서 사용된 this도 일반 메서드와 마찬가지로 해당 메서드를 호출한 객체에 바인딩 된다.

```JavaScript
function Person(name) {
  this.name = name ;
}

Person.prototype.getName = function () {
  return this.name;
};

const me = new Person('Lee');

// getName 메서드를 호출한 객체는 me 다.
console.log(me.getName()); // 1.Lee

Person.prototype.name = 'Kim';

// getName 메서드를 호출한 객체는 Person.prototype이다.
console.log(Person.prototype.getName()); // 2. Kim
```

 `1.Lee` 의 경우 getName 메서드를 호출한 객체는 me다. 따라서 getName 메서드 내부의 this는 me를 가리키며 this.name은 'Lee'다.

 `2.Kim` 의 경우 getName 메서드를 호출한 객체는 Person.prototype 이다. Person.prototype도 객체이므로 직접 메서드를 호출할 수 있다. 따라서 getName 메서드 내부의 this는 Persone.prototype을 가리키며 this.name은 'Kim'이다.

--------

 #### 생성자 함수 호출