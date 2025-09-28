# 모던 자바스크립트 Deep Dive

## 27장 배열

## 배열이란

배열은 여러 개의 값을 순차적으로 나열한 자료구조다.

```jsx
const arr = ["apple", "banana", "orange"];

arr[0]; // apple
arr[1]; // banana
arr[2]; // orange

arr.length; //3
```

- 배열이 가지고 있는 값을 **요소**라고 부른다.
- 자신의 위치를 나타내는 0이상의 정수인 **인덱스**를 갖는다.
- 배열은 요소의 개수, 즉 배열의 길이를 나타내는 **length 프로퍼티**를 갖는다

```jsx
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]); // 'apple', 'banana', 'orange';
}

typeof arr; //object
```

- 배열은 인덱스와 length프로퍼티를 갖기 때문에 for문을 통해 순차적으로 요소에 접근할 수 있다.
- 배열은 객체 타입이다.

배열은 객체지만 일반 객체와는 구별되는 독특한 특징이 있다.
|구분|객체|배열|
|---|---|---|
|구조|프로퍼티 키와 프로퍼티 값| 배열|
|값의 참조|프로퍼티 키|인덱스|
|값의 순서|X|O|
|length 프로퍼티|X|O|

### 자바스크립트 배열은 배열이 아니다

자료구조에서 말하는 배열은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조를 말한다. 즉, 배열의 요소는 하나의 데이터 타입으로 통일되어 있으며 서로 연속적으로 인접해 있다. 이러한 배열을 **밀집 배열** 이라한다.

자바스크립트의 배열은 자료구조에서 말하는 일반적인 의미의 배열과 다르다. 즉, 배열의 요소를 위한 각각의 메모리 공간은 동일한 크기를 갖지 않아도 되며, 연속적으로 이어져 있지 않을 수도 있다. 배열의 요소가 연속적으로 이어져 있지 않는 배열을 **희소 배열** 이라한다. **자바스크립트의 배열은 일반적인 배열의 동작을 흉내 낸 특수한 객체다.**

자바스크립트 배열은 인덱스를 나타내는 문자열을 프로퍼티 키로 가지며, length 프로퍼티를 갖는 특수한 객체다.

자바스크립트 배열은 인덱스로 배열 요소에 접근하는 경우에는 일반적인 배열보다 느리지만 요소를 삽입 또는 삭제하는 경우에느 일반적인 배열보다 빠르다.

## length 프로퍼티와 희소 배열

length 프로퍼티는 요소의 개수, 즉 배열의 길이를 나타내는 0 이상의 정수를 값으로 갖는다. length 프로퍼티의 값은 빈 배열일 경우 0이며, 빈 배열이 아닐 경우 가장 큰 인덱스에 1을 더한 것과 같다.

length 프로퍼티의 값은 배열의 요소를 추가하거나 삭제하면 자동 갱신된다.

```jsx
const arr = [1, 2, 3];
console.log(arr.length); //3

arr.push(4);
console.log(arr.length); //4

arr.pop();
console.log(arr.length); //4
```

length 프로퍼티 값은 요소 개수, 즉 배열의 길이를 바탕으로 결정되지만 임의의 숫자 값을 명시적으로 할당할 수도 있다.

```jsx
const arr = [1, 2, 3, 4, 5];
arr.length = 3;
console.log(arr); // [1, 2, 3]
```

주의할 것은 현재 length 프로퍼티 값보다 큰 숫자 값을 할당하는 경우다. 이때 length 프로퍼티 값은 변경되지만 실제로 배열의 길이가 늘어나지는 않는다.

```jsx
const arr = [1];
arr.length = 3;

console.log(arr.length); //3
console.log(arr); // [1, empty * 2]
```

이처럼 배열의 요소가 연속적으로 위치하지 않고 일부가 비어 있는 배열을 희소 배열이라 한다.

```jsx
const sparse = [, 2, , 4];

console.log(sparse.length); // 4
console.log(sparse); // [empty, 2, empty, 4]
```

희소배열은 length와 배열 요소의 개수가 일치하지 않는다. 희소 배열은 length는 희소 배열의 실제 요소 개수보다 언제나 크다.

자바스크립트에서는 희소배열을 허용하지만 사용하지 않는 것이 좋다. 희소 배열은 연속적인 값의 집합이라는 배열의 기본적인 개념과 맞지 않으며, 성능에도 좋지 않은 영향을 준다.

## 배열 생성

### 배열 리터럴

객체와 마찬가지로 배열도 다양한 생성 방식이 있다. 가장 일반적이고 간편한 배열 생성 방식은 배열 리터럴이다.

