# 27장 배열

## 27.1 배열이란?

- 배열은 여러 개의 값을 순차적으로 나열한 자료구조다. 배열은 사용 빈도가 매우 높은 기본적인 자료구조다.

```jsx
const arr = ["apple", "banana", "orange"];
```

- 위 배열은 배열 리터럴을 통해 생성한 것이다. 배열이 가지고 있는 값을 **요소**라고 부른다. JS의 모든 값(원시 값, 객체, 함수, 배열 등)은 배열의 요소가 될 수 있다.
- 배열의 요소는 배열에서 자신의 위치를 나타내는 0이상의 정수인 **인덱스**를 갖는다. ( apple의 인덱스는 0, banan의 인덱스는 1, orange의 인덱스는 2)
- 요소에 접근할 때는 대괄호 표기법을 사용한다. 대괄호 내에는 접근하고 싶은 요소의 인덱스를 지정한다.

```jsx
arr[0]; // apple
arr[1]; // banana
arr[2]; // orange
```

- 배열은 요소의 개수, 즉 배열의 길이를 나타내는 **length 프로퍼티**를 갖는다.
- 배열은 인덱스와 length 프로퍼티를 갖기 때문에 for문을 통해 순차적으로 요소에 접근이 가능하다.
- 배열은 객체 타입이다. JS에 배열이라는 타입은 존재하지 않는다.

```jsx
arr.length; // 3

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]); //' apple', 'banana', 'orange'
}
```

## 27.2 자바스크립트 배열은 배열이 아니다

- 자바스크립트의 배열은 일반적인 의미의 배열과 다르다. 배열의 요소를 위한 각각의 메모리 공간은 동일한 크기를 갖지 않아도 되며, 연속적으로 이어져 있지 않을 수도 있다.
- **자바스크립트의 배열은** **일반적인 배열의 동작을 흉내 낸 특수한 객체다.** 인덱스를 나타내는 문자열을 프로퍼티 키로 가지며, length 프로퍼티를 갖는 특수한 객체다.
- 자바스크립의 배열은 인덱스로 배열 요소에 접근하는 경우에는 일반적인 배열보다 느리지만 요소를 삽입 또는 삭제하는 경우에는 일반적인 배열보다 빠르다.

## 27.3 length 프로퍼티와 희소 배열

- length 프로퍼티는 요소의 개수, 즉 배열의 길이를 나타내는 0 이상의 정수를 값으로 갖는다. length 프로퍼티의 값은 빈 배열일 경우 0이며, 빈 배열이 아닐 경우 가장 큰 인덱스의 1을 더한 것과 같다.

```jsx
[].length[(1, 2, 3)].length; // -> 0 // -> 3
```

- length 프로퍼티의 값은 **배열에 요소를 추가하거나 삭제하면 자동 갱신된다.**
- length 프로퍼티 값은 요소의 개수, 즉 배열의 길이를 바탕으로 결정되지만 임의의 숫자 값을 명시적으로 할당할 수도 있다.

```jsx
const arr = [1, 2, 3, 4, 5];

arr.length = 3;

// 배열의 길이가 5에서 3으로 줄어든다.
console.log(arr); // [1, 2, 3]
```

- 현재 length 프로퍼티 값보다 큰 숫자 값을 할당할 경우 length 프로퍼티 값은 변경되지만 **실제로 배열의 길이가 늘어나지는 않는다.** 값 없이 비어 있는 요소를 위해 메모리 공간을 확보하지 않으며 빈 요소를 생성하지도 않는다.
- **배열의 요소가 연속적으로 위치하지 않고 일부가 비어 있는 배열**을 **희소 배열**이라 한다. JS는 희소 배열을 문법적으로 허용한다. 즉 배열의 중간이나 앞부분이 비어있을 수도 있다. 하지만 배열을 생성할 경우 희소 배열을 생성하지 않도록 주의해야 한다. **배열에는 같은 타입의 요소를 연속적으로 위치시키는 것이 최선이다.**
- 희소 배열은 length와 배열 요소의 개수가 일치하지 않는다. **희소 배열의 length는 희소 배열의 실제 요소 개수보다 언제나 크다.**

## 27.4 배열 생성

### 27.4.1 배열 리터럴

