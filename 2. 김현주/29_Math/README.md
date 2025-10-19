1) Math 객체의 성격
- 표준 빌트인 객체이면 생성자 함수가 아님.
→ new Math() ❌, 인스턴스 없음.
- 전부 정적 프로퍼티/메서드만 제공: Math.PI, Math.abs(...) 같이 Math에 직접 호출.
2) 자주 쓰는 프로퍼티
Math.PI
- 원주율 π(≈ 3.141592653589793).
```javascript
Math.PI    // 3.141592653589793
```
3) 숫자 변환(암묵적 ToNumber) 규칙 메모
대부분의 Math.*(x)는 먼저 x를 숫자로 변환한다.
- '10' → 10, '' → 0, null → 0, true → 1, false → 0
- undefined → NaN, {} → NaN
- [] → 0, [1,2,3] → NaN (배열이 여러 값을 담으면 숫자로 못 바꿔서 NaN)
4) 절대값
Math.abs(x)
- 절대값 반환. 숫자로 바꾸지 못하면 NaN.
```javascript
Math.abs(-1);        // 1
Math.abs('');        // 0
Math.abs(null);      // 0
Math.abs(undefined); // NaN
Math.abs([1,2]);     // NaN
```
5) 반올림/올림/내림

음수에서의 동작이 자주 헷갈려!

Math.round(x) – 반올림(가장 가까운 정수)
- .5는 위쪽(+) 방향으로 간다.
```javascript
Math.round(1.4);   // 1
Math.round(1.6);   // 2
Math.round(-1.4);  // -1
Math.round(-1.6);  // -2
Math.round(-1.5);  // -1  (tie는 +∞ 방향)
Math.round();      // NaN
```
Math.ceil(x) – 올림(소수점 올려서 더 큰 정수)
```javascript
Math.ceil(1.4);   // 2
Math.ceil(-1.4);  // -1   (올리면 0쪽으로 접근)
```
Math.floor(x) – 내림(소수점 버려서 더 작은 정수)
```javascript
Math.floor(1.9);   // 1
Math.floor(-1.1);  // -2   (내리면 -∞ 쪽으로)
```
소수점 자리 반올림 팁
x를 소수 첫째자리에서 반올림 → Math.round(x * 10) / 10
(부동소수점 오차 주의: 0.1 + 0.2 !== 0.3)
```
6) 제곱근
Math.sqrt(x)
- x의 제곱근. x < 0이면 NaN.
```javascript
Math.sqrt(9);      // 3
Math.sqrt(2);      // 1.41421356...
Math.sqrt(0);      // 0
Math.sqrt(-1);     // NaN
Math.sqrt(null);   // 0  (null → 0)
```
7) 난수
Math.random()
- [0, 1) 구간의 부동소수 난수 (0 ≤ x < 1).
- 정수 범위 뽑기(포함 범위):
```javascript
// [min, max] 범위의 정수
const randInt = (min, max) =>
  Math.floor(Math.random() * (max - min + 1)) + min;

randInt(1, 10); // 1~10
```
- 0은 포함 가능하지만 1은 절대 포함되지 않음.

8) 거듭제곱
Math.pow(base, exponent) / ES7 지수 연산자 **
- 같은 의미. **가 가독성 좋고 최신 스타일.
```javascript
Math.pow(2, 8);  // 256
2 ** 8;          // 256

Math.pow(2 ** 2, 2 ** 2); // 16
0 ** -1;         // Infinity (0의 음수 지수는 1/0)
Math.pow(NaN, 2) // NaN
```
9) 최댓값/최솟값
Math.max(a, b, c, ...) / Math.min(a, b, c, ...)
- 전달된 인수들 중 최댓값/최솟값.
- 인수가 하나도 없으면:
Math.max() → -Infinity, Math.min() → Infinity
- 배열을 그대로 주면 안 됨 (배열 한 덩어리 → 숫자 변환 시 NaN가 되기 쉬움).
```javascript
Math.max(1, 2, 3);             // 3
Math.max();                    // -Infinity
Math.min();                    //  Infinity
Math.max([1,2,3]);             // NaN (배열 한 개를 인수로 줌)
```
배열에서 최댓값/최솟값 구하기
1. 스프레드 문법(권장)
```javascript
const arr = [1, 2, 3];
Math.max(...arr); // 3
Math.min(...arr); // 1
```
2. apply 사용(구문 이해용)
```javascript
const arr = [1, 2, 3];
Math.max.apply(null, arr); // 3
Math.min.apply(null, arr); // 1
// thisArg는 의미 없으므로 null/undefined 사용
```
⚠️ 매우 큰 배열(수십만 요소)에서 스프레드/apply는 호출 인수 길이 제한에 걸릴 수 있음.
그런 경우 **루프나 reduce**로 처리:
```javascript
const maxOf = arr => arr.reduce((m, x) => x > m ? x : m, -Infinity);
const minOf = arr => arr.reduce((m, x) => x < m ? x : m,  Infinity);
```