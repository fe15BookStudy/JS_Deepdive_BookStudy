## DOM(Document Object Model)이란?
- 브라우저의 렌더링 엔진이 HTML 문서를 파싱(parsing)하여 문서의 계층적 구조와 정보를 표현하는 트리 자료구조.
- 이 트리 구조의 각 노드는 HTML 문서의 요소, 속성, 텍스트 등을 객체로 표현한다.
- DOM은 단순히 구조 표현에 그치지 않고, 이를 조작할 수 있는 API(프로퍼티, 메서드) 를 제공한다.
→ 즉, HTML 문서 내용이나 스타일을 자바스크립트로 동적으로 바꿀 수 있다.
## 39.1 노드
- DOM 트리의 기본 단위
- HTML 문서의 모든 요소, 속성, 텍스트가 각각 노드로 표현된다.
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
<div class="greeting">Hello</div>
```
- <div> 자체는 요소 노드
- class="greeting" 은 어트리뷰트 노드
- "Hello" 는 텍스트 노드

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
- DOM은 트리 자료구조로 표현된다.
- 노드 간 관계:
  - 부모(parent), 자식(child), 형제(sibling)
- 루트 노드(root): document 노드
- 자식이 없는 노드: leaf node (예: 텍스트 노드)
```javascript
<ul id="fruits">
  <li>Apple</li>
  <li>Banana</li>
</ul>
```
트리 구조:
- document
   - html
      - body
        - ul#fruits
           - li → "Apple"
           - li → "Banana"
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
### 39.1.4 노드 객체의 타입과 상속 구조
(1) 노드 타입
- DOM은 총 12종류의 노드 타입이 있음. 그 중 중요한 4가지:
  - Document
  - Element
  - Attribute
  - Text

(2) 프로토타입 체인
 - 모든 노드 객체는 Object → EventTarget → Node → Element → HTMLElement → 구체적 요소 인터페이스 순으로 상속.
 - 예: <input> 요소
    - Object → EventTarget → Node → Element → HTMLElement → HTMLInputElement
```javascript
const input = document.querySelector('input');
console.log(Object.getPrototypeOf(input) === HTMLInputElement.prototype); // true
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
1. querySelector / querySelectorAll

- querySelector
  - 인수로 전달된 CSS 선택자와 일치하는 첫 번째 요소 노드만 반환.
  - 없으면 null.
  - 반환 타입: Element 객체.
- querySelectorAll
  - 일치하는 모든 요소 노드를 반환.
  - 반환 타입: NodeList (유사 배열, forEach 사용 가능).
  - NodeList는 대개 non-live라서 DOM이 바뀌어도 즉시 반영되지 않음.

| 분류  | API                        | 반환 타입          | 특징                      |
| --- | -------------------------- | -------------- | ----------------------- |
| 선택  | getElementById             | Element        | 단일 반환                   |
| 선택  | getElementsByClassName     | HTMLCollection | live                    |
| 선택  | querySelectorAll           | NodeList       | 보통 non-live, forEach 가능 |
| 탐색  | parentNode / parentElement | Node / Element | 부모 탐색                   |
| 탐색  | children                   | HTMLCollection | 요소 자식만                  |
| 탐색  | nextElementSibling         | Element        | 형제 탐색                   |
| 정보  | nodeType                   | Number         | 1, 3, 9 등               |
| 정보  | nodeName                   | String         | 태그명, #text, #document   |
| 텍스트 | nodeValue                  | String         | 텍스트 노드 전용               |
| 텍스트 | textContent                | String         | 내부 전체 텍스트               |

2. Element.prototype.matches
 - 특정 요소가 주어진 CSS 선택자 조건에 부합하는지 확인할 때 사용.
 - 반환값: true / false.
 - 이벤트 위임(delegate) 패턴에서 매우 유용. (부모에서 이벤트 처리 후 자식 판별)
```javascript
<ul id="fruits">
  <li class="apple">Apple</li>
  <li class="banana">Banana</li>
</ul>
<script>
  const apple = document.querySelector('.apple');
  
  console.log(apple.matches('#fruits > li.apple'));   // true
  console.log(apple.matches('#fruits > li.banana'));  // false
</script>
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
   - 실시간 반영(live) → DOM 변화가 있으면 즉시 반영됨.
   - 유사 배열 객체(배열 메서드 사용 불가).
- NodeList
   - querySelectorAll 등이 반환.
   - 대부분 non-live 객체 → DOM 변경 반영 X.
   - 일부 경우(childNodes)는 live.

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
- 따라서 childNodes 탐색 시 예상치 못한 텍스트 노드가 포함될 수 있음.
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
<ul id="fruits">
  <li class="red">Apple</li>
  <li class="red">Banana</li>
  <li class="red">Orange</li>
</ul>
<script>
  const elems = document.getElementsByClassName('red');
  console.log(elems.length);  // 3

  // 하나를 blue로 변경
  elems[0].className = 'blue';
  console.log(elems.length);  // 2 (live라 바로 반영됨!)
</script>

```

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
### 39.3.4 형제 노드 탐색
- Node.prototype.previousSibling/nextSibling: 이전/다음 형제 노드
- Element.prototype.previousElementSibling/nextElementSibling: 이전/다음 형제 요소 노드