- 객체와 마찬가지로 배열도 다양한 생성 방식이 있다. 가장 일반적이고 간편한 배열 생성 방식은 배열 리터럴을 사용하는 것이다.
- 배열 리터럴은 0개 이상의 요소를 쉼표로 구분하여 대괄호로 묶는다. 배열 리터럴은 객체 리터럴과 달리 **프로퍼티 키가 없고 값만 존재한다.**

```jsx
const arr = [1, 2, 3];
console.log(arr.length); // 3

const arr1 = [];
console.log(arr1.length); // 0
```

### 27.4.2 Array 생성자 함수

- Object 생성자 함수를 통해 객체를 생성할 수 있듯이 Array 생성자 함수를 통해 배열을 생성할 수도 있다. Array 생성자 함수는 전달된 인수의 개수에 따라 다르게 동작하므로 주의가 필요하다.

```jsx
const arr = new Array(10);

console.log(arr); // [empty * 10]
console.log(arr.length); // 10
```

- 전달된 인수가 없는 경우 빈 배열을 생성한다. 즉, 배열 리터럴 []과 같다.

```jsx
new Array(); *// ->[]*
```

- 전달된 인수가 2개 이상이거나 숫자가 아닌 경우 인수를 요소로 갖는 배열을 생성한다.

```jsx
new Array(1, 2, 3); // [1, 2, 3]

// 전달된 인수가 1개지만 숫자가 아니면 인수를 요소로 갖는 배열을 생성한다.
new Array({}); // -> [{}]
```

- Array.of 메서드를 쓰면 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성한다.

```jsx
Array.of(1); // -> [1]
Array.of(1, 2, 3); // -> [1, 2, 3]
Array.of("string"); // -> ['string']
```

## 27.5 배열 요소의 참조

- 배열의 요소를 참조할 때에는 []를 사용하고 대괄호 안에는 인덱스가 와야 한다. 인덱스는 객체의 프로퍼티 키와 같은 역할을 한다.

```jsx
const arr = [1, 2];

console.log(arr[0]); // 1
console.log(arr[1]); // 2
```

- 존재하지 않는 요소에 접근하면 undefined가 반환된다.

## 27.6 배열 요소의 추가와 갱신

- 객체의 프로퍼티를 동적으로 추가할 수 있는 것처럼 배열에도 요소를 동적으로 추가할 수 있다. 추가하는 방법은 존재하지 않는 인덱스를 사용해 값을 할당하면 새로운 요소가 추가된다. 이때 length 프로퍼티는 값은 자동 갱신된다.

```jsx
const arr = [0];

// 배열 요소 추가
arr[1] = 1;

console.log(arr); // [0, 1]
console.log(arr.length); // 2
```

- 만약 현재 배열의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 희소 배열이 된다. **이때 인덱스로 요소에 접근하여 명시적으로 값을 할당하지 않은 요소는 생성되지 않는다는 것에 주의하자.**
- 인덱스는 0 이상의 정수 또는 정수 형태의 문자열을 사용해야 한다. 만약 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다. 이때 추가된 프로퍼티는 length 프로퍼티 값에 영향을 주지 않는다.

```jsx
const arr = [];

// 배열 요소 추가
arr[0] = 1;
arr["1"] = 2;

// 프로퍼티 추가
arr["foo"] = 3;
arr.bar = 4;
arr[1.1] = 5;

console.log(arr); // [1, 2, foo: 3, bar: 4, '1.1': 5]

// 프로퍼티는 length에 영향을 주지 않는다.
console.log(arr.length); // 2
```

## 27.7 배열 요소의 삭제

- 배열은 사실 객체이기 때문에 배열의 특정 요소를 삭제하기 위해 객체와 마찬가지로 delete 연산자를 사용할 수 있다. 하지만 delete 연산자는 희소 배열이 될 수 있어 사용하지 않는 것이 좋다.

```jsx
const arr = [1, 2, 3];

// 배열 요소 삭제
delete arr[1];
console.log(arr); // [1, empty, 3]

// length 프로퍼티에 영향을 주지 않는다. 즉, 희소 배열이 된다.
console.log(arr.length); // 3
```

