# 27. 배열

## 배열이란 ?

배열(Array)은 여러 개의 값을 순차적으로 나열한 자료구조

```js
const arr = ["apple", "banana", "orange"];
```

배열이 가지고 있는 값을 요소(element)라고 부른다.  
자바스크립트의 모든 값은 배열의 요소가 될 수 있다.  
요소는 배열에서 자신의 위치를 나타내는 0 이상의 정수인 인덱스(index)를 가진다.  
인덱스는 0부터 시작한다.

요소에 접근할 때에는

```js
arr[0]; // apple
arr[1]; // banana
arr[2]; // orange
```

대괄호 안에 인덱스를 넣어 접근한다.

배열의 요소의 개수, 길이를 나타내는 length 프로퍼티를 갖는다.

```js
arr.length; // 3
```

```js
typeof arr; // object
```

배열이라는 타입은 존재하지 않고, 객체 타입이다.

| 구분            | 객체                      | 배열          |
| --------------- | ------------------------- | ------------- |
| 구조            | 프로퍼티 키와 프로퍼티 값 | 인덱스와 요소 |
| 값의 참조       | 프로퍼티 키               | 인덱스        |
| 값의 순서       | X                         | O             |
| length 프로퍼티 | X                         | O             |

## 자바스크립트 배열은 배열이 아니다

## length 프로퍼티와 희소배열

## 배열 생성

### 배열 리터럴

배열 리터럴은 0개 이상의 요소를 쉼표로 구분하여 대괄호[]로 묶는다.  
배열 리터럴은 객체 리터럴과 달리 프로퍼티 키가 없고 값만 존재한다.

```js
const arr1 = [1, 2, 3];
console.log(arr1.length); // 3

const arr2 = [];
console.log(arr2.length); // 0

const arr3 = [1, , 3]; // 희소 배열
console.log(arr3.length); // 3
console.log(arr3); // [1, empty, 3]
console.log(arr3[1]); // undefined
```

### Array 생성자 함수

```js
const arr = new Array(10);

console.log(arr); // [empty x 10]
console.log(arr.length); // 10
```

```js
new Array(); // []
new Array({}); // [{}]
```

new 연산자와 함께 호출하지 않더라도, 배열을 생성하는 생성자 함수로 동작한다.

### Array.of

Array.of 메서드는 전달된 인수를 요소로 갖는 배열을 생성한다.

```js
Array.of(1); // [1]
Array.of(1, 2, 3); // [1, 2, 3]
Array.of("string"); // ['string']
```

### Array.from

Array.from 메서드는 유사 배열 객체 또는 이터러블 객체를 인수로 전달받아 배열로 변환하여 반환한다.

```js
// 유사 배열 객체를 변환하여 배열을 생성
Array.from({ length: 2, 0: "a", 1: "b" }); // ['a', 'b']

// 이터러블을 변환하여 배열을 생성
Array.from("Hello"); // ['H','e','l','l','o']
```

유사배열객체는 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체를 말한다.  
배열처럼 for문으로 순회할 수도 있다.

```js
const arrayLike = {
  0: "apple",
  1: "banana",
  2: "orange",
  length: 3,
};

console.log(arrayLike[0]); // "a"
console.log(arrayLike.length); // 3
console.log(arrayLike.map); // undefined (map 없음)

for (let i = 0, i < arrayLike.length; i++) {
  console.log(arrayLike[i]); // apple banana orange
}
```

## 배열 요소의 참조

배열 요소를 참조할때는 [] 대괄호 표기법을 사용하고 대괄호 안에는 인덱스가 와야한다.

```js
const arr = [1, 2];

console.log(arr[0]); // 1

// 존재하지 않는 요소에 접근하면 undefined 반환
console.log(arr[2]); // undefined
```

## 배열 요소의 추가와 갱신

객체처럼 배열에도 요소를 인덱스를 사용해 값을 동적으로 추가할 수 있다.

```js
const arr = [0];

arr[100] = 1;

console.log(arr); // [0, empty x 99, 1]
console.log(arr.length); // 101

// 인덱스를 사용해 값을 갱신할 수 있다.
arr[0] = 10;
console.log(arr); // [10, empty x 99, 1]
```

