# 8장 제어문

## 8.1 제어문

- 제어문은 조건에 따라 코드 블록을 실행하거나 반복 실행할 때 사용한다. 일반적으로는 코드는 위에서 아래 방향으로 순차적으로 실행되지만 제어문을 사용하면 **코드의 실행 흐름을 인위적으로 제어할 수 있다.**

<br>

## 8.2 블록문

- 블록문은 0개 이상의 문을 중괄호로 묶은 것으로, 블록이라고 부른다. JS는 블록문을 하나의 실행 단위로 취급한다.
- 블록문은 단독으로 사용하는 것보단 일반적으로 제어문이나 함수를 정의할 때 사용한다.
- 블록문은 언제나 문의 종료를 의미하는 **자체 종결성**을 갖기 때문에 블록문의 끝에는 ;를 붙이지 않는다.

```jsx
// 블록문
{
  var num = 10;
}

// 제어문
var x = 1;
if (x < 10) {
  x++;
}

// 함수 선언문
function sum(a, b) {
  return a + b;
}
```

<br>

## 8.3 조건문

- 조건문은 주어진 조건식에 따라서 코드 블록문의 실행을 결정한다. JS에는 if-else문, switch문이 있다.

### 8.3.1 if-else문

- if-else문은 주어진 조건식(boolean값으로 평가될 수 있는 표현식)에 따라 조건식이 true면 if문의 코드 블록을, false면 else문의 코드 블록을 실행한다.
- if문의 조건식은 boolean 값으로 평가되어야 한다. 만약 if문의 조건식이 boolean 값이 아닌 값으로 평가되면 JS 엔진에 의해 암묵적으로 boolean 값으로 강제 변환된다.
- 조건식을 추가하여 조건에 따라 실행될 코드 블록을 늘리고 싶으면 else if 문을 쓴다.
- 만약 코드 블록 내의 문이 하나뿐이라면 중괄호를 생략할 수 있다.

```jsx
if (조건식1) {
  // 조건식1이 참이면 이 코드 블록이 실행된다.
} else if (조건식2) {
  // 조건식2가 참이면 이 코드 블록이 실행된다.
} else {
  // 조건식이 거짓이면 이 코드 블록이 실행된다.
}
```

- if-else문은 삼항 조건 연산자로 바꿔 쓸 수 있다.

if-else문

```jsx
var x = 2;
var result;

if (x % 2) {
  result = "홀수";
} else {
  result = "짝수";
}

console.log(result); // 짝수
```

삼항 연산자

```jsx
var x = 2;

// 0은 false로 취급된다.
var result = x % 2 ? "홀수" : "짝수";
console.log(result); // 짝수
```

### 8.3.2 switch문

- switch문은 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case문으로 실행 흐름을 옮긴다. switch문의 표현식과 일치하는 case문이 없다면 실행 순서는 default문으로 이동한다. default문은 사용할 수도, 사용하지 않을 수도 있다.
- switch문은 case문에 해당하는 문의 마지막에 break문을 사용해야 한다. break문은 코드 블록에서 탈출하는 역할을 하는데 break문이 없다면 case문의 표현식과 일치하지 않더라도 실행 흐름이 다음 case문으로 연이어 이동한다.
- default문은 switch문의 맨 마지막에 위치하여 해당 문이 종료되면 switch문을 빠져나가기 때문에 break문을 생략한다.

```jsx
var month = 11;
var monthName;

switch (month) {
  case 1:
    monthName = "January";
    break;
  case 2:
    monthName = "February";
    break;
  case 3:
    monthName = "March";
    break;
  case 4:
    monthName = "April";
    break;
  case 5:
    monthName = "May";
    break;
  case 6:
    monthName = "June";
    break;
  case 7:
    monthName = "July";
    break;
  case 8:
    monthName = "August";
    break;
  case 9:
    monthName = "September";
    break;
  case 10:
    monthName = "October";
    break;
  case 11:
    monthName = "November";
    break;
  case 12:
    monthName = "December";
    break;

  default:
    monthName = "Invalid month";
}

console.log(monthName); // November
```

<br>

## 8.4 반복문

- 반복문은 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다. 그 후 조건식을 다시 평가하여 여전히 참인 경우 코드 블록을 다시 실행한다. **이는 조건식이 거짓일 때까지 반복된다.**
- JS에서 반복문에는 for문, while문, do-while문이 있다.

### 8.4.1 for문

- for문은 조건식이 거짓일 때까지 계속 코드 블록을 반복 실행한다.

```jsx
// for문 기본형식
for (변수 선언문 또는 할당문; 조건식; 증감식) {
    조건식이 참인 경우 반복 실행될 문;
}

// 예시
for (var i = 0; i < 2; i++){
    console.log(i);  // 0, 1 출력
}
```

- for문의 변수 선언문, 조건식, 증감식을 모두 생략하면 무한루프가 된다. 무한루프란 코드 블록을 무한히 반복 실행하는 문이다.

```jsx
// 무한루프
for(;;){...}
```

- for문 안에 for문을 사용할 수 있는데 이를 중첩 for문이라 한다.

### 8.4.2 while문

- while문은 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행한다. 그러다 조건문의 평가 결과가 거짓이 되면 코드 블록을 실행하지 않고 while문을 종료한다.
- while문은 실행문에 while문을 탈출할 수 있는 코드가 있어야 한다. (아래 코드에선 count++; 가 이에 해당한다.)

```jsx
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count);
  count++;
}
```

- 조건식의 평가 결과가 언제나 참이면 무한루프가 된다.
- 무한루프를 탈출하기 위해선 코드 블록 내에 if문으로 탈출 조건을 만들고 break문으로 코드 블록을 탈출한다.

```jsx
// 무한루프
while(true){...}
```

### 8.4.3 do-while문

- do-while문은 **코드 블록을 먼저 실행**하고 조건식을 평가한다. (**무조건 실행문은 한 번 이상 실행된다.**)

```jsx
var count = 0;

do {
  console.log(count); // 0 1 2
  count++;
} while (count < 3);
```

<br>

## 8.5 break문

- break문은 레이블 문, 반복문의 코드 블록을 탈출한다.(레이블 문이란 식별자가 붙은 문을 말한다.) 그 이외에 break문을 사용하면 SyntaxError가 발생한다.

```jsx
// foo라는 레이블 식별자가 붙은 레이블 문
foo: console.log("foo");
```

- 레이블 문은 프로그램의 실행 순서를 제어하는 데 사용하는데 레이블 문을 탈출하려면 break문에 레이블 식별자를 지정한다.

```jsx
// foo라는 식별자가 붙은 레이블 블록문
foo: {
  console.log(1);
  break foo; // foo 레이블 문 탈출
  console.log(2);
}

console.log("Done"); // 1 Done 출력
```

<br>

## 8.6 continue문

- continue문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. break문처럼 반복문을 탈출하진 않는다.

```jsx
// Hello World!에서 l의 개수를 출력하는 프로그램
var string = "Hello World!";
var search = "l";
var count = 0;

for (var i = 0; i < string.length; i++) {
  if (string[i] !== search) continue;
  count++; // 조건식이 참이면 이 문은 실행되지 않음
}

console.log(count);
```
