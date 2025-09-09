# 모던 자바스크립트 Deep Dive

## 09장 타입 변환과 단축 평가

### 타입 변환이란?

자바스크립트의 모든 값은 타입이 있다. 개발자의 의도에 따라 값의 타입을 변환하는 것을 **명시적 타입변환** 또는 **타입 캐스팅**이라고 한다. 개발자의 의도와 상관없이 자바스크립트 엔진에 의해 타입이 변환되기도 하는데 이것을 **암묵적 타입변환** 또는 **타입 강제변환** 이라고한다.

```jsx
//명시적 타입변환
var x = 10;
var str1 = x.toString();
console.log(typeof str1, str1); // string 10

//암묵적 타입변환
var str2 = x + "";
console.log(typeof str2, str2); // string 10

//x의 값이나 타입이 바뀐것은 아니다.
```

자바스크립트 엔진은 표현식을 에러 없이 평가하기 위해 피연산자의 값을 암묵적 타입변환해 새로운 타입의 값을 만들어 단 한 번 사용하고 버린다. 암묵적 타입변환은 드러나지 않게 자동 변환되므로 예측이 불가능하다. **따라서 자신이 작성한 코드에서 암묵적 타입변환이 일어나는지, 발생한다면 어떤 타입으로 변환되는지, 변환된 값이 어떻게 평가 될것인지 예측 가능해야한다.** 그렇지않다면 오류가 발생할 확률이 높아진다.

---

### 암묵적 타입변환

자바스크립트 엔진은 코드의 문맥을 고려해 암묵적으로 데이터 타입을 강제 변환할 때 가 있다.

```jsx
"10" + 2; //'102'
5 * "10"; //50
!0; //true
if (1) {
}
```

#### 문자열 타입으로 변환

```jsx
1 + "2"; // "12"
```

위의 예제는 피연산자중 하나 이상이 문자열이므로 문자열 연결 연산자로 동작한다. 그래서 문자열 연결 연산자의 모든 피연산자는 코드의 문맥상 모두 문자열 타입이어하기 때문에 자바스크립트 엔진이 문자열 타입으로 변환한다.

```jsx
0 + ""; //"0"
-0 + ""; //"0"
1 + ""; //"1"
-1 + ""; //"-1"
NaN + ""; //"NaN"
Infinity + ""; //"Infinity "
-Infinity + ""; //"-Infinity"

//불리언타입
true + ""; // "true"
false + ""; // "false"

//null타입
null + ""; //"null"

//undifined 타입
undifined + ""; // "undifined"

//심벌타입
Symbol() + ""; ?? //요건 에러

//객체타입
({}) + ""; //[object Object]
[]+''; // ""
[10, 20] + ""; // "10, 20"
(function () {}) + ""; // "function(){}"
Array + ""; // "function Array(){[native code]}"
```

#### 숫자 타입으로 변환

```jsx
1 - "1"; // 0
1 * "10"; // 10
1 / "one"; //NaN
```

위 예제에서 사용한 연산자는 모두 산술 연산자이다. 산술연산자는 숫자 값을 만드는 역할을 하므로 문맥상 모두 숫자타입이어야 한다. 그래서 자바스크립트 엔진은 산술 연산자 표현식을 평가하기 위해 암묵적으로 숫자 타입으로 변환한다. 변환하지 못하는 것들은 연산을 수행 못하므 NaN이 된다. 산술연산자뿐만 아니라 비교 연산자와 +단항 연산자도 암묵적으로 숫자타입으로 변환한다.

```jsx
"1" > 0; //true

+""; //0
+"0"; //0
+"1"; //1
+"string"; //NaN

+true; //1
+flase; //0

+null; //0
+undifined; // NaN

+Symbol(); // 요건 에러
+{}; // NaN
+[]; // 0
+[10, 20]; // NaN
+function () {}; // NaN
```

### 불리언 타입으로 변환

if문이나 for문과 같은 제어문 또는 삼항 조건 연산자의 조건식은 불리언 값, 즉 논리적 참/거짓으로 평가되어야 하는 표현식이다.

```jsx
if ("") console.log("1");
if (true) console.log("2");
if (0) console.log("3");
if ("str") console.log("4");
if (null) console.log("5");
// 2 4
```

자바스크립트 엔진은 불리언 타입이 아닌값을 Truthy값 또는 Falsy값으로 구분한다. 아래값들은 false로 평가되는 Falsy값이다.

- false
- undefined
- null
- 0, -0;
- NaN
- ''(빈문자열)

이외에는 모두 true로 평가되는 Truthy값이다.

### 명시적 타입 변환

