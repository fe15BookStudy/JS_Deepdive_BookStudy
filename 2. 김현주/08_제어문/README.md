# 블록문 : 0개 이상의 문을 중괄호로 묶은 것

```javascript
// 블록문
{
  var foo = 10;
  console.log(foo);
}
```

# 조건문

- if...else문 : 조건에 따른 분기 처리

```javascript
var num = 2;
var kind;

// if 문
if (num > 0) {
  kind = '양수'; // 음수를 구별할 수 없다
}
console.log(kind); // 양수

// if…else 문
if (num > 0) {
  kind = '양수';
} else {
  kind = '음수'; // 0은 음수가 아니다
}
console.log(kind); // 양수

// if…else if 문
if (num > 0) {
  kind = '양수';
} else if (num < 0) {
  kind = '음수';
} else {
  kind = '영';
}
console.log(kind); // 양수
```

# 삼항 조건 연산자: 삼항 연산자를 이용한 간단한 조건 처리

```javascript
// x가 짝수이면 '짝수'를 홀수이면 '홀수'를 반환한다.
var x = 2;

// 0은 false로 취급된다.
var result = x % 2 ? '홀수' : '짝수';
console.log(result); // 짝수
```

# switch문 : 여러 조건을 체계적으로 처리

- 여러 개의 if...else if 문을 연속해서 쓰는 것보다 훨씬 깔끔하고 가독성이 좋습니다. 하나의 변수나 표현식의 값에 따라 여러 가지 경우의 수를 처리할 때 사용합니다.
- break의 중요성: case 블록 끝에 break가 없으면, 일치하는 case를 찾더라도 switch 문을 빠져나오지 않고 다음 case의 코드를 계속 실행합니다. 이를 **"fall-through(폴스루)"**라고 부릅니다. 이 현상은 의도치 않은 버그를 유발할 수 있으므로, 대부분의 경우 break를 꼭 써주는 것이 좋습니다.
- default: 모든 case가 일치하지 않을 때 실행되는 기본값입니다. if...else if 문의 else와 같은 역할을 합니다. default는 switch 문 어디에든 위치할 수 있지만, 일반적으로 가독성을 위해 맨 마지막에 둡니다.

```javascript
switch (표현식) {
 case 표현식1:
   switch 문의 표현식과 표현식1이 일치하면 실행될 문;
   break;
 case 표현식2:
   switch 문의 표현식과 표현식2가 일치하면 실행될 문;
   break;
 default;
   switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
}
```

```javascript
// 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1:
    monthName = 'January';
    break;
  case 2:
    monthName = 'February';
    break;
  case 3:
    monthName = 'March';
    break;
  case 4:
    monthName = 'April';
    break;
  case 5:
    monthName = 'May';
    break;
  case 6:
    monthName = 'June';
    break;
  case 7:
    monthName = 'July';
    break;
  case 8:
    monthName = 'August';
    break;
  case 9:
    monthName = 'September';
    break;
  case 10:
    monthName = 'October';
    break;
  case 11:
    monthName = 'November';
    break;
  case 12:
    monthName = 'December';
    break;
  default:
    monthName = 'Invalid month';
}

console.log(monthName); // November
```

# 반복문

- for문 : 횟수가 정해진 반복. 초기화, 조건, 증감식을 한 줄에 작성하는 반복문

```javascript
for(초기화식; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문;
}
```

```javascript
for (var i = 0; i < 2; i++) {
  console.log(i);
}
```

- 초기화(initialization): 루프가 시작될 때 단 한 번 실행됩니다. 보통 반복 횟수를 셀 변수를 선언하고 초기화합니다.

- 조건식(condition): 매 반복이 시작되기 전에 평가됩니다. 이 조건식이 **true**일 때만 코드 블록이 실행됩니다. false가 되면 루프가 종료됩니다.

- 증감식(increment/decrement): 각 반복이 끝날 때마다 실행됩니다. 보통 초기화 변수의 값을 증가시키거나 감소시킵니다.

# while문과 do...while문

- while문 : 조건이 참인 동안 코드 블록 반복 실행

  - 동작 방식: 루프가 시작되기 전에 조건식을 먼저 평가합니다. 조건식이 **true**이면 코드 블록을 실행하고, 다시 조건식을 평가하는 과정을 반복합니다.
  - 무한 루프: 조건식이 항상 true인 경우, 루프가 영원히 멈추지 않는 무한 루프에 빠질 수 있습니다. 이를 방지하려면 루프 내부에서 조건식을 false로 만들 수 있는 코드를 포함해야 합니다.

  ```javascript
  var count = 0;
  // count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
  while (count < 3) {
    console.log(count);
    count++;
  } // 0 1 2
  ```

- do...while문 : 코드 블록을 먼저 실행한 후 조건 확인(최소 1번은 실행)
  - while 문과 비슷하지만, 최소 한 번은 코드 블록을 실행한다는 점에서 차이가 있습니다.
  - 동작 방식: 먼저 do 블록의 코드를 실행한 후, while 괄호 안의 조건식을 평가합니다. 조건이 true이면 다시 do 블록을 실행합니다. 이 특징 때문에 사용자의 입력을 최소 한 번은 받아야 할 때 유용하게 쓰입니다.

# break문

- 반복문이나 switch문을 완전히 빠져나올 때 사용
- 레이블과 함께 사용하여 중첩된 루프에서 특정 루프 탈출 가능
- switch문과 case실행 후 다음 case로 넘어가지 않도록 제어

```javascript
  if (true) {
  break; // Uncaught SyntaxError: Illegal break statement(문법에러)
}
```

# continue문

- 반복문에서 현재 반복을 건너뛰고 다음 반복으로 이동
- for, while, do...while 루프에서 사용 가능
- 동작 방식: continue가 실행되면, 그 아래에 있는 코드는 무시됩니다.
  - for 문에서는 continue 후 증감식으로 이동합니다.
  - while 문에서는 continue 후 조건식으로 돌아갑니다.
- 조건을 만족할 때 나머지 코드를 실행하지 않고 다음 반복으로 넘어감

```javascript
// continue 문을 사용면 if 문 밖에 코드를 작성할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 카운트를 증가시키지 않는다.
  if (string[i] !== 'l') continue;

  count++;
}
```
