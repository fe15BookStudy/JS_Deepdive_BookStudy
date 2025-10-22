# Math

- 수학적인 상수와 함수를 위한 프로퍼티와 메서드를 제공한다.
- Math는 생성자 함수가 아니다.
- 정적 프로퍼티와 정적 메서드만 제공한다.

## Math.PI

```javascript
Math.PI; // 3.141592653589793
```

- 원주율 PI 값을 반환한다.

## Math.abs

```javascript
Math.abs(-1); // 1
Math.abs("-1"); // 1
Math.abs(""); // 0
Math.abs([]); // 0
Math.abs(null); // 0

Math.abs(undefined); // NaN
Math.abs({}); // NaN
Math.abs("string"); // NaN
Math.abs(); // NaN
```

- 인수로 전달된 숫자의 절대값을 반환한다.
- 절대값은 반드시 0 또는 양수이어야 한다.

## Math.round

```javascript
Math.round(1.4); // 1
Math.round(1.6); // 2
Math.round(-1.4); // -1
Math.round(-1.6); // -2
Math.round(1); // 1
Math.round(); // NaN
```

- 인수로 전달된 숫자의 소수점 이하를 반올림한 정수를 반환한다.

## Math.ceil

```javascript
Math.ceil(1.4); // 2
Math.ceil(1.6); // 2
Math.ceil(-1.4); // -1
Math.ceil(-1.6); // -1
Math.ceil(1); // 1
Math.ceil(); // NaN
```

- 인수로 전달된 숫자의 소수점 이하를 올림한 정수를 반환한다.

## Math.floor

```javascript
Math.floor(1.9); // 1
Math.floor(9.1); // 9
Math.floor(-1.9); // -2
Math.floor(-9.1); // -10
Math.floor(1); // 1
Math.floor(); // NaN
```

- 인수로 전달된 숫자의 소수점 이하를 내림한 정수를 반환한다.

## Math.sqrt

```javascript
Math.sqrt(9); // 3
Math.sqrt(-9); // NaN
Math.sqrt(2); // 1.414
Math.sqrt(1); // 1
Math.sqrt(0); // 0
Math.sqrt(); // NaN
```

- 인수로 전달된 숫자의 제곱근을 반환한다.

## Math.random

```javascript
Math.random(); // 0에서 1 미만의 랜덤 실수 (ex. 0.8)

// 1에서 10 사이의 정수
const random = Math.floor(Math.random() * 10 + 1);
```

- 임의의 난수를 반환한다.
- 기본 값은 0에서 1미만의 랜덤 실수이다.

## Math.pow

```javascript
Math.pow(2, 8); // 256
Math.pow(2, -1); // 0.5
Math.pow(2); // NaN
```

- 첫 번째 인수를 베이스로, 두 번째 인수를 거듭제곱한 결과를 반환한다.
- 첫 번째, 두 번째 인수는 필수로 넣어야 한다.

## Math.max

```javascript
Math.max(1); // 1
Math.max(1, 2); // 2
Math.max(1, 2, 3); // 3
Math.max(); // -Infinity
```

- 전달받은 인수 중에서 가장 큰 수를 반환한다.
- 인수가 전달되지 않으면 -Infinity를 반환한다.

```javascript
// apply 메서드
Math.max.apply(null, [1, 2, 3]);

// 스프레드 문법
Math.max(...[1, 2, 3]);
```

- 배열을 인수로 전달받아 최대값을 구하려면 apply 메서드 또는 스프레드 문법을 사용하면 된다.

## Math.min

```javascript
Math.min(1); // 1
Math.min(1, 2); // 1
Math.min(1, 2, 3); // 1
Math.min(); // Infinity
```

- 전달받은 인수 중에서 가장 작은 수를 반환한다.
- 인수가 전달되지 않으면 Infinity를 반환한다.
