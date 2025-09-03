# 9장 타입 변환과 단축 평가

<br>

## 9.1 타입 변환이란?

- 명시적 타입 변환(타입 캐스팅) : **개발자가 의도적**으로 값의 타입을 변환하는 것을 뜻한다.
- 암묵적 타입 변환(타입 강제 변환): **개발자의 의도와는 상관없이** 표현식을 평가하는 도중에 JS에 의해 암묵적으로 타입이 자동 변환되는 것을 뜻한다.

<br>

## 9.2 암묵적 타입 변환

```jsx
// 피연산자가 모두 문자열 타입이어야 한다.
"10" + 2; // '102'

// 피연산자가 모두 숫자 타입이어야 한다.
5 * "10"; // 50

// 피연산자 또는 표현식이 boolean 타입이어야 한다.
!0; // true
```

- 이처럼 표현식을 평가할 때 코드의 문맥에 부합하지 않을 때가 있는데 JS는 가급적 에러를 발생시키지 않고 암묵적 타입 변환을 통해 표현식을 평가한다.

### 9.2.1 문자열 타입으로 변환

```jsx
1 + "2"; // '12'
```

- 위 예제에서 +연산자는 피연산자 중 하나 이상이 문자열이므로 문자열 연결 연산자로 동작한다. 따라서 JS 엔진은 숫자 1을 문자열 타입으로 암묵적 타입 변환한다.

### 9.2.2 숫자 타입으로 변환

```jsx
1 - "1"; // 0
1 * "10"; // 10
1 / "one"; // NaN
"1" > 0; // true
```

- 위의 연산자들 중 -, \*, /는 산술 연산자다. 따라서 피연산자가 모두 숫자 타입이어야 하므로 문자열 타입 피연산자는 암묵적 타입 변환이 된다.
- 피연산자를 숫자 타입으로 변환할 수 없는 경우 산술 연산을 수행할 수 없으므로 표현식의 평가 결과는 NaN이 된다.
- 비교 연산자도 피연산자가 모두 숫자 타입이어야 하므로 숫자 타입이 아닌 피연산자는 암묵적 타입 변환이 된다.

```jsx
+""; // 0
+"1"; // 1
+"string"; // NaN
+true; // 1
+false; // 0
+null; // 0
+undefined; // NaN
```

- \+ 단항 영산자는 피연산자가 숫자 타입의 값이 아니면 숫자 타입의 값으로 암묵적 타입 변환을 수행한다.

### 9.2.3 boolean 타입으로 변환

- if문이나 for문과 같은 제어문 또는 삼항 조건 연산자의 조건식은 boolean 값으로 평가되어야 하는 표현식이다. JS 엔진은 조건식의 평가 결과를 boolean 타입으로 암묵적 타입 변환한다.
- JS 엔진은 boolean 타입이 아닌 값을 Truthy 값(참으로 평가되는 값) Falsy 값(거짓으로 평가되는 값)으로 구분한다. 아래 값들은 false로 평가되는 Falsy값이다. 이 값들을 제외한 모든 값은 모두 true로 평가되는 Truthy 값이다.
  - false
  - undefined
  - null
  - 0, -0
  - NaN
  - ‘’(빈 문자열)

<br>

## 9.3 명시적 타입 변환

- 명시적 타입 변환 방법에는 생성자 함수를 new 연산자 없이 호출하는 방법과 빌트인 메서드, 암묵적 타입 변환을 사용하는 방법이 있다.

### 9.3.1 문자열 타입으로 변환

