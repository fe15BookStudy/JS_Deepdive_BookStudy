# 32. String

### String 생성자 함수

표준 빌트인 객체인 String 객체는 생성자 함수 객체다. 따라서 new 연산자와 함께 호출하여 String 인스턴스를 생성 할 수 있다.

String 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[StringData]] 내부 슬롯에 빈 문자열을 할당한 String 래퍼 객체를 생성한다.

```JavaScript
const strObj = new String();
console.log(StrObj); // String {length:0, [[PrimitiveValue]]: ""}
```

위 예제를 크롬 브라우저 개발자 도구에서 실행하면 [[PrimitiveValue]]라는 접근할 수 없는 프로퍼티가 보인다.

이는 [[String]] 내부 슬롯을 가리키는데, ES5 에서는 [[String]]를 [[PrimitiveValue]]라 불렀다.

String 생성자 함수의 인수로 문자열을 전달하면서 new 연산자와 함께 호출하면  [[StringData]] 내부 슬롯에 인수로 전달받은 문자열을 할당한 String 래퍼 객체를 생성한다.

```JavaScript
const strObj = new String('Lee');
console.log(strObj);
// String {0: "L", 1: "e", 2: "e", length: 3, [[PrimitiveValue]]: "Lee"}
```

Sting 래퍼 객체는 배열과 마찬가지로 length 프로퍼티와 인덱스를 나타내는 숫자 형식의 문자열을 프로퍼티 키로, 각 문자를 프로퍼티 값으로 갖는 유사 배열 객체이면서 이터러블이다. 

```JavaScript
console.log(strObj[0]); // L
```

단, 문자열은 원시 값이므로 변경할 수 없다. 이때 에러가 발생하지 않는다.

```JavaScript
// 문자열은 원시 값이므로 변경할 수 없다. 이때 에러가 발생하지 않는다.
strObj[0] = 'S' ;
console.log(strObj); // 'Lee'
```

String 생성자 함수의 인수로 문자열이 아닌 값을 전달하면 인수를 문자열로 강제 변환한 후, [[StringData]] 내부 슬롯에 변환된 문자열을 할당한 String 래퍼 객체를 생성한다.

```JavaScript
let strObj = new String(123);
console.log(StrObj);
// String {0 : "1", 1 : "2", 2: "3" , length : 3, [[PrimitiveValue]]: "123"}

strObj = new String(null);
console.log(strObj);
// String {0 : "n", 1: "u", 2: "l", 3: "l", length: 4, [[PrimitiveValue]]: "null"}
```

new 연산자를 사용하지 않고 String 생성자 함수를 호출하면 String 인스턴스가 아닌 문자열을 반환한다. 이를 이용하여 명시적으로 타입을 변환하기도 한다.

```JavaScript
// 숫자 타입 => 문자열 타입
String(1);  // -> "1"
String(NaN);  // -> "NaN"
String(Infinity);  // -> "Infinity"

// 불리언 타입 => 문자열 타입
String(true);  // -> "true"
String(false);  // -> "false"
```


### length 프로퍼티 

length 프로퍼티는 문자열의 문자 개수를 반환한다.

```JavaScript
'Hello'.length; //-> 5
'안녕하세요!.'length; // -> 6
```

String 래퍼 객체는 배열과 마찬가지로 length 프로퍼티를 갖는다. 그리고 인덱스를 나타내는 숫자를 프로퍼티 키로, 각 문자를 프로퍼티 값으로 가지므로 String 래퍼 객체는 유사 배열 객체다.

### String 메서드

배열에는 원본 배열 ( 배열 메서드를 호출한 배열 ) 을 직접 변경하는 메서드와 원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메서드가 있다.

하지만 String 객체에는 원본 String 래퍼 객체 ( String 메서드를 호출한 String 래퍼 객체) 를 직접 변경하는 메서드는 존재하지 않는다.

즉, String 객체의 메서드는 언제나 새로운 문자열을 반환한다. 문자열은 변경 불가능한 원시 값이기 때문에 String 래퍼 객체도 읽기 전용 객체로 제공된다.

```JavaScript
const strObj = new String('Lee');

console.log(Object.getOwnPropertyDescriptors(StrObj));

/* String 래퍼 객체는 읽기 전용 객체다. 즉, writable 프로퍼티 어트리뷰트 값이 false 다.
{
  '0' : { value : 'L' , writable : false, enumerable: true, configurable: false},
  '1' : { value : 'e' , writable : false, enumerable: true, configurable: false},
  '2' : { value : 'e' , writable : false, enumerable: true, configurable: false},
  length : { value : '3' , writable : false, enumerable: false, configurable: false},
}
*/
```

