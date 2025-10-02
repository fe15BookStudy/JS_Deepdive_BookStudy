# DOM(Document Object Model)

- DOM은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조이다.

## 노드

### HTML 요소와 노드 객체

```html
<div class="greeting">Hello</div>
```

- HTML 요소는 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 요소 노드 객체로 변환된다.
- 이 때 HTML 요소의 어트리뷰트는 어트리뷰트 노드로 변환된다.
- HTML 요소의 텍스트 콘텐츠는 텍스트 노드로 변환된다.
- HTML 문서는 HTML 요소들의 집합으로 이뤄지며, HTML 요소는 중첩 관계를 갖는다.
  즉, HTML 요소의 콘텐츠 영역(시작 태그와 종료 태그 사이)에는 텍스트뿐만 아니라 다른 HTML 요소도 포함될 수 있다.
- 이 때 HTML 요소 간에는 중첩 관계에 의해 계층적인 부자 관계가 형성된다.
- 이러한 HTML 요소 간의 부자 관계를 반영하여 HTML 문서의 구성 요소인 HTML 요소를 객체화한 모든 노드 객체들을 트리 자료구조로 구성한다.

#### 트리 자료구조

<img width="650" height="308" alt="Image" src="https://github.com/user-attachments/assets/bdb6ce19-051f-4918-a4ff-8a9452b0bc0d" />
- 트리 자료구조는 노드들의 계층 구조로 이뤄진다.
- 즉, 트리 자료구조는 부모 노드와 자식 노드로 구성되어 노드 간의 계층적 구조(부자, 형제 관계)를 표현하는 비선형 자료구조를 말한다.
- 트리 자료구조는 하나의 최상위 노드에서 시작한다.
- 최상위 노드는 부모 노드가 없으며, 루트 노드라 한다.
- 루트 노드는 0개 이상의 자식 노드를 갖는다.
- 자식 노드가 없는 노드를 리프 노드라 한다.
- 노드 객체들로 구성된 트리 자료구조를 **DOM(Document Object Model)** 이라 한다.

### 노드 객체 타입

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <link rel="stylesheet" href="style.css" />
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

<img width="669" height="349" alt="Image" src="https://github.com/user-attachments/assets/e38229a7-e801-4fc1-9657-ee80298afb2d" />
- 렌더링 엔진은 위 HTML 문서를 파싱하여 다음과 같이 DOM을 생성한다.
- 이처럼 DOM은 노드 객체의 계층적인 구조로 구성된다.
- 노드 객체에는 종류가 있고 상속 구조를 갖는다.
- 노드 객체는 총 12개의 종류(노드 타입)가 있다. 그 중에서 중요한 노드 타입은 4개이다.
  - **문서 노드(document node)**
    - DOM 트리의 최상위에 존재하는 루트 노드로서 document 객체를 가리킨다.
    - document 객체는 브라우저가 렌더링한 HTML 문서 전체를 가리키는 객체로서 전역 객체 window의 document 프로퍼티에 바인딩되어 있다.
    - 브라우저 환경의 모든 자바스크립트 코드는 script 태그에 의해 분리되어 있어도 하나의 전역 객체 window를 공유한다. 따라서 모든 자바스크립트 코드는 전역 객체 window의 document 프로퍼티에 바인딩되어 있는 하나의 document 객체를 바라본다. 즉, HTML 문서당 document 객체는 유일하다.
    - 문서 노드, 즉 document 객체는 DOM 트리의 루트 노드이므로 DOM 트리의 노드들에 접근하기 위한 진입점 역할을 담당한다. 즉, 요소, 어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다.
  - **요소 노드(element node)**
    - HTML 요소를 가리키는 객체다.
    - 요소 노드는 HTML 요소 간의 중첩에 의해 부자 관계를 가지며, 이 부자 관계를 통해 정보를 구조화한다.
    - 따라서 요소 노드는 문서의 구조를 표현한다고 할 수 있다.
  - **어트리뷰트 노드(attribute node)**
    - HTML 요소의 어트리뷰트를 가리키는 객체다.
    - 어트리뷰트가 지정된 HTML 요소의 요소 노드와 연결되어 있다.
    - 단, 요소 노드는 부모 노드와 연결되어 있지만 어트리뷰트 노드는 부모 노드와 연결되어 있지 않고 요소 노드에만 연결되어 있다.
    - 어트리뷰트 노드는 부모 노드가 없으므로 요소 노드의 형제 노드는 아니다. 어트리뷰트 노드에 접근하여 어트리뷰트를 참조하거나 변경하려면 먼저 요소 노드에 접근해야 한다.
  - **텍스트 노드(text node)**
    - HTML 요소의 텍스트를 가리키는 객체다.
    - 요소 노드가 문서의 구조를 표현한다면 텍스트 노드는 문서의 정보를 표현한다.
    - 텍스트 노드는 요소 노드의 자식 노드이며, 자식 노드를 가질 수 없는 리프 노드다.
    - 텍스트 노드는 DOM 트리의 최종단이다.
    - 텍스트 노드에 접근하려면 먼저 부모 노드인 요소 노드에 접근해야 한다.

