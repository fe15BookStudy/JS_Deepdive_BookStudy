# 15.1 var 키워드의 문제점

중복 선언 허용

- var는 같은 변수명을 여러 번 선언할 수 있어 의도치 않은 재할당 발생 가능

```javascript
var x = 1;
var y = 1;

//var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
//초기화문이 있는 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.
var x = 100;
//초기화문이 없는 변수 선언문은 무시된다.
var y;

console.log(x); //100
console.log(y); //1
```

함수 레벨 스코프

- var는 함수 내에서만 지역 스코프를 가짐
- 코드 블록(if, for 등) 내에서 선언해도 전역 변수가 됨

```javascript
var x = 1;

if (true) {
  //x는 전역 변수다. 이미 선언된 전역 변수 x가 잇으므로 x 변수는 중복 선언된다.
  //이는 의도치 않게 변수값이 변경되는 부작용을 발생시킨다.
  var x = 10;
}
console.log(x); //10
```

변수 호이스팅

- 변수 선언이 스코프 최상단으로 끌어올려짐
- 선언 전에 참조 시 undefined 반환

```javascript
//이 시점에는 변수 호이스팅에 의해 이미 foo 변수가 선언되었다.(1. 선언단계)
//변수 foo는 undefined로 초기화된다.(2. 초기화 단계)
console.log(foo);

//변수에 값을 할당(3. 할당 단계)

console.log(foo); //123

//변수 선언은 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 실행된다.
var foo;
```

# 15.2 let 키워드

중복 선언 금지

- 같은 스코프에서 중복 선언 시 SyntaxError 발생

```javascript
var foo = 123;
//var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
// 아래 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.
var foo = 456;

let bar = 123;
//let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.
let bar = 456; //SyntaxError: Identifier 'bar' has already been decleared
```

블록 레벨 스코프

- if, for, while 등 모든 코드 블록에서 지역 스코프 생성

```javascript
let foo = 1; //전역 변수
{
  let foo = 2; //지역 변수
  let bar = 3; //지역 변수
}
console.log(foo); //1
console.log(bar); //ReferenceError: bar is not defined
```

변수 호이스팅과 TDZ

- 호이스팅은 되지만 초기화 전까지 일시적 사각지대(TDZ)에 있음
- 선언 전 접근 시 ReferenceError 발생

변수 호이스팅

```javascript
console.log(foo); //ReferenceError:foo is not defined
let foo;
```

```javascript
//var 키워드로 선언한 변수는 런타임 이전에 선언 단계와 초기환 단계가 실행된다.
//따라서 변수 선언문 이전에 변수를 참조할 수 있다.
console.log(foo); //undefined

var foo;
console.log(foo); //undefined

foo = 1; //할당문에서 할당 단계가 실행된다.
console.log(foo); //1
```

전역 객체와 let

- let으로 선언한 전역 변수는 window 객체의 프로퍼티가 되지 않음

```javascript
//이 예제는 브라우저 환경에서 실행해야 한다.

//전역 변수
var x = 1;
//암묵적 전역
y = 2;
//전역 함수
function foo() {}

//var 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티다.
console.log(window.x); //1
//전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(x); //1

//암묵적 전역은 전역 객체 window의 프로퍼티다.
console.log(window.y); //2
console.log(y); //2

//함수 선언문으로 정의한 전역 함수는 전역 객체 window의 프로퍼티다.
console.log(window.foo); //f foo() {}
//전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(foo); f foo() {}
```

# 15.3 const 키워드

선언과 초기화

- 선언과 동시에 반드시 초기화해야 함
- 초기화하지 않으면 SyntaxError 발생

재할당 금지

- const로 선언한 변수는 재할당 불가
- 원시값의 경우 완전한 상수

상수

- const로 선언한 원시값은 변경 불가능한 값(immutable value)
- 객체의 경우 객체 자체를 변경하는 것은 불가하지만 프로퍼티 동적 생성, 삭제, 변경은 가능

# 15.4 var vs. let vs. const

권장사항:

- ES6에서는 var 사용을 피하고 let과 const 사용 권장
- 재할당이 필요한 경우에만 let 사용
- 변경이 발생하지 않는 원시값과 객체에는 const 사용
- const → let → var 순으로 우선순위