- 희소 배열을 만들지 않으면서 배열의 특정 요소를 완전히 삭제하려면 **Array.prototype.splice** 메서드를 사용한다.
- **Array.prototype.splice(삭제를 시작할 인덱스, 삭제할 요소 수)**

```jsx
const arr = [1, 2, 3];

// Array.prototype.splice(삭제를 시작할 인덱스, 삭제할 요소 수)
// arr[1]부터 1개의 요소를 제거
arr.splice(1, 1);
console.log(arr); // [1, 3]

// length 프로퍼티가 자동 갱신된다.
console.log(arr.length); // 2
```

## 27.8 배열 메서드

- Array 생성자 함수는 정적 메서드를 제공하며, 배열 객체의 프로토타입인 Array.prototype(배열 인스턴스들이 공통으로 쓰는 메서드들)은 프로토타입 메서드를 제공한다.
- **인스턴스란?**

  ```jsx
  // a는 배열 인스턴스이다. 인스턴스는 어떤 “타입/클래스/생성자”로부터 만들어진
  // 개별 객체 한 개이다.
  // 같은 타입이라도 인스턴스는 각자 다른 객체(식별성/메모리 위치)
  const a = [1, 2, 3];

  const p = new Person("Jisub"); // p는 Person "인스턴스"
  ```

- 배열에는 원본 배열(배열 메서드를 호출한 배열)을 직접 변경하는 메서드와 원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 **메서드가 있다. 가급적 원본 배열을 직접 변경하지 않는 메서드를 사용하는 편이 좋다.**

```jsx
const arr = [1];

// push 메서드는 원본 배열(arr)을 직접 변경한다.
arr.push(2);
console.log(arr); // [1, 2]

// concat 메서드는 원본 배열(arr)을 직접 변경하지 않고 새로운 배열을 생성하여 반환한다.
const result = arr.concat(3);
console.log(arr); // [1, 2]
console.log(result); // [1, 2, 3]
```

### 27.8.1 Array.isArray

- Array.isArray는 Array 생성자 함수의 정적 메서드로 전달된 인수가 배열이면 true, 배열이 아니면 false를 반환한다.

```jsx
Array.isArray([1, 2]); //true
Array.isArray(new Array()); // true

Array.isArray({}); // false
Array.isArray(1); // false
Array.isArray("Arr"); // false
```

### 27.8.2 Array.prototype.indexOf

- indexOf 메서드는 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.
- 원본 배열에 인수로 전달한 요소와 중복되는 요소가 여러 개 있다면 **첫 번째로 검색된 요소의 인덱스를 반환한다.**
- 원본 배열에 인수로 전달한 **요소가 존재하지 않으면 -1을 반환한다.**
- **indexOf 메서드는 배열에 특정 요소가 존재하는지 확인할 때 유용하다.**

```jsx
const arr = [1, 2, 2, 3];

// 배열 arr에서 요소 2를 검색하여 첫 번째로 검색된 요소의 인덱스를 반환한다.
arr.indexOf(2); // 1
arr.indexOf(4); // -1
// 두 번째 인수는 검색을 시작할 인덱스다. 두 번째 인수를 생략하면 처음부터 검색한다.
arr.indexOf(2, 2); // 2
```

- ES7에서 도입된 **Array.prototype.includes** 메서드를 사용하면 가독성이 더 좋다.

```jsx
const foods = ["apple", "banana", "orange"];

// foods 배열에 'orange' 요소가 존재하는지 확인한다.
if (!foods.includes("orange")) {
  // foods 배열에 'orange' 요소가 존재하지 않으면 추가한다.
  foods.push("orange");
}
```

### 27.8.3 Array.prototype.push

- push 메서드는 인수로 전달받은 모든 값을 **원본 배열의 마지막 요소로 추가**하고 **변경된 length 프로퍼티 값을 반환한다.** push 메서드는 **원본 배열을 직접 변경한다.**

```jsx
const arr = [1, 2];

// 인수로 전달받은 모든 값을 원본 배열 arr의 마지막 요소로 추가하고 변경된 length 값을 반환한다.
let result = arr.push(3, 4);
console.log(result); // 4

console.log(arr); // [1, 2, 3, 4]
```

- push 메서드는 성능 면에서 좋지 않다. 마지막 요소로 추가할 요소가 하나뿐이라면 length 프로퍼티를 사용하는 것이 더 빠르다.

