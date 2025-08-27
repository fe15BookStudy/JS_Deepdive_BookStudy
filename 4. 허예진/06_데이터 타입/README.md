# 06. 데이터 타입

데이터 타입은 **값의 종류**를 말한다.  
7개의 타입이 제공되며 **원시타입**과 **객체타입**으로 분류할 수 있다.

| 구분          | 타입                      | 설명                                  | 예시                                |
| ------------- | ------------------------- | ------------------------------------- | ----------------------------------- |
| **원시 타입** | 숫자                      | 숫자(정수, 실수, NaN, Infinity 포함)  | `10`, `3.14`, `NaN`                 |
|               | 문자                      | 문자열 (텍스트 데이터)                | `"hello"`, `'안녕'`, `` `템플릿` `` |
|               | Boolean                   | 논리형                                | `true`, `false`                     |
|               | undefined                 | 값이 할당되지 않은 변수의 초기값      | `let x; // undefined`               |
|               | null                      | 의도적으로 "값 없음"                  | `let y = null;`                     |
|               | Symbol (ES6)              | 유일무이한 값(주로 객체 프로퍼티 key) | `Symbol('id')`                      |
| **객체 타입** | Object                    | 키-값 쌍의 집합                       | `{ name: "heo", age: 20 }`          |
|               | Array                     | 순서 있는 리스트                      | `[1, 2, 3]`                         |
|               | Function                  | 함수도 객체                           | `function add(x,y){ return x+y }`   |
|               | Date, RegExp, Map, Set 등 | 내장 객체들                           | `new Date()`, `/[a-z]+/g`           |

## 숫자 타입(Number)

**자바스크립트에서는 하나의 숫자 타입(Number)**만 존재한다.  
64비트 부동소수점 형식을 사용한다.  
`NaN(Not-a-Number)`, `Infinity`, `-Infinity`도 Number 타입에 포함된다.

```javascript
let integer = 10; // 정수
let float = 10.5; // 실수
let nan = NaN; // 산술연산 불가능할 때
let inf = Infinity; // 무한대
```

## 문자열 타입 (String)

텍스트 데이터를 표현하는 타입이다.  
작은따옴표(''), 큰따옴표(""), 백틱(`````) 모두 문자열 표현 가능  
변경 불가능(immutable) → 한 번 생성되면 수정 불가하다.

```javascript
let string;
string = "문자열"; // 작은따옴표
string = "문자열"; // 큰따옴표
string = `문자열`; // 백틱
```

## 템플릿 리터럴

ES6에서 도입된 문자열 표현 방식이다.  
백틱(``)을 사용한다.  
줄바꿈, 표현식 삽입이 자유롭다.

### 멀티라인 문자열

기존 문자열('' 또는 "")은 줄바꿈 시 \n을 사용해야 했음  
템플릿 리터럴(``)은 그냥 줄바꿈 가능

```javascript
const multiLine = `이렇게
여러 줄을
직접 작성 가능`;
console.log(multiLine);
```

### 표현식 삽입

${...} 구문을 사용하면 변수나 연산식을 문자열 안에 바로 삽입 가능

```javascript
const name = "예진";
const age = 20;
const msg = `안녕하세요, ${name}님! 올해 나이는 ${age + 1}세 입니다.`;
console.log(msg);
```

```html
안녕하세요, 예진님! 올해 나이는 21세 입니다.
```

## 불리언 타입(Boolean)

(true) 또는 거짓(false) 두 값만 가질 수 있다.  
조건문, 제어문의 조건식에서 주로 사용한다.

```javascript
let isLogin = true;
let isAdmin = false;
```

## undefined 타입

변수를 선언만 하고 값을 할당하지 않았을 때 자동으로 할당되는 값  
"아직 값이 정의되지 않음"을 의미한다.

```javascript
let x;
console.log(x); // undefined
```

## null 타입

변수에 값이 없음을 명시할 때 사용한다.
변수에 null을 할당하는 것은 변수가 이전에 참조하던 값을 더 이상 참조하지 않겠다는 의미다. 이는 이전에 할당되어 있던 값에 대한 참조를 명시적으로 제거하는 것을 의미한다.

```javascript
var name = "Lee";

// 이전 참조를 제거. name 변수는 더 이상 'Lee'를 참조하지 않는다.
// 하지만 이 방법은 유용하진 않다. 변수의 스코프를 좁게 만들어 변수 자체를 재빨리 소멸시키는 편이 낫다.
name = null;
```

## 심벌 타입

ES6에서 도입  
**유일무이한 값**을 생성할 때 사용한다.  
주로 객체의 키 값으로 활용 (중복 방지)

```javascript
let key1 = Symbol("id");
let key2 = Symbol("id");
console.log(key1 === key2); // false
```

## 객체 타입

자바스크립트를 이루고 있는 거의 모든 것이 객체이다.

- 원시 타입을 제외한 모든 값은 객체 타입
- 키(key)-값(value) 형태로 구성
- 배열, 함수, 정규표현식, Date, Map, Set 등도 모두 객체 타입

## 데이터 타입의 필요성

1. 값을 저장할 때 확보할 메모리 공간의 크기를 결정
2. 값을 참조할 때 읽어올 메모리 공간의 크기를 결정
3. 값을 어떻게 해석하고 연산할지를 결정

## 동적 타이핑

자바스크립트는 변수 선언 시 타입을 명시하지 않고, 값에 따라 타입이 자동으로 결정된다.  
즉, 변수의 타입이 실행 중에 동적으로 바뀔 수 있음

```javascript
let x = 10; // Number 타입
x = "Hello"; // String 타입으로 동적 변경
x = true; // Boolean 타입으로 동적 변경
```

- 단점: 타입 관련 버그 발생 가능 → 필요시 typeof 연산자나 TypeScript로 보완

```javascript
let y = 100;
console.log(typeof y); // number
y = "100";
console.log(typeof y); // string
```
