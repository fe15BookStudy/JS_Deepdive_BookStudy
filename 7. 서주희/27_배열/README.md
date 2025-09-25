# 27. 배열

### 배열이란? 

- 배열은 여러 개의 값을 순차적으로 나열한 자료 구조.

배열 리터럴을 통해 생성한 다음의 배열을 보면

```JavaScript
const arr = ['apple' , 'banana' , 'orange'];
// 3개의 요소로 이루어짐 
// apple의 인덱스는 0, banana는 1, orange는 2
```

배열이 가지고 있는 값을 **요소**라 부른다. 자바스크립트의 모든 값 ( 원시값, 객체, 함수, 배열 등 ) 은 배열의 요소가 될 수 있다.

배열의 요소는 배열에서 자신의 위치를 나타내는 0이상의 정수인 **인덱스**를 갖는다. ( 보통 0 부터 시작)

요소에 접근할 때는 대괄호 표기법을 사용함

```JavaScript
arr[0] // -> 'apple'
arr[1] // -> 'banana'
arr[2] // -> 'orange'
```

배열은 요소의 개수, 즉 배열의 길이는 나타내는 **length 프로퍼티**를 갖는다.

```JavaScript
arr.length // -> 3
```

자바스크립트에 배열이라는 타입은 존재하지 않는다. 배열은 객체 타입이다.

```JavaScript
typeof arr // -> object
```

배열은 객체지만 일반 객체와는 구별되는 독특한 특징이 있다.

일반 객체와 배열을 구분하는 가장 명확한 차이는 **값의 순서**와 **length 프로퍼티**다. 

```JavaScript
const arr = [1,2,3];

// 반복문으로 자료구조를 순서대로 순회하기 위해서는 자료구조의 요소에 순서대로 접근할 수 있어야 하며
// 자료구조의 길이를 알 수 있어야 한다.

for (let i = 0; i < arr.length; i++ ) {
  console.log(arr[i]); // 1 2 3 
}
```

배열의 장점은 순차적으로 요소에 접근할 수도 있고, 마지막부터 역순으로 접근할 수도 있으며, 특정 위치부터 순차적으로 요소에 접근할 수도 있다는 것이다. 

이는 배열이 인덱스, 즉 값의 순서와 length 프로퍼티를 갖기 때문에 가능한 것이다.

<br>

### 자바스크립트 배열은 배열이 아니다

배열의 요소는 하나의 데이터 타입으로 통일되어 있으며 서로 연속적으로 인접해 있다. 이러한 배열을 **밀집 배열** 이라 한다.

이처럼 일반적인 의미의 배열은 각 요소가 동일한 데이터 크기를 가지며, 빈틈없이 연속적으로 이어져 있으므로 다음과 같이 인덱스를 통해 단 한번의 연산으로 임의의 요소에 접근할 수 있다 ( `시간 복잡도 O(1)` ) . 이는 매우 효율적이며 고속으로 동작한다.

```
검색 대상 요소의 메모리 주소 = 배열의 시작 메모리 주소 + 인덱스 * 요소의 바이트 수 
```

이처럼 배열은 인덱스를 통해 매우 효율적으로 요소에 접근할 수 있다는 장점이 있다. 하지만 정렬되지 않은 배열에서 특정한 요소를 검색하는 경우 배열의 모든 요소를 특정 요소를 발견할 때까지 차례대로 검색 ( `시간 복잡도 O (n)`) 해야 한다.


자바스크립트의 배열은 지금까지 살펴본 자료구조에서 말하는 일반적인 의미의 배열과 다르다. 자바스크립트에서 배열의 요소를 위한 각각의 메모리 공간은 동일한 크기를 갖지 않아도 되며, `연속적으로 이어져 있지 않을 수도 있다` -> **희소 배열**


### length 프로퍼티와 희소 배열

length 프로퍼티는 요소의 개수를 나타내는 0이상의 정수를 값으로 갖는다. 