인덱스를 사용할때에는 0이상의 정수 또는 정수형태의 문자열을 사용해야 한다.
그 외의 값을 인덱스로 사용하면 요소가 생성되는 것이 아닌 프로퍼티가 생성된다.

```js
const arr = [];

arr[0] = 1;
arr["1"] = 2;

arr["foo"] = 3;
arr.bar = 4;
arr[1.1] = 5;
arr[-1] = 6;

console.log(arr); // [1, 2, foo: 3, bar: 4, '1.1': 5, '-1': 6]
console.log(arr.length); // 2
```

## 배열 요소의 삭제

배열의 특정 요소를 삭제하기 위해 delete 연산자를 사용할 수 있다.

```js
const arr = [1, 2, 3];

delete arr[1];
console.log(arr); // [1, empty, 3]

// length 프로퍼티에 영향을 주지 않는다. => 희소배열이 된다.
console.log(arr.length); // 3
```

희소배열을 만들지 않고 완전히 삭제하려면 `Array.prototype.splice` 메서드를 사용한다.

```js
const arr = [1, 2, 3];

arr.splice(1, 1);
console.log(arr); // [1, 3]

console.log(arr.length); // 2
```

## 배열 메서드

### 1. Array.isArray

전달된 인수가 배열이면 true, 배열이 아니면 false를 반환한다.

```js
// true
Array.isArray([]);
Array.isArray([1, 2]);
Array.isArray(new Array());

// false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(1);
Array.isArray("Array");
Array.isArray(true);
Array.isArray(false);
Array.isArray({ 0: 1, length: 1 });
```

### 2. Array.prototype.indexOf

해당 값의 첫 번째 인덱스 반환. 없으면 -1 반환.  
존재 유무 파악

```js
const arr = [1, 2, 2, 3];

arr.indexOf(2); // 1
arr.indexOf(4); // -1
arr.indexOf(2, 2); // 2
```

### 3. Array.prototype.push

배열의 마지막 요소로 새로운 값 추가.

```js
const arr = [1, 2];

let result = arr.push(3, 4);
console.log(result); // 4

console.log(arr); // [1, 2, 3, 4]
```

```js
// 요소를 하나만 추가한다면 push 보다 빠른 방법
const arr = [1, 2];

arr[arr.length] = 3;
console.log(arr); // [1, 2, 3]
```

### 4. Array.prototype.pop

원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환. (마지막 값 꺼내기 - 스택(후입선출))

```js
const arr = [1, 2, 3];
console.log(arr.pop()); // 3
console.log(arr); // [1, 2]
```

### 5. Array.prototype.unshift

인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 프로퍼티 값을 반환

```js
const arr = [1, 2];

let result = arr.unshift(3, 4);

console.log(arr); // [3, 4, 1, 2]
```

### 6. Array.prototype.shift

원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환 - 큐(선입선출)

```js
const arr = [1, 2];

let result = arr.shift();

console.log(result); // 1

console.log(arr); // [2]
```

### 7. Array.prototype.concat

인수로 전달된 값들을 원본 배열의 마지막 요소로 추가 후 새로운 배열 반환.  
**원본 배열은 변경되지 않는다.**

```js
const arr1 = [1, 2];
const arr2 = [3, 4];

let result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4]

let result = arr1.concat(3);
console.log(result); // [1, 2, 3]
```

### 8. Array.prototype.splice

원본 배열의 중간에 요소를 추가하거나 제거하는 메서드.  
**원본 배열 변경됨**

```js
const arr = [1, 2, 3, 4];

const result = arr.splice(1, 2, 20, 30); // 인덱스 1부터 2개를 제거하고 새로운 요소 20, 30 을 삽입

console.log(result); //[2, 3] 제거한 요소 배열로 반환
console.log(arr); // [1, 20, 30, 4] 원본 배열이 변경됨
```

```js
const arr = [1, 2, 3, 4];

const result = arr.splice(1);

console.log(result); // [2, 3, 4]
console.log(arr); // [1]
```

### 9. Array.prototype.slice

인수로 전달된 범위의 요소들을 복사하여 배열로 반환.  
**원본 배열은 변경되지 않는다.** (splice는 원본 배열 변경됨)