```jsx
const arr=[1,2,3];

const arr=[];

consr arr=[1,,3]; //희소 배열
```

### Array 생성자 함수

Object 생성자 함수를 통해 객체를 생성할 수 있듯이 Array 생성자 함수를 통해 배열을 생성할 수도 있다. Array 생성자 함수는 전다로딘 인수의 개수에 따라 다르게 동작하므로 주의가 필요하다.

```jsx
// 전달된 인수가 1개이고 숫자인 경우 length 프로퍼티 값이 인수인 배열을 생성한다.

const arr = new Array(10);

console.log(arr); // [empty * 10]
console.log(arr.length); // 10

// 배열은 요소를 최대 2^32 - 1개 가질수 있다. 음수면 에러난다.
new Array(4294967295);
new Array(-1); // error

new Array(); // []

// 전달된 인수가 2개 이상이면 인수를 요소로 갖는 배열을 생성한다.
new Array(1, 2, 3); // [1, 2, 3]

// 전달된 인수가 1개지만 숫자가 아니면 인수를 요소로 갖는 배열을 생성한다.
new Array({}); //[{}]
```

### Array.of

전달된 인수를 요소로 갖는 배열을 생성한다.

```jsx
Arrat.of(1); // [1]
Arrat.of(1, 2, 3); // [1, 2, 3]
Arrat.of("string"); // ['string']
```

### Array.from

유사 배열 객체 또는 이터러블 객체를 인수로 전달받아 배열로 변환하여 반환한다.

```jsx
Array.from({ length: 2, 0: "a", 1: "b" }); //[a, b]

// 문자열은 이터러블
Array.from("Hello"); // ['H', 'e', 'l', 'l', 'o']
```

## 배열 요소의 참조

배열의 요소를 참조할 때는 대괄호 표기법을 사용한다.

```jsx
const arr = [1, 2];

console.log(arr[0]); // 1
console.log(arr[1]); // 2
console.log(arr[2]); // undefined

// 존재하지 않은 인덱스에 접근하면 undefined
```

## 배열 요소의 추가와 갱신

존재하지 않는 인덱스를 사용해 값을 할당하면 새로운 요소가 추가된다. 이때 length 프로퍼티 값은 자동 갱신된다.

```jsx
const arr = [0];

arr[1] = 1;
console.log(arr); // [0, 1]
console.log(arr.length); // 2

arr[100] = 100;
console.log(arr); // [0, 1, empty * 98, 100]
console.log(arr.length); // 101

// 이미 요소가 존재하는 요소에 값을 재할당하면 요소값이 갱신된다.

arr[1] = 10;

console.log(arr); // [0, 10, empty * 98, 100]
```

인덱스는 요소의 위치를 나타내므로 반드시 0 이상의 정수(또는 정수 형태의 문자열)를 사용해야 한다. 만약 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다. 이때 추가된 프로퍼티는 length 프로퍼티 값에 영향을 주지 않는다.

```jsx
const arr = [];
arr[0] = 1;
arr["1"] = 2;

arr["foo"] = 3;
arr.bar = 4;
arr[1.1] = 5;
arr[-1] = 6;

console.log(arr); // [1, 2, foo : 3, bar : 4 ,'1.1': 5 ,'-1' : 6]
console.log(arr.length); // 2
```

## 배열 요소의 삭제

배열은 사실 객체이기 때문에 배열의 특징 요소를 삭제하기 위해 delete연산자를 사용할 수 있다.

```jsx
const arr = [1, 2, 3];

delete arr[1];
console.log(arr); // [1, empty, 3]

console.log(arr.length); // 3
```

delete 연산자는 객체의 프로퍼티를 삭제한다. 이때 배열은 희소 배열이 돠며 length 프로퍼티의 값은 변하지 않는다. 따라서 delete 연산자보다 splice 메서드를 사용하는 것이 좋다.

```jsx
const arr = [1, 2, 3];

// arr[1]부터 1개의 요소를 삭제
arr.splice(1, 1);
console.log(arr); // [13]

console.log(arr.length); // 2
```

## 배열 메서드

배열은 사용 빈도가 높은 자료구조이므로 배열 메서드의 사용법을 잘 알아둬야 한다. **배열에는 원본 배열을 직접 변경하는 메서드와 원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메서드가 있다**.

```jsx
// 원본 배열을 직접 변경하는 메서드
const arr = [1];
arr.push(2);
console.log(arr); // [1, 2];

// 원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메서드
const result = arr.concat(3);
console.log(arr); // [1, 2];
console.log(result); // [1, 2, 3];
```

