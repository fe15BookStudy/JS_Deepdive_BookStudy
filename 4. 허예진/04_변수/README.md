# 04. 변수

하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 메모리 공간을 식별하기 위해 붙인 이름

## 식별자

어떤 값을 구별해서 식별할 수 있는 고유한 이름. 변수의 이름을 말한다.

식별자는 값이 아닌 **메모리 주소**를 기억하고 있다.

## 변수 선언

변수에 값을 담기 위해서는 먼저 변수를 선언해야 한다.
변수 선언으로 메모리 공간의 주소를 확보할 수 있고, 해제되기 전까지는 누구도 확보된 메모리 공간을 사용할 수 없도록 보호된다.

예시)

```javascript
// 변수 선언
let myName;

// 변수에 선언과 동시에 값을 담는 방법
let userNm = "hong-gildong";

// 객체
const myInfo = { name: "heo", age: 29 };

// 여러개의 값을 저장하는 방법
let studyMember = ["hong", "heo", "choi"];
```

## 호이스팅

**호이스팅(Hoisting)**은 자바스크립트에서 변수가 선언되기 전에 마치 끌어올려진 것처럼 동작하는 특징을 말한다.  
자바스크립트 엔진은 코드 실행 전에 **변수 선언**과 **함수 선언**을 먼저 메모리에 등록한다.  
→ 이 때문에 코드에서 선언 전에 참조해도 오류가 안 나고 undefined가 출력되기도 합니다.

```javascript
console.log(a); // undefined
var a = 10;
console.log(a); // 10
```

다음과 같이 코드를 짰다고 해보자.

```javascript
console.log(score);
score = 80;
var score;
console.log(score);
```

하지만 실행 과정은 다음과 같다.

```javascript
var score; // 선언이 끌어올려짐, 초기값은 undefined

console.log(score); // undefined
score = 80; // 값 할당
console.log(score); // 80
```

## 값의 재할당

이미 값이 할당되어 있는 변수에 새로운 값을 또 다시 할당하는 것을 말한다.  
`var`, `let`, `const`는 공통적으로 변수를 선언할 때 사용하지만 "재할당 가능 여부"에서 차이가 있다.

1.`var`

재할당 가능

중복 선언도 가능 (⚠️ 의도치 않은 버그 발생 위험)

```javascript
var a = 10;
a = 20; // 재할당 가능
var a = 30; // 같은 이름 다시 선언도 가능
console.log(a); // 30
```

2.`let`

재할당 가능

하지만 같은 블록 스코프에서 중복 선언 불가능

```javascript
let b = 10;
b = 20; // 재할당 가능
console.log(b); // 20
```

3.`const`

재할당 불가능

선언과 동시에 초기화 필수 (값을 나중에 넣을 수 없음)

단, 객체나 배열 같은 참조 타입은 "주소값"만 고정 → 내부 값은 변경 가능

```javascript
const c = 10;
// c = 20; // TypeError: Assignment to constant variable.

const obj = { name: "heo" };
obj.name = "yejin"; // 객체 프로퍼티 수정은 가능
console.log(obj); // { name: "yejin" }
```

## 식별자 네이밍 규칙

- 식별자는 특수문자를 제외한 문자, 숫자, 언더스코어(\_), 달러 기호($)를 포함할 수 있다.
- 단, 식별자는 특수문자를 제외한 문자, 언더스코어(\_), 달러기호($)로 시작해야한다. 숫자로 시작하는 것은 허용하지 않는다.
- 예약어는 식별자로 사용할 수 없다.
