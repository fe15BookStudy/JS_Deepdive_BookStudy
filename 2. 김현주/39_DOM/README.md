## 39.1 노드
### 39.1.1 HTML 요소와 노드 객체
HTML 요소는 HTML 문서를 구성하는 개별적인 요소를 의미하며, 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 요소 노드 객체로 변환됩니다.

### 노드 객체의 상속 구조
DOM을 구성하는 노드 객체는 ECMAScript 사양에 정의된 표준 빌트인 객체가 아니라 브라우저 환경에서 추가로 제공하는 호스트 객체입니다. 노드 객체는 JavaScript 객체이므로 프로토타입에 의한 상속 구조를 갖습니다.

### 39.1.2 노드 객체의 타입
DOM은 노드 객체의 계층적 구조로 구성되며, 노드 객체는 종류가 있고 상속 구조를 갖습니다.
주요 노드 타입:
- 문서 노드: DOM 트리의 최상위에 존재하는 루트 노드 (document 객체)
- 요소 노드: HTML 요소를 가리키는 객체
- 어트리뷰트 노드: HTML 요소의 어트리뷰트를 가리키는 객체
- 텍스트 노드: HTML 요소의 텍스트를 가리키는 객체
```javascript
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li>
    </ul>
    <script src="app.js"></script>
  </body>
</html>
```

### 39.1.3 노드 객체의 상속 구조
DOM을 구성하는 노드 객체는 자신의 구조와 정보를 제어할 수 있는 DOM API를 통해 HTML의 구조나 내용 또는 스타일 등을 동적으로 조작할 수 있습니다.
```javascript
<!DOCTYPE html>
<html>
<body>
  <input type="text">
  <script>
  //input 요소 노드 객체를 선택
  const $input = document.querySelector('input);

  //input 요소 노드 객체의 프로토 타입 체인
  console.log(
    Object.getPrototypeOf($input) === HTMLInputElement.prototype,
    Object.getPrototypeOf(HTMLInputElement.prototype) === HTMLInputElement.prototype,
    Object.getPrototypeOf(HTMLInputElement.prototype) === Element.prototype,
    Object.getPrototypeOf(Element.prototype) === Node.prototype,
    Object.getPrototypeOf(Node.prototype) === EventTarget.prototype,
    Object.getPrototypeOf(EventTarget.prototype) === Object.prototype
  ); //모두 true
  </script>
</body>
</html>
```


## 39.2 요소 노드 취득
### 39.2.1 id를 이용한 요소 노드 취득
- document.getElementById() 메서드 사용
- 유일한 id값을 가진 첫번째 요소 반환
- 해당 요소가 없으면 null 반환
```javascript
<!DOCTYPE html>
<html>
  <body>
    <div id="foo"></div>
    <script>
    let foo = 1;

    // id 값과 동일한 이름 전역 변수가 이미 선언되어 있으면 노드 객체가 재할당되지 않는다.
    console.log(foo);
    </script>
  </body>
</html>
```

### 39.2.2 태그 이름을 이용한 요소 노드 취득
- document.getElementsByTagName() 메서드 사용
- HTMLCollection 객체 반환 (live 컬렉션)
- 모든 해당 태그 요소들을 포함

## 39.2 노드 탐색
### 39.2.3 class를 이용한 요소 노드 취득
- document.getElementsByClassName() 메서드 사용
- 인수로 전달한 class 값을 갖는 모든 요소들 탐색
- HTMLCollection 객체 반환 (live 컬렉션)
- 공백으로 구분하여 여러 개의 class 지정 가능
```javascript
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li class="fruit apple">Apple</li>
      <li class="fruit banana">Banana</li>
      <li class="fruit orange">Orange</li>
    </ul>
    <script>
     //class 값이 'fruit'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
     const $elems = document.getElementsByClassName('fruit');

     //취득한 모든 요소의 CSS color 프로퍼티 값을 변경한다.
     [...$elems].forEach(elem => {elem.style.color = 'red';});

     //class값이 'fruit apple'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
     const $apples = document.getElementsByClassName('fruit apple');

     //취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
     [...$apples].forEach(elem => elem.style.color = 'blue';);
    </script>
  </body>
</html>
```

