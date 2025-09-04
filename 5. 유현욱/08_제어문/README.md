# 모던 자바스크립트 Deep Dive

## 08장 제어문

### 조건문

조건문은 조건식의 평가 결과에 따라 코드블록의 실행을 결정한다.

if...else문은 조건식의 평가 결과가 true이면 if문의 블록이 실행되고 false이면 else문의 블록이 실행된다. 조건을 더 추가하고 싶으면 else if를 넣으면된다. else if문과 else는 옵션이고 if와 else는 2번이상 사용할 수 없지만 else if문은 여러번 사용할 수 있다.

```jsx
var n=10;
if(n>0) {
  console.log('양수');
}
else {
  console.log('음수');
}

//else if
if(n>0) {
  console.log('양수');
}
else if(n<0>) {
  console.log('음수');
}
else {
  console.log('0');
}
```

조건에 따라 단순히 값을 결정하여 변수에 할당하는 경우 if...else문 보다 삼항연산자를 사용하는 것이 가독성이 좋다.
하지만 조건이 많고 복잡하여 많은 줄이 필요하다면 if...else문을 사용하는 것이 좋다.

```jsx
var n = 10;
var result = n ? (n > 0 ? "양수" : "음수") : "0";

console.log(result); // 양수
```

#### switch문

스위치 문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case문으로 실행흐름을 옮긴다. case문은 상황을 의미하는 표현식을 지정하고 콜론으로 마친다. 그리고 뒤에 실행시킬 문들을 위치시킨다. switch문의 표현식과 일치하는 case문이 없으면 default 문으로 이동한다. default문은 옵션이다.

```jsx
switch(조건식){
  case 1:
    case1일때 실행
    break;
  case 2:
    case2일때 실행
    break;
  case 3:
    case3일때 실행
    break;
  default:
    default일때 실행
}
```

switch문을 작성할 때 조심해야할 점이 있는데 바로 break문을 잘 작성해야한다는 것이다. break를 잘 작성하지 않으면 다른 case문과 default문을 실행하고 switch문을 빠져나갈 수 있다. 이러한 현상을 폴스루(fall through)라고 한다.

```jsx
var month=11;
var monthName;
switch(month){
  case1: monthName='January';
  case2: monthName='Febuary';
  case3: monthName='March';
  case4: monthName='April';
  case5: monthName='May';
  case6: monthName='June';
  case7: monthName='July';
  case8: monthName='August';
  case9: monthName='September';
  case10: monthName='October';
  case11: monthName='November';
  case12: monthName='December';
  default: monthName='Invalid month';
}
console.log(monthName); Invalid month

```

month를 11로 했으면 monthName이 'November'로 지정되어야하는데 break를 작성하지 않아서 default까지 내려간것이다. 그래서 알맞게 코드를 고쳐야한다면 case문이 끝나기전에 break를 작성 해야한다.

---

### 반복문

자바스크립트에서는 세가지 반복문인 for문, while문, do..while문을 제공한다.

for문은 조건식이 거짓으로 평가될 때까지 코드를 반복실행한다.

```jsx
for(변수 선언문 또는 할당문; 조건식; 증감식){
  조건식이 참인 경우 반복해서 실행될 문
}

for(var i=0; i<2; i++){
  console.log(i);
}
//0
//1

```

while문은 주어진 조건식의 평가결과가 참이면 코드블록을 계속해서 반복 실행한다. for문은 반복횟수가 명확할때 주로 사용하고 while문은 불명확할 때 주로 사용한다.

```jsx
var count = 0;
while (count < 3) {
  console.log(count);
  count++;
}
// 0 1 2
```

do..while문은 코드블록을 먼저 실행하고 조건식을 평가한다. 그래서 무조건 한번이상 코드블록이 실행된다.

```jsx
var count = 0;
do {
  console.log(count);
  count++;
} while (count < 3);

//0 1 2
```

---

### break문

break문은 레이블 문, 반복문 또는 스위치문의 코드 블록을 탈출한다. 이외에 사용한다면 문법에러가 나타난다.

참고로 레이블 문이란 식별자가 붙은 문을 말한다.

```jsx
hyun: console.log("wook");

yoo: {
  console.log("hyun");
  break yoo; // yoo 레이블 블록문을 탈출한다.
  console.log("wook");
}
// hyun만 출력된다.
```

중첩 반복문에서 유요하게 쓰일 수 있다. 그 밖의 경우에는 권장하지 않는다.

```jsx
outer: for (var i = 0; i < 3; i++) {
  for (varj = 0; j < 3; j++) {
    if (i + j === 3) break outer;
    console.log("inner[${i}, ${j}]");
  }
}

// 레이블문을 지정안하고 그냥 break만쓴다면 안쪽 반복문만 빠져나오고 바깥쪽 반복문을 못빠져나옴
```

### continue문

continue문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. break문처럼 탈출하지는 않는다.

```jsx
var string = "Hello World";
var search = "l";
var count = 0;
// 문자 개수를 찾는 코드
for (var i = 0; i < string.length; i++) {
  if (string[i] !== search) continue;
  count++;
}
console.log(count); //3

``;
```
