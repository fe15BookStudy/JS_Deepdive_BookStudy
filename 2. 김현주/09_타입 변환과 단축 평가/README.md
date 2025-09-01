# 명시적 타입 변환(Explicit Type Conversion)

: 명시적 타입 변환은 개발자가 의도적으로 데이터의 타입을 바꾸는 것을 말합니다.

- 개발자가 의도적으로 값의 타입을 변환

- 문자열로 변환 : String() 생성자 함수, toString() 메서드, 또는 문자열 연결 연산자(+)를 사용할 수 있습니다.
- 숫자로 변환 : Number() 생성자 함수, parseInt() / parseFloat() 함수, 또는 단항 연산자(+)를 사용할 수 있습니다.
- 불리언으로 변환 : Boolean() 생성자 함수나 부정 논리 연산자(!!)를 두 번 사용하여 불리언 타입으로 사용할 수 있습니다.

```javascript
var x = 10;

// 명시적 타입 변환
var str = x.toString();
console.log(typeof str); // string

// 암묵적 타입 변환 (x 변수의 값은 변경되지 않음)
var str2 = x + '';
console.log(typeof str2); // string
console.log(typeof x); // number (원본은 변경 안됨)
```

# 암묵적 타입 변환(Implicit Coercion)

: JavaScript 엔진은 표현식을 평가할 때 개발자의 의도와 상관없이 코드의 문맥을 고려해 암묵적으로 타입을 변환합니다.

1. 문자열(String) 타입으로 변환

- 핵심 규칙: + 연산자 양쪽에 하나라도 문자열이 있으면, 다른 쪽 값도 문자열로 변환하여 두 문자열을 이어 붙입니다.

- 예시:

  - 1 + '2' → '12' (숫자 1이 문자 '1'로 변환)

  - true + '' → 'true' (불리언이 문자로 변환)

  - [10, 20] + '' → '10,20' (배열이 문자로 변환)

  - {} + '' → '[object Object]' (객체가 문자로 변환)

2. 숫자(Number) 타입으로 변환

- 핵심 규칙: -, \*, / 같은 산술 연산자나 > 같은 비교 연산자를 사용하면, 값들을 숫자로 변환하여 계산하려고 시도합니다.

- 예시:

- '5' \* '10' → 50 (문자가 숫자로 변환되어 곱셈)

- '10' - 1 → 9

- - '10' → 10 (단항 + 연산자는 숫자 변환 기능)

- - true → 1 (true는 1, false와 null은 0으로 변환)

- - 'hello' → NaN (숫자로 바꿀 수 없는 문자는 NaN(Not a Number)이 됨)

3. 불리언(Boolean) 타입으로 변환

- 핵심 규칙: if (...)나 while (...)처럼 조건문이 필요한 곳에서는 값을 불리언 타입으로 자동 변환하여 참/거짓을 판단합니다.

- 이때 Truthy(참 같은 값) / Falsy(거짓 같은 값) 규칙이 적용됩니다.

  - if ('') → false로 평가 (빈 문자열은 Falsy)

  - if ('hello') → true로 평가 (내용이 있는 문자열은 Truthy)

  - if (0) → false로 평가 (숫자 0은 Falsy)

# 단축 평가(Short-Circuit Evaluation)

논리 연산자(&&, ||)는 두 피연산자를 모두 평가하지 않고 결과를 결정하는 경우가 있습니다. 이를 단축 평가라고 합니다.

- && (논리 AND): 첫 번째 피연산자가 falsy값이면 뒤의 피연산자를 평가하지 않고 첫번째 피연산자를 반환합니다. 첫 번째 피연산자가 truthy이면 두 번쨰 피연산자를 반환합니다.
  - 활용 : 객체나 속성에 접근하기 전, 해당 값이 유효한지 확인하느데 유용합니다. (예: user && user.name )
- || (논리 OR) : 첫 번째 피연산자가 truthy값이면 뒤의 피연산자를 평가하지 않고 첫번쨰 피연산자를 반환합니다. 첫 번째 피연산자가 falsy이면 두 번쨰 피연산자를 반환합니다.
  - 활용 : 변수에 기본값을 할당할 때 유용합니다. (예: let name = myname || 'default';)
    | 단축 평가 표현식 | 평가 결과 |
    | -------------------- | ------------------------------ |
    | true \|\| anything | true |
    | false \|\| anything | anything |
    | true && anything | anything |
    | false && anything | false |

# 옵셔널 체이닝과 null 병합 연산자

이 두 연산자는 null 또는 undefined 값을 안전하게 다루기 위해 ES11(ECMAScript 2020)에 도입되었습니다.

- ?. (옵셔널 체이닝 연산자) : 객체의 속성에 접근할 떄, 참조가 null 또는 undefined이면 오류를 발생시키지 않고 undefined를 반환합니다. 이 연산자가 없었다면 TypeError가 발생했을 것입니다.
  - obj?.prop : obj가 null이나 undefined면 undefined를 반환
- ?? (null 병합 연산자) : 좌항의 피연산자가 null 또는 undefined일떄만 우항의 값을 반환합니다. 그 외의 falsy값(0, '', falsy 등)에 대해서는 좌항의 값을 그대로 반환합니다.

  - || 연산자와의 차이점 : || 는 falsy값 전체에 대해 동작하지만, ??는 null과 undefined에만 동작합니다. 이 차이 때문에 기본값을 설정할 때 의도하지 않은 동작을 막을 수 있습니다.

  정리:

  - || : Falsy 값이면 기본값 반환
  - ?? : null/undefined일 때만 기본값 반환
  - ?. : 안전하게 프로퍼티 접근
