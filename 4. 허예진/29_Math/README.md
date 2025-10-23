# 29. Math

## Math 프로퍼티

### Math.PI

원주율 PI 값(pi는 3.141592653589793238에 근사) 을 반환한다.

## Math 메서드

Math.abs 메서드는 인수로 전달된 숫자의 절대값을 반환한다.
절대값은 반드시 0 또는 양수여야한다.

```js
Math.abs(-1); // 1
Math.abs("-1"); //  1
Math.abs(" "); //  0
Math.abs([]); // 0
Math.abs(null); // 0
Math.abs(undefined); // NaN
Math.abs({}); // NaN
Math.abs("string"); // NaN
Math.abs(); // NaN
```

### Math.round

Math.round 메서드는 인수로 전달된 숫자의 소수점 이하를 반올림한 정수를 반환한다.

```js
Math.round(1.4); // 1
Math.round(1.6); // 2
Math.round(-1.4); // -1
Math.round(-1.6); // -2
Math.round(1); // 1
Math.round(); // NaN
```

### Math.ceil

Math.ceil 메서드는 인수로 전달된 숫자의 소수점 이하를 올림한 정수를 반환한다. 소수점 이하를 올림하면 더 큰 정수가 된다. 예를 들어 1.4의 소수점 이하를 올림하면 2가 되고, -1.4의 소수점 이하를 올림하면 -1이 된다.

```js
Math.ceil(1.4); // 2
Math.ceil(1.6); // 2
Math.ceil(-1.4); // -1
Math.ceil(-1.6); // -1
Math.ceil(1); // 1
Math.ceil(); // NaN
```

### Math.floor

Math.floor 메서드는 인수로 전달된 숫자의 소수점 이하를 내림한 정수를 반환한다. 즉, Math.ceil 메서드의 반대 개념  
소수점 이하를 내림하면 더 작은 정수가 된다. 예를 들어, 1.9의 소수점 이하를 내림하면 1이 되고, -1.9의 소수점 이하를 내림하면 -2가 된다.

```js
Math.floor(1.9); // 1
Math.floor(9.1); // 9
Math.floor(-1.9); // -2
Math.floor(-9.1); // -10
Math.floor(1); // 1
Math.floor(); // NaN
```

### Math.sqrt

Math.sqrt 메서드는 인수로 전달된 숫자의 제곱근을 반환한다.

```js
Math.sqrt(9); // 3
Math.sqrt(-9); // NaN
Math.sqrt(2); // 1.414213562373095
Math.sqrt(1); // 1
Math.sqrt(0); // 0
Math.sqrt(); // NaN
```

### Math.random

Math.random 메서드는 임의의 난수( 랜덤 숫자)를 반환한다. Math.random 메서드가 반환한 난수는 0 에서 1미만의 실수다. 즉, 0은 포함되지만 1은 포함되지 않는다.

```js
Math.random(); // 0 에서 1미만의 랜덤 실수 (0.820872083921)

const random = Math.floor(Math.random() * 10 + 1);
console.log(random); // 1에서 10 범위의 정수
```

### Math.pow

Math.pow 메서드는 첫 번째 인수를 밑으로, 두 번째 인수를 지수로 거듭제곱한 결과를 반환한다.

```js
Math.pow(2, 8); // 256
Math.pow(2, -1); // 0.5
Math.pow(2); // NaN
```

```js
// ES7 지수 연산자
2 ** (2 ** 2); // 16
Math.pow(Math.pow(2, 2), 2); // 16
```

### Math.max

Math.max 메서드는 전달받은 인수 중에서 가장 큰 수를 반환한다. 인수가 전달되지 않으면 =Infinity를 반환한다.

```js
Math.max(1); // 1
Math.max(1, 2); // 2
Math.max(1, 2, 3); // 3
Math.max(); // -Infinity
```

#### Math.min

Math.min 메서드는 전달받은 인수 중에서 가장 작은 수를 반환한다. 인수가 전달되지 않으면 Infinity를 반환한다.

```js
Math.min(1); // 1
Math.min(1, 2); // 1
Math.min(1, 2, 3); // 1
Math.min(); // Infinity
```
