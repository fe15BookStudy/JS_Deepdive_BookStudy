### 22.1 this 키워드
- this는 자신이 속한 객체(또는 그 객체를 생성한 주체)를 참조하는 특수한 식별자.
- 하지만 어떤 객체를 참조하는지는 "함수 호출 방식"에 따라 동적으로 결정됨.
- 함수가 어디서 선언되었는지가 아니라 어떻게 호출되었는지가 핵심.
예제22-01)
```javascript
const circle = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  }
};
console.log(circle.getDiameter()); // 10
```
- getDiameter는 circle 객체의 메서드로 호출되었으므로,
  - this는 circle을 가리킴.
- 메서드는 자신을 “호출한 객체”를 가리키는 것이지, “정의된 객체”를 가리키는 게 아님. 

예제 22-02)
```javascript
function Circle(radius) {
  this.radius = radius;
}

Circle.prototype.getDiameter = function () {
  return 2 * this.radius;
};

const circle = new Circle(5);
console.log(circle.getDiameter()); // 10
```
- 생성자 함수에서의 this는 미래에 생성될 인스턴스 객체
- new로 호출하면 새로운 객체가 생성되고 this에 바인딩됨.

### 22.2 함수 호출 방식과 this 바인딩
> this의 바인딩(연결)은 “호출 방식”에 따라 결정된다.
📘 4가지 호출 방식
1. 일반 함수 호출
2. 메서드 호출
3. 생성자 호출 (new)
4. 간접 호출 (call/apply/bind)

1) 일반 함수 호출
예제 22-05)
```javascript
function square(number) {
  console.log(this);  // window
  return number * number;
}
square(2);
```
- 일반 함수 호출에서는 전역 객체(window 또는 global) 가 this로 바인딩.
- **엄격 모드(strict mode)**에서는 undefined가 됨.

예제 22-06)
```javascript
const foo = function () {
  console.dir(this);
};

foo();        // 일반 함수 호출 → window
const obj = { foo };
obj.foo();    // 메서드 호출 → obj
new foo();    // 생성자 호출 → 새 인스턴스
```
>하나의 함수라도 호출 방식에 따라 this가 다름.

예제 22-07)
```javascript
function foo() {
  console.log('foo\'s this:', this); // window
  function bar() {
    console.log('bar\'s this:', this); // window
  }
  bar();
}
foo();
```
- 중첩 함수(bar) 도 일반 함수로 호출되면 this는 전역 객체.
- 즉, 바깥 함수의 this를 내부 함수가 자동 상속하지 않는다.

예제 22-08 (strict mode)
```javascript
function foo() {
  'use strict';
  console.log(this); // undefined
  function bar() {
    console.log(this); // undefined
  }
  bar();
}
foo();
```
- 엄격 모드에서는 일반 함수의 this가 undefined.

예제 22-09)
```javascript
var value = 1;

const obj = {
  value: 100,
  foo() {
    console.log(this);         // obj
    console.log(this.value);   // 100

    function bar() {
      console.log(this);       // window
      console.log(this.value); // 1
    }
    bar();
  },
};
obj.foo();
```
- 메서드 내부에서 중첩함수(bar) 를 일반함수로 호출하면,
중첩함수 내부의 this는 전역 객체로 바인딩됨.
- (콜백/타이머 내부에서도 같은 이유)

예제 22-10)
```javascript
var value = 1;

const obj = {
  value: 100,
  foo() {
    console.log(this.value); // 100

    setTimeout(function() {
      console.log(this.value); // 1 (전역)
    }, 100);
  },
};
obj.foo();
```
- setTimeout 콜백 함수도 일반함수처럼 호출되므로 this는 전역 객체.

2) 메서드 호출
예제 22-11 (전통적 방법)
```javascript
const obj = {
  value: 100,
  foo() {
    const that = this;
    setTimeout(function() {
      console.log(that.value); // 100
    }, 100);
  },
};
obj.foo();
```
- setTimeout 안의 함수는 일반함수 호출 → 전역 this
- 따라서 미리 that = this로 저장해 참조를 우회하는 방식.

예제 22-12 (bind 메서드)
```javascript
const obj = {
  value: 100,
  foo() {
    setTimeout(function() {
      console.log(this.value); // 100
    }.bind(this), 100);
  },
};
obj.foo();
```
- bind(this)로 새로운 함수 생성 → 내부 this를 obj로 고정.
- bind는 즉시 호출하지 않고, 새로운 this가 고정된 함수를 반환.

예제 22-13 (화살표 함수)
```javascript
const obj = {
  value: 100,
  foo() {
    setTimeout(() => console.log(this.value), 100);
  },
};
obj.foo();
```
- 화살표 함수는 자체적인 this를 가지지 않고,
상위 스코프의 this(obj) 를 그대로 상속받는다.
- 콜백에서 this를 잃지 않게 하는 가장 깔끔한 방법.