```jsx
const arr = [1, 2];

// arr.push(3)과 동일한 처리를 한다. 이 방법이 push 메서드보다 빠르다.
arr[arr.length] = 3;
console.log(arr); // [1, 2, 3]
```

### 27.8.4 Array.prototype.pop

- pop 메서드는 원본 배열에서 마지막 요소를 제거하고 **제거한 요소를 반환한다.** 원본 배열이 빈 배열이면 undefined를 반환한다.

```jsx
const arr = [1, 2];

let result = arr.pop();
console.log(result); // 2

// pop 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1]
```

- push와 pop 메서드를 사용하면 스택을 쉽게 구현할 수 있다. 스택은 후입 선출 LIFO(Last-In-First-Out) 방식의 자료구조이다.

### 27.8.5 Array.prototype.unshift

- unshift 메서드는 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 **변경된 length 프로퍼티 값을 반환한다.** unshift 메서드는 **원본 배열을 직접 변경한다.**

```jsx
const arr = [1, 2];

// 인수로 전달받은 모든 값을 원본 배열 arr의 마지막 요소로 추가하고 변경된 length 값을 반환한다.
let result = arr.unshift(3, 4);
console.log(result); // 4

console.log(arr); // [3, 4, 1, 2]
```

### 27.8.6 Array.prototype.shift

- shift 메서드는 원본 배열에서 첫 번째 요소를 제거하고 **제거한 요소를 반환한다.** 원본 배열이 빈 배열이면 undefined를 반환한다. shift 메서드도 **원본 배열을 직접 변경한다.**

```jsx
const arr = [1, 2];

let result = arr.shift();
console.log(result); // 2

// shift 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [2]
```

- shift 메서드와 push 메서드를 사용하면 큐를 쉽게 구현할 수 있다. 큐는 선입 선출 FIFO(First-In-First-Out) 방식의 자료구조이다.

### 27.8.7 Array.prototype.concat

- concat 메서드는 **인수로 전달된 값들(배열 또는 원시값)을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다. 인수로 전달한 값이 배열인 경우 배열을 해체하여 새로운 배열의 요소로 추가한다.** **원본 배열은 변경되지 않는다.**
- push와 unshift 메서드는 concat 메서드로 대체할 수 있다. 유사하게 동작하지만 다음과 같은 미묘한 차이가 있다.
  - push/unshift는 원본 배열을 직접 변경하지만 concat 메서드는 원본 배열을 변경하지 않고 새로운 배열을 반환한다. 따라서 push/unshift 메서드를 사용할 경우 원본 배열을 반드시 변수에 저장해 두어야 하고 concat 메서드를 사용할 경우 반환값을 반드시 변수에 할당받아야 한다.

```jsx
const arr1 = [1, 2];
const arr2 = [3, 4];

// 배열 arr2를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환한다.
let result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4]

// 원본 배열은 변경되지 않는다.
console.log(arr1); // [1, 2]
```

### 27.8.8 Array.prototype.splice

- 원본 배열의 **중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우 s**plice 메서드를 사용한다. splice 메서드는 3개의 매개변수가 있으며 **원본 배열을 직접 변경한다.**
  - start: 원본 배열의 요소를 제거하기 시작할 인덱스다. start만 지정하면 원본 배열의 start부터 모든 요소를 제거한다. start가 -1이면 마지막 요소를 가리키고 -n이면 마지막에서 n번째 요소를 가리킨다.
  - deleteCount: 원본 배열의 요소를 제거하기 시작할 인덱스인 start부터 제거할 요소의 개수다. 0인 경우 아무런 요소도 제거되지 않고 새로운 요소들을 삽입할 수 있다.
  - items: 제거한 위치에 삽입할 요소들의 목록이다. 생략할 경우 원본 배열에서 요소들을 제거하기만 한다.

```jsx
const arr1 = [1, 2, 3, 4];

// 원본 배열의 인덱스 1부터 2개의 요소를 제거하고 그 자리에 새로운 요소 20, 30을 삽입한다.
const result = arr1.splice(1, 2, 20, 30);

console.log(result); // [2, 3]

// splice 메서드는 원본 배열을 직접 변경한다.
console.log(arr1); // [1, 20, 30, 4]
```

