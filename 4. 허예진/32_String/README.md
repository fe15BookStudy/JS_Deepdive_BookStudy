# 32. String

## String 생성자 함수

String 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[StringData]] 내부 슬롯에 빈 문자열을 할당한 String 레퍼 객체를 생성한다.

```js
const strObj = new String("Lee");
console.log(strObj);
// String {0: "L", 1: "e", 2: "e", length: 3, [[PrimitiveValue]]: "Lee"}

console.log(strObj[0]); // L

// 문자열은 원시 값이므로 변경할 수 없다. 이때 에러가 발생하지 않는다.
strObj[0] = "S";
console.log(strObj); // 'Lee'
```

문자열이 아닌 값도 문자열로 강제변환 한다.

```js
// 숫자 타입 => 문자열 타입
String(1); // "1"
String(NaN); // "NaN"
String(Infinity); // "Infinity"

// 불리언 타입 => 문자열 타입
String(true); // "true"
String(false); // "false"
```

## length 프로퍼티

length 프로퍼티는 문자열의 문자 개수를 반환한다.

```js
'Hello'.length; //5
'안녕하세요!.'length; // 6
```

## String 메서드

String 객체에는 원본 레퍼 객체를 직접 변경하는 메서드는 존재하지 않는다. String 객체의 메서드는 언제나 새로운 문자열을 반환한다.  
문자열은 변경 불가능한 원시값이기 때문에 String 레퍼 객체도 읽기 전용 객체로 제공된다.

### String.prototype.indexOf

indexOf 메서드는 대상 문자열에서 인수로 전달받은 문자열을 검색하여 첫 번째 인덱스를 반환한다. 검색에 실패하면 -1을 반환한다.

```js
const str = "Hello World";

// 문자열 str에서 'l'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf("l"); // ->2

// 문자열 str에서 'or'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf("or"); // ->7

// 문자열 str에서 'x'를 검색하여 첫 번째 인덱스를 반환한다. 검색에 실패하면 -1을 반환한다.
str.indexOf("x"); // -1

// 문자열 str의 인덱스 3부터 'l'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf("l", 3); // 3

if (Str.indexOf("Hello") !== -1) {
  // 문자열 str에 'Hello'가 포함되어 있는 경우에 처리할 내용
}

if (str.includes("Hello")) {
  // 문자열 str에 'Hello'가 포함되어 있는 경우에 처리할 내용
}
```

### String.prototype.search

```js
const str = "Hello world";

// 문자열 str에서 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환한다.
str.search(/o/); // 4
str.search(/x/); // -1
```

### String.prototype.includes

ES6에서 도입된 includes 메서드는 대상 문자열에 인수로 전달받은 문자열이 포함되어 있는지 확인하여 그 결과를 true 또는 false로 반환한다.

```js
const str = "Hello world";

str.includes("Hello"); // true
str.includes(""); // true
str.includes("x"); // false
str.includes(); // false

const str = "Hello world";

// 문자열 str의 인덱스 3부터 'l'이 포함되어 있는지 확인
str.includes("l", 3); // true
str.includes("H", 3); // false
```

### String.prototype.startsWith

```js
const str = "Hello world";

// 문자열 str이 'He'로 시작하는지 확인
str.startsWith("He"); // true
// 문자열 str이 'x'로 시작하는지 확인
str.startsWith("x"); // false

// 문자열 str의 인덱스 5부터 시작하는 문자열이 ' ' 로 시작하는지 확인
str.startsWith(" ", 5); // true
```

### String.prototype.endsWith

ES6에서 도입된 endsWith 메서드는 대상 문자열이 인수로 전달받은 문자열로 끝나는지 확인하여 그 결과를 true 또는 false로 반환한다.