```JavaScript
const arr = [1, 2 ,3];
console.log(arr.length); //3

//요소 추가
arr.push(4);
//요소를 추가하면 length 프로퍼티의 값이 자동 갱신된다.
console.log(arr.length); //4

//요소 삭제
arr.pop();
//요소를 삭제하면 length 프로퍼티의 값이 자동 갱신된다.
console.log(arr.length); //3
```

```JavaScript
const arr = [1,2,3,4,5];

//현재 length 프로퍼티 값인 5보다 작은 숫자 값 3을 length 프로퍼티에 할당
arr.length = 3;

//배열의 길이가 5에서 3으로 줄어든다.
console.log(arr); // [1,2,3]
```

length 프로퍼티값보다 큰 숫자 값을 할당하는 경우, length 프로퍼티 값은 변경되지만 실제로 배열의 길이가 늘어나지는 않는다.

```JavaScript
const arr = [1];

//현재 length 프로퍼티 값인 1보다 큰 숫자 값 3을 length 프로퍼티에 할당
arr.length = 3;

// length 프로퍼티 값은 변경되지만 실제로 배열의 길이가 늘어나지는 않는다.
console.log(arr.length); //3
console.log(arr); //[1, empty x 2]
```

위 예제의 출력 결과에서 empty x 2 는 실제로 추가된 배열의 요소가 아니다. 즉, arr[1] 과 arr[2] 에는 값이 존재하지 않는다.

이처럼 현재 length 프로퍼티 값보다 큰 숫자 값을 length 프로퍼티에 할당하는 경우 length 프로퍼티 값은 성공적으로 변경되지만 실제 배열에는 아무런 변함이 없다. 값 없이 비어 있는 요소를 위해 메모리 공간을 확보하지 않으며 빈 요소를 생성하지도 않는다.

```JavaScript
console.log(Object.getOwnPropertyDescriptors(arr));

/*
{
    '0' : {value : 1, writable : true, enumerable: ture, configurable: true},
    length : {value : 3, enumerable : false, configurable :false}
}
*/

이렇게 배열의 요소가 연속적으로 위치하지 않고 일부가 비어있느 배열을 희소 배열이라 한다. 자바스크립트는 희소 배열을 문법적으로 허용한다.

```


일반적인 배열의 length 는 배열 요소 개수, 즉 배열의 길이와 언제나 일치한다. 하지만 **희소 배열은 length와 배열 요소의 개수가 일치하지 않는다. 희소 배열의 length는 희소 배열의 실제 요소 개수보다 언제나 크다.**

**배열에는 같은 타입의 요소를 연속적으로 위치시키는 것이 최선이다.**

<br>

### 배열 생성

#### 배열 리터럴

가장 일반적이고 간편한 배열 생성 방식은 배열 리터럴을 사용하는 것이다.

배열 리터럴은 0개 이상의 요소를 쉼표로 구분하여 대괄호 ([])로 묶는다. 배열 리터럴은 객체 리터럴과 달리 프로퍼티 키가 없고 값만 존재한다.

```JavaScript
cost arr = [1,2,3];
console.log(arr.length); //3
```

배열 리터럴에 요소를 하나도 추가하지 않으면 배열의 길이, 즉 length 프로퍼티 값이 0인 빈 배열이 된다.

```JavaScript
const arr = [];
console.log(arr.length); //0
```
배열 리터럴에 요소를 생략하면 희소 배열이 생성된다.

```JavaScript
const arr = [ 1, , 3] ; // 희소 배열

//희소 배열의 length 배열의 실제 요소 개수보다 언제나 크다.
console.log(arr.length); //3
console.log(arr); //[1,empty,3]
console.log(arr[1]); //undefined
```

#### Array 생성자 함수

object 생성자 함수를 통해 객체를 생성할 수 있듯이 Array 함수를 통해 배열을 생성할 수도 있다.

Array 생성자 함수는 전달된 인수의 개수에 따라 다르게 동작하므로 주의가 필요하다.