3) 생성자 함수 호출
예제 22-17)
```javascript
function Circle(radius) {
  this.radius = radius;
}
const circle = new Circle(15);
console.log(circle.radius); // 15
```
- new를 사용하면 빈 객체가 생성되어 this로 바인딩되고,
생성자 함수 내부 코드가 실행되며 프로퍼티가 그 객체에 추가됨.
- return이 없으면 자동으로 this(즉, 새 객체)가 반환.
예제 22-18)
```javascript
const circle2 = Circle(15); // new 없이 호출
console.log(radius); // 15 (전역 변수로 생김)
```
- new 없이 호출하면 일반 함수 호출이므로 this는 전역 객체!

4) 간접 호출(apply, call, bind)
✅ 공통 개념

모든 함수는 Function.prototype을 상속받으므로
apply, call, bind 메서드를 사용할 수 있다.
| 메서드                       | 설명                | 즉시 실행 여부  | 인수 전달 방식 |
| ------------------------- | ----------------- | --------- | -------- |
| `call(thisArg, a, b, c)`  | this를 지정하고 호출     | ✅ 즉시      | 개별 나열    |
| `apply(thisArg, [a,b,c])` | this를 지정하고 호출     | ✅ 즉시      | 배열로 전달   |
| `bind(thisArg)`           | this를 고정한 새 함수 반환 | ❌ (나중 실행) | —        |

예제 22-20)
```javascript
function getThisBinding() { return this; }
const thisArg = { a: 1 };

console.log(getThisBinding.apply(thisArg)); // {a:1}
console.log(getThisBinding.call(thisArg));  // {a:1}
```
- 두 메서드는 거의 동일하지만 인수 전달 방식만 다름.

예제 22-21)
```javascript
function convertArgsToArray() {
  const arr = Array.prototype.slice.call(arguments);
  return arr;
}
console.log(convertArgsToArray(1, 2, 3)); // [1,2,3]
```
- arguments는 배열이 아니므로,
Array.prototype.slice를 빌려와(call) 변환하는 패턴.

예제 22-22)
```javascript
function getThisBinding() {
  return this;
}
const thisArg = { a: 1 };
console.log(getThisBinding.bind(thisArg)()); // {a:1}
```
- bind는 함수를 호출하지 않고,
this가 고정된 새로운 함수를 반환한다.

5) 콜백 내부 this 바인딩 문제(22-23, 22-24)
❌ 잘못된 예
```javascript
const person = {
  name: 'Lee',
  foo(callback) {
    setTimeout(callback, 100);
  },
};
person.foo(function() {
  console.log(`Hi! my name is ${this.name}.`);
});
// Hi! my name is (window.name or undefined)
```
-콜백은 일반함수로 실행 -> this는 전역 객체

✅ 올바른 해결
```javascript
const person = {
  name: 'Lee',
  foo(callback) {
    setTimeout(callback.bind(this), 100);
  },
};
person.foo(function() {
  console.log(`Hi! my name is ${this.name}.`);
});
// Hi! my name is Lee.
```
- bind(this)로 콜백의 this를 person으로 고정
- 또는 콜백을 화살표 함수로 만들어도 같은 결과.

## 1. this의 결정 기준
자바스크립트에서 this는 함수가 호출되는 방식에 따라 바인딩되는 객체가 달라집니다.
즉, 선언 시점이 아니라 호출 시점에 따라 동적으로 결정됩니다.
| 호출 방식                      | this 바인딩 대상                             |
| -------------------------- | --------------------------------------- |
| 일반 함수 호출                   | 전역 객체 (`window` / `global`)             |
| 메서드 호출                     | 메서드를 호출한 객체                             |
| 생성자 함수 호출                  | 새로 생성된 인스턴스                             |
| `apply`, `call`, `bind` 호출 | 첫 번째 인자로 전달한 객체                         |
| 화살표 함수                     | 자신을 감싸는 상위 스코프의 `this`를 상속받음 (렉시컬 this) |
## 2. 일반 함수 호출의 this
```javascript
function foo() {
  console.log(this);
}
foo(); // window (브라우저), global (Node)
```
- 일반 함수 호출시 this는 전역 객체를 가리킵니다.
- strict mode('use strict')에서는 undefined가 됩니다.
- **중첩 함수나 콜백 함수 내부**에서도 기본적으로 전역 객체가 바인딩됩니다.
📍 따라서, 중첩함수 내부에서 외부 함수의 this를 유지하려면 다음과 같은 방법이 필요합니다.