개발자의 의도에 따라 명시적으로 타입을 변경하는 방법은 다양하다. 표준 빌트인 생성자함수(String, Number, Boolean)를 연산자 없이 호출하는 방법과 빌트인 메서드를 사용하는 방법, 그리고 앞에서 살펴본 암묵적 타입 변환을 이용하는 방법이 있다.

#### 문자열 타입으로 변환

문자열 타입이 아닌 값을 문자열 타입으로 변환하는 방법은 다음과 같다.

1. String 생성자 함수를 new연산자 없이 호출하는 방법
2. Object.prototype.toString메서드를 사용하는 방법
3. 문자열 연결 연산자를 이용하는 방법

```jsx
// 1. String 생성자 함수를 new연산자 없이 호출하는 방법
String(1); // "1"
String(NaN); // "NaN"
String(Infinity); //"Infinity"
String(true); //"true"
String(false); //"false"

// 2. Object.prototype.toString메서드를 사용하는 방법
(1).toString(); //"1"
NaN.toString(); //"NaN"
Infinity.toString(); //"Infinity"
true.toString(); //"true"
false.toString(); //"false"

// 3. 문자열 연결 연산자를 이용하는 방법
1 + ""; // "1"
NaN + ""; //"NaN"
Infinity + ""; //"Infinity"
true + ""; //"true"
false + ""; //"false"
```

#### 숫자 타입으로 변환

숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법은 다음과 같다.

1. Number 생성자 함수를 new 연산자없이 호출하는 방법
2. parseInt,parsFloat함수를 사용하는 방법(문자열만 숫자타입으로 변환)
3. +단항 산술 연산자를 이용하는 방법
4. \*산술 연산자를 이용하는 방법

```jsx
//1. Number 생성자 함수를 new 연산자없이 호출하는 방법
Number("0");
Number("-1");
Number("10.53");
Number(true);
Number(false);

//2. parseInt,parsFloat함수를 사용하는 방법(문자열만 숫자타입으로 변환)
parseInt("0");
parseInt("-1");
parseInt("10.53");

//3. +단항 산술 연산자를 이용하는 방법
+"0";
+"-1";
+"10.53";
+true;
+false;

//4. *산술 연산자를 이용하는 방법
"0" * 1;
"-1" * 1;
"10.53" * 1;
true * 1;
false * 1;
```

#### 불리언 타입으로 변환

불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법은 다음과 같다.

1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
2. ! 부정논리 연산자를 두번 사용하는 방법

```jsx
//1. Boolean 생성자 함수를  new 연산자 없이 호출하는 방법
Boolean("x"); //true
Boolean("");
Boolean("false"); //true
Boolean(0);
Boolean(1);
Boolean(NaN);
Boolean(Infinity); //true

Boolean(null);
Boolean(undefined);
Boolean({}); //true
Boolean([]); //true

//2. ! 부정논리 연산자를 두번 사용하는 방법
!!"x"; //true
!!"";
!!"false"; //true

!!0;
!!1;
!!NaN;
!!Infinity; //true

!!null;
!!undefined;

!!{}; //true
!![]; //true
```

### 단축평가

### 논리연산자를 사용한 단축 평가

논리합 또는 논리곱 연산자 표현식의 평가결과는 불리언값이 아닐 수도있다. 논리합 또는 논리곱 연산자 표현식은 언제나 2개의 피연산자 중 어느 한쪽으로 평가된다.

` 'cat'&&'dog'; // -> dog`
논리곱 연산자는 둘다 true일때 true를 반환한다. 위의 식은 cat값이 true이다. 둘다 true여야지 표현식이 평가가 되므로 두번째 피연산자까지 평가해야 표현식이 평가된다. 따라서 dog가 평가 결과를 결정을 하고 dog가 반환된다.

`'cat'||'dog' ->'cat';`
논리합도 동일하게 동작한다. 논리합은 둘중에 하나만 true여도 true를 반환한다. cat이 ture이므로 그대로 cat을 반환한다.

| 단축 평가 표현식    | 평가결과 |
| ------------------- | -------- |
| true \|\| anything  | true     |
| false \|\| anything | anything |
| true && anything    | anything |
| false && anything   | false    |

### 옵셔널 체이닝 연산자

옵셔널 체이닝 연산자 ?.는 좌항의 피연산자가 null또는 undefined인 경우 undefined를 반환하고 그렇지않으면 우항의 프로퍼티 참조를 이어간다.

```jsx
var elem = null;

var value = elem?.value;
console.log(value); //undefined
```

### null 병합 연산자

null 병합 연산자 ??는 좌항의 피연산자가 null또는 undefined인 경우 우항의 피연산자를 반환하고 그렇지않으면 좌항의 피연산자를 반환한다. null 병합 연산자는 변수에 기본값을 설정할 때 유용하다.

```jsx
var foo = null ?? "default string";
console.log(foo); //"default string"
```