```js
const str = "Hello world";

// 문자열 str이 'ld'로 끝나는지 확인
str.endsWith("ld"); // true
// 문자열 str이 'x'로 끝나는지 확인
str.endsWith("x"); //false

// 문자열 str의 처음부터 5자리까지 ('Hello')가 'lo'로 끝나는지 확인
str.endsWith("lo", 5); // true
```

### String.prototype.charAt

chatAt 메서드는 대상 문자열에서 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환한다.

```js
const str = "Hello";

for (let i = 0; i < str.length; i++) {
  console.log(str.charAt(i)); // HELLO
}

// 인덱스가 문자열의 범위(0 ~ 문자열 길이-1)를 벗어난 경우 빈 문자열을 반환한다.
str.charAt(5); // ->''
```

### String.prototype.substring

substring 메서드는 대상 문자열에서 첫 번째 인수로 전달받은 인덱스에서 위치하는 문자부터 두 번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 이전 문자까지의 부분 문자열을 반환한다.

```js
const str = "Hello World";

// 인덱스 1부터 인덱스 4 이전까지의 부분 문자열을 반환한다.
str.substring(1, 4); // ell
```

substring 메서드의 두 번째 인수는 생략할 수 있다. 이때 첫 번째 인수로 전달한 인덱스에 위치하는 문자부터 마지막 문자까지 부분 문자열을 반환한다.

```js
const str = "Hello World";

// 인덱스 1부터 마지막 문자까지 부분 문자열을 반환한다.
str.substring(1); // 'ello World'
```

substring 메서드의 첫 번째의 인수는 두 번째 인수보다 작은 정수이어야 정상이다. 하지만 다음과 같이 인수를 전달하여도 정상 동작한다.

- 첫 번째 인수 > 두 번째 인수인 경우 두 인수는 교환된다.
- 인수 < 0 또는 NaN인 경우 0으로 취급된다.
- 인수 > 문자열의 길이(str.length) 인 경우 인수는 문자열의 길이(str.length)로 취급된다.

```js
const str = "Hello World"; // str.length == 11

str.substring(4, 1); // 'ell'
str.substring(-2); // 'Hello World'
str.substring(1, 100); // 'ello World'
str.substring(20); // ->''
```

String.prototype.indexOf 메서드와 함께 사용하면 특정 문자열을 기준으로 앞뒤에 위치한 부분 문자열을 취득할 수 있다.

```js
const str = "Hello World";

// 스페이스를 기준으로 앞에 있는 부분 문자열 취득
str.substring(0, str.indexOf("")); // ->'Hello'

//스페이스를 기준으로 뒤에 있는 부분 문자열 취득
str.substring(Str.indexOf("") + 1, str.length); // 'World'
```

### String.prototype.slice

slice 메서드는 substring 메서드와 동일하게 동작한다. 단, slice 메서드에는 음수인 인수를 전달할 수 있다. 음수인 인수를 전달하면 대상 문자열의 가장 뒤에서부터 시작하여 문자열을 잘라내어 반환한다.

```js
const str = "hello world";

//substring과 slice 메서드는 동일하게 동작한다.
// 0번째부터 5번째 이전 문자까지 잘라내어 반환
str.substring(0, 5); //->'hello'
str.slice(0, 5); //->'hello'

// 인덱스가 2인 문자부터 마지막 문자까지 잘라내어 반환
str.substring(2); // 'llo world'
str.slice(2); // 'llo world'

// 인수 < 0 또는 NaN인 경우 0으로 취급한다.
str.substring(-5); // 'hello world'

// slice 메서드는 음수인 인수를 전달할 수 있다. 뒤에서 5자리를 잘라내어 반환한다.
str.slice(-5); // 'world'
```

### String.prototype.toUpperCase

toUpperCase 메서드는 대상 문자열을 모두 소문자로 변경한 문자열을 반환한다.

```js
const str = "Hello World!";

str.toLowerCase(); // ->'hello world!'
```

### String.prototype.toLowerCase

toLowerCase 메서드는 대상 문자열을 모두 소문자로 변경한 문자열을 반환한다.