### Array.isArray

Array.isArray는 전달된 인수가 배열이면 true 아니면 false를 반환한다.

```jsx
// true
Array.isArray([1, 2]);

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

### Array.prototype.indexOf

indexOf메서드는 원본배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.

- 원본 배열에 인수로 전달한 요소가 중복되는 요소가 여러 개 있다면 첫 번째로 검색된 요소의 인덱스를 반환한다.
- 원본 배열에 인수로 전달한 요소가 존재하지 않으면 -1을 반환한다.

```jsx
const arr = [1, 2, 2, 4];
arr.indexOf(2); // 1
arr.indexOf(4); // -1

// 두 번째 인수는 검색을 시작할 인덱스다.
arr.indexOf(2, 2); // 2
```

### Array.prototype.push

push 메서드는 인수로 전달받은 모드 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.

```jsx
const arr = [1, 2];

// 인수로 전달받은 모든 값을 원본 배열 arr의 마지막 요소로 추가하고 변경된 length값을 반환한다.
let result = arr.push(3, 4);
console.log(result); // 4

console.log(arr); // [1, 2, 3, 4]

// 추가할 요소가 하나라면 length 프로퍼티를 사용하요 추가하는 것이 성능 면에서 좋다.
const arr = [1, 2];
arr[arr.length] = 3;
console.log(arr); // [1, 2, 3]
```

### Array.prototype.pop

pop메서드는 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.

```jsx
const arr = [1, 2];

let result = arr.pop();
console.log(result); // 2
```

### Array.prototype.unshift

unshift 메서드는 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.

```jsx
const arr = [1, 2];

let result = arr.unshift(3, 4);
console.log(result); // 4

console.log(arr); // [3, 4, 1, 2]
```

### Array.prototype.shift

shift 메서드는 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.

```jsx
const arr = [1, 2];
let result = arr.shift();
console.log(result); // 1

console.log(arr); // [2]
```

### Array.prototype.concat

concat 메서드는 인수로 전달된 값들을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다.

```jsx
const arr1 = [1, 2];
const arr2 = [3, 4];

let result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4]

let result = arr1.concat(3);
console.log(result); // [1, 2, 3]

let result = arr1.concat(arr2, 5);
console.log(result); // [1, 2, 3, 4, 5]
```

### Array.prototype.splice

push, pop, unshift, shift 메서드는 모두 원본 배열을 직접 변경하는 메서드이며 원본 배열의 처음이나 마지막에 요소를 추가하거나 제거한다.

원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우 splice 메서드를 사용한다. splice 메서드는 3개의 매개변수가 있으며 원본 배열을 직접 변경한다.

- start : 원본 배열의 요소를 제거하기 시작할 인덱스다.
- deleteCount : 원본 배열의 요소를 제거하기 시작할 인덱스인 start부터 제거할 요소의 개수다.
- items : 제거한 위치에 삽입할 요소들의 목록이다.

```jsx
const arr= [1,2,3,4];

// 원본 배열의 인덱스 1부터 2개의 요소를 제거하고 그 자리에 새로운 요소 20, 30을 삽입한다.
cosnt result = arr.splice(1,2,20,30);

// 제거한 요소가 배열로 반환된다.
console.log(result); // [2,3];

// splice 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 20, 30, 4]
```

splice 메서드의 두 번째 인수, 즉 제거할 요소의 개수를 0으로 지정하면 아무런 요소도 제거하지 않고 새로운 요소들을 삽입한다.

```jsx
const arr = [1, 2, 3, 4];
const result = arr.splice(1, 0, 100);

console.log(arr); // [1, 100, 2, 3, 4]
console.log(result); // []
```

splice 메서드의 세 번째 인수, 즉 제거한 위치에 추가할 요소들의 목록을 전달하지 않으면 원본 배열에서 지정된 요소를 제거하기만 한다.

```jsx
const arr = [1, 2, 3, 4];

const result = arr.splice(1, 2);

console.log(arr); // [1, 4]
console.log(result); // [2, 3]
```

splice 메서드의 두 번째 인수, 즉 제거할 요소의 개수를 생략하면 첫 번째 인수로 전달된 시작 인덱스부터 모든 요소를 제거한다.

```jsx
const arr = [1, 2, 3, 4];

const result = arr.splice(1);

console.log(arr); // [1]
console.log(result); // [2, 3, 4]
```

배열에서 특정 요소를 제거하려면 indexOf 메서드를 통해 특정 요소의 인덱스를 취득한 다음 splice 메서드를 사용한다.

```jsx
const arr = [1, 2, 3, 1, 2];

