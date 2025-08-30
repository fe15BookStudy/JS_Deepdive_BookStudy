# 06. 데이터 타입

### 숫자 타입

<br>

- 자바스크립트에서 숫자는 정수와 실수를 구분하지 않고, 모두 하나의 `Number` 타입으로 처리된다. 다른 프로그래밍 언어와 다르게, **하나의 데이터 타입만 사용** 한다는 점이 특징이다. 자바스크립트의 모든 숫자는 **64비트 부동소수점 형식** 으로 저장되는데, 이 형식은 정수와 실수를 모두 표현할 수 있어 매우 편리하다.

<br>

- 숫자 타입의 종류

  자바 스크립트의 숫자 타입은 크게 세 가지로 나눌 수 있다.

  - 정수 ( Integer) : 10, -5, 100과 같은 소수점이 없는 숫자

  - 실수(Float): 3.12, -0.5, 2.718과 같이 소수점이 있는 숫자

  - 특수 숫자 값

    1.  `Infinity  ` : 무한대를 나타내는 값. 어떤 숫자를 0으로 나누면 이 값을 얻게 된다.

    2.  `Infinity` : 음의 무한대를 나타내는 값.

    3.  `NaN` : Not a Numer의 약자로, 숫자가 아님을 나타내는 특별한 값.

    <br>

- 연산자

  숫자 타입에 적용할 수 있는 주요 연산자들은 다음과 같다.

  - 사칙역산 : `+` (더하기), `-` (빼기), `*` (곱하기), `/`(나누기)

  - 기타 : `%` ( 나머지 연산) , `**` (거듭제곱)

  ```JavaScript
  let a = 10;
  let b = 3;

  console.log(a + b); // 13
  console.log(a - b); // 7
  console.log(a * b); // 30
  console.log(a / b); // 3.3333333333333335
  console.log(a % b); // 1
  console.log(a ** b); // 1000
  ```

<br>

---

<br>

### 문자열 타입

- 문자열은 텍스트 데이터를 나타내는 타입. 큰 따옴표(")나 작음따옴표(')로 감싸서 표현한다.

<br>

- 문자열 생성 :

```JavaScript
    let name = "멋사";
    let greeting = '안녕하세요!';
```

- 문자열 길이 : `length` 속성으로 문자열의 길이를 알 수 있다.

```JavaScript
    console.log(name.length); // 2
```

- 문자열 결합 : `+` 연산자를 사용해 여러 문자열을 합칠 수 있다.

```JavaScript
   let fullName = "서" + "주희";
console.log(fullName); // "서주희"
```

<br>

---

<br>

### 템플릿 리터럴

<br>

- 템플릿 리터럴은 **백틱(`)** 으로 감싸는 문자열로, 여러 줄의 문자열을 작성하거나 변수를 쉽게 삽입할 수 있어 매우 유용하다. 이를 **_템플릿 문자열_** 이라고도 부른다.

<br>

- 변수 삽입: `${변수명}` 문법을 사용해 문자열 안에 변수나 표현식을 넣을 수 있다.

```JavaScript
let name = "길동";
let age = 80;
let message = `제 이름은 ${name}이고, 나이는 ${age}살입니다.`;
console.log(message); // "제 이름은 길동이고, 나이는 80살입니다."
```

- 여러 줄 작성: 별도의 줄 바꿈 문자를 사용하지 않아도 여러 줄로 나눌 수 있다.

```JavaScript
let multiLine = `
    안녕하세요.
    저는 자바스크립트를 배우고 있습니다.
  `;
  console.log(multiLine);
```

<br>

---

<br>

### 불리언 타입

<br>

- 불리언 타입의 값은 `true` 와 `false` 뿐이다. 이 타입은 주로 **조건문(if, else)** 이나 **반복문(for, while)** 에서 조건을 판단하는 데 사용된다.

<br>

---

### Undefined 타입

<br>

- `Undefined`는 값이 할당되지 않은 상태를 나타내는 특별한 값을 일컫는다. 변수를 선언만 하고 값을 할당하지 않으면 해당 변수는 자동으로 `Undefined` 로 초기화 된다.

<br>

- 예를 들면

```JavaScript
let myVariable; // 변수는 선언되었지만 값이 할당되지 않음
console.log(myVariable); // undefined 출력
```

---

`Null 타입과 undefined의 차이`

자바 스크립트에는 undefined와 유사한 **null** 이라는 개념도 존재하는데,

- `undefined` : 시스템이 값이 **할당되지 않았음을 나타내기 위해 자동으로 부여**

- `null` : 개발자가 **값이 없음 을 의도적으로 나타내기 위해 명시적으로** 할당

---

<br>

### 심벌 타입

<br>

- 심벌은 **_ES6(ECMAScript 2015)에서 새롭게 도입된 데이터 타입_** . 유일하고 변경 불가능한 값으로, 주로 객체 속성(property)의 키로 사용.

- 심벌은 다른 어떤 값과도 중복되지 않는 **고유성을 보장** 하기 때문에 이름 충돌을 피하고 싶은 객체 속성을 만들 때 유용.

<br>

---

<br>

### 객체 타입

<br>

- 객체는 여러 데이터와 함수를 **하나의 단위** 로 묶어놓은 **복합적인 데이터 타입**. 자바스크립트의 거의 모든 것이 객체라고 할 수 있을 정도로 중요한 개념이다. 함수 ,배열, 심지어 `null` 을 제외한 모든 원시 타입 (숫자 ,문자열, 불리언 등 ) 도 객체처럼 다뤄질 수 있다.

- 객체는 `키(key)` 와 `값(value)`의 쌍으로 이루어진 속성(property)들의 집합이다.

```JavaScript
const person = {
  name: '홍길동', // name은 키, '홍길동'은 값
  age: 80, // age는 키, 80은 값
  isStudent: false
};

console.log(person.name); // '홍길동'
console.log(person['age']); // 80
```

---

<br>

### 동적 타이핑

<br>

- 자바스크립트는 동적 타이핑 언어다. 이는 **_변수의 타입이 고정되어 있지 않고 할당되는 값에 따라 타입이 동적으로 결정된다_** 는 것을 의미한다. C++이나 Java와 같은 정적 타이핑 언어에서는 변수를 선언할 때 타입을 미리 지정해야 하지만 자바스크립트는 그렇지 않다.

```JavaScript
let myVariable = 10; // myVariable은 Number 타입
console.log(typeof myVariable); // "number"

myVariable = 'Hello, world!'; // 같은 변수에 문자열을 할당하면 String 타입으로 바뀜
console.log(typeof myVariable); // "string"

myVariable = true; // Boolean 타입으로 다시 바뀜
console.log(typeof myVariable); // "boolean"
```

- 동적 타이핑은 코드를 유연하게 작성할 수 있다는 장점이 있으나, 예상치 못한 타입 오류가 발생할 수 있다는 단점도 존재한다.