### 노드 객체의 상속 구조

- DOM은 HTML 문서의 계층적 구조와 정보를 표현하며, 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조이다. 즉 DOM을 구성하는 노드 객체는 자신의 구조와 정보를 제어할 수 있는 DOM API를 사용할 수 있다. 이를 통해 노드 객체는 자신의 부모, 형제, 자식을 탐색할 수 있으며, 자신의 어트리뷰트와 텍스트를 조작할 수도 있다.
- 노드 객체에는 노드 객체의 종류, 즉 노드 타입에 상관없이 모든 노드 객체가 공통으로 갖는 기능도 있고, 노드 타입에 따라 고유한 기능도 있다. 예를 들어, 모든 노드 객체는 공통적으로 이벤트를 발생시킬 수 있다.
  또한 모든 노드 객체는 트리 자료구조의 노드로서 공통적으로 트리 탐색 기능이나 노드 정보 제공 기능이 필요하다. 이와 관련된 기능은 노드 인터페이스가 제 공한다.
- HTML 요소가 객체화된 요소 노드 객체는 HTML 요소가 갖는 공통적인 기능이 있다. 예를 들어, input 요소 노드 객체와 div 요소 노드 객체는 모두 HTML 요소의 스타일을 나타내는 style 프로퍼티가 있다. 이처럼 HTML 요 소가 갖는 고통적인 기능은 HTMLElement 인터페이스가 제공한다.
- 요소 노드 객체는 HTML 요소의 종류에 따라 고유한 기능도 있다. 예를 들어, input 요소 노드 객체는 value 프로퍼티가 필요하지만 div 요소 노드 객체는 value 프로퍼티가 필요하지 않다. 따라서 필요한 기능을 제공하는 인터페이스가 HTML 요소의 종류에 따라 각각 다르다.
- DOM은 HTML 문서의 계층적 구조와 정보를 표현하는 것은 물론 노드 객체의 종류, 즉 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드의 집합인 DOM API로 제공한다. 이 DOM API를 통해 HTML의 구조나 내용 또는 스타일 등을 동적으로 조작할 수 있다.

## 요소 노드 취득

- HTML의 구조나 내용 또는 스타일 등을 동적으로 조작하려면 먼저 요소 노드를 취득해야 한다.
- 요소 노드의 취득은 HTML 요소를 조작하는 시작점이다. 이를 위해 DOM은 요소 노드를 취득할 수 있는 다양한 메서드를 제공한다.

### id를 이용한 요소 노드 취득

- document.getElementById 메서드는 인수로 전달한 id 어트리뷰트 값을 갖는 하나의 요소 노드를 탐색하여 반환한다.

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li>
    </ul>
  </body>
  <script>
    const elem = document.getElementById("banana");

    elem.style.color = "red";
  </script>