// 배열 array에서 item 요소를 제거한다. item 요소가 여러 개 존재하면 첫번째 요소만 제거한다.
function remove(array, item) {
  const index = array.indexOf(item);

  if (index !== -1) array.splice(index, 1);

  return array;
}

console.log(remove(arr, 2)); //[1, 3, 1, 2]
console.log(remove(arr, 10)); //[1, 3, 1, 2]
```

filter 메서드를 사용하여 특정요소를 제거할 수도 있다. 하지만 특정 요소가 중복된 경우 모두 제거된다.

```jsx
const arr = [1, 2, 3, 1, 2];

function removeAll(array, item) {
  return array.filter((v) => v !== item);
}

console.log(removeAll(arr, 2)); // [1, 3, 1];
```

### Array.prototype.slice

slice 메서드는 인수로 전달된 범위의 요소들을 복사하여 배열로 반환한다.
slice 메서드는 두 개의 매개변수를 갖는다.

- start : 복사를 시작할 인덱스다. 음수인 경우 배열의 끝에서의 인덱스를 나타낸다. 예를 들어, slice(-2)는 배열의 마지막 두 개의 요소를 복사하여 배열로 반환한다.
- end : 복사를 종료할 인덱스다. 이 인덱스에 해당하는 요소는 복사되지 않는다. end는 생략 가능하며 생략 시 기본값은 length 프로퍼티 값이다.

```jsx
const arr = [1, 2, 3];
arr.slice(0, 1); //[1];

arr.slice(1, 2); //[2];

console.log(arr); //[1, 2, 3] 원본 배열은 변경x

arr.slice(1); // [2, 3]

arr.slice(-1); // [3]
arr.slice(-2); // [2, 3]

const copy = arr.slice(); //인수를 모두 생략하면 원본 배열의 복사본을 생성하여 반환한다.

console.log(copy); // [1, 2, 3]
console.log(copy === arr); // false

// 얕은 복사를 통해 생성된다.
```

### Array.prototype.join

join 메서드는 원본 배열의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 문자열, 즉 구분자로 연결한 문자열을 반환한다. 구분자는 생략 가능하며 기본 구분자는 콤마다.

```jsx
const arr = [1, 2, 3, 4];
arr.join(); // '1,2,3,4'
arr.join(""); // '1234'
arr.join(":"); // '1:2:3:4'
```

### Array.prototype.reverse

reverse 메서드는 원본 배열의 순서를 반대로 뒤집는다. 이때 원본 배열이 변경된다. 반환값은 변경된 배열이다.

```jsx
const arr = [1, 2, 3];
const result = arr.reverse();

console.log(arr); // [3, 2, 1]
console.log(result); // [3, 2, 1]
```

### Array.prototype.fill

ES6에서 도입된 fill 메서드는 인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채운다. 이때 원본 배열이 변경된다.

```jsx
const arr = [1, 2, 3];
arr.fill(0);
console.log(arr); // [0, 0, 0]
```

```jsx
const arr = [1, 2, 3];
arr.fill(0, 1);
console.log(arr); // [1, 0, 0]
```

```jsx
const arr = [1, 2, 3, 4, 5];

// 인수로 전달받은 값 0을 배열의 인덱스 1부터 3이전(인덱스 3 미포함)까지 요소로 채운다
arr.fill(0, 1, 3);
console.log(arr); // [1, 0, 0, 4, 5]
```

### Array.prototype.includes

ES7에서 도입된 includes 메서드는 배열 내에 특정 요소가 포함되어 있는지 확인하여 ture 또는 false를 반환한다. 첫번째 인수로 검색할 대상을 지정한다.

```jsx
const arr = [1, 2, 3];
arr.includes(2); // true
arr.includes(100); //false

// 배열에 요소 1이 포함되어 있는지 인데스 1부터 확인한다.
arr.includes(1, 2); // false

// 배열에 요소 3이 포함되어 있는지 인덱스 2(arr.length - 1)부터 확인한다.
arr.includes(3, -1); // true
```

### Array.prototype.flat

ES10에서 되입된 flat 메서드는 인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화 한다.

```jsx
[1, [2, 3, 4, 5]].flat(); // [1, 2, 3, 4, 5]
```

중첩 배열을 평탄화할 깊이를 인수로 전달할 수 있다. 기본값은 1이다. 인수로 Infinity를 전달하면 중첩 배열 모두를 평탄화 한다.

```jsx
[1, [2, [3, [4]]]].flat(); // [1, 2, [3, [4]]];
[1, [2, [3, [4]]]].flat(1); // [1, 2, [3, [4]]];