### 27.8.9 Array.prototype.slice

- slice 메서드는 **인수로 전달된 범위의 요소들을 복사하여 배열로 반환한다.** **원본 배열은 변경되지 않는다.** slice 메서드는 두 개의 매개변수를 갖는다.
  - start: 복사를 시작할 인덱스다. 음수인 경우 배열의 끝에서의 인덱스를 나타낸다.
  - end: 복사를 종료할 인덱스다. 이 인덱스에 해당하는 요소는 복사되지 않는다. end는 생략이 가능하며 생략 시 기본 값은 length 프로퍼티 값이다.
- slice 메서드의 인수를 모두 생략하면 원본 배열의 복사본을 생성하여 반환한다.

```jsx
const arr1 = [1, 2, 3];

arr1.slice(0, 1); // -> [1]

arr1.slice(1, 2); // -> [2]

// 원본은 변경되지 않는다.
console.log(arr); // [1, 2, 3]
```

### 27.8.10 Array.prototype.join

- join 메서드는 원본 배열의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 문자열, 즉 구분자로 연결한 문자열을 반환한다. 구분자는 생략 가능하며 기본 구분자는 콤마(,)다.

```jsx
const arr1 = [1, 2, 3, 4];

// 기본 구분자는 콤마다.
arr1.join(); // -> '1,2,3,4'

arr1.join(""); // -> '1234'

arr1.join(":"); // -> '1:2:3:4'
```

### 27.8.11 Array.prototype.reverse

- reverse 메서드는 원본 배열의 순서를 반대로 뒤집는다. 이때 원본 배열이 변경된다. 반환값은 변경된 배열이다.

```jsx
const arr1 = [1, 2, 3];
const result = arr1.reverse();

// reverse 메서드는 원본 배열을 직접 변경한다.
console.log(arr1); // [3, 2, 1]
//반환값은 변경된 배열이다.
console.log(result); // [3, 2, 1]
```

### 27.8.12 Array.prototype.fill

- ES6에서 도입된 fill 메서드는 인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채운다. 이때 원본 배열이 변경된다.

```jsx
const arr1 = [1, 2, 3];

// 인수로 전달받은 값 0을 배열의 처음부터 끝까지 요소로 채운다.
arr1.fill(0);

// fill 메서드는 원본 배열을 직접 변경한다.
console.log(arr1); // [0, 0, 0]

// 인수로 전달받은 값 2를 배열의 인덱스 1부터 끝까지 요소로 채운다.
arr1.fill(2, 1);

console.log(arr1); // [0, 2, 2]

const arr2 = [1, 2, 3, 4, 5];

// 인수로 전달받은 값 0을 배열의 인덱스 1부터 3 이전(인덱스 3 미포함)까지 요소로 채운다.
arr2.fill(0, 1, 3);

console.log(arr2); // [1, 0, 0, 4, 5]
```

### 27.8.13 Array.prototype.includes

- ES7에서 도입된 includes 메서드는 배열 내에 특정 요소가 포함되어 있는지 확인하여 true 또는 false를 반환한다. 첫 번째 인수로 검색할 대상을 지정한다. 두 번째 인수로 검색을 시작할 인덱스를 전달할 수 있다. 두 번째 인수를 생략할 경우 기본 값이 0이 설정된다.

```jsx
const arr = [1, 2, 3];

// 배열에 요소 1이 포함되어 있는지 인덱스 1부터 확인한다.
arr.includes(1, 1); // -> false

// 배열에 요소 3이 포함되어 있는지 인덱스 2 부터 확인한다.
arr.includes(3, -1); // -> true
```

## 27.9 배열 고차 함수

- 고차 함수는 **함수를 인수로 전달받거나 함수를 반환하는 함수를 말한다.** JS의 함수는 일급 객체이므로 함수를 값처럼 인수로 전달할 수 있으며 반환할 수도 있다.
- 고차 함수는 외부 상태의 변경이나 **가변 데이터를 피하고 불변성을 지향**하는 함수형 프로그래밍에 기반을 두고 있다.
- 함수형 프로그래밍은 **순수 함수를 통해 부수 효과를 최대한 억제하여** 오류를 피하고 프로그램의 안정성을 높이려 한다.