```js
const arr = [1, 2, 3];

arr.slice(1, 2); // [2] => arr[1] 부터 arr[2] 이전까지
arr.slice(-2); // [2, 3] => 배열의 끝에서부터 요소 두개 반환

arr.slice(); // [1, 2, 3] => 얕은 복사본. 원본과 완전히 같지 않다(!===)
```

### 10. Array.prototype.join

원본 배열의 모든 요소를 문자열로 변환 후 인수로 전달받은 문자열. 즉 구분자(,)로 연결한 문자열을 반환

```js
const arr = [1, 2, 3, 4];

arr.join(); // '1,2,3,4'
arr.join(""); // '1234'
arr.join(":"); // '1:2:3:4'
```

### 11. Array.prototype.reverse

원본 배열의 순서를 반대로 뒤집는다. -> **원본 배열 변경**

```js
const arr = [1, 2, 3];
const result = arr.reverse();

console.log(arr); // [3, 2, 1]
console.log(result); // [3, 2, 1]
```

### 12. Array.prototype.fill

인수로 전달받은 값을 배열의 처음붙터 끝까지 요소로 채운다. -> **원본 배열 변경**

```js
const arr = [1, 2, 3];
arr.fill(0);
console.log(arr); // [0, 0, 0]
```

```js
const arr = [1, 2, 3];
arr.fill(0, 1); // 값 0을 인덱스1부터 끝까지
console.log(arr); // [1, 0, 0]
```

```js
const arr = [1, 2, 3, 4, 5];
arr.fill(0, 1, 3); // 값 0을 인덱스1부터 인덱스3 이전 까지
console.log(arr); // [1, 0, 0, 4, 5]
```

### 13. Array.prototype.includes

배열 내에 특정 요소가 포함되어 있는지 확인하여 true/false 반환

```js
const arr = [1, 2, 3];

arr.includes(2); // true

arr.includes(100); // false
```

### 14. Array.prototype.flat

인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화  
중첩 배열을 평탄화할 깊이를 인수로 전달할 수 있다. 생략시 기본값은 1.

```js
[1, [2, 3, 4, 5]].flat(); // [1, 2, 3, 4, 5]
[1, [2, [3, [4]]]].flat(2); // [1, 2, 3, [4]] => 2단계 깊이까지 평탄화
```

## 배열 고차 함수

### 1. Array.prototype.sort

배열의 요소를 정리한다. **원본 배열을 변경하며** 정렬된 배열을 반환

```js
const fruits = ["Banana", "Orange", "Apple"];

fruits.sort(); // 오름차순 정렬
console.log(fruits); // ['Apple', 'Banana', 'Orange']

fruits.reverse(); // 내림차순 정렬
console.log(fruits); // ['Orange', 'Banana', 'Apple']
```

숫자는 주의할 필요가 있음. 문자열로 변환 후 유니코드 코드 포인트의 순서를 기준으로 정렬한다.

```js
const points = [40, 100, 1, 5, 2, 25, 10];

points.sort();
console.log(points); // [1, 10, 100, 2, 25, 40, 5]

scores.sort((a, b) => b - a); // 내림차순
console.log(points); // [100, 40, 25, 10, 5, 2, 1]
```

### 2. Array.prototype.forEach

for문을 대체할 수 있는 고차함수. **원본 배열을 변경하지 않는다.**  
반환값은 언제나 `undefined`

```js
const users = ["철수", "영희", "민수"];
users.forEach((name, i) => {
  console.log(`${i + 1}번째 유저: ${name}`);
});
```

### 3. Array.prototype.map

자신이 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출.  
콜백 함수의 반환값들로 구성된 새로운 배열을 반환. **원본 배열은 변경되지 않음**

```js
const prices = [1000, 2000, 3000];
const withTax = prices.map((p) => p * 1.1);
console.log(withTax); // [1100, 2200, 3300]
```

### 4. Array.prototype.filter

콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환.  
**원본 배열은 변경되지 않음**

```js
const ages = [15, 22, 18, 30];
const adults = ages.filter((a) => a >= 20);
console.log(adults); // [22, 30]
```

### 5. Array.prototype.reduce

누적 계산하여 하나의 결과값을 만들어 반환.  
**원본 배열은 변경하지 않음**

```js
const sum = [1, 2, 3, 4].reduce(
  (accumulater, currentValue, index, array) => accumulater + currentValue,
  0
);
console.log(sum); // 10
```