[1, [2, [3, [4]]]].flat(2); // [1, 2, 3, [4]];
// 2번 평탄화한 것과 같다.
[1, [2, [3, [4]]]].flat().flat(); // [1, 2, 3, [4]];

[1, [2, [3, [4]]]].flat(Infinity); // [1, 2, 3, 4];
```

## 배열 고차 함수

고차 함수는 함수를 인수로 전달받거나 함수를 반환하는 함수를 말한다. 고차 함수는 외부 상태의 변경이나 가변 데이터를 피하고 **불변성**을 지향하는 함수형 프로그래밍에 기반을 두고 있다.

함수형 프로그래밍은 순수 함수와 보조 함수의 조합을 통해 로직 내에 존재하는 **조건문과 반복문을 제거**하여 복삽성을 해결하고 **변수의 사용을 억제**하여 상태변경을 피하려는 프로그래밍 패러다임이다. 함수형 프로그래밍은 순수 함수를 통해 부수 효과를 최대한 억제하여 오류를 피하고 프로그램의 안정성을 높이려는 노력의 일환이다.

### Array.prototype.sort

sort 메서드는 배열의 요소를 정렬한다. 원본 배열을 직접 변경하며 정렬된 배열을 반환한다.

```jsx
const fruits = ["Banana", "Orange", "Apple"];
fruits.sort();
console.log(fruits); //['Apple', 'Banana', 'Orange']

const fruits = ["바나나", "오렌지", "사과"];
fruits.sort();
console.log(fruits); //['바나나', '사과', '오렌지']
```

sort메서드는 기본적으로 오름차순으로 정렬 하므로 내림차순으로 정렬하고 싶으면 sort메서드 사용 후 reverse 메서드를 사용하면 된다.

문자열 요소로 이루어진 배열의 정렬은 아무 문제 없지만 숫자는 주의가 필요하다.

```jsx
const points = [40, 100, 1, 5, 2, 25, 10];

points.sort();

console.log(points); // [1, 10, 100, 2, 25, 40, 5]
```

sort 메서드의 기본 정렬 순서는 유니코드 코드 포인트의 순서를 따른다.
배열의 요소가 숫자 타입이라도 일시적으로 문자열로 변환한 후 유니코드 포인트의 순서를 기준으로 정렬한다.

```jsx
["2", "10"].sort(); // ['10', '2']
[2, 10].sort(); // [10, 2]
```

따라서 숫자를 정렬할 때는 sort메서드에 정렬 순서를 정의하는 비교 함수를 인수로 전달해야 한다. 비교 함수는 양수나 음수 또는 0을 반환해야 한다. 비교 함수의 반환값이 0보다 작으면 비교 함수의 첫 번째 인수를 우선하여 정렬하고, 0이면 정렬하지 않으며, 0보다 크면 두 번째 인수를 우선하여 정렬한다.

```jsx
const points = [40, 100, 1, 5, 2, 25, 10];
points.sort((a, b) => a - b);
console.log(points); // [1, 2, 5, 10, 25, 40, 100]
```

객체를 요소로 갖는 배열을 정렬하는 예제는 다음과 같다.

```jsx
const todos = [
  { id: 4, content: "JavaScript" },
  { id: 1, content: "HTML" },
  { id: 2, content: "CSS" },
];

function compare(key) {
  // 프로퍼티 값이 문자열인 경우 산수연산으로 비교하면 NaN이 나오므로 비교 연산
  return (a, b) => (a[key] > b[key] ? 1 : a[key] < b[key] ? -1 : 0);
}

todos.sort(compare("id"));
console.log(todos);
/*
[
  {id:1, content:'HTML'},
  {id:2, content:'CSS'},
  {id:4, content:'JavaScript'}
]
*/
```

### Array.prototype.forEach

forEach 메서드는 for문을 대체할 수 있는 고차 함수다. forEach 메서드는 자신의 내부에서 반복문을 실행한다.
즉, forEach 메서드는 반복문을 추상화한 고차 함수로서 내부에서 반복문을 통해 자신을 호출한 배열을 순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출한다.

```jsx
const numbers = [1, 2, 3];
const pows = [];
numbers.forEach((item) => pows.push(item ** 2));
console.log(pows); // [1, 4, 9]
```

forEach메서드는 콜백 함수를 호출할 때 3개의 인수, 즉 forEach 메서드를 호출한 배열의 요소값과 인덱스, forEach 메서드를 호출한 배열(this)을 순차적으로 전달한다.

```jsx
[1, 2, 3].forEach((item, index, arr) => {
  console.log(
    `요소값 : ${item}, 인덱스 : ${index}, this : ${JSON.stringify(arr)}`
  );
});
/*
요소값 : 1, 인덱스 : 0, this : [1, 2, 3]
요소값 : 2, 인덱스 : 1, this : [1, 2, 3]
요소값 : 3, 인덱스 : 2, this : [1, 2, 3]
*/
```

forEach 메서드는 원본 배열을 변경하지 않는다. 하지만 콜백 함수를 통해 원본 배열을 변경할 수는 있다.

```jsx
const numbers = [1, 2, 3];