### 27.9.1 Array.prototype.sort

- sort 메서드는 배열의 요소를 정렬한다. **원본 배열을 직접 변경하며 정리된 배열을 반환한다.**
- sort 메서드는 기본적으로 오름차순으로 요소를 정렬한다.

```jsx
const fruits = ["Banana", "Orange", "Apple"];

// 오름차순 정렬
fruits.sort();

// sort 메서드는 원본 배열을 직접 변경한다.
console.log(fruits);
```

- sort 메서드는 문자열 요소로 이루어진 배열의 정렬은 아무 문제가 없다. 하지만 숫자 요소로 이루어진 배열을 정렬할 때는 주의가 필요하다.

  - sort 메서드의 기본 정렬 순서는 유니코드 코드 포인트의 순서를 따른다. 배열의 요소가 숫자 타입이라 할지라도 배열의 요소를 일시적으로 문자열로 변환한 후 유니코드 코드 포인트의 순서를 기준으로 정렬한다.
  - 따라서 숫자 요소를 정렬할 때는 sort 메서드에 **정렬 순서를 정의하는 비교 함수를 인수로 전달해야 한다.** 비교 함수는 양수나 음수 또는 0을 반환해야 한다.
    - 비교 함수의 반환값 < 0 : 비교 함수의 첫 번째 인수를 우선하여 정렬.
    - 비교 함수의 반환값 = 0 : 정렬하지 않음.
    - 비교 함수의 반환값 > 0 : 두 번째 인수를 우선하여 정렬.

  ```jsx
  const points = [40, 100, 1, 5, 2, 25, 10];

  // 숫자 배열의 오름차순 정렬. 비교 함수의 반환값이 0보다 작으면 a를 우선하여 정렬한다.
  // 비교 함수 : (a, b) => a - b
  points.sort((a, b) => a - b);
  console.log(points); // [1, 2, 5, 10, 25, 40 ,100]

  points.sort((a, b) => b - a);
  console.log(points); // [100, 40, 25, 10, 5, 2, 1]
  ```

### 27.9.2 Array.prototype.forEach

- forEach 메서드는 for문을 대체할 수 있는 고차 함수다. forEach 메서드는 자신의 내부에서 반복문을 실행한다. 즉, forEach 메서드는 내부에서 반복문을 통해 자신을 호출한 배열을 순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출한다.
- for문은 반복을 위한 변수를 선언해야 하며, 조건식과 증감식으로 이루어져 있어서 함수형 프로그래밍이 추구하는 바와 맞지 않다.

```jsx
const numbers = [1, 2, 3];
const pows = [];

// forEach 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출한다.
// 요소값(item)만 인수로 전달. 인덱스와 배열 인수는 사용 안 함
numbers.forEach((item) => pows.push(item ** 2));
console.log(pows); // [1, 4, 9]

// 원본 배열은 변경되지 않는다.
console.log(numbers); // [1, 2, 3]
```

- 위의 예시에서 forEach 메서드는 numbers 배열의 모든 요소를 순회하며 콜백 함수를 반복 호출한다. numbers 배열의 요소가 3개이므로 콜백 함수도 3번 호출된다.
- forEach 메서드는 콜백 함수를 호출할 때 3개의 인수를 전달한다.
  - forEach 메서드를 호출한 배열의 요소값
  - forEach 메서드를 호출한 배열의 인덱스
  - forEach 메서드를 호출한 배열 자체(this)
- forEach 메서드는 for문과는 달리 break, continue 문을 사용할 수 없다. 따라서 **배열의 모든 요소를 빠짐없이 모두 순회하며 중간에 순회를 중단할 수 없다.**
- **forEach의 반환값은 언제나 undefined이다.(새 배열을 만드는 용도가 아니다.)**

### 27.9.3 Array.prototype.map

- map 메서드는 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 함수를 반복 호출한다. 그리고 **콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.** 이때 원본 배열은 변경되지 않는다.
- forEach **vs** map
  - 공통점: 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다.
  - 차이점: forEach는 언제나 undefined를 반환하고, **map은 콜백 함수의 반환값들로 구성된 새로운 배열을 반환하는 차이가 있다.(같은 길이의 새 배열을 만든다.)**
