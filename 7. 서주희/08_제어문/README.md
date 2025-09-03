# 08. 제어문

### 블록문

<br>

- 블록문이란 ! **0개 이상의 문을 중괄호로 묶은 것**을 말한다.
  블록문은 코드 블록 또는 블록이라고 부르기도 한다.
  자바스크립트에서는 블록문을 하나의 실행 단위로 취급하기도 한다. **블록문은 단독으로 사용할 수도 있으나 일반적으로 제어문이나 함수를 정의 할 때 사용한다.**

<br>

일반적으로는 문의 끝에는 세미콜론을 붙이나, 블록문은 문의 종료를 의미하기에 블록문의 끝에는 세미콜론을 붙이지 않는다.

```JavaScript
//블록문
{
    var foo = 10;
}

//제어문
var x = 1;
if (x<10>) {
    x++;
}

//함수 선언문
function sum(a,b) {
    return a + b;
}
```

<br>

---

### 조건문

<br>

- 조건문은 주어진 조건식의 평가 결과에 따라 코드 블록의 실행을 결정한다.

- 조건 식은 불리언 값으로 평가될 수 있는 표현식이다.

  **_자바스크립트는 if ...else 문과 switch 문으로 두 가지 조건문을 제공한다._**

<br>

1. if...else 문

<br>

if ... else 문은 주어진 조건식의 평가 결과, 즉 **논리적 참 또는 거짓**에 따라 실행할 코드 블록을 결정한다.

**_조건식의 평가 결과가 true일 경우 if 문의 코드 블록이 실행되고, false 일 경우 else 문의 코드 블록이 실행된다._**

<br>

```JavaScript
if(조건식) {
 //조건식이 참이면 이 코드 블록이 실행
 } else {
 //조건식이 거짓이면 이 코드 블록이 실행

 }
```

따라서 if 문의 조건식은 불리언 값으로 평가되어야 한다.

만일 if 문의 조건식이 불리언 값이 아닌 값으로 평가되는 상황이 발생하면 , 자바스크립트 엔진에 의해 암묵적으로 불리언 값으로 강제 변환되어
실행할 코드 블록을 결정하게 된다.

조건식을 추가하여 조건에 따라 실행될 코드 블록을 늘리고 싶다면 else if 문을 사용하면 된다.

```JavaScript
if (조건식1) {
    //조건식1이 참이면 이 코드 블록이 실행된다.
} else if (조건식2){
    //조건식2가 참이면 이 코드 블록이 실행된다.
} else {
    //조건식1과 조건식2가 모두 거짓이면 이 코드 블록이 실행된다.
}
```

else if 문과 else 문은 **필수가 아니다.** if 문과 else 문은 2번 이상 사용할 수 없으나 **else if 문은 여러번 사용해도 된다.**

다음의 예제를 살펴보면,

```JavaScript
var num = 2;
var kind;

//if 문
if (num > 0) {
kind = '양수'; // 음수를 구별 할 수 없다 : 조건문은 양수인 경우만 처리, 0이거나 음수인 경우는 다루지 x

}
console.log(kind); // 양수
// 이 경우 num=-1일때, console.log(kind);는 undefined를 출력.


// if ...else 문
if (num > 0 ) {
    kind = '양수';
} else {
    kind = '음수' ; //0은 음수가 아니다. ---> 논리적 오류 포함!! if...else if 문으로 논리적 오류 수정 가능

}
console.log(kind); //양수

// if...else if 문
if (num > 0 ) {
    kind = ' 양수 ';
} else if (num < 0) {
    kind = '음수';
}   else {
    kind = '영';
}
console.log(kind); //양수
```

만일 코드 블록 내의 문이 하나뿐이라면 문법적으로는 중괄호를 생략 가능하다.

```JavaScript
var num = 2;
var kind;

if(num >0) kind = '양수' ;
else if (num < 0) kind = '음수' ;
else                kind ='영';

console.log(kind); //양수
```

대부분의 if ...else 문은 삼항 조건 연산자로 바꿔 쓸 수 있다.

예시:

<br>

```JavaScript
// x가 짝수이면 result 변수에 문자열 '짝수'를 할당하고, 홀수이면 문자열 '홀수'를 할당한다.
var x = 2;
var result;

if (x % 2 ) { // 2% 2는 0이다. 이때 0은 false로 암묵적 강제 변환된다.
    result = '홀수';
}   else {
    result = '짝수';
}

console.log(result); //짝수
```