## HTMLCollection 객체의 특성
live 객체의 문제점:
- 실시간으로 노드 객체의 상태 변경을 반영
- DOM 컬렉션을 사용하면 예상과 다른 동작 발생 가능
- for 문으로 순회하면서 노드 객체의 상태를 변경하면 주의 필요
해결 방법:
- for 문을 역방향으로 순회
- while 문 사용하여 HTMLCollection에 요소가 남아 있을 때까지 무한 반복
- 배열로 변환하여 사용 (HTMLCollection → Array)
### 39.2.4 CSS 선택자를 이용한 요소 노드 취득
- querySelector(): 첫 번째 요소 노드만 반환
- querySelectorAll(): 모든 요소를 NodeList로 반환
- CSS 선택자 문법 사용 가능
```javascript
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li class="apple">Apple</li>
      <li class="banana">Banana</li>
      <li class="orange">Orange</li>
    </ul>
    <script>
    //class 어트리뷰트 값이 'banana'인 첫번째 요소 노드를 탐색하여 반환한다.
    cosnt $elem = document.querySelector('banana');

    //취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
    $elem.style.color = 'red';
    </script>
  </body>
</html>
```
```javascript
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li class="apple">Apple</li>
      <li class="banana">Banana</li>
      <li class="orange">Orange</li>
    </ul>
    <script>
    //ul 요소의 자식요소인 li요소를 모두 탐색하여 반환한다.
    const $elems = document.querySelectAll('ul > li')'
    //취득한 요소 노드들은 NodeList 객체에 담겨 반환된다.
    console.log($elems); //NodeList(3) [li.apple, li.banana, li.orange]

    //취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
    //NodeList는 forEach 메서드를 제공한다.
    $elems.forEach(elem => {elem.style.color = 'red';});
    </script>
  </body>
</html>
```
## 39.2.5 특정 요소 노드를 취득할 수 있는지 확인
- Element.prototype.matches() 메서드
   - 전달된 CSS 선택자와 요소가 일치하는지 확인할 수 있음.
   - 반환값은 true 또는 false.
   - 주로 이벤트 위임(event delegation) 상황에서 유용.
```javascript
const $apple = document.querySelector('.apple');

console.log($apple.matches('#fruits > li.apple')); // true
console.log($apple.matches('#fruits > li.banana')); // false

```
- #fruits > li.apple 은 실제로 apple 요소이므로 true.
- #fruits > li.banana 는 apple 요소가 아님 → false.
## 39.2.6 HTMLCollection과 NodeList
1) 공통점
 - 둘 다 유사 배열 객체(array-like) 이며 이터러블.
 - for...of 문이나 스프레드 문법을 사용해 배열로 변환 가능.

2) 차이점

- HTMLCollection
   - getElementsByTagName, getElementsByClassName 등이 반환.
   - Live 객체: DOM 구조 변경이 실시간으로 반영됨.
- NodeList
   - querySelectorAll 등이 반환.
   - 대부분은 Non-live 객체: 반환 시점의 상태만 유지.

👉 따라서 HTMLCollection은 DOM 변경 즉시 반영, NodeList는 대부분 그렇지 않음.
```javascript
const $elems = document.getElementsByClassName('red');
console.log($elems); 
// HTMLCollection(3) [li.red, li.red, li.red]
```
- class="red" 인 요소들을 실시간으로 담음.
- 이후 DOM에서 li.red 를 추가/삭제하면 컬렉션도 자동 반영됨.

## 39.3 자식 노드 존재 확인
- Node.prototype.hasChildNodes() 메서드 사용
- 자식 노드가 존재하면 true, 없으면 false 반환
- 텍스트 노드도 자식 노드로 포함하여 확인
- 대안: children.length 또는 childElementCount 프로퍼티 사용
### 39.3.1 공백 텍스트 노드
- HTML 요소 사이의 공백, 탭, 줄바꿈도 텍스트 노드로 생성
- DOM 트리 구조에서 주의해야 할 요소

### 39.3.2 자식 노드 탐색
주요 프로퍼티들:
- Node.prototype.childNodes: 모든 자식 노드 (텍스트 노드 포함)
- Element.prototype.children: 요소 노드만
- Node.prototype.firstChild/lastChild: 첫 번째/마지막 자식 노드
- Element.prototype.firstElementChild/lastElementChild: 첫 번째/마지막 요소 노드
### 39.3.3 부모 노드 탐색
- Node.prototype.parentNode 프로퍼티 사용
```javascript
<!DOCTYPE html>
<html>
<body>
  <div id="foo">Hello</div>
  <script>
  //요소 노드의 텍스트 노드는 firstChild 프로퍼티로 접근할 수 있다.
  console.log(document.getElementById('foo').firstChild); // #text
  </script>
</body>
</html>
```
### 39.3.4 형제 노드 탐색39.3.4 형제 노드 탐색
- Node.prototype.previousSibling/nextSibling: 이전/다음 형제 노드
- Element.prototype.previousElementSibling/nextElementSibling: 이전/다음 형제 요소 노드

## 39.4 노드 정보 취득
- Node.prototype.nodeType: 노드 타입 (요소: 1, 텍스트: 3, 문서: 9)
- Node.prototype.nodeName: 노드 이름

## 39.5 요소 노드의 텍스트 조작
### 39.5.1 nodeValue
- 텍스트 노드의 텍스트 값 접근/변경
- 요소 노드에서는 null 반환

### 39.5.2 textContent
- 요소 노드의 모든 텍스트 내용 접근/변경
- HTML 마크업 무시하고 텍스트만 처리

## 39.6 DOM 조작
- innerHTML: HTML 마크업을 포함한 텍스트 설정/취득
- CSS에 의해 비표시되는 요소의 텍스트도 반환

## HTMLCollection과 NodeList
- HTMLCollection: 실시간(live) 객체, DOM 변경사항 즉시 반영
- NodeList: 대부분 정적(non-live) 객체이지만, childNodes는 live
- 배열 메서드 사용 시 Array.from()으로 변환 필요