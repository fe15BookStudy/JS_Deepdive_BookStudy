# 09. 타입 변환과 단축 평가

### 타입 변환이란?

- 개발자가 의도적으로 값의 타입을 변환하는 것을 **명시적 타입 변환(explicit coercion)** , 또는 **타입 캐스팅(type casting)** 이라 한다.

<br>

```JavaScript
var x = 10;

// 명시적 타입 변환
// 숫자 -> 문자열 타입 캐스팅

var str = x.toString();
console.log(typeof str, str); // string 10

// x 변수의 값이 변경된 것은 아니다.
console.log(typeof x,x); //number 10
```

가끔 자바스크립트 엔진에 의해 암묵적으로 타입이 자동변환 되기도 하는데, 이를 **암묵적 타입 변환(implicit coercion)** 또는 **타입 강제 변환(type coercion)** 이라 한다.

<br>

```JavaScript
var x = 10;

// 암묵적 타입 변환
// 문자열 연결 연산자는 숫자 타입 x의 값을 바탕으로 새로운 문자열을 생성
var str= x + '';
console.log(typeof str, str); // string 10

// x 변수의 값이 변경된 것은 아니다.
console.log(typeof x,x); //number 10
```

두 방식이 원시 값을 변경하는 것은 아니고, 타입 변환이란 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하는 것이다.

<br>

### 암묵적 타입 변환

1. 문자열 타입으로의 변환

- 자바스크립트 엔진은 문자열 연결 연산자인 +를 사용할 때 피연산자 중 하나라도 문자열 타입이라면 다른 피연산자도 문자열로 변환한다.

```JavaScript
// 숫자와 문자열
10 + '20' // '1020' (숫자 10이 문자열 '10'으로 변환)

// 불리언과 문자열
true + 'text' // 'truetext' (불리언 true가 문자열 'true'로 변환)

// 객체와 문자열
{} + 'object' // '[object Object]object' (빈 객체가 문자열 '[object Object]'로 변환)
```

2. 숫자 타입으로의 변환

- 자바스크립트 엔진은 **산술 연산자(-, \*, /)** 를 사용하거나 **비교 연산자(>, <, ==)** 를 사용할 때 피연산자를 숫자로 변환한다. **단항 연산자 +** 는 피연산자를 숫자로 변환하는 가장 간단하고 명확한 방법이다.

```JavaScript

// 문자열과 숫자
'10' * 5 // 50 (문자열 '10'이 숫자 10으로 변환)
'5' - 3 // 2 (문자열 '5'가 숫자 5로 변환)
'5' / 2 // 2.5 (문자열 '5'가 숫자 5로 변환)

// 빈 문자열과 null
'' * 10 // 0 (빈 문자열이 숫자 0으로 변환)
null * 10 // 0 (null이 숫자 0으로 변환)

// true와 false
true * 1 // 1 (true가 숫자 1로 변환)
false * 1 // 0 (false가 숫자 0으로 변환)
```

3. 불리언 타입으로의 변환

- 자바스크립트 엔진은 **논리 연산자(&&, ||, !)**나 **조건문(if, while)**에서 피연산자를 불리언 타입으로 변환한다. 이때 false로 변환되는 값들을 "Falsy" 값이라고 부른다. 이 외의 모든 값은 true로 변환된다.

- Falsy 값 : `false`, `0`, `-0`, `''(빈 문자열)`, `null`, `undefined`, `Nan`

```JavaScript
// Falsy 값
if (0) {
    console.log('실행되지 않음');
}
if (null) {
    console.log('실행되지 않음');
}
if ('') {
    console.log('실행되지 않음');
}

// Truthy 값
if ('hello') {
    console.log('실행됨'); // 'hello'는 true로 변환
}
if (10) {
    console.log('실행됨'); // 10은 true로 변환
}
```

### 단축 평가

1. 논리 연산자를 사용한 단축 평가

```JavaScript
'Cat' && 'Dog' // -> "Dog"
```

논리곱(&&) 연산자는 두 개의 피연산자가 모두 true로 평가될 때 true를 반환한다. 위 예제에서 첫 번째 피연산자 `'Cat'`은 `Truthy'` 값이므로 true로 평가된다. 그렇지만 결국 두번 째 연산자가 이 논리곱 연산자 표현식의 평가 결과를 결정한다. 이때 논리곱 연산자는 **논리 연산의 결과를 결정하는 두 번째 피연산자, 즉 문자열 `'Dog'`를 그대로 반환한다.**