numbers.forEach((item, index, arr) => {
  arr[index] = item ** 2;
});
console.log(numbers); // [1, 4, 9]
```

forEach 메서드의 반환값은 언제나 undefined 이다.

```jsx
const result = [1, 2, 3].forEach(console.log);
console.log(result); // undefined
```

forEach 메서드의 두 번째 인수로 forEach 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달할 수 있다.

forEach 메서드의 콜백 함수 내부의 this와 multifly 메서드 내부의 this를 일치시키려면 forEach 메서드의 두 번째 인수로 forEach 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달한다.

```jsx
class Numbers {
  numberArray = [];

  multifly(arr) {
    arr.forEach(function (item) {
      this.numberArray.push(item * item);
    }, this);
  }
}

const numbers = new Numbers();
numbers.multifly([1, 2, 3]);
console.log(numbers.numberArray); // [1, 4, 9]
```

더 나은 방법으로는 화살표 함수를 사용하는 것이다.

```jsx
class Numbers {
  numberArray = [];

  multifly(arr) {
    arr.forEach((item) => this.numberArray.push(item * item));
  }
}

const numbers = new Numbers();
numbers.multifly([1, 2, 3]);
console.log(numbers.numberArray); // [1, 4, 9]
```

forEach 메서드는 break, continue문을 사용할 수 없다. 다시 말해 중간에 순회를 중단할 수 없다.

희소 배열의 경우 존재하지 않는 요소는 순회 대상에서 제외된다.

```jsx
const arr = [1, , 3];

arr.forEach((v) => console.log(v)); // 1, 3
```

### Array.prototype.map

map 메서드는 자신을 호풀한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. 그리고 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.

```jsx
const numbers = [1, 4, 9];

const roots = numbers.map((item) => Math.sqrt(item));

console.log(roots); // [1, 2, 3]
console.log(numbers); // [1, 4, 9]
```

map 메서드는 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다. map 메서드는 요소값을 다른 값으로 매핑한 새로운 배열을 생성하기 위한 고차 함수다.

map 메서드가 생성하여 반환하는 새로운 배열의 length프로퍼티 값은 map 메서드를 호출한 배열의 length 값과 반드시 일치한다.

map 메서드도 콜백 함수를 호출할 때 3개의 인수, 즉 forEach 메서드를 호출한 배열의 요소값과 인덱스, forEach 메서드를 호출한 배열(this)을 순차적으로 전달한다.

```jsx
[1, 2, 3].map((item, index, arr) => {
  console.log(
    `요소값 : ${item}, 인덱스 : ${index}, this : ${JSON.stringify(arr)}`
  );
  return item;
});
/*
요소값 : 1, 인덱스 : 0, this : [1, 2, 3]
요소값 : 2, 인덱스 : 1, this : [1, 2, 3]
요소값 : 3, 인덱스 : 2, this : [1, 2, 3]
*/
```

forEach 메서드와 마찬가지로 map 메서드의 두번째 인수로 map 메서드의 콜백 함수 내부에서 this로 사용 객체를 전달할 수 있다.

```jsx
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }

  add(arr) {
    return arr.map(function (item) {
      return this.prefix + item;
    }, this);
  }
}
const prefixer = new Prefixer("-webkit-");
console.log(prefixer.add(["transition", "user-select"]));
//['-webkit-transition','-webkit-user-select']
```

더 나은 방법은 화살표 함수를 사용하는 것이다.

```jsx
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }

  add(arr) {
    return arr.map((item) => this.prefix + item);
  }
}
const prefixer = new Prefixer("-webkit-");
console.log(prefixer.add(["transition", "user-select"]));
//['-webkit-transition','-webkit-user-select']
```

### Array.prototype.filter

filter 메서드는 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. 그리고 콜백 함수의 반환값이 ture인 요소로만 구성된 새로운 배열을 반환한다.

```jsx
const numbers = [1, 2, 3, 4, 5];