</html>
```

- id 값은 HTML 문서 내에서 유일한 값이어야 하며, class 어트리뷰트와는 달리 공백 문자로 구분하여 여러 개의 값을 가질 수 없다.
- 단 HTML 문서 내에 중복된 id 값을 갖는 HTML 요소가 여러 개 존재하더라도 어떠한 에러도 발생하지 않는다.
- 즉, HTML 문서 내에는 중복된 id 값을 갖는 요소가 여러 개 존재할 가능성이 있다.

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li id="banana">Apple</li>
      <li id="banana">Banana</li>
      <li id="banana">Orange</li>
    </ul>
  </body>
  <script>
    const elem = document.getElementById("banana");

    elem.style.color = "red";
  </script>
</html>
```

- 이러한 경우 getElementById 메서드는 인수로 전달된 id 값을 갖는 첫 번째 요소 노드만 반환한다.
- getElementById 메서드는 언제나 단 하나의 요소 노드를 반환한다.

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li id="banana">Apple</li>
      <li id="banana">Banana</li>
      <li id="banana">Orange</li>
    </ul>
  </body>
  <script>
    const elem = document.getElementById("grape"); // null

    elem.style.color = "red"; // typeError
  </script>
</html>
```

- 인수로 전달된 id 값을 갖는 HTML 요소가 존재하지 않는 경우 getElementById 메서드는 null을 반환한다.

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <div id="foo"></div>
  </body>
  <script>
    // id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당된다.
    console.log(foo === document.getElementById("foo")); // true

    delete foo;
    console.log(foo); // <div id="foo"></div>

    // ====================================================================
    let foo = 1;

    console.log(foo); // 1
  </script>
</html>
```

- HTML 요소에 id 어트리뷰트를 부여하면 id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당되는 부수 효과가 있다.
- 단 id 값과 동일한 이름의 전역 변수가 이미 선언되어 있으면 이 전역 변수에 노드 객체가 재할당되지 않는다.

### 태그 이름을 이용한 요소 노드 취득

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li id="banana">Apple</li>
      <li id="banana">Banana</li>
      <li id="banana">Orange</li>
    </ul>
  </body>
  <script>
    // 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
    // 탐색된 요소 노드들은 HTMLCollection 객체에 담겨 반환한다.
    // HTMLCollection 객체는 유사 배열 객체이면서 이터러블이다.
    const elems = document.getElementsByTagName("li");

    // 취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
    // HTMLCollection 객체를 배열로 변환하여 순회하며 color 프로퍼티 값을 변경한다.
    [...elems].forEach((elem) => {
      elem.style.color = "red";
    });
  </script>
</html>
```

- document.getElementsByTagName 메서드는 인수로 전달한 태그 이름을 가지는 모든 요소 노드들을 탐색하여 반환한다.
- 여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체를 반환한다.
- 해당 메서드가 반환하는 객체는 유사 배열 객체이면서 이터러블이다.

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li id="banana">Apple</li>
      <li id="banana">Banana</li>
      <li id="banana">Orange</li>
    </ul>
    <ul>
      <li>HTML</li>
    </ul>
  </body>
  <script>
    // DOM 전체에서 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
    const lisFromDocument = document.getElementsByTagName("li");
    console.log(lisFromDocument);

    // ul태그의 id가 fruits인 요소의 자손 노드 중에서 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
    const fruits = document.getElementById("fruits");
    const lisFromFruits = fruits.getElementsByTagName("li");
    console.log(lisFromFruits);
  </script>
</html>
```

- 해당 메서드는 특정 요소 노드를 통해 호출하며, 특정 요소 노드의 자손 노드 중에서 요소 노드를 탐색하여 반환할 수도 있다.