| 구분         | accumulator | currentValue | index | array     | 콜백 함수의 반환값              |
| ------------ | ----------- | ------------ | ----- | --------- | ------------------------------- |
| 첫 번째 순회 | 0 (초기값)  | 1            | 0     | [1,2,3,4] | 1 (accumulator + currentValue)  |
| 두 번째 순회 | 1           | 2            | 1     | [1,2,3,4] | 3 (accumulator + currentValue)  |
| 세 번째 순회 | 3           | 3            | 2     | [1,2,3,4] | 6 (accumulator + currentValue)  |
| 네 번째 순회 | 6           | 4            | 3     | [1,2,3,4] | 10 (accumulator + currentValue) |

#### 1. 평균 구하기

```js
const values = [1, 2, 3, 4, 5, 6];

const average = values.reduce((acc, cur, i, { length }) => {
  return i === length - 1 ? (acc + cur) / length : acc + cur;
}, 0);

console.log(average); // 3.5
```

#### 2. 최댓값 구하기

##### (1) reduce 이용

```js
const values = [1, 2, 3, 4, 5];

const max = values.reduce((acc, cur) => (acc > cur ? acc : cur), 0);

console.log(max); // 5
```

##### (2) Math.max 이용

```js
const values = [1, 2, 3, 4, 5];

const max = Math.max(...values);
// var max = Math.max.apply(null, values);

console.log(max); // 5
```

#### 3. 요소의 중복 횟수 구하기

```js
const fruits = ["banana", "apple", "orange", "orange", "apple"];

const count = fruits.reduce((acc, cur) => {
  acc[cur] = (acc[cur] || 0) + 1;
  return acc;
}, {});

console.log(count);
// { banana: 1, apple: 2, orange: 2 }
```

#### 4. 중첩 배열 평탄화

##### (1) reduce 이용

```js
const values = [1, [2, 3], 4, [5, 6]];

const flatten = values.reduce((acc, cur) => acc.concat(cur), []);

console.log(flatten);
// [1, 2, 3, 4, 5, 6]
```

##### (2) flat 메서드 이용

```js
console.log([1, 2, [3, 4, 5]].flat()); // [1, 2, 3, 4, 5]
console.log([1, 2, [3, [4, 5]]].flat(2)); // [1, 2, 3, 4, 5]
```

#### 5. 중복 요소 제거 -> filter가 더 직관적

```js
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];

const result = values.reduce(
  (unique, val, i, _values) =>
    _values.indexOf(val) === i ? [...unique, val] : unique,
  []
);

console.log(result);
// [1, 2, 3, 5, 4]
```

### 6. Array.prototype.some

조건을 만족하는 요소가 하나라도 있으면 true, 모두 거짓이면 false 반환  
빈 배열인 경우 언제나 false

```js
[5, 10, 15].some((item) => item > 10); // true
[5, 10, 15].some((item) => item < 0); // false
```

### 7. Array.prototype.every

모든 요소가 조건을 만족해야 true, 하나라도 거짓이면 false 반환
빈 배열인 경우 언제나 true

```js
[5, 10, 15].every((item) => item > 3); // true
[5, 10, 15].every((item) => item > 10); // false
```

### 8. Array.prototype.find

조건을 만족하는 첫 번째 값 반환

```js
const user = [
  { id : 1, name: 'Lee'}
  { id : 2, name: 'Kim'}
  { id : 3, name: 'Choi'}
  { id : 4, name: 'Park'}
];

users.find(user => user.id === 2); // {id : 2, name : 'Kim'}
```

### 9. Array.prototype.findIndex

조건을 만족하는 첫 번째 인덱스 반환

```js
const user = [
  { id : 1, name: 'Lee'}
  { id : 2, name: 'Kim'}
  { id : 3, name: 'Choi'}
  { id : 4, name: 'Park'}
];

users.findIndex(user => user.id === 2); // 1
users.findIndex(user => user.name === 'Park'); // 3
```

### 10. Array.prototype.flatMap

map과 flat 메서드를 순차적으로 실행하는 효과를 가진 메서드

```js
const arr = ["hello", "world"];

arr.flatMap((x) => x.split("")); // ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']
```