## 3. 중첩함수(콜백)에서 this를 잃는 문제
(1)that = this패턴
```javascript
const obj = {
  value: 100,
  foo() {
    const that = this;
    setTimeout(function() {
      console.log(that.value); // 100
    }, 100);
  },
};
obj.foo();
```
this를 변수(that)에 담아서 콜백 내부에서 참조하는 전통적인 방법입니다.

(2) bind 메서드
```javascript
const obj = {
  value: 100,
  foo() {
    setTimeout(function() {
      console.log(this.value); // 100
    }.bind(this), 100);
  },
};
obj.foo();
```
- Function.prototype.bind(thisArg)는 **새로운 함수를 반환**하며,
그 내부의 `this`가 **강제로 지정된 객체**(`thisArg`)로 고정됩니다.
- 한 번 바인딩하면 바뀌지 않습니다.

(3) 화살표 함수
```javascript
const obj = {
  value: 100,
  foo() {
    setTimeout(() => console.log(this.value), 100); // 100
  },
};
obj.foo();
```
- 화살표 함수는 **자신의 this를 갖지 않습니다.**
- 대신 **상위 스코프가 this를 그대로 상속(lexical this)**합니다.
- 즉, `obj.foo` 안의 this가 setTimeout 내부에도 그대로 전달됩니다.

## 4. 메서드 호출의 this
```javascript
const person = {
  name: 'Lee',
  getName() {
    return this.name;
  },
};
console.log(person.getName()); // 'Lee'
```
- **메서드 내부의 this는 메서드를 호출한 객체를 가리킵니다.**
- 메서드가 객체의 프로퍼티로 바인딩되어 호출될 때만 유효합니다.
```javascript
const another = { name: 'Kim' };
another.getName = person.getName;
console.log(another.getName()); // 'Kim'
```
>같은 함수라도 **호출한 객체가 다르면** `this`가 달라집니다.

## 5. 생성자 함수 호출의 this
```javascript
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function() {
    return 2 * this.radius;
  };
}

const c1 = new Circle(5);
console.log(c1.getDiameter()); // 10
```
- new 연산자로 호출하면 새로운 인스턴스 객체가 생성되고,
- this는 그 새로운 객체를 가리킵니다.
- 만약 new 없이 호출하면 일반 함수 호출이 되어 this는 전역 객체가 됩니다.
```javascript
const c2 = Circle(10); // new 없음
console.log(window.radius); // 10
```
## 6. apply / call / bind에 의한 간접 호출
모든 함수는 Function.prototype을 상속받기 때문에
apply, call, bind를 사용할 수 있습니다.
| 메서드                              | 역할                      | 인수 전달 방식 |
| -------------------------------- | ----------------------- | -------- |
| `call(thisArg, arg1, arg2, ...)` | `thisArg`를 지정해 즉시 호출    | 개별 나열    |
| `apply(thisArg, [argsArray])`    | `thisArg`를 지정해 즉시 호출    | 배열 형태    |
| `bind(thisArg)`                  | `thisArg`를 지정한 새 함수를 반환 | 인수 전달 X  |
```javascript
function getThisBinding() {
  return this;
}

const obj = { a: 1 };

console.log(getThisBinding()); // window
console.log(getThisBinding.call(obj)); // { a: 1 }
console.log(getThisBinding.apply(obj)); // { a: 1 }

const bound = getThisBinding.bind(obj);
console.log(bound()); // { a: 1 }
```
>즉, apply와 call은 “즉시 실행”,
bind는 “this가 고정된 새 함수 반환”입니다.

## 7. 콜백에서 this 문제 해결 요약
아래 예제처럼 콜백 함수 내부에서 this가 달라질 때는 bind를 이용해 해결합니다.
```javascript
const person = {
  name: 'Lee',
  foo(callback) {
    setTimeout(callback.bind(this), 100);
  },
};

person.foo(function() {
  console.log(`Hi! my name is ${this.name}.`);
}); // Hi! my name is Lee.
```
| 구분           | 호출 예시                                | this         |
| ------------ | ------------------------------------ | ------------ |
| **일반 함수 호출** | `foo()`                              | 전역 객체        |
| **메서드 호출**   | `obj.method()`                       | `obj`        |
| **생성자 호출**   | `new Func()`                         | 새로 생성된 인스턴스  |
| **간접 호출**    | `func.call(obj)` / `func.apply(obj)` | `obj`        |
| **bind 호출**  | `func.bind(obj)()`                   | `obj` (고정됨)  |
| **화살표 함수**   | `() => this`                         | 상위 스코프의 this |