```js
const str = "Hello World!";

str.toLowerCase(); // ->'hello world!'
```

### String.prototype.trim

trim 메서드는 대상 문자열 앞뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환한다.

```js
const str = "    foo    ";
str.trim(); // 'foo'

str.trimStart(); // 'foo    '
str.trimEnd(); // '    foo'
```

### String.prototype.repeat

repeat 메서드는 대상 문자열을 인수로 전달받은 정수만큼 반복해 연결한 새로운 문자열을 반환한다.  
인수로 전달받은 정수가 0이면 빈 문자열을 반환하고, 음수이면 RangeError를 발생시킨다. 인수를 생략하면 기본값 0 이 설정된다.

```js
const str = "abc";

str.repeat(); // ->''
str.repeat(0); // ->''
str.repeat(1); // ->'abc'
str.repeat(2); // ->'abcabc'
str.repeat(2.5); // ->'abcabc' (2.5 => 2)
str.repeat(-1); // RangeError : Invalid count value
```

### String.prototype.replace

replace 메서드는 대상 문자열에서 첫 번째 인수로 전달받은 문자열 또는 정규표현식을 검색하여 두 번째 인수로 전달한 문자열로 치환한 문자열을 반환한다.

```js
const str = "Hello world";

// str에서 첫 번째 인수 'world'를 'Lee'로 치환한다.
str.replace("world", "Lee"); // 'Hello Lee'
```

검색된 문자열이 여럿 존재할 경우 첫 번째로 검색된 문자열만 치환한다.

```js
const str = " Hello world world";
str.replace("world", "Lee"); // 'Hello Lee world'
```

특수한 교체 패턴을 사용할 수 있다. 예를 들어, $&는 검색된 문자열을 의미한다.

```js
const str = "Hello world";

// 특수한 교체 패턴을 사용할 수 있다. ($& => 검색된 문자열)
str.replace("world", "<strong>$&</strong>");
```

replace 메서드의 첫 번째 인수로 정규 표현식을 전달할 수도 있다.

```js
const str = "Hello Hello";

//'hello'를 대소문자를 구별하지 않고 전역 검색한다.
str.replace(/hello/gi, "Lee"); // 'Lee Lee'
```

### String.prototype.split

split 메서드는 대상 문자열에서 첫 번째 인수로 전달한 문자열을 구분 한 후 분리된 각 문자열로 이루어진 배열을 반환한다. 인수로 빈 문자열을 전달하면 각 문자를 모두 분리하고, 인수를 생략하면 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.

```js
const str = "How are you doing?";

// 공백으로 구분(단어로 구분)하여 배열로 반환한다.
str.split(" "); // ["How", "are", "you", "doing?"]

// \s는 여러 가지 공백 문자(스페이스, 탭 등)를 의미함. 즉, [\t\r\n\v\f]와 같은 의미
str.split(/\s/); // ["How", "are", "you", "doing?"]

// 인수로 빈 문자열을 전달하면 각 문자를 모두 분리한다.
str.split("");
// ["H", "o", "w", " ", "a", "r", "e", " ", "y", "o", "u", " ", "d", "o", "i", "n", "g", "?"]

// 인수를 생략하면 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.
str.split(); // ["How are you doing?"]
```

두 번째 인수로 배열의 길이를 지정할 수 있다.

```js
// 공백으로 구분하여 배열로 반환. 단, 배열의 길이는 3이다.
str.split(" ", 3); // ["How", "are", "you"]
```

**split 메서드는 배열을 반환합니다.** 따라서 Array.prototype.reverse, Array.prototype.join 메서드와 함께 사용하면 문자열을 역순으로 뒤집을 수 있습니다.

```js
// 인수로 전달받은 문자열을 역순으로 뒤집는다.
function reverseString(str) {
  return str.split("").reverse().join("");
}

reverseString("Hello world!"); // '!dlrow olleH'
```
