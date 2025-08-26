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

# 데이터 타입의 필요성

- **값을 저장할 때 확보해야 하는 메모리 공간의 크기를 결정하기 위해**
- **값을 참조할 때 한 번에 읽어 들여야 할 메모리 공간의 크기를 결정하기 위해**
- **메모리에서 읽어 들인 2진수를 어떻게 해석할지 결정하기 위해**

# 동적 타이핑

# 정적 타이핑 언어와 동적 타이핑 언어

- `정적 타이핑 언어`: 변수를 선언할 때 변수에 할당할 수 있는 값의 데이터 타입을 사전에 선언해야 한다.
  - **명시적 타입 선언**
  - C, C++, Java, TypeScript 등
  - 컴파일 시점에 타입 체크를 수행한다 → 타입의 일관성을 강제하면서 더욱 안정적인 코드의 구현을 통해 런타임에 발생하는 에러를 줄인다.
  - 동적 타이핑 언어: 변수가 선언이 아닌 할당에 의해 타입이 결정된다. 변수의 타입은 재할당을 통해 언제든지 동적으로 변할 수 있다.
  - JavaScript, Python, PHP, Ruby 등

# 동적 타이핑 언어의 단점

- 변수 값이 언제든지 변경될 수 있기 때문에 복잡한 프로그램에서는 변화하는 변수 값을 추적하기 어려울 수 있다.
- 값의 변경에 의해 타입도 언제든지 변경될 수 있어서 동적 타입 언어의 변수는 값을 확인하기 전에는 타입을 확신할 수 없다.
- **동적 타입 언어는 `유연성은 높지만` `신뢰성은 떨어진다.`**

# 변수 사용시 주의할 점

- 변수는 꼭 필요한 경우에 한해 제한적으로 사용한다.
- 유효 범위(스코프)를 최대한 좁게 만들어서 변수의 부작용을 억제해야 한다.
- 전역 변수는 최대한 사용하지 않는다.
- 변수보다 상수의 값을 사용해서 값의 변경을 억제한다.
- 변수 이름은 변수의 목적이나 의미를 파악할 수 있도록 네이밍하자.
