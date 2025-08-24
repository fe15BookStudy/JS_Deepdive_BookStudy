# 숫자 타입 : JavaScript는 하나의 숫자 타입만 존재(64비트 부동소수점 형식)

- 정수, 실수, 2진수, 8진수, 16진수 모두 메모리에 64비트로 저장

```jsx
//예제 6-1
//모두 숫자타입이다
var integer = 10;
var double = 10.12;
var negative = -20;
```

- 특별한 값: Infinity(양의 무한대), -Infinity(음의 무한대), NaN(Not a Number)

# 문자열 타입 : 16비트 유니코드 문자(UTF-16)의 집합

- 작은따옴표(''), 큰따옴표(""), 백틱(`) 사용 가능
- 문자열은 원시 타입으로 변경 불가능

# 템플릿 리터럴

- ES6부터 도입된 새로운 문자열 표기법
- 백틱(`)으로 표현
- 멀티라인 문자열, 표현식 삽입, 태그드 템플릿 기능 제공

# 불리언 타입 : 참, 거짓을 나타내는 true와 false

# undefined 타입

- undefined가 유일한 값
- 변수 선언 후 값을 할당하지 않으면 자동으로 undefined 할당

```jsx
//예제 6-17
var foo;
console.log(foo); //undefined
```

# null타입 : null이 유일한 값

- 값이 없다는 것을 의도적으로 명시할 때 사용
- typeof null은 "object"를 반환 (JavaScript의 버그)

# 심벌 타입

- ES6에서 추가된 7번째 타입
- 변경 불가능한 원시 타입의 값
- 다른 값과 중복되지 않는 유일무이한 값

```jsx
//심벌 값 생성
var key = Symbol('key');
console.log(typeof key); //symbol

//객체 생성
var obj = {};

//이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용한다.
obj[key] = 'value';
console.log(obj[key]); //value
```

# 객체 타입 : 원시타입 7가지 데이터 타입 이외의 값은 모두 객체 타입(number, string, boolean, undefined, symbol, bigint 제외)

# 동적 타이핑 : JavaScript는 동적 타입 언어

- 변수는 타입을 갖지 않고, 값이 타입을 가짐(var, let, const키워드를 사용해 변수를 선언한다.)
- 할당에 의해 타입이 결정되고 재할당에 의해 변경 가능

```jsx
//예제6-23
var foo;
console.log(typeof foo); //undefined

foo = 3;
console.log(typeof foo); //number

foo = 'Hello';
console.log(typeof foo); //string

foo = true;
console.log(typeof foo); //boolean

foo = null;
console.log(typeof foo); //object

foo = Symbol();
console.log(typeof foo); //symbol
```