##  8. this 바인딩의 추가 개념 및 원리
### $\mathrm{var}$로 선언된 전역 변수와 const/let으로 선언된 전역 변수의 차이
일반 함수 호출 시 this는 전역 객체에 바인딩되는데, 이때 전역 객체의 프로퍼티를 참조할 때 var와 const/let의 차이가 드러납니다.
- var로 선언된 전역 변수: 전역 객체(브라우저의 window, Node.js의 global)의 프로퍼티로 추가됩니다.
  - 예시: var value = 1; → window.value가 1이 됩니다. 따라서 일반 함수에서 this.value는 1이 됩니다.
- const나 let으로 선언된 전역 변수: 전역 객체의 프로퍼티가 아닙니다.
  - 예시: const value = 1; → window.value는 undefined 또는 기존 전역 객체에 있던 값이 유지됩니다. 따라서 일반 함수에서 this.value는 1이 아닌 다른 값이 됩니다 

### this 바인딩과 렉시컬 스코프의 결정 시점
this 바인딩과 렉시컬 스코프(lexical scope)는 결정되는 시점이 다릅니다.
- 렉시컬 스코프: 함수가 정의되는 시점에 결정되며, 상위 스코프가 무엇인지 정해집니다.
- this 바인딩: 함수가 호출되는 시점에 결정되며, 호출 방식에 따라 동적으로 바뀝니다.

## 9. Function.prototype 메서드의 심층 활용
### $\mathrm{apply}$와 $\mathrm{call}$의 인수 전달 방식
apply와 call은 this 바인딩의 대상 객체(thisArg)를 첫 번째 인수로 받는 것은 동일하지만, 함수에 전달할 나머지 인수를 다루는 방식에서 차이가 납니다.
- apply(thisArg, argsArray): 인수를 배열 또는 유사 배열 객체로 묶어서 전달합니다.
- call(thisArg, arg1, arg2, [...]): 인수를 쉼표로 구분된 리스트 형식으로 전달합니다.

### $\mathrm{apply}$와 $\mathrm{call}$을 이용한 유사 배열 객체에 배열 메서드 사용
arguments 객체와 같이 유사 배열 객체는 배열이 아니므로 Array.prototype.slice와 같은 배열 메서드를 직접 사용할 수 없습니다. 이때 apply나 call을 사용하여 이 문제를 해결합니다.
- 원리: Array.prototype.slice를 호출하되, call이나 apply를 사용하여 this를 arguments 객체로 설정하면, 마치 arguments가 배열인 것처럼 배열 메서드를 사용할 수 있게 됩니다.
  - 예시: Array.prototype.slice.call(arguments) → arguments 객체를 배열로 변환하는 데 사용됩니다.
### bind 메서드의 역할
 bind 메서드는 this 바인딩을 영구적으로 고정하는 데 사용되며, apply나 call처럼 함수를 즉시 호출하지 않습니다.
 - 동작: bind는 첫 번째 인수로 전달된 this 바인딩이 고정된 새로운 함수를 생성하여 반환합니다.
 - 예시: getThisBinding.bind(thisArg)는 this가 {a: 1}로 고정된 새로운 함수를 반환하며, 이 함수를 나중에 호출할 때 this는 항상 {a: 1}입니다.

 ## 10. 콜백 함수 this 바인딩 문제 해결 심화
 메서드 내부의 $\mathrm{setTimeout}$과 같은 **보조 함수(헬퍼 함수)**의 콜백 함수는 일반 함수로 호출되면서 this가 전역 객체에 바인딩되어 외부 this와 불일치하는 문제가 발생합니다.
 ### 10.1. $\mathrm{bind}$를 사용한 명시적 this 바인딩
 - setTimeout(callback.bind(this), 100);와 같이 bind를 사용하여 콜백 함수의 this를 외부 메서드의 this와 일치시킵니다.
 ### 10.2 that 변수를 사용한 this 우회
 - ES6 이전에는 메서드 진입 시 const that = this;와 같이 this를 that 변수에 할당하여 클로저를 통해 that 변수를 참조하는 방식으로 문제를 해결했습니다.
 ### 10.3 화살표 함수를 사용한 this 바인딩
 - 화살표 함수는 자체적인 this 바인딩을 갖지 않습니다. 대신, 자신이 선언될 당시의 상위(렉시컬) 스코프의 this를 계승합니다.
 - 따라서 메서드 내부에서 화살표 함수를 사용하면, 콜백 함수 내부의 this가 메서드를 호출한 객체(obj)를 자연스럽게 가리키게 됩니다.

| 해결방법      | this 설정 방식                 | 적용 가능성                 |
| ------------ | ------------------------------ | ---------------------------|
| `bind` 메서드 | 명시적으로 `this`를 고정         | 모든 함수                  |
| `that` 변수  | 클로저를 통해 `this`를 참조        | 모든 함수(ES6이전 주류)    |
| 화살표 함수 | 렉시컬 스코플의 `this` 계승          | ES6+                      |
