# 산술 연산자

- 이항 산술 연산자 : +, -, \*, / , %(덧셈, 뺄셈, 곱셈, 나눗셈, 나머지)
- 단항 산술 연산자: ++(증가), --(감소), +(양수), -(음수)
- 문자열 연결 연산자 : + 연산자로 문자열 결합

# 할당 연산자

- 기본 할당 : =
- 복합 할당: +=, -=, \*=, /=, %=

# 비교 연산자

- 동등/일치 비교 : ==, ===, !=, !==

```jsx
//예제 7-13
//동등 비교, 결과를 예측하기 어렵다.
'0' == ''; // -> false
0 ==''; //  -> true
0 = '0'; // -> true
false = 'false'; // -> false
false = '0'; // -> true
false = null; // -> null
false = undefined; // -> false
```

- 대소 관계 비교 : >, <, >=, <=

# 삼항 조건 연산자

- 조건식? 참일때 값: 거짓일때 값 형식
- if...else문의 간단한 대안

# 논리 연산자

- ||(논리합, OR)
- &&(논리곱, AND)
- !(부정, NOT)

```jsx
//논리합 연산자
true || true; // -> true
true || false; // -> true
false || true; // - > true
false || true; // -> false

//논리곱 연산자
true && true; // -> true
true && false; // -> false
false && true; // -> false
false && false; // -> false
```

# 기타 연산자들

- 쉼표 연산자(,) : 여러 표현식을 순차 실행
- 그룹 연산자(()): 연산 우선순위 조절
- typeof연산자: 데이터 타입 확인
- 지수 연산자(\*\*) : 거듭제곱 계산
- 그 외 연산자들 : ? , ??, del, new, instanceof, in 등
