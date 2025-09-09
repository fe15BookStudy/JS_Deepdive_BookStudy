# 타입 변환과 단축 평가

1. 타입 변환이란

- js의 모든 값은 타입이 있다. 값의 타입은 개발자의 의도에 따라 다른 타입으로 변환할 수 있다.
  개발자가 의도적으로 값의 타입을 변환하는 것은 명시적 타입변환 또는 타입 캐스팅이라고 한다.

  ```
  var x = 10;
  var str = x.toString(); // "10"
  console.log(str); // "10"
  console.log(typeof str, str); // "string" "10"
  console.log(typeof x, x);

  ```

  해설
  `var x = 10;
x는 숫자형(number) 값 10.
x.toString();
숫자 10을 문자열 "10"으로 변환해서 str에 저장.
console.log(str);
"10" 출력.
console.log(typeof str, str);
typeof str → "string"
따라서 "string 10" 출력.\
console.log(typeof x, x);
원래 변수 x는 여전히 숫자형(number).
따라서 "number 10" 출력.`

  - 명시적 타입 변환이나 암묵적 타입 변환이 기존 원시 값을 직접 변경하는 것은 아니다. 원시값은 변경 불가능한 값이므로 변경할 수 없다.
    타입 변환이란 기존 원시 값을 사용하 다른 타입의 새로운 원시값을 생성하는 것이다. ?

2. 암묵적 타입 변환

'10' + 2

- 연산자는 문자열이 하나라도 있으면 문자열 연결로 동작.
  따라서 "10" + "2" → "102"

5 \* '10'

- 연산자는 숫자 연산만 가능하기 때문에 "10"을 숫자 10으로 변환.
  5 \* 10 = 50

  !0

- 0은 falsy 값 (false로 취급됨).
  !0 → !false → true

if (1) {}

- 1은 truthy 값 (true로 취급됨).
  따라서 if 조건문 안의 블록이 실행됨.

+는 피연산자중 하나 이상이 문자열이면 문자열로 동작한다.
-,\*,/는 모두 산술 연산자라 숫자로 변환한다.
if문이나 for문 같은 제어문 또는 삼항 조건 연산자의 조건식은 불리언값 (참, 거짓)으로 평가 된다.

3. 불리언 타입으로 변환

- 불리언 타입 변환

```
Boolean(0);       // false
Boolean(1);       // true
Boolean("hello"); // true
Boolean("");      // false (빈 문자열)
Boolean(null);    // false
Boolean(undefined); // false
Boolean([]);      // true (빈 배열도 객체라서 true)
Boolean({});      // true (빈 객체도 true)
```

```
Boolean(false)      // false
Boolean(0)          // false
Boolean(-0)         // false
Boolean("")         // false
Boolean(null)       // false
Boolean(undefined)  // false
Boolean(NaN)        // false
```

이 7가지만 false 값이다. 이 외에는 모두 true로 평가 된다.

- 명시적 타입 변환

```
Boolean(0);       // false
Boolean(1);       // true
Boolean("");      // false
Boolean("hello"); // true
Boolean(null);    // false
Boolean(undefined); // false
Boolean([]);      // true
Boolean({});      // true

```

이런 Boolean() 함수를 사용한것을

```
!!0;        // false
!!1;        // true
!!"";       // false
!!"hello";  // true
!!null;     // false
!!undefined;// false
!![];       // true
!!{};       // true
```

!! 이중 NOT 연산자를 사용하여 나타낼수 있다.

- 단축 평가
  js에서 자주쓰이는 논리 연산자 활용 기법이다. 쉽게 말하면, 앞쪽 조건만으로 결과가 결정되면 뒤쪽 코드는 실행하지 않는 것이다.

  ```
  const a = 0;
  const b = 10;

  console.log(a && b); // 0
  ```

  a가 false 값이므로 0이 반환된다.
  만약 0 대신 5가 들어간다면 10이 반환된다.

  ```
  const a = 0;
  const b = 10;

  console.log(a || b); // 10
  ```

  a가 false 값이므로 오른쪽 값을 평가 한다. 따라서 결과가 10이다.
  만약 0대신 5가 들어간다면 왼쪽이 true값이므로 오른쪽을 평가하지 않아 결과가 5이다.