위 예제는 다음과 같이 삼항 조건 연산자로 바꿔 쓸 수 있다.

```JavaScript
var x = 2 ;

// 0 은 false로 취급된다.
var result = x % 2 ? '홀수' : '짝수' ;
console.log(result); //짝수
```

만일 조건에 따라 단순히 값을 결정하여 변수에 할당하는 경우 if...else 문보다 삼항 조건 연산자를 사용하는 편이 가독성이 좋다.
하지만 조건에 따라 실행해야 할 내용이 복잡하여 여러 줄의 문이 필요하다면 if ...else 문을 사용하는 편이 가독성이 좋을 것이다.

2. switch 문

- switch문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다.
  case 문은 상황(case)을 의미하는 표현식을 지정하고 콜론으로 마친다. 그리고나서 그 뒤에 실행할 문들을 위치시킨다.

switch문의 표현식과 일치하는 case 문이 없다면 실행 순서는 default 문으로 이동한다. default 문은 필수는 아니다.

```JavaScript
switch (표현식) {
    case 표현식1:
        switch 문의 표현식과 표현식1이 일치하면 실행될 문;
        break;
    case 표현식2:
        switch 문의 표현식과 표현식2가 일치하면 실행될 문;
        breack;
    default:
        switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;

}
```

if...else 문의 조건식은 불리언 값으로 평가되어야 하나 switch 문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많다.

다시말해, switch문은 논리적 참,거짓 보다는 다양한 상황(case)에 따라 실행할 코드 블록을 결정할 때 사용한다.

```JavaScript
let day = '화요일';
let result;

switch (day) {
  case '월요일':
  case '화요일':
  case '수요일':
  case '목요일':
  case '금요일':
    result = '오늘은 평일입니다.';
    break;
  case '토요일':
  case '일요일':
    result = '오늘은 주말입니다!';
    break;
  default:
    result = '올바른 요일이 아닙니다.';
}

console.log(result); // "오늘은 평일입니다."
```

이 예제는 특정 요일에 따라 '주말' 또는 '평일' 메시지를 출력하는데

switch 문에서는 폴스루라는 현상이 발생한다. **폴스루(fall-through)** 는 switch 문에서 특정 case에 break 문이 없을 때, 다음 case로 코드가 계속 실행되는 현상을 말한다.

본 예제에서는 switch 문의 표현식의 평가 결과와 일치하는 case문 ( `'화요일'`)으로 실행 흐름이 이동하여 문을 실행한 것은 맞지만 문을 실행한 후 switch를 탈출하지 않고 switch문이 끝날 때 까지 이후의 모든 case 문과 default 문을 실행했다.

위 예시 코드에서

1. switch 문은 `case '화요일':` 과 일치하는 코드를 찾는다.

2. case `'화요일':` 에는 코드가 없고 break도 없으므로, 코드는 자동으로 다음 case인 case '수요일':로 넘어간다.

3. 이런 식으로 break가 나올 때까지 계속 진행된다. 이 예시에서는 `'월요일'`, `'화요일'`, `'수요일'`, `'목요일'` 모두 break가 없으므로 최종적으로 `result = '오늘은 평일입니다.';` 코드가 실행되고 break를 만나 switch 문을 빠져나간다.

위와 같은 일련의 과정이 이루어졌다.

이러한 결과가 나온 이유는 case 문에 해당하는 문의 마지막에 break 문을 사용하지 않았기 때문이다. 폴스루가 일어나지 않으려면 각 case 마다 break를 넣어줘야 한다.

**default 문에는 break문을 생략하는 것이 일반적이다.**

이러한 폴스루를 활용하는 경우도 존재한다.

다음과 같은 월의 일수를 구할 때는 폴스루를 적극 활용하기도 한다.

```JavaScript
function getDaysInMonth(month) {
  let days;

  switch (month) {
    case '1':
    case '3':
    case '5':
    case '7':
    case '8':
    case '10':
    case '12':
      days = 31;
      break;
    case '4':
    case '6':
    case '9':
    case '11':
      days = 30;
      break;
    case '2':
      days = 28; // 윤년은 고려하지 않는다고 가정
      break;
    default:
      days = '유효하지 않은 월입니다.';
  }
  return days;
}

console.log(getDaysInMonth('3')); // 출력: 31
console.log(getDaysInMonth('4')); // 출력: 30
console.log(getDaysInMonth('2')); // 출력: 28
console.log(getDaysInMonth('13')); // 출력: 유효하지 않은 월입니다.
```