### class를 이용한 요소 노드 취득

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li class="fruit apple">Apple</li>
      <li class="fruit banana">Banana</li>
      <li class="fruit orange">Orange</li>
    </ul>
  </body>
  <script>
    // class 값이 'fruit'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
    const elems = document.getElementsByClassName("fruit");

    // 취득한 모든 요소의 CSS color 프로퍼티 값을 변경한다.
    [...elems].forEach((elem) => {
      elem.style.color = "red";
    });

    // class 값이 'fruit apple'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
    const apples = document.getElementsByClassName("fruit apple");

    // 취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
    [...apples].forEach((elem) => {
      elem.style.color = "blue";
    });
  </script>
</html>
```

- document.getElementsByClassName 메서드는 인수로 전달한 class 어트리뷰트 값을 갖는 모든 요소 노드들을 탐색하여 반환한다.
- 인수로 전달할 class 값은 공백으로 구분하여 여러 개의 class를 지정할 수 있다.
- 만약 인수로 전달된 class 값을 갖는 요소가 존재하지 않는 경우 빈 객체를 반환한다.

### CSS 선택자를 이용한 요소 노드 취득

```css
/* */

/* 전체 선택자: 모든 요소를 선택 */
* {
  ...;
}

/* 태그 선택자: 모든 p 태그 요소를 모두 선택 */
p {
  ...;
}

/* id 선택자: id 값이 'foo'인 요소를 모두 선택 */
#foo {
  ...;
}

/* class 선택자: class 값이 'foo'인 요소를 모두 선택 */
.foo {
  ...;
}

/* 어트리뷰트 선택자: input 요소 중에 type 어트리뷰트 값이 'text'인 요소를 모두 선택 */
input[type="text"] {
  ...;
}

/* 후손 선택자: div 요소의 후손 요소 중 p 요소를 모두 선택 */
div p {
  ...;
}

/* 자식 선택자: div 요소의 자식 요소 중 p 요소를 모두 선택 */
div > p {
  ...;
}

/* 인접 형제 선택자: p 요소의 형제 요소 중에 p 요소 바로 뒤에 위치하는 ul 요소를 선택 */
p + ul {
  ...;
}

/* 일반 형제 선택자: p 요소의 형제 요소 중에 p 요소 뒤에 위치하는 ul 요소를 모두 선택 */
p ~ ul {
  ...;
}

/* 가상 클래스 선택자: hover 상태인 a 요소를 모두 선택 */
a:hover {
  ...;
}
```

- CSS 선택자는 스타일을 적용하고자 하는 HTML 요소를 특정할 때 사용하는 문법이다.

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li class="fruit apple">Apple</li>
      <li class="fruit banana">Banana</li>
      <li class="fruit orange">Orange</li>
    </ul>
  </body>
  <script>
    // class 어트리뷰트 값이 'banana'인 첫 번째 요소 노드를 탐색하여 반환한다.
    const elem = document.querySelector(".banana");

    // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
    elem.style.color = "red";
  </script>
</html>
```

- querySelector 메서드는 인수로 전달한 CSS 선택자를 만족 시키는 하나의 요소 노드를 탐색하여 반환한다.

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li class="fruit apple">Apple</li>
      <li class="fruit banana">Banana</li>
      <li class="fruit orange">Orange</li>
    </ul>
  </body>
  <script>
    // ul 요소의 자식 요소인 li 요소를 모두 탐색하여 반환한다.
    const elems = document.querySelectorAll("ul > li");

    // 취득한 요소 노드들은 NodeList 객체에 담겨 반환된다.
    console.log(elems);

    // 취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
    elems.forEach((elem) => {
      elem.style.color = "red";
    });
  </script>
</html>
```

- querySelectorAll 메서드는 인수로 전달한 CSS 선택자를 만족시키는 모든 요소 노드를 탐색하여 반환한다.
- 여러 개의 요소 노드 객체를 갖는 NodeList 객체를 반환한다.

### 특정 요소 노드를 취득할 수 있는지 확인

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li class="fruit apple">Apple</li>
      <li class="fruit banana">Banana</li>
      <li class="fruit orange">Orange</li>
    </ul>
  </body>
  <script>
    const apple = document.querySelector(".apple");

    // apple 노드는 fruit id를 갖는 li 태그의 apple class로 취득할 수 있다.
    console.log(apple.matches("#fruits > li.apple")); // true

    // apple 노드는 fruit id를 갖는 li 태그의 banana class로 취득할 수 있다.
    console.log(apple.matches("#fruits > li.banana")); // false
  </script>
</html>
```