- **map 메서드를 호출한 배열과 map 메서드가 생성하여 반환한 배열은 1:1 매핑한다.(호출한 배열과 반환된 배열의 length 프로퍼티 값이 일치한다.)**
- forEach 메서드와 마찬가지로 map 메서드의 콜백 함수는 map 메서드를 호출한 배열의 요소값과 인덱스, this 3개의 인수를 순차적으로 전달받는다.

```jsx
const numbers = [1, 4, 9];

const roots = numbers.map((item) => Math.sqrt(item));

//위 코드는 다음과 같다.
// const roots = numbers.map(Math.sqrt);

// map 메서드는 새로운 배열을 반환한다.
console.log(roots); // [1, 2, 3]
// map 메서드는 원본 배열을 변경하지 않는다.
console.log(numbers); // [1, 4, 9]
```

### 27.9.4 Array.prototype.filter

- filter 메서드는 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다.
- **콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환한다.** 이때 원본 배열은 변경되지 않는다.

```jsx
const numbers = [1, 2, 3, 4, 5];

// 다음의 경우 numbers 배열에서 홀수인 요소만 필터링한다.(1,3,5는 나머지가 1이라 truthy 2,4는 나머지가 0이라 falsy)
const odds = numbers.filter((item) => item % 2);
console.log(odds); // [1, 3, 5]
```

- **filter 메서드가 생성하여 반환한 새로운 배열의 length 프로퍼티 값은 filter 메서드를 호출한 배열의 length 프로퍼티 값과 같거나 작다.**(위의 예시에서 새로운 배열의 length 프로퍼티 값이 3 호출한 배열의 값은 5다.)
- filter 메서드도 마찬가지로 배열의 요소값, 인덱스, filter 메서드를 호출한 배열 자체 this를 인수로 전달한다.

### 27.9.5 Array.prototype.reduce

- reduce 메서드는 모든 요소를 순회하며 인수로 전달받은 콜백 함수를 반복 호출한다.
- **콜백 함수의 반환값을 다음 순회 시에 콜백 함수의 첫 번째 인수로 전달하면서 콜백 함수를 호출하여 하나의 결과값(누적값)을 만들어 반환한다.** 이때 원본 배열은 변경되지 않는다.
- reduce 메서드는 첫 번째 인수로 콜백 함수, 두번 째 인수로 초기값을 전달받는다.
- reduce 메서드의 콜백 함수에는 4개의 인수가 전달된다.
  - 초기값 또는 콜백 함수의 이전 반환값
  - reduce 메서드를 호출한 배열의 요소값
  - reduce 메서드를 호출한 배열의 인덱스값
  - reduce 메서드를 호출한 배열 자체, this
- **reduce 메서드는 하나의 결과값을 반환한다.**
- 초기값을 설정하지 않으면 원본 배열의 첫 번째 요소가 초기값으로 전달된다. **하지만 reduce 메서드를 호출할 때는 언제나 초기값을 전달하는 것이 안전하다.**

```jsx
// 1부터 4까지 누적을 구한다.
// 인수로 콜백 함수와 초기값(0)을 전달
const sum = [1, 2, 3, 4];
const total = sum.reduce(
  (accumulator, currentValue, index, array) => accumulator + currentValue,
  0
);

console.log(total); // 10
```

- 평균 구하기

```jsx
const values = [1, 2, 3, 4, 5, 6];

// {length}는 원본 배열의 length 프로퍼티를 바로 꺼내 쓰는 문법이다.
// 따라서 values.length의 값인 6을 꺼내 쓴다.(네 번째 인수는 배열을 넘겨준 다음 length 속성만 사용)
const average = values.reduce((acc, cur, i, { length }) => {
  return i === length - 1 ? (acc + cur) / length : acc + cur;
}, 0);

console.log(average);
```

### 27.9.6 Array.prototype.some

- some 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다.
- some 메서드는 콜백 함수의 반환값이 단 한 번이라도 참이면 true, 모두 거짓이면 false를 반환한다. **즉, 배열의 요소 중에 콜백 함수를 통해 정의한 조건을 만족하는 요소가 1개 이상 존재하는지 확인하여 그 결과를 boolean 타입으로 반환한다.**
- some 메서드도 마찬가지로 배열의 요소값, 인덱스, some 메서드를 호출한 배열 자체 this를 인수로 전달한다.