만약 String 래퍼 객체가 읽기 전용 객체가 아니라면 변경된 String 래퍼 객체를 문자열로 되돌릴 때 문자열이 변경된다. 따라서 String 객체의 모든 메서드는 String 래퍼 객체를 직접 변경할 수 없고, String 객체의 메서드는 언제나 새로운 문자열을 생성하여 반환한다.

사용 빈도가 높은 String 메서드에 대해 살펴보자.

#### String.prototype.indexOf

indexOf 메서드는 대상 문자열 ( 메서드를 호출한 문자열 ) 에서 인수로 전달받은 문자열을 검색하여 첫 번째 인덱스를 반환한다 .검색에 실패하면 -1을 반환한다.

```JavaScript
const str = 'Hello World';

// 문자열 str에서 'l'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf('l'); // ->2

// 문자열 str에서 'or'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf('or'); // ->7

// 문자열 str에서 'x'를 검색하여 첫 번째 인덱스를 반환한다. 검색에 실패하면 -1을 반환한다.
str.indexOf('x'); // -> -1
```

indexOf 메서드의 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

```JavaScript
// 문자열 str의 인덱스 3부터 'l'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf('l',3); // -> 3
```

indexOf 메서드는 대상 문자열에 특정 문자열이 존재하는지 확인할 때 유용하다.

```JavaScript
if (Str.indexOf('Hello') !== -1){
  // 문자열 str에 'Hello'가 포함되어 있는 경우에 처리할 내용
}
```

ES6에서 도입된 String.prototype.includes 메서드를 사용하면 가독성이 더 좋다.

```JavaScript
if (str.includes('Hello')) {
  // 문자열 str에 'Hello'가 포함되어 있는 경우에 처리할 내용
}
```

#### String.prototype.search

search 메서드는 대상 문자열에서 인수로 전달받은 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환한다. 검색에 실패하면 -1을 반환한다.

```JavaScript
const str = 'Hello world';

// 문자열 str에서 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환한다.
str.search(/o/); // -> 4
str.search(/x/); // -> -1

// 일치하는 문자열이 여러 개 있더라도 가장 먼저 발견된 문자열의 인덱스만 반환한다. 오직 첫 번째 일치 항목의 시작 위치를 찾는용도.
```

#### String.prototype.includes

ES6에서 도입된 includes 메서드는 대상 문자열에 인수로 전달받은 문자열이 포함되어 있는지 확인하여 그 결과를 true 또는 false로 반환한다.

```JavaScript
const str = 'Hello world';

str.includes('Hello'); // -> true
str.includes(''); // -> true
str.includes('x'); // -> false
str.includes(); // -> false
```

includes 메서드 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

```JavaScript
const str = 'Hello world';

// 문자열 str의 인덱스 3부터 'l'이 포함되어 있는지 확인
str.includes('l',3); // -> true
str.includes('H',3); // -> false
```

#### String.prototype.startsWith

ES6에서 도입된 startsWith 메서드는 대상 문자열이 인수로 전달받은 문자열로 시작하는지 확인하여 그 결과를 true 또는 false로 반환한다.

```JavaScript
const str = 'Hello world';

// 문자열 str이 'He'로 시작하는지 확인
str.startsWith('He'); // -> true
// 문자열 str이 'x'로 시작하는지 확인
str.startsWith('x'); // -> false
```

startsWith 메서드의 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

```JavaScript
// 문자열 str의 인덱스 5부터 시작하는 문자열이 ' ' 로 시작하는지 확인
str.startsWith(' ',5); // -> true
```

#### String.prototype.endsWith

ES6에서 도입된 endsWith 메서드는 대상 문자열이 인수로 전달받은 문자열로 끝나는지 확인하여 그 결과를 true 또는 false로 반환한다.

```JavaScript
const str = 'Hello world';

// 문자열 str이 'ld'로 끝나는지 확인
str.endsWith('ld'); // -> true
// 문자열 str이 'x'로 끝나는지 확인
str.endsWith('x'); //-> false
```

endsWith 메서드의 2번째 인수로 검색할 문자열의 길이를 전달할 수 있다.

```JavaScript
// 문자열 str의 처음부터 5자리까지 ('Hello')가 'lo'로 끝나는지 확인
str.endsWith('lo',5); // -> true
```