위 예제는 각 case 마다 break를 넣지 않고, `30일`,`31일`,`28일`로 나뉘어지는 월들을 풀스루를 이용하여 효과적으로 처리한다.

<br>

3. 반복문

반복문은 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다. 그 후 조건식을 다시 평가하여 여전히 참인 경우 코드 블록을 다시 실행한다. 이는 조건식이 거짓일 때까지 반복된다.

자바스크립트는 세 가지 반복문인 for문, while문, do ...while문을 제공한다.

- for 문

for문은 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행한다.

```JavaScript
for ( 변수 선언문 또는 할당문; 조건식; 증감식) {
    조건식이 참인 경우 반복 실행될 문;
}
```

예제 :

```JavaScript
for (var i = 0; i < 2; i++ ) {
  console.log(i);
}
```

```
0
1
```

위 예제의 for 문은 i 변수가 0으로 초기화된 상태에서 시작하여 i가 2보다 작을 때까지 코드 블록을 2번 반복 실행한다.

```JavaScript
for(var i = 1; i >= 0; i--) {
  console.log(i);
}
```

for문의 변수 선언문, 조건식, 증감식은 모두 옵션이므로 반드시 사용할 필요는 없으나 , 어떤 식도 선언하지 않으면 무한루프에 빠진다.

무한루프란 코드 블록을 무한히 반복 실행하는 문이다.

```JavaScript
//무한루프
for (;;) {...}
```

- while 문

while문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행한다. for문은 반복 횟수가 명확할 때 주로 사용하고 while 문은 반복 횟수가 불명확할 때 주로 사용한다.

while문은 조건문의 평과 결과가 거짓이 되면 코드 블록을 실행하지 않고 종료한다. 만약 조건식의 평가 결과가 불리언 값이 아니면 불리언 값으로 강제 변환하여 논리적 참, 거짓을 구별한다.

```JavaScript
var count = 0;

// count 가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count); // 0 1 2
  count ++
}
```

조건식의 평가 결과가 언제나 참이면 무한루프가 된다. -> while은 거짓일 때만 종료할 수 있으므로 !

```JavaScript
//무한루프
while (true) {...}
```

무한루프에서 탈출하기 위해서는 코드 블록 내에 if 문으로 탈출 조건을 만들고 break 문으로 코드 블록을 탈출한다.

```JavaScript
var count = 0;

//무한루프
while (true) {
  console.log(count);
  count++;

  //count가 3이면 코드 블록을 탈출한다.
  if (count ===3 ) break;
} // 0 1 2
```

- do...while 문

do ...while 문은 코드 블록을 먼저 실행하고 조건식을 평가한다. 따라서 코드 블록은 무조건 한 번 이상 실행된다.

```JavaScript
var count = 0;

//count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
do {
  console.log(count); // 0 1 2
  count++;
} while (count < 3);
```

4. break 문

- break문은 레이블 문, 반복문 또는 switch 문의 코드 블록을 탈출한다. 레이블 문, 반복문, switch 문의 코드 블록 외에 break 문을 사용하면 SytaxError 가 발생한다.

```JavaScript
var string = 'Hello World.';
var search = 'l';
var index;

//문자열은 유사 배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  //문자열의 개별 문자가 'l'dlaus
  if (string[i] === search) {
    index = i;
    break; //반복문을 탈출한다.
  }
}

console.log(index); //2
```

위 예제 코드에서

1. break 문은 if (string[i] === search) 조건이 **true**가 될 때 실행된다.

2. for 문은 i = 0부터 시작해 문자열을 한 글자씩 확인한다.

3. i가 2가 되면 string[2]는 'l'이므로 if문의 조건('l' === 'l')이 충족된다.

4. if문 안의 코드가 실행되면서 index 변수에 2가 할당되고 바로 이어서 break; 문이 실행된다.

5. break 문은 현재 진행 중인 for 반복문 자체를 즉시 멈추고 빠져나오게 한다.
