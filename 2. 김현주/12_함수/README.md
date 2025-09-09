# 12.1 함수란?

- 함수는 JavaScript에서 가장 중요한 핵심 개념
- 특정 작업을 수행하는 코드 블록을 재사용 가능하게 만드는 기능
- function 키워드로 정의하고 매개변수와 반환값을 가질 수 있음

# 12.2 함수를 사용하는 이유

- 코드 재사용성: 같은 작업을 반복할 때 중복을 제거
- 모듈화: 복잡한 프로그램을 작은 단위로 나누어 관리
- 유지 보수성: 코드 수정이 용이함

# 12.3 함수 리터럴

- 함수는 객체이므로 리터럴로 생성 가능
- 함수명, 매개변수 목록, 함수 몸체로 구성
- 구성 요소별 역할과 특징 설명

# 12.4 함수 정의

다양한 함수 정의 방법들

# 12.4.1 함수 선언문

```javascript
function add(x, y) {
  return x + y;
}
```

# 12.4.2 함수 표현식

```javascript
var add = function (x, y) {
  return x + y;
};
```

# 12.4.3 함수 생성 시점과 함수 호이스팅

- 함수 선언문과 함수 표현식의 차이점
- 호이스팅(hoisting)개념과 동작 방식

# 12.4.4 Function 생성자 함수

```javascript
const add = (x, y) => x + y;
```

# 12.5 함수 호출

# 12.5.1 매개변수와 인수

- 매개변수(parameter)와 인수(argument)의 차이
- 함수 호출 시 인수 전달 방식
- 매개변수는 함수 내부에서만 사용 가능 (스코프 제한).
- 인수 개수와 매개변수 개수가 달라도 에러 X.
  - 부족하면 undefined, 많으면 초과분 무시됨.
- arguments 객체를 통해 모든 인수를 확인 가능.
- ES6부터는 기본값 매개변수 사용 가능:

```javascript
function add(a = 0, b = 0) {
  return a + b;
}
```

# 12.5.2 인수 확인

- JavaScript는 동적 타입 언어이므로 타입 체크가 중요
- 매개변수 개수와 인수 개수 불일치 처리

```javascript
function add(x, y) {
  if (typeof x !== 'number' || typeof y !== 'number') {
    throw new TypeError('숫자여야 합니다');
  }
  return x + y;
}
```

- 매개변수 개수
  - 공식적으로 제한 없음.
  - 하지만 3개 이하 권장 (가독성과 유지보수성).
  - 더 많으면 객체를 인수로 전달하는 방식이 좋음:
  ```javascript
  $.ajax({ method: 'POST', url: '/user', data: { id: 1, name: 'Lee' } });
  ```

````

# 12.5.4 반환문

- return 키워드로 함수 실행 결과 반환
- 반환문이 없으면 undefined 반환

# 12.5.5 화살표 함수(ES6)

```javascript
var add = (x, y) => x + y;
```

- 간결한 문법, this 바인딩 방식 다름.

# 12.6 참조에 의한 전달과 외부 상태의 변경

값에 의한 전달 vs 참조에 의한 전달

- 원시값: 값 자체가 복사되어 전달(값에 의한 전달)
- 객체: 참조값이 복사되어 전달(참조에 의한 전달)

```javascript
function changeVal(primitive, obj) {
  primitive += 100;
  obj.name = 'Kim';
}

var num = 100;
var person = { name: 'Lee' };
changeVal(num, person);

console.log(num); // 100 (변경되지 않음)
console.log(person); // {name: "Kim"} (변경됨)
```

핵심 포인트: 함수 내부에서 객체를 변경하면 원본 객체가 직접 변경되므로 부수 효과가 발생할 수 있음

# 12.7 다양한 함수의 형태

# 12.7.1 즉시 실행 함수(IIFE)

```javascript
(function () {
  var a = 3;
  var b = 5;
  return a * b;
})();
```

- 함수 정의와 동시에 즉시 호출
- 단 한 번만 호출되며 다시 호출할 수 없음

# 12.7.2 재귀함수

```javascript
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i);
  }
}
// 재귀 함수로 구현
function repeat(n, f) {
  if (n <= 0) return;
  f(n);
  repeat(n - 1, f);
}
```

- 자기 자신을 호출하는 함수
- 반복 처리를 구현할 때 사용
- 콜백 함수, 고차 함수와 함께 함수형 프로그래밍에서 중요한 개념

# 12.7.3 중첩 함수와 외부 함수

```javascript
function outer() {
  var x = 1;

  function inner() {
    // 중첩 함수
    var y = 2;
    console.log(x + y); // 외부 함수의 변수 참조 가능
  }

  inner();
}
```

# 12.7.4 콜백 함수

```javascript
// 고차 함수
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i);
  }
}

// 콜백 함수
var logAll = function (i) {
  console.log(i);
};

repeat(5, logAll); // 0 1 2 3 4
```

고차 함수: 함수를 매개변수로 전달받거나 함수를 반환하는 함수
콜백 함수: 다른 함수에 매개변수로 전달되어 특정 시점에 호출되는 함수

# 12.7.5 순수 함수와 비순수 함수

순수함수

```javascript
var count = 0;

function increase(n) {
  return ++n; // 외부 상태에 의존하지 않고 변경하지도 않음
}
```

비순수함수

```javascript
var count = 0;

function increase() {
  return ++count; // 외부 상태(count)에 의존하고 변경함
}
```

핵심 개념:

- 순수 함수: 동일한 인수로 호출하면 항상 동일한 값 반환, 외부 상태 변경 없음
- 비순수 함수: 외부 상태에 의존하거나 외부 상태를 변경하는 함수
- 함수형 프로그래밍에서는 순수 함수를 통해 부수 효과를 최소화하고 안정성을 높임
````
