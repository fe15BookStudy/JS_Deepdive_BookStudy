# 모던 자바스크립트 Deep Dive

## 15장 let, const 키워드와 블록 레벨 스코프

### var 키워드로 선언한 변수의 문제점

### 변수 중복 선언 허용

var 키워드로 선언된 변수는 중복 선언이 가능하다.

```jsx
var x = 1;
var y = 1;

var x = 100;
var y; //초기화 문이 없는 변수 선언문은 무시된다.

console.log(x); // 100
console.log(y); // 1
```

초기화문이 있는 변수 선언문은 자바스크립트 엔진에 의해 var키워드가 없는 것처럼 동작하고 초기화문이 없는 변수 선언문은 무시된다.

### 함수 레벨 스코프

var 키워드로 선언한 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정한다. 따라서 함수외부에서 var키워드로 선언한 변수는 코드 블록내에서 선언해도 모두 전역 변수가 된다.

```jsx
var x = 1;
if (true) {
  var x = 10;
}
console.log(x); //10
```

### 변수 호이스팅

var 키워드로 변수를 선언하면 변수 호이스팅에 의해 변수 선언문이 스코프의 선두로 끌어 올려진 것처럼 동작한다. 즉, 변수 호이스팅에 의해 var 키워드로 선언한 변수는 변수 선언문 이전에 참조할 수 있다. (단, undefined반환)

```jsx
console.log(foo); //undefined
foo = 123;
console.log(foo); //123
var foo;
```

변수 선언문 이전에 변수를 참조하는 것은 변수 호이스팅에 의해 에러를 발생시키지는 않지만 가독성을 떨어뜨리고 오류를 발생시킬 여지를 남긴다.

### let 키워드

var 키워드의 단점을 보완하기 위해 ES6에서는 새로운 변수 선언 키워드인 let과 const를 도입했다.

### 변수 중복 선언 금지

let 키워드로 이름이 같은 변수를 중복 선언하면 문법에러가 난다.

```jsx
var foo = 123;
var foo = 456;
let bar = 123;
let bar = 456; //error
```

### 블록 레벨 스코프

var 키워드로 선언한 변수는 어러지 함수의 코드 블록만을 지역 스코프로 인정하는 함수 레벨 스코프를 따르지만 let 키워드로 선언한 변수는 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.

```jsx
let foo = 1;
{
  let foo = 2; //지역
  let bar = 3; //지역
}
console.log(foo); //1
console.log(bar); //error
```

### 변수 호이스팅

var 카워드로 선언한 변수와 달리 let키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 동작한다.

```jsx
console.log(x); //error
let x;
```

let 키워드로 선언한 변수를 변수 선언문 이전에 참조하면 참조 에러가 발생한다. let 키워드로 선언한 변수는 **선언단계**와 **초기화단계**가 분리되어 진행된다. 즉, 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 선언 단계가 먼저 실행되지만 초기화 단계는 변수 선언문에 도달했을 때 실행된다.

스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 일시적 사각지대라고 부른다.

결국 let 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 보인다. 하지만 그렇지않다.

```jsx
let foo = 1;
{
  console.log(foo); //error
  let foo = 2;
}
```

let 키워드로 선언한 변수의 경우 변수 호이스팅이 발생하지 않는다면 위 예제는 전역 변수 foo의 값을 출력해야 한다. 하지만 let키워드로 선언한 변수도 여전히 호이스팅이 발생하기 때문에 참조 에러가 발생한다.

ES6에서 도입된 let, const, class를 사용한 선언문은 호이스팅이 발생하지 않는 것처럼 동작한다.

## 전역 객체와 let

var 키워드로 선언한 전역 변수와 전역 함수, 그리고 선언하지 않은 변수에 값을 할당한 암묵적 전역은 전역 객체 window의 프로퍼티가 된다.

```JavaScript
// 이 예제는 브라우저 환경에서 실행 해야 한다.

var x = 1;

y = 2;

function foo() {}

console.log(window.x); //1
console.log(x); //1

console.log(window.y); //2
console.log(y); //2

console.log(window.foo); // f foo() {}

console.log(foo); // f foo() {}
```

let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다. 즉, window.foo와 같이 접근할 수 없다.

```jsx
let x = 1;

console.log(window.x); // undefined
console.log(x); // 1
```

## const 키워드

const키워드는 상수를 선언하기 위해 사용한다. 하지만 반드시 상수만을 위해 사용하지는 않는다.

### 선언과 초기화

const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다.

```jsx
const foo = 1;
```

const 키워드로 선언한 변수는 let 키워드로 선언한 변수와 마찬가지로 블록 레벨 스코프를 가지며, 변수 호이스팅이 발생하지 않는 것처럼 동작한다.

```jsx
{
  console.log(foo); //error
  const foo = 1;
  console.log(foo);
  1;
}
console.log(foo); //error
```

### 재할당 금지

const키워드로 선언한 변수는 재할당이 금지된다

```jsx
const foo = 1;
foo = 2; //error
```

### 상수

const 키워드로 선언한 변수에 원시 값을 할당한 겨웅 변수 값을 변경할 수 없다. 이러한 특징을 이용해 const키워드를 상수를 표현하는데 사용하기도 한다.

```JavaScript
//세전 가격
let preTaxPrice = 100;

//세후 가격
// 0.1의 의미를 명확히 알기 어렵기 때문에 가독성이 좋지 않다.
let afterTaxPrice = preTaxPrice + (preTaxPrice + 0.1 );

console.log(afterTaxPrice); //110
```

코드 내에서 사용한 0.1은 어떤 의미로 사용했는지 명확히 어렵기 때문에 가독성이 좋지 않다. 일반적으로 상수의 이름은 대문자로 선언해 상수임을 명확히 나타낸다. 여러 단어로 이뤄진 경우에느 언더스코어로 구분해서 표현한다.

```jsx
const TAX_RATE = 0.1;

let preTaxPrice = 100;

let afterTaxPrice = preTaxPrice + preTaxPrice * TAX_RATE;

console.log(afterTaxPrice); //110
```

### const와 객체

const키워드로 선언된 변수에 원시값을 할당한 경우 값을 변경할 수 없다. 하지만 const 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있다.

```jsx
const person = {
  name: "Lee",
};

// 객체는 변경 가능한 값이다. 따라서 재할당 없이 변경이 가능하다.
person.name = "Kim";

console.log(person); //{name: "Kim"}
```