- Element.matches 메서드는 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인한다.

### HTMLCollection과 NodeList

#### HTMLCollection

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li class="red">Apple</li>
      <li class="red">Banana</li>
      <li class="red">Orange</li>
    </ul>
  </body>
  <script>
    // class 값이 'red'인 요소 노드를 모두 탐색하여 객체에 담아 반환한다.
    const elems = document.getElementsByClassName("red");

    console.log(elems); // [li.red, li.red, li.red]

    // 객체의 모든 요소의 class 값을 'blue'로 변경한다.
    for (let i = 0; i < elems.length; i++) {
      elems[i].className = "blue";
    }

    // 하지만 모든 red class가 blue로 변경되지 않는다.
    // 이는 for문을 돌면서 elems에서 실시간으로 객체의 프로퍼티가 제거되기 때문이다.
    console.log(elems); // [li.red]

    // 해당 부작용을 해결하기 위해선 배열의 고차함수를 사용하면 된다.
    [...$elems].forEach((elem) => (elem.className = "blue"));
  </script>
</html>
```

- HTML 노드 객체의 상태 변화를 실시간으로 반영하는 살아 있는 DOM 컬렉션 객체다.
- getElementsByTagName, getElementsByClassName 메서드가 있다.

#### NodeList

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li>Apple</li>
      <li>Banana</li>
      <li>Orange</li>
    </ul>
  </body>
  <script>
    const fruits = document.getElementById("fruits");

    // childNodes 프로퍼티는 NodeList의 객체를 반환한다.
    const { childNodes } = fruits;
    console.log(childNodes); // [text, li, text, li, text]

    for (let i = 0; i < childNodes.length; i++) {
      fruits.removeChild(childNodes[i]);
    }

    // 예상과 다르게 fruits 요소의 모든 자식 노드가 삭제되지 않는다.
    // removeChild 메서드가 호출될 때마다 NodeList 객체인 childNodes가 실시간으로 변경된다.
    // 따라서 첫 번째, 세 번째, 다섯 번째 요소만 삭제된다.
    console.log(childNodes);

    // ===========================================================

    // 스프레드 문법을 사용하여 NodeList 객체를 배열로 반환한다.
    [...childNodes].forEach((childNodes) => {
      fruits.removeChild(childNodes);
    });

    // fruits 요소의 모든 자식 노드가 모두 삭제되었다.
    console.log(childNodes);
  </script>
</html>
```

- HTMLCollection 객체의 부작용을 해결하기 위한 객체다.
- 대부분의 경우 실시간으로 노드 객체의 상태 변경을 반영하지 않고 과거의 정적 상태를 유지한다.
- querySelector, querySelectorAll 메서드가 있다.
- 하지만 childNode 프로퍼티가 반환하는 NodeList 객체는 실시간으로 노드 객체의 상태를 반영하므로 주의가 필요하다.

### 노드 탐색

```html
<ul id="fruits">
  <li class="apple">Apple</li>
  <li class="banana">Banana</li>
  <li class="orange">Orange</li>
</ul>
```

- 요소 노드를 취득한 다음, 취득한 요소 노드를 기점으로 DOM 트리의 노드를 옮겨 다니며 부모, 형제, 자식 노드 등을 탐색해야할 때가 있다.