- 전달된 인수가 1개이고 숫자인 경우 length 프로퍼티 값이 인수인 배열을 생성한다.

```JavaScript
const arr = new Array(10);

console.log(arr); // [empty x 10]
console.log(arr.length); //10
```

이때 생성된 배열은 희소 배열이다. length 프로퍼티 값은 0이 아니지만 실제로 배열의 요소는 존재하지 않는다.

```JavaScript
console.log(Object.getOwnPropertyDescriptors(Arr));

/*
{   
   length : { value : 10, writable, enumerable : false, configurable : false}   
}
*/

```

배열은 요소를 최대 2^32 - 1(4,294,967,295)개 가질 수 있다.따라서 Array 생성자 함수에 전달할 인수는 0 또는 2 ^ 32 - 1 (4,294,967,295) 이하인 양의 정수이어야 한다. 전달된 인수가 범위를 벗어나면 RangeError가 발생한다.

```JavaScript
// 배열은 인수를 최대 4,294,967,295개 가질 수 있다.
new Array (4294967295);

// 전달된 인수가 0~ 4,294,967,295를 벗어나면 RangeError가 발생한다.
new Array (4294967296); // RangeError : Invaild array length

// 전달된 인수가 음수이면 에러가 발생한다.
new Array(-1); // Range Error : Invalid array length
```

- 전달된 인수가 없는 경우 빈 배열을 생성한다. 즉, 배열 리터럴 []과 같다.

```JavaScript
new Array(); // -> []
```

- 전달된 인수가 2개 이상이거나 숫자가 아닌 경우 인수를 요소로 갖는 배열을 생성한다.

```JavaScript
// 전달된 인수가 2개 이상이면 인수를 요소로 갖는 배열을 생성한다.
new Array (1,2,3); // -> [1,2,3]

// 전달된 인수가 1개지만 숫자가 아니면 인수를 요소로 갖는 배열을 생성한다.
new Array({}); // -> [{}]
```

Array 생성자 함수는 new 연산자와 함께 호출하지 않더라도, 즉 일반 함수로서 호출해도 배열을 생성하는 생성자 함수로 동작한다. 이는 Array 함수 내부에서 new.target을 확인하기 때문이다.

```JavaScript
Array(1,2,3); //-> [1,2,3]
```

#### Array.of

ES6에서 도입된 Array.of 메서드는 전달된 인수를 요소로 갖는 배열을 생성한다. Array.of 는 Array 생성자 함수와 다르게 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성한다.

```JavaScript
// 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성한다.
Array.of(1); // ->[1]

Array.of(1,2,3); // ->[1,2,3]

Array.of('string'); // ->['sting']
```

#### Array.from

ES6에서 도입된 Array.from 메서드는 유사 배열 객체 또는 이터러블 객체를 인수로 전달받아 배열로 변환하여 반환한다.

```JavaScript
//유사 배열 객체를 변환하여 배열을 생성한다.
Array.from({length: 2,0 : 'a', 1: 'b'}) // -> ['a', 'b']

//이터러블을 변환하여 배열을 생성한다. 문자열을 이터러블이다.
Array.from('Hello'); //-> ['H','e','l','l','o']
```

Array.from 을 사용하면 두 번째 인수로 전달한 콜백 함수를 통해 값을 만들면서 요소를 채울 수 있다. Array.from 메서드는 두 번째 인수로 전달한 콜백 함수에 첫 번째 인수에 의해 생성된 배열의 요소값과 인덱스를 순차적으로 전달하면서 호출하고, 콜백 함수의 반환값으로 구성된 배열을 반환한다.

```JavaScript
//Array.from에 length만 존재하는 유사 배열 객체를 전달하면 undefined를 요소로 채운다.
Array.from({ length: 3 }) ; // -> [undefined, undefined, undefined]

//Array.from은 두 번째 인수로 전달한 콜백 함수의 반환값으로 구성된 배열을 반환한다.
Array.from({length:3} , (_,) => i ); // -> [0, 1 ,2 ]
```