논리합(||) 연산자도 논리곱(&&) 연산자와 동일하게 동작한다.

```JavaScript
'Cat || 'Dog' // -> "Cat"
```

논리합(||) 연산자는 두 개의 피연산자 중 하나만 true로 평가되어도 true를 반환한다.

논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환하는 것을 **단축 평가** 라고 한다.

**단축 평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.**

| 단축 평가 표현식  | 평가 결과 |
| :---------------: | :-------: |
| true :: anything  |   true    |
| false :: anything | anything  |
|  true&&anything   | anything  |
| false && anything |   false   |

단축 평가는 다음과 같은 상황에서 유용하게 사용된다.

1. 객체를 가리키기 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때

   객체는 키와 값으로 구성된 프로퍼티의 집합이다. 만일 객체를 가리키기를 기대하는 변수의 값이 객체가 아니라 null 또는 undefined 인 경우 객체의 프로퍼티를 참조하면 타입 에러가 발생한다. 에러가 발생하면 프로그램이 강제 종료된다.

   ```JavaScript
   var elem = null;
   var value = elem.value; // TypeError: Cannot read property 'value' of null
   ```

   이때 단축 평가를 사용하면 에러가 발생하지 않는다

   ```JavaScript
   var elem = null;
   // elem이 null 이나 undefined와 같은 Falsy 값이면 elem으로 평가되고
   // elem이 Truthy 값이면 elem.value로 평가된다.
   var value = elem && elem.value; // -> null
   ```

2. 함수 매개변수에 기본값을 설정할 때

   함수를 호출할 때 인수를 전달하지 않으면 매개변수에는 undefined가 할당된다. 이때 단축 평가를 사용해 매개변수의 기본값을 설정하면 undefined로 인해 발생할 수 있는 에러를 방지할 수 있다.

   ```JavaScript
   //단축 평가를 사용한 매개변수의 기본값 설정
   function getStringLength(str) {
       str = str :: '';
       return str.length;

   }

   getStringLength(); //->0
   getStringLength('hi'); //->2


   //ES6의 매개변수의 기본값 설정
   function getStringLength(str =''){
   return str.length;
   }

   getStringLength(); //->0
   getStringLength('hi'); //->2
   ```

<br>

2. 옵셔널 체이닝 연산자 `?.`

   - 옵셔널 체이닝 연산자는 **ES11 (ECMAScript 2020)**에서 도입된 문법으로 객체의 프로퍼티를 참조할 때 해당 객체가 null 또는 undefined인지 확인하는 과정을 간결하게 만들어 준다.

   `?.` 연산자 왼쪽의 피연산자가 `null` 또는 `undefined`이면 연산은 중단되고 `undefined`를 반환한다. 그렇지 않으면 오른쪽의 프로퍼티 참조를 계속 진행한다.

   이러한 옵셔널 체이닝 연산자느 객체 프로퍼티에 접근하기 전에 해당 객체가 존재하는지 일일이 if문으로 확인하는 번거로움을 줄여준다. 기존에는 논리 연산자 `&&`를 사용해 동일한 기능을 구현했지만 `&&`는 `false`, `0`, `'' (빈 문자열)`과 같은 `Falsy` 값일 경우에도` undefined`가 아닌 해당 `Falsy` 값 자체를 반환하는 차이가 있다. `?.`는 오직 `null`과 `undefined`에만 반응한다.

3. 널 병합 연산자 (Nullish Coalescing) `??`

   - 널 병합 연산자도 **ES11 (ECMAScript 2020)**에서 도입된 문법으로, 기본값을 설정할 때 유용하게 사용된다.

   `??` 연산자 왼쪽의 피연산자가 `null` 또는 `undefined이면` 오른쪽의 피연산자를 반환한다. 그렇지 않으면 왼쪽의 피연산자를 반환한다.

   널 병합 연산자는 변수에 `null` 또는 `undefined`가 할당되었을 때만 기본값을 사용하도록 명확하게 지정할 수 있다. 기존에 사용하던 논리 연산자 `||`는 `false`,` 0`,`'' (빈 문자열)`등 모든 `Falsy` 값에 대해 오른쪽 피연산자를 반환하는 문제가 있었다. 이로 인해 예상치 못한 동작이 발생할 수 있었다.` ??`는 오직 ` null`과 `undefined`일 때만 기본값을 반환하기 때문에 더 안전하고 예측 가능한 코드를 작성할 수 있게 해준다.