- ul#fruits 요소는 3개의 자식 요소를 갖는다. 이 때 먼저 ul#fruits 요소 노드를 취득한 다음, 자식 노드를 모두 탐색하거나 자식 노드 중에 하나만 탐색할 수 있다.
- li.banana 요소는 2개의 형제 요소와 부모 요소를 갖는다. 이 때 먼저 li.banana 요소 노드를 취득한 다음, 형제 노드를 탐색하거나 부모 노드를 탐색할 수 있다.
- 이처럼 DOM 트리 상의 노드를 탐색할 수 있도록 트리 탐색 프로퍼티를 제공한다.

### 공백 텍스트 노드

- HTML 요소 사이의 스페이스, 탭, 줄바꿈(개행) 등의 공백 문자는 텍스트 노드를 생성한다.
- HTML 문서에 스페이스 키, 탭 키, 엔터 키 등을 입력하면 공백 문자가 추가된다.
- 노드를 탐색할 때는 공백 문자가 생성한 공백 텍스트 노드에 주의해야 한다.

### 자식 노드 탐색

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li class="apple">Apple</li>
      <li class="banana">Banana</li>
      <li class="orange">Orange</li>
    </ul>
  </body>
  <script>
    // 노드 탐색의 기점이 되는 fruits 요소 노드를 취득한다.
    const fruits = document.getElementById("fruits");

    // fruits 요소의 모든 자식 노드를 탐색한다.
    // childNode 프로퍼티가 반환한 NodeList에는 요소 노드뿐만 아니라 텍스트 노드도 포함되어 있다.
    console.log(fruits.childNodes); // [text, li.apple, text, li.banana, text, li.orange, text]

    // fruits 요소의 모든 자식 노드를 탐색한다.
    console.log(fruits.children); // [li.apple, li.banana, li.orange]

    // fruits 요소의 첫 번째 자식 노드를 탐색한다.
    console.log(fruits.firstChild); // text

    // fruits 요소의 마지막 자식 노드를 반환한다.
    console.log(fruits.lastChild); // text

    // fruits 요소의 첫 번째 자식 노드를 탐색한다.
    console.log(fruits.firstElementChild); // li.apple

    // fruits 요소의 마지막 자식 노드를 탐색한다.
    console.log(fruits.lastElementChild); // li.orange
  </script>
</html>
```

- 자식 노드를 탐색하기 위해서는 다음과 같은 노드 탐색 프로퍼티를 사용한다.
  - Node.childNodes - 자식 노드를 모두 탐색하여 반환한다.
  - Element.children - 자식 노드 중에서 요소 노드만 모두 탐색하여 반환한다.
  - Node.firstChild - 첫 번째 자식 노드를 반환한다. 프로퍼티가 반환한 노드는 텍스트 노드이거나 요소 노드이다.
  - Node.lastChild - 마지막 자식 노드를 반환한다. 프로퍼티가 반환한 노드는 텍스트 노드이거나 요소 노드이다.
  - Element.firstElementChild - 첫 번째 자식 요소 노드를 반환한다.
  - Element.lastElementChild - 마지막 자식 요소 노드를 반환한다.

### 자식 노드 존재 확인

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li class="apple">Apple</li>
      <li class="banana">Banana</li>
      <li class="orange">Orange</li>
    </ul>
  </body>
  <script>
    // 노드 탐색 기점이 되는 fruits 요소 노드를 취득한다.
    const fruits = document.getElementById("fruits");

    // hasChildNodes 메서드는 텍스트 노드를 포함하여 자식 노드의 존재를 확인한다.
    console.log(fruits.hasChildNodes()); // true
  </script>
</html>
```

- Node.hasChildNodes 메서드는 자식 노드가 존재하면 true, 존재하지 않으면 false를 반환한다.

### 부모 노드 탐색

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li class="apple">Apple</li>
      <li class="banana">Banana</li>
      <li class="orange">Orange</li>
    </ul>
  </body>
  <script>
    // 노드 탐색의 기점이 되는 .banana 요소 노드를 취득한다.
    const banana = document.querySelector(".banana");

    // .banana 요소 노드의 부모 노드를 탐색한다.
    console.log(banana.parentNode); // ul#fruits
  </script>