- 문자열 타입이 아닌 값을 문자열 타입으로 변환하는 방법은 다음과 같다.

  - String 생성자 함수를 new 연산자 없이 호출하는 방법
  - Object.prototype.toString 메서드를 사용하는 방법
  - 문자열 연결 연산자를 이용하는 방법

  ```jsx
  // 1. String 생성자 함수를 new 연산자 없이 호출하는 방법
  // 숫자 타입 -> 문자열 타입
  String(1); // '1'
  String(NaN); // 'NaN'
  // 불리언 타입 -> 문자열 타입
  String(true); // 'true'
  String(flase); // 'false'

  // 2. Object.prototype.toString 메서드를 사용하는 방법
  (1).toString(); // '1'
  NaN.toString(); // 'NaN'
  true.toString(); // 'ture'
  false.toString(); // 'false'

  // 3.문자열 연결 연산자를 이용하는 방법
  1 + ""; // '1'
  NaN + ""; // 'NaN'
  true + ""; // 'true'
  false + ""; // 'false'
  ```

### 9.3.2 숫자 타입으로 변환

- 숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법은 다음과 같다.

  - Number 생성자 함수를 new 연산자 없이 호출하는 방법
  - parseInt, parseFloat 함수를 사용하는 방법 → 문자열만 숫자 타입으로 변환 가능
  - +단항 산술 연산자를 이용하는 방법
  - \*산술 연산자를 이용하는 방법

  ```jsx
  // 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
  Number("1"); // 1
  Number("10;53"); // 10.53
  Number(true); // 1
  Number(flase); // 0

  // 2. parseInt, parseFloat 함수를 사용하는 방법 → 문자열만 숫자 타입으로 변환 가능
  parseInt("0"); // 0
  parseFloat("10.53"); // 10.53

  // 3. +단항 산술 연산자를 이용하는 방법, *산술 연산자를 이용하는 방법
  +"0"; // 0
  +"10.53"; // 10.53
  +true; // 1
  +false; // 0
  "1" * 3; // 3
  ture * 1; // 1
  false * 1; // 0
  ```

### 9.3.3 boolean 타입으로 변환

- boolean 타입으로 변환하는 방법은 다음과 같다.

  - Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
  - ! 부정 논리 연산자를 두 번 사용하는 방법

  ```jsx
  // 1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
  Boolean("x"); // true
  Boolean(""); // false
  Boolean("false"); // true
  Boolean(1); // true
  Boolean(0); // false
  Boolean(null); // false
  Boolean({}); // true
  Boolean([]); // true

  // 2. ! 부정 논리 연산자를 두 번 사용하는 방법
  !!"x"; // true
  !!""; // false
  !!0; // false
  !!1; //true
  !!null; // false
  ```

<br>

## 9.4 단축 평가

### 9.4.1 논리 연산자를 사용한 단축 평가

- 논리합(||) : 논리합 연산자는 두 개의 피연산자 중 하나만 true이면 true를 반환한다. 논리합 연산자는 좌항에서 우항으로 평가가 진행된다.
- 논리곱(&&) : 논리곱 연산자는 두 개의 피연산자가 모두 true로 평가될 때 true를 반환한다. 논리곱 연산자도 좌항에서 우항으로 평가가 진행된다.

| 단축 평가 표현식    | 평가 결과 |
| ------------------- | --------- |
| ture \|\| anything  | true      |
| false \|\| anything | anything  |
| ture && anything    | anything  |
| false && anything   | false     |

```jsx
"Cat" || "Dog"; // 'Cat'
false || "Dog"; // 'Dog'
"Cat" || false; // 'Cat'

"Cat" && "Dog"; // 'Dog'
false && "Dog"; // false
"Cat" && false; // false
```

### 9.4.2 옵셔널 체이닝 연산자

- ES11에서 도입된 옵셔널 체이닝 연산자 ?.는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.

```jsx
var elem = null;

// elem이 null 또는 undefined면 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
var value = elem?.value;
console.log(value); // undefined
```

### 9.4.3 null 병합 연산자

- ES11에서 도입된 null 병합 연산자 ??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.
- null 병합 연산자 ??는 변수에 기본값을 설정할 때 유용하다.

```jsx
var foo = null ?? "default string";
console.log(foo); // 'default string'
```