```jsx
//배열의 요소 중 10보다 큰 요소가 1개 이상 존재하는지 확인
[5, 10, 15].some((item) => item > 10); // true

// 배열의 요소 중 'banana'가 1개 이상 존재하는지 확인
["apple", "banana", "mango"].some((item) => item === "banana"); // -> true

// some 메서드를 호출한 배열이 빈 배열인 경우 언제나 false를 반환한다.
[].some((item) => item > 3); // -> false
```

### 27.9.7 Array.prototype.every

- every 메서드는 some과 반대로 콜백 함수의 반환값이 모두 참이면 true, 단 한 번이라도 거짓이면 false를 반환한다.

```jsx
[5, 10, 15].every((item) => item > 3); // true

[5, 10, 15].every((item) => item > 10); // false

// every 메서드를 호출한 배열이 빈 배열인 경우 언제나 tru를 반환한다.
[].every((item) => item > 3); // -> true
```

### 27.9.8 Array.prototype.find

- find 메서드는 인수로 전달된 콜백 함수를 호출하여 **반환값이 true인 첫 번째 요소를 반환한다.** 콜백 함수의 반환값이 true인 요소가 존재하지 않는다면 undefined를 반환한다.
- find 메서드도 마찬가지로 배열의 요소값, 인덱스, find 메서드를 호출한 배열 자체 this를 인수로 전달한다.

```jsx
const users = [
  { id: 1, name: "Lee" },
  { id: 2, name: "Kim" },
  { id: 2, name: "Choi" },
  { id: 3, name: "Park" },
];

// id가 2인 첫 번째 요소를 반환한다. find 메서드는 배열이 아니라 요소를 반환한다.
users.find((user) => user.id === 2); // {id: 2, name: 'Kim'}
```

- filter는 반환값이 배열이지만 find의 반환값은 배열이 아닌 해당 요소값이다.

```jsx
// filter 메서드는 배열을 반환한다.
[1, 2, 2, 3].filter((item) => item === 2); // [2, 2]

// find 메서드는 요소를 반환한다.
[1, 2, 2, 3].filter((item) => item === 2); // 2
```

### 27.9.9 Array.prototype.findIndex

- findIndex 메서드는 인수로 전달된 콜백 함수를 호출하여 **반환값이 true인 첫 번째 요소의 인덱스를 반환한다.** 콜백 함수의 반환값이 true인 요소가 존재하지 않는다면 -1을 반환한다.
- findIndex 메서드도 마찬가지로 배열의 요소값, 인덱스, findIndex 메서드를 호출한 배열 자체 this를 인수로 전달한다.

```jsx
const users = ["Lee", "Kim", "Park"];

const index = users.findIndex((users) => users === "Park");

console.log(index); // 2
```

### 27.9.10 Array.prototype.flatMap

- flatMap 메서드는 map 메서드를 통해 생성된 새로운 배열을 평탄화한다. 즉, map 메서드와 flat 메서드를 순차적으로 실행하는 효과가 있다.
- 평탄화는 **배열 안에 또 배열이 들어있는 ‘중첩 구조’를 한 단계(또는 지정한 단계) 풀어서** 납작하게 만드는 걸 말한다.
- flatMap 메서드는 평탄화 깊이를 지정할 수 없고 1단계만 평탄화한다. map 메서드를 통해 생성된 중첩 배열의 평탄화 깊이를 지정해야 한다면 flatMap을 사용하지 말고 map 메서드와 flat 메서드를 각각 호출한다.

```jsx
const arr = ["hello", "world"];

// map과 flat을 순차적으로 실행
arr.flat((x) => x.split(""));
// -> ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']

const arr1 = ["hello", "world"];

// flatMap은 1단계만 평탄화한다.
arr.flatMap((str, index) => [index, [str, str.length]]);
// -> [0, ['hello', 5], 1, ['world', 5]]

// 평탄화 깊이를 지정해야 한다면 flatMap을 사용하지 말고 map과 flat을 각각 호출한다.
arr.map((str, index) => [index, [str, str.length]]).flat(2);
// -> [0, 'hello', 5, 1, 'world', 5]
```