</html>
```

- Node.parentNode 메서드는 트리의 부모 노드를 탐색한다.

### 형제 노드 탐색

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <ul id="fruits">
      <li class="apple">Apple</li>
      <li class="banana">Banana</li>
      <li class="orange">Orange</li>
    </ul>
  </body>
  <script>
    // 노드 탐색의 기점이 되는 fruits 요소 노드를 취득한다.
    const fruits = document.getElementById("fruits");

    // fruits 요소의 첫 번째 자식 노드를 탐색한다.
    const { firstChild } = fruits;
    console.log(firstChild); // text

    // fruits 요소의 첫 번째 자식 노드의 다음 형제 노드를 탐색한다.
    const { nextSibling } = firstChild;
    console.log(nextSibling); // li.apple

    // li.apple 요소의 이전 형제 노드를 탐색한다.
    const { previousSibling } = nextSibling;
    console.log(previousSibling); // text

    // fruits 요소의 첫 번째 자식 요소 노드를 반환한다.
    const { firstElementChild } = fruits;
    console.log(firstElementChild); // li.apple

    // fruits 요소의 첫 번째 자식 요소 노드(li.apple)의 다음 형제 노드를 탐색한다.
    const { nextElementSibling } = firstElementChild;
    console.log(nextElementSibling);

    // li.banana 요소의 이전 형제 요소 노드를 탐색한다.
    const { previousElementSibling } = nextElementSibling;
    console.log(previousElementSibling);
  </script>
</html>
```

- 부모 노드가 같은 형제 노드를 탐색하려면 다음과 같은 노드 탐색 프로퍼티를 사용한다.
- 단 어트리뷰트 노드는 요소 노드와 연결되어 있지만 부모 노드가 같은 형제 노드가 아니기 때문에 반환되지 않느낟.
  - Node.previousSibling - 부모 노드가 같은 형제 노드 중에서 자신의 이전 형제 노드를 탐색하여 반환한다.
  - Node.nextSibling - 부모 노드가 같은 형제 노드 중에서 자신의 다음 형제 노드를 탐색하여 반환한다.
  - Element.previousElementSibling - 부모 노드가 같은 형제 요소 노드 중에서 자신의 이전 형제 요소 노드를 탐색하여 반환한다.
  - Element.nextElementSibling - 부모 노드가 같은 형제 요소 노드 중에서 자신의 다음 형제 요소 노드를 탐색하여 반환한다.

## 노드 정보 취득

```html
<!DOCTYPE html>
<html lang="ko">
  <body>
    <div id="foo">Hello</div>
  </body>
  <script>
    // 문서 노드의 노드 정보를 취득한다.
    console.log(document.nodeType); // 9
    console.log(document.nodeName); // document

    // 요소 노드의 노드 정보를 취득한다.
    const foo = document.getElementById("foo");
    console.log(foo.nodeType); // 1
    console.log(foo.nodeName); // div

    // 텍스트 노드의 노드 정보를 취득한다.
    const textNode = foo.firstChild;
    console.log(textNode.nodeType); // 3
    console.log(textNode.nodeName); // text
  </script>
</html>
```

- 노드 객체에 대한 정보를 취득하려면 다음과 같은 노드 정보 프로퍼티를 사용한다.
  - Node.nodeType - 노드 객체의 종류, 노드 타입을 나타내는 상수를 반환한다.
    Node.ELEMENT_NODE : 요소 노드 타입을 나타내는 상수 1을 반환
    Node.TEXT_NODE : 텍스트 노드 타입을 나타내는 상수 3을 반환
    Node.DOCUMENT.NODE : 문서 노드 타입을 나타내는 상수 9를 반환
  - Node.nodeName - 노드의 이름을 문자열로 반환한다.
    요소 노드 : 대문자 문자열로 태그 이름을 반환
    텍스트 노드 : 문자열 text를 반환
    문서 노드 : 문자열 document를 반환