## 39.4 노드 정보 취득
- Node.prototype.nodeType: 노드 타입 (요소: 1, 텍스트: 3, 문서: 9)
- Node.prototype.nodeName: 노드 이름

## 39.5 요소 노드의 텍스트 접근
firstChild.nodeValue 와 textContent는 비슷하지만,
### 39.5.1 nodeValue
- 텍스트 노드의 텍스트 값 접근/변경
- 요소 노드에서는 null 반환

### 39.5.2 textContent
- 요소 노드의 모든 텍스트 내용 접근/변경
- HTML 마크업 무시하고 텍스트만 처리

```javascript
const foo = document.getElementById('foo');
console.log(foo.textContent);          // "Hello"
console.log(foo.firstChild.nodeValue); // "Hello"
```
- 노트 탐색 프로퍼티
  - parentNode, childNodes, firstChild, lastChild
  - previousSibling, nextSibling (텍스트 노드 포함)
  - firstElementChild, lastElementChild, previousElementSibling, nextElementSibling (요소 노드만 탐색)
- 노드 정보 확인
  - nodeType: 노드 종류 (1=ELEMENT, 3=TEXT, 9=DOCUMENT 등)
  - nodeName: 노드 이름 (요소 태그명, #text, #document 등) 
```javascript
console.log(document.nodeType);  // 9 (DOCUMENT_NODE)
console.log(document.nodeName);  // "#document"
```

## 39.6 DOM 조작
- innerHTML: HTML 마크업을 포함한 텍스트 설정/취득
- CSS에 의해 비표시되는 요소의 텍스트도 반환

## DOM 탐색 API
(1) 자식, 부모, 형제 탐색
- parentNode, childNodes, firstChild, lastChild
- 요소 노드만: children, firstElementChild, lastElementChild
- 형제 탐색: previousSibling, nextSibling
- 요소 형제만: previousElementSibling, nextElementSibling

## HTMLCollection과 NodeList
- HTMLCollection: 실시간(live) 객체, DOM 변경사항 즉시 반영, getElementsByTagName, getElementsByClassName 반환
- NodeList: 대부분 정적(non-live) 객체이지만, childNodes는 live, forEach 사용가능
- 배열 메서드 사용 시 Array.from()으로 변환 필요

## 공백 텍스트 노드
- HTML 요소 사이의 공백, 줄바꿈, 탭 같은 whitespace도 텍스트 노드로 생성됨.
- childNodes 탐색 시 예상치 못한 #text 노드가 껴있을 수 있다.
- 따라서 요소 노드만 탐색하려면 children, firstElementChild 등을 쓰는 것이 안전하다.
```javascript
<ul id="fruits">
  <li class="apple">Apple</li>
  <li class="banana">Banana</li>
</ul>
<script>
  const fruits = document.getElementById('fruits');
  console.log(fruits.childNodes); // NodeList(5) → li, text, li, text, ...
  console.log(fruits.children);   // HTMLCollection(2) → li.apple, li.banana
</script>
```
## 텍스트 접근
🔹 nodeValue
 - 텍스트 노드에 직접 접근해야 사용 가능.
 - 번거로움.

🔹 textContent
- 요소 내부의 모든 텍스트를 한 번에 가져옴.
- 자식 노드가 HTML 태그라도 그대로 문자열로 반환됨.
- 보통 innerText보다 textContent를 쓰는 게 효율적.
```javascript
<div id="foo">Hello <span>World</span></div>
<script>
  const foo = document.getElementById('foo');
  console.log(foo.firstChild.nodeValue); // "Hello "
  console.log(foo.textContent);          // "Hello World"
</script>
```

## 노드 탐색 프로퍼티

노드 간의 관계를 탐색할 때 쓰는 프로퍼티.

- 부모: parentNode, parentElement
- 자식: childNodes(모든 노드), children(요소만), firstChild, lastChild
- 형제: previousSibling, nextSibling (모든 노드)
→ previousElementSibling, nextElementSibling (요소만)
```javascript
const first = document.querySelector('.apple');
console.log(first.nextElementSibling); // li.banana
console.log(first.previousElementSibling); // null
```
## 노드 정보 확인

- nodeType
  - 1 = ELEMENT_NODE
  - 3 = TEXT_NODE
  - 9 = DOCUMENT_NODE

- nodeName
  - 요소 노드면 태그명 (예: "DIV", "LI")
  - 텍스트 노드면 #text
  - 문서 노드면 #document
  ```javascript
  console.log(document.nodeType);  // 9
  console.log(document.nodeName);  // "#document"
```