const odds = numbers.filter((itme) => item % 2);
console.log(odds); //[1, 3, 5]
```

forEach 메서드는 undefined를 반환하고, map 메서드는 콜백함수의 반환값들로 구성된 새로운 배열을 반환하지만 filter 메서드는 콜백함수의 반환값이 true인 요소만 추출한 새로운 배열을 반환한다.
**filter 메서드가 생성하여 반환한 새로운 배열의 length 프로퍼티 값은 filter 메서드를 호출한 배열의 length 프로퍼티 값과 같거나 작다.**

filter 메서드도 콜백 함수를 호출할 때 3개의 인수, 즉 forEach 메서드를 호출한 배열의 요소값과 인덱스, forEach 메서드를 호출한 배열(this)을 순차적으로 전달한다.

```jsx
[1, 2, 3].filter((item, index, arr) => {
  console.log(
    `요소값 : ${item}, 인덱스 : ${index}, this : ${JSON.stringify(arr)}`
  );
  return item % 2;
});
/*
요소값 : 1, 인덱스 : 0, this : [1, 2, 3]
요소값 : 2, 인덱스 : 1, this : [1, 2, 3]
요소값 : 3, 인덱스 : 2, this : [1, 2, 3]
*/
```

filter 메서드는 자신을 호출한 배열에서 특정 요소를 제거하기 위해 사용할 수도 있다.

```jsx
class Users {
  constructor() {
    this.users = [
      { id: 1, name: "Lee" },
      { id: 2, name: "Kim" },
    ];
  }

  findById(id) {
    return this.users.filter((user) => user.id === id);
  }

  remove(id) {
    this.users = this.users.filter((user) => user.id !== id);
  }
}

const users = new User();
let user = users.findById(1);
console.log(user); // [{ id: 1, name: "Lee" }]

users.remove(1);
user = users.findById(1);
console.log(user); // []
```

### Array.prototype.reduce

reduce 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. 그리고 콜백 함수의 반환값을 다음 순회 시에 콜백 함수의 첫 번째 인수로 전달하면서 콜백 함수를 호출하여 **하나의 결과값**을 만들어 반환한다.

reduce 메서드는 첫 번째 인수로 콜백함수, 두번째 인수로 초기값을 전달받는다. reduce 메서드의 콜백 함수에는 4개의 인수, 초기값 또는 콜백 함수의 이전 반환값, reduce 메서드를 호출한 배열의 요소값과 인덱스, reduce 메서드를 호출한 배열 자체, 즉 this가 전달된다.

```jsx
const sum = [1, 2, 3, 4].reduce(
  (accumulator, currentValue, index, array) => accumulator + currentValue,
  0
);

console.log(sum); //10
```

#### reduce 메서드의 다양한 활용법

```jsx
// 평균 구하기
const values = [1, 2, 3, 4, 5, 6];
const average = values.reduce((acc, cur, i, { length }) => {
  return i === length - 1 ? (acc + cur) / length : acc + cur;
}, 0);
console.log(average); // 3.5
```

```jsx
// 최대값 구하기
const values = [1, 2, 3, 4, 5];
const max = values.reduce((acc, cur) => (acc > cur ? acc : cur), 0);
console.log(max); // 5

// 최대값 구할때는 Math.max 메서드를 사용하는 것이 더 직관적이다
```

```jsx
// 요소의 중복 횟수 구하기
const fruits = ["banana", "apple", "orange", "orange", "apple"];

const count = fruits.reduce((acc, cur) => {
  acc[cur] = (acc[cur] || 0) + 1;
  return acc;
}, {});

console.log(count); // { banana: 1, apple: 2, orange: 2 }
```

```jsx
// 중첩 배열 평탄화
const values = [1, [2, 3], 4, [5, 6]];
const flatten = values.reduce((acc, cur) => acc.concat(cur), []);
// [1] => [1, 2, 3] => [1, 2, 3, 4] => [1, 2, 3, 4, 5, 6]

console.log(flatten); // [1, 2, 3, 4, 5, 6]

// 중첩 배열을 평탄화할때는 flat 메서드를 사용하는 것이 더 직관적이다.
```

```jsx
// 중복 요소 제거
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];
const result = values.reduce(
  (unique, valmi, _values) =>
    _values.indexOf(val) === i ? [...unique, val] : unique,
  []
);

console.log(result); // [1, 2, 3, 4, 5]