### 배열 요소의 참조

배열의 요소를 참조할 때는 대괄호를 사용한다.

대괄호 안에는 인덱스가 와야 한다.

```JavaScript
const arr = [1,2];

// 인덱스가 0 인 요소를 참조
console.log(arr[0]); //1
// 인덱스가 1인 요소를 참조
console.log(arr[1]); //2
```

존재하지 않는 요소에 접근하면 undefined가 반환된다.

```JavaScript
const arr = [1,2];

// 인덱스가 2인 요소를 참조. 배열 arr에는 인덱스가 2인 요소가 존재하지 않는다.
console.log(arr[2]); //undefined
```

배열은 사실 인덱스를 나타내는 문자열을 프로퍼티 키로 갖는 객체다. 따라서 존재하지 않는 프로퍼티 키로 객체의 프로퍼티에 접근했을 때 undefined를 반환하는 것처럼 배열도 존재하지 않는 요소를 참조하면 undefined를 반환한다.

같은 이유로 희소 배열의 존재하지 않는 요소를 참조해도 undefined가 반환된다.

```JavaScript
// 희소 배열
const arr = [1,3];

// 배열 arr 에는 인덱스가 1인 요소가 존재하지 않는다.
console.log(Object.getOwnPropertyDescriptors(arr));

/*

{
  '0' : { value : 1, writable: true, enumerable: true, configurable: true},
  '2' : { value : 3, writable: true, enumerable: true, configurable: true},
  length : { value : 3, writable: true, enumerable: , configurable: true},

}

*/

// 존재하지 않는 요소를 참조하면 undefined가 반환된다.
console.log(arr[1]); //undefined
console.log(arr[3]); //undefined
```

### 배열 요소의 추가와 갱신

객체에 프로퍼티를 동적으로 추가할 수 있는 것처럼 배열에도 요소를 동적으로 추가할 수 있다. 존재하지 않는 인덱스를 사용해 값을 할당하면 새로운 요소가 추가된다. 이때 length 프로퍼티 값은 자동 갱신된다.

```JavaScript
const arr = [0];

// 배열 요소의 추가
arr[1] = 1;

console.log(arr); //[0,1]
console.log(arr.length); //2
```

만약 현재 배열의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 희소 배열이 된다.

```JavaScript
arr[100] = 100;

console.log(arr); // [0,1,empty x 98, 100]
console.log(arr.length); //101
```

이때 인덱스로 요소에 접근하여 명시적으로 값을 할당하지 않은 요소는 생성되지 않는 것에 주의하라.

```JavaScript
// 명시적으로 값을 할당하지 않은 요소는 생성되지 않는다.
console.log(Object.getOwnPropertyDescriptors(arr));

/*

{
  '0' : {value : 0, writable: true, enumerable: true, configurable: true},
  '1' : {value : 1, writable: true, enumerable: true, configurable: true},
  '100' : {value : 100, writable: true, enumerable: true, configurable: true},
  length : {value : 101, writable: true, enumerable: false, configurable: false},

}

*/
```

이미 요소가 존재하는 요소에 값을 재할당하면 요소값이 갱신된다.

```JavaScript
//요소값의 갱신
arr[1] = 10;

console.log(arr); //[0,10, empty x 98, 100]
```

인덱스는 요소의 위치를 나타내므로 반드시 0 이상의 정수를 사용해야 한다. 만약 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다. 이때 추가된 프로퍼티는 length 프로퍼티 값에 영향을 주지 않는다.

```JavaScript
const arr = [];

// 배열 요소의 추가
arr[0] = 1;
arr['1'] = 2;

// 프로퍼티 추가
arr['foo'] = 3;
arr.bar = 4;
arr[1.1] = 5;
arr[-1] = 6;

console.log(arr); // [1,2, foo:3, bar: 4, '1.1' :5, '-1' : 6]

//프로퍼티는 length에 영향을 주지 않는다.
console.log(arr.length); //2
```


### 배열 요소의 삭제