// 중복 요소를 제거할 때는 filter메서드를 사용하는 것이 더 직관적이다.
// 또는 중복되지 않는 유일한 값들의 집합인 Set을 사용할 수도 있다. 중복 요소를 제거할 때는 이 방법을 추천한다.
```

reduce 메서드의 두 번째 인수로 전달하는 초기값은 옵션이지만 안제나 초기값을 전달하는 것이 안전하다.

reduce 메서드로 객체의 특정 프로퍼티 값을 합산하는 경우를 보자.

```jsx
const products = [
  { id: 1, price: 100 },
  { id: 2, price: 200 },
  { id: 3, price: 300 },
];

const priceSum = products.reduce((acc, cur) => acc.price + cur.price);

console.log(priceSum); //NaN
```

첫번째 순회시 acc는 `{ id: 1, price: 100 }`이고 cur은 `{ id: 2, price: 200 }`인데 `acc.price + cur.price` 하게되면 숫자 300이 전달된다. 숫자값에 price라는 속성값이 없으므로 계산할 수 없어 NaN이 나오게된다. 그래서 초기값을 전달 하는 것이 안전하다.

```jsx
const products = [
  { id: 1, price: 100 },
  { id: 2, price: 200 },
  { id: 3, price: 300 },
];

const priceSum = products.reduce((acc, cur) => acc + cur.price, 0);

console.log(priceSum); // 600
```

### Array.prototype.some

some 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다. 이때 every 메서드는 콜백함수의 반환값이 단 한 번이라도 참이면 true, 모두 거짓이면 false를 반환한다.

```jsx
[5, 10, 15].some((item) => item > 10); // true
[5, 10, 15].some((item) => item < 0); // false

["apple", "banana", "mango"].some((item) => item === "banana"); //true

// 빈 배열일 경우 언제나 false
[].some((item) => item > 3); // false
```

### Array.prototype.every

every 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다. 이때 every 메서드는 콜백함수의 반환값이 모두 참이면 true, 단 한 번이라도 거짓이면 false를 반환한다.

```jsx
[5, 10, 15].every((item) => item > 3); // true
[5, 10, 15].every((item) => item > 10); // false

// 빈 배열일 경우 언제나 true
[].every((item) => item > 3); //true
```

### Array.prototype.find

find 메서드는 자신을 호출한 배열의 요소를 순회 하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫 번째 요소를 반환한다.

```jsx
const users = [
  { id: 1, name: "Lee" },
  { id: 2, name: "Kim" },
  { id: 2, name: "Choi" },
  { id: 3, name: "Park" },
];

// id가 2인 첫 번째 요소를 반환한다. find 메서드는 배열이 아니라 요소를 반환 한다.
users.find((user) => user.id === 2); // { id: 2, name: "Kim" }
users.find((user) => user.id === 5); // undefined
```

### Array.prototype.findIndex

findIndex 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫 번째 요소의 인덱스를 반환한다.

```jsx
const users = [
  { id: 1, name: "Lee" },
  { id: 2, name: "Kim" },
  { id: 2, name: "Choi" },
  { id: 3, name: "Park" },
];

users.findIndex((user) => user.id === 2); // 1
users.findIndex((user) => user.id === "park"); // 3

function predicate(key, value) {
  return (item) => item[key] === value;
}

users.findeIndex(predicate("id", 2)); // 1
users.findeIndex(predicate("name", "park")); // 3
```

### Array.prototype.flatmap

flatMap 메서드를 통해 새로운 배열을 평탄화한다. 즉, map 메서드와 flat 메서드를 순차적으로 실행하는 효과가 있다.

```jsx
const arr = ["hello", "world"];

const arr2 = arr.map((x) => x.split("")).flat();
console.log(arr2);
// ['h','e','l','l','o','w','o','r','l','d']

const arr3 = arr.flatMap((x) => x.split(""));
console.log(arr3);
// ['h','e','l','l','o','w','o','r','l','d']
```

단, flatMap 메서드는 flat 메서드처럼 인수를 전달하여 평탄화 깊이를 지정할 수는 없고 1단계만 평탄화한다.

```jsx
const arr = ["hello", "world"];

// flatMap은 1단계만 평탄화한다.
arr.flatMap((str, index) => [index, [str, str.length]]);
// [[0, ['hello', 5]], [1, ['world', 5]]] => [0, ['hello', 5], 1, ['world', 5]]

arr.map((str, index) => [index, [str, str.length]]).flat(2);
// [[0, ['hello', 5]], [1, ['world', 5]]] => [0, 'hello', 5, 1, 'world', 5]
```
