# 39. DOM

### 노드

#### HTML 요소와 노드 객체

**DOM은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API(Application Programming Interface), 즉 프로퍼티와 메서드를 제공하는 트리 자료구조다. **  

HTML 요소는 HTML 문서를 구성하는 개별적인 요소를 의미한다.

노드(Node)는 HTML 문서의 모든 구성 요소를 의미한다. 웹 페이지에 있는 모든 요소, 속성, 텍스트 등이 각각 하나의 노드이다.


HTML 요소는 렌더링 엔진에 의해 파싱( 텍스트, 문서, 코드 등 데이터를 분해하고 분석하여 구조화된 정보로 변환하는 과정 ) 되어 DOM을 구성하는 요소 노드 객체로 변환된다. 

HTML 요소의 어트리뷰트는 어트리뷰트 노드로, HTML 요소의 텍스트 콘텐츠는 텍스트 노드로 변환된다.

HTML 문서는 HTML 요소들의 집합으로 이뤄지며, HTML 요소는 중첩 관계를 갖는다. 즉, HTML 요소의 콘텐츠 영역에는 텍스트뿐만 아니라 다른 HTML 요소도 포함 할 수 있다.

이때 HTML 요소 간에는 중첩 관계에 의해 계층적인 부자(parent-child) 관계가 형성된다. 이러한 HTML 요소 간의 부자 관계를 반영하여 HTML 문서의 구성 요소인 HTML 요소를 객체화한 모든 노드 객체들을 트리 자료 구조로 구성한다.

#### 트리 자료구조

트리 자료구조는 노드들의 계층 구조로 이뤄진다.

즉, 트리 자료구조는 부모 노드와 자식노드로 구성되어 노드 간의 계층적 구조를 표현하는 비선형 자료구조를 말한다.

트리 자료구조는 하나의 최상위 노드에서 시작한다. 최상위 노드는 부모 노드가 없으며, **루트 노드**라고 한다. 루트 노드는 0개 이상의 자식 노드를 갖는다. 자식 노드가 없는 노드를 **리프 노드** 라 한다.

노드 객체들로 구성된 트리 자료구조를 DOM(Document Object Model)이라 한다.

노드 객체의 트리로 구조화되어 있기 때문에 DOM을 DOM트리라고 부르기도 한다.

#### 노드 객체의 타입

```HTML
<!DOCTYPE html>
<html>
  <head>
      <meat charset = "UTF-8">
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

위 HTML 문서를 렌더링 엔진이 파싱한다고 생각해보면, 렌더링 엔진은 위 HTML 문서를 파싱하여 다음과 같이 DOM을 생성한다.

![DOM tree]](C:\Users\user\bootcamp\JS_Deepdive_BookStudy\7. 서주희\39_DOM\DOM.png)

이처럼 DOM은 노드 객체의 계층적인 구조로 구성된다. 노드 객체는 종류가 있고 사옥 구조를 갖는다. 노드 객체는 총 12개의 종류(노드 타입)가 있다.

중요한 노드 타입이 몇가지 있다.

1. 문서 노드 (document node)

문서 노드는 DOM 트리의 최상위에 존재하는 루트 노드로서 document 객체를 가리킨다. document 객체는 브라우저가 렌더링한 HTML 문서 전체를 가리키는 객체로서 전역 객체 window의 document 프로퍼티에 바인딩되어 있다. 따라서 문서 노드는 window.document 또는 document 로 참조할 수 있다.


브라우저 환경의 모든 자바스크립트 코드는 script 태그에 의해 분리되어 있어도 하나의 전역 객체 window를 공유한다. 따라서 모든 자바스크립트 코드는 전역 객체 window의 document 프로퍼티에 바인딩되어 있는 하나의 document 객체를 바라본다. 즉, HTML 문서당 document 객체는 유일하다.

문서 노드 , 즉 document rorcpsms DOM 트리의 루트 노드이므로 DOM 트리의 노드들에 접근하기 위한 진입점 역할을 담당한다. 즉 , 요소 ,어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다.

2. 요소 노드 (element node)

요소 노드는 HTML 요소를 가리키는 객체다. 요소 노드는 HTML 요소 간의 중첩에 의해 부자 관계를 가지며, 이 부자 관계를 통해 정보를 구조화한다. 따라서 요소 노드는 문서의 구조를 표현한다고 할 수 있다.

3. 어트리뷰트 노드 (attribute node)

어트리뷰트 노드는 HTML 요소의 어트리뷰트를 가리키는 객체다. 어트리뷰트 노드는 어트리뷰트가 지정된 HTML 요소의 노드와 연결되어 있다. 단, 요소 노드는 부모 노드와 연결되어 있지만 어트리뷰트 노드는 부모 노드와 연결되어 있지 않고 요소 노드에만 연결되어 있다. 즉, 어트리뷰트 노드는 부모 노드가 없으므로 요소 노드의 형제 노드는 아니다. 따라서 어트리뷰트 노드에 접근하여 어트리뷰트를 참조하거나 변경하려면 먼저 요소 노드에 접근해야 한다.

4. 텍스트 노드 (test node)

텍스트 노드는 HTML 요소의 텍스트를 가리키는 객체다. 요소 노드가 문서의 구조를 표현한다면 텍스트 노드는 문서의 정보를 표현한다고 할 수 있다. 텍스트 노드는 요소 노드의 자식 노드이며, 자식 노드를 가질 수 없는 리프노드다. 즉, 텍스트 노드는 DOM 트리의 최종단이다. 따라서 텍스트 노드에 접근하려면 먼저 부모 노드인 요소 노드에 접근해야 한다.


#### 노드 객체의 상속 구조

DOM은 HTML 문서의 계층적 구조와 정보를 표현하며, 이를 제어할 수 있는 API , 즉 프로퍼티와 메서드를 제공하는 트리 자료구조이다. 

다시말해, DOM을 구성하는 노드 객체는 자신의 구조와 정보를 제어할 수 있는 DOM API를 사용할 수 있다.

DOM을 구성하는 노드 객체는 ECMAScript 사양에 정의된 표준 빌트인 객체가 아니라 브라우저 환경에서 추가적으로 제공하는 호스트 객체다. 하지만 노드 객체도 자바스크립트 객체이므로 프로토타입에 의한 상속 구조를 갖는다. 

모든 노드 객체는 Object, EventTarget, Node 인터페이스를 상속받는다. 추가적으로 문서 노드는 Document, HTMLDocument 인터페이스를 상속받고 어트리뷰트 노드는 Attr, 텍스트 노드는 CharacterData 인터페이스를 각각 상속받는다.

요소 노드는 Element 인터페이스를 상속받는다. 또 요소 노드는 HTMLElement와 태그의 종류별로 세분화된 HTMLHtmlElement,HTMLHeadElement,HTMLBodyElement, HTMLUListElement 등의 인터페이스를 상속받는다.

이를 프로토타입 체인 관점에서 보면, input 요소를 파싱하여 객체화한 input 요소 노드 객체는 HTMLInputElement, HTMLElement, ElEMENT, Node, EventTarget, Object의 prototype에 바인딩되어 있는 프로토타입 객체를 상속받는다. 즉, input 요소 노드 객체는 프로토타입 체인에 있는 모든 프로토타입의 프로퍼티나 메서드를 상속받아 사용할 수 있다.

----------------

## 자바스크립트와 DOM, 프로토타입, 상속

1. DOM과 자바스크립트의 관계

- 웹페이지는 HTML로 구성되어 있고 브라우저는 이를 DOM(Document Object Model) 구조로 변환한다.

- DOM은 자바스크립트가 HTML 요소를 인식하고 조작할 수 있도록 돕는다.

- DOM 요소들은 노드 객체(Node Object) 로 만들어지며 자바스크립트 객체처럼 동작한다.

2. 객체와 프로토타입 상속

- 자바스크립트의 객체는 다른 객체로부터 프로토타입을 통해 기능(메서드, 속성)을 상속받는다.

- DOM 노드 객체들도 이런 상속 구조를 따른다.

```JavaScript
// 예 : <input> 요소의 상속 구조

HTMLInputElement
↑
HTMLElement
↑
Element
↑
Node
↑
EventTarget
↑
Object
```

- 각 단계에서 상위 객체의 기능을 물려받는다.

- `input.value` 는 `HTMLInputElement`에 정의된 속성이므로 상위 객체인 Object에서는 사용할 수 없다


3. 그 외 

- 콘솔에서 console.dir(객체)를 사용하면 해당 객체가 상속받은 구조와 속성을 확인할 수 있다.

- 개발자 문서(MDN 등)를 통해 각 요소가 제공하는 속성과 메서드를 확인할 수 있다.

- 처음부터 외울 필요는 없으며 자주 사용하는 기능 위주로 자연스럽게 익히는 것이 좋다.

- HTML을 직접 수정하면 고정된 화면만 만들 수 있다.

- 자바스크립트를 사용하면 사용자의 행동(클릭, 입력 등)에 따라 실시간으로 HTML을 조작할 수 있다.

- 실제 웹사이트에서는 사용자 입력, 데이터 응답 등에 따라 화면이 동적으로 바뀌는 경우가 많아 자바스크립트가 필수적이다.

--------

배열이 객체인 동시에 배열인 것 처럼, input 요소 노드 객체도 다양한 특성을 갖는 객체이며 이러한 특성을 나타내는 기능들을 상속을 통해서 제공받는다.


| input 요소 노드 객체의 특성 | 프로토타입을 제공하는 객체 |
|---|---|
| 객체 | Object | 
| 이벤트를 발생시키는 객체 | Event Target |
| 트리 자료구조의 노드 객체 | Node |
| 브라우저가 렌더링할 수 있는 웹 문서의 요소(HTML, XML, SVG)를 표현하는 객체 | Element |
| 웹 문서의 요소 중에서 HTML 요소를 표현하는 객체 | HTMLElment |
| HTML 요소 중에서 input 요소를 표현하는 객체 | HTMLInputElment |


노드 객체의 상속 구조는 개발자 도구의 Elements 패널 우측의 Properties 패널에서 확인할 수 있다.

지금까지 살펴본 바와 같이 **DOM은 HTML 문서의 계층적 구조와 정보를 표현하는 것은 물론 노드 객체의 종류, 즉 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드 집합인 DOM API 로 제공한다. 이 DOM API를 통해 HTML 의 구조나 내용 또는 스타일 등을 동적으로 조작할 수 있다.**

### 요소 노드 취득

HTML의 구조나 내용, 스타일 등을 동적으로 조작하려면 요소 노드를 취득해야 한다.

요소 노드의 취득은 HTML 요소를 조작하는 시작점이다. 이를 위해서 DOM 은 요소 노드를 취득할 수 있는 다양한 메서드를 제공한다.


------

#### id를 이용한 요소 노드 취득

Document.prototype.getElementById 메서드는 인수로 전달한 id 어트리뷰트 값 ( 이하 id 값 )을 갖는 하나의 요소 노드를 탐색하여 반환한다. getElementById 메서드는 DocumentById메서드는 Document.prototype의 프로퍼티다. 따라서 반드시 문서 노드인 document를 통해 호출해야 한다.

```HTML
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="Orange">Orange</li>
    </ul>
  <script>
    // id 값이 'banana'인 요소 노드를 탐색하여 반환한다.
    // 두 번째 li 요소가 파싱되어 생성된 요소 노드가 반환된다.
    const $elem = document.getElementById('banana');

    // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
    $elem.style.color = 'red';
    </script>
  </body>
</html>
```

id 값은 HTML 문서 내에서 유일한 값이어야 하며 class 어트리뷰트와는 달리 공백 문자로 구분하여 여러 개의 값을 가질 수 없다. 단, HTML 문서 내에서 중복된 id 값을 갖는 HTML 요소가 여러 개 존재하더라도 어떠한 에러도 발생하지 않는다. 중복된 id 값을 갖는 요소가 여러 개 존재할 가능성이 있다는 말이다.


이러한 경우에 getElementById 메서드는 인수로 전달된 id 값을 갖는 첫 번째 요소 노드만 반환한다. 즉 이 메서드는 언제나 단 하나의 요소 노드를 반환한다.

```HTML
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li id="banana">Apple</li>
      <li id="banana">Banana</li>
      <li id="banana">Orange</li>
    </ul>
  <script>
    // getElementById 메서드는 언제나 단 하나의 요소 노드를 반환한다.
    // 첫 번째 li 요소가 파싱되어 생성된 요소 노드가 반환된다.
    const $elem = document.getElementById('banana');

    // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
    $elem.style.color = 'red';
    </script>
  </body>
</html>
```

만약 인수로 전달된 id 값을 갖는 HTML 요소가 존재하지 않는 경우 getElementById 메서드는 null을 반환한다.

```HTML
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="Orange">Orange</li>
    </ul>
  <script>
    // id 값이 'grape'인 요소 노드를 탐색하여 반환한다. null이 반환된다.
    const $elem = document.getElementById('grape');

    // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
    $elem.style.color = 'red';
    // -> TypeError: Cannot read property 'style' of null
    </script>
  </body>
</html>
```

HTLM 요소에 id 어트리뷰트를 부여하면 id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당노드 객체가 할당되는 부수 효과가 있다.

```HTML
<!DOCTYPE html>
<html>
  <body>
    <div id="foo"></div>
  <script>
    // id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당된다.
    console.log(foo === document.getElementById('foo')); //true

    // 암묵적 전역으로 생성된 전역 프로퍼티는 삭제되지만 전역 변수는 삭제되지 않는다
    delete foo;
    console.log(foo); // <div id="foo"></div>
   </script>
  </body>
</html>
```

단, id 값과 동일한 이름의 전역 변수가 이미 선언되어 있으면 이 전역 변수에 노드 객체가 재할당되지 않는다.

```HTML
<!DOCTYPE html>   
<html>
  <body>
    <div id="foo"></div>
  <script>
    let foo =1;
    // id 값과 동일한 이름의 전역 변수가 이미 선언되어 있으면 노드 객체가 재할당되지 않는다.
   
    console.log(foo); // 1
   </script>
  </body>
</html>
```

-----

#### 태그 이름을 이용한 요소 노드 취득

Document.prototype/Element.prototype.getElementsByTagName 메서드는 인수로 전달한 태그 이름을 갖는 모든 요소 노드들을 탐색하여 반환한다. 메서드 이름에 포함된 Elements 가 복수형인 것에서 알 수 있듯이 getElemetsByTagName 메서드는 여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체를 반환한다.

```HTML
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="orange">Orange</li>
    </ul>
  <script>
    // 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
    // 탐색된 요소 노드들은 HTMLCollection 객체에 담겨 반환된다.
    // HTMLCollection 객체는 유사 배열 객체이면서 이터러블이다.
    const $elem = document.getElementById('grape');

    // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
    $elem.style.color = 'red';
    // -> TypeError: Cannot read property 'style' of null
    </script>
  </body>
</html>
```

함수는 하나의 값만 반환할 수 있으므로 여러 개의 값을 반환하려면 배열이나 객체와 같은 자료구조에 담아 반환해야 한다.
getElementsByTagName 메서드가 반환하는 DOM 컬렉션 객체인 HTMLCollection 객체는 유사 배열 객체이면서 이터러블이다. 

HTML 문서의 모든 요소를 취득하려면 getElementsByTagName 메서드의 인수로 '*'를 전달한다.

```JavaScript
// 모든 요소 노드를 탐색하여 반환한다.

const $all = document.getElementsByTagName('*');
// -> HTMLCollection(8) [html, head, body, ul, li#apple, li#banana, li#orange, script, apple: li#apple, banana: li#banana, orange: li#orange ]
```

getElementsByTagName 메서드는 Document.prototype에 정의된 멧드와 Element.prototype에 정의된 메서드가 있다. Document.prototype.getElementsByTagName 메서드는 DOM의 루트 노드인 문서, 즉 document를 통해 호출하며 DOM 전체에서 요소 노드를 탐색하여 반환한다. 하지만 Element.prototype.getElementByTagName 메서드는 특정 요소 노드를 통해 호출하며, 특정 요소 노드의 자손 노드 중에서 요소 노드를 탐색하여 반환한다.

```HTML
<!DOCTYPE html>
<html>
  <body>
    <ul>
      <li>Apple</li>
      <li>Banana</li>
      <li>Orange</li>
    </ul>
    <ul>
      <li>HTML</li>
    </ul>
  <script>
    // DOM 전체에서 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
    const $listFromDocument = document.getElementsByATagName('li');
    console.log($listFromDocument); // HTMLCollection(4) [li,li,li,li]



    // ul#fruit 요소의 자손 노드 중에서 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
    const $fruits = document.getElementById('fruits');
    const $lisFromFruits = $fruits.getElementByTagName('li');
    console.log($listFromFruits); // HTMLCollection(3) [li, li, li]


    </script>
  </body>
</html>
```

만약 인수로 전달된 태그 이름을 갖는 요소가 존재하지 않는 경우 gettElementByTagName 메서드는 빈 HTMLCollection 객체를 반환한다.

-----

#### class를 이용한 요소 노드 취득

Document.prototype/Element.prototype.getElemetsByClassName 메서드는 인수로 전달한 class 어트리뷰트 값을 갖는 모든 요소 노드들을 탐색하여 반환한다. 인수로 전달할 class 값은 공백으로 구분하여 여러 개의 class를 지정할 수 있다. getElementsByTagName 메서드와 마찬가지로 getElementsByTagName 메서드는 여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체를 반환한다.

```HTML
<!DOCTYPE html>
<html>
<body>
  <ul>
    <li class="fruit apple">Apple</li>
    <li class="fruit banana">Banana</li>
    <li class="fruit orange">Orange</li>
  </ul>
  <script>
    // class 값이 'fruit'인 요소 노드를 모두 탐색하여 HTMLCollecion 객체에 담아 반환한다.
    const $elems = document.getElementsByClassName('fruit');

    // 취득한 모든 요소의 CSS color 프로퍼티 값을 변경한다.
    [...$elems].forEach(elem => { elem.style.color = 'red';});

    // class 값이 'fruit apple'인 요소 노드를 모두 탐색하여 HTMLCollecion 객체에 담아 반환한다.
    const $apples = document.getElementsByClassName('fruit apple');

    // 취득한 모든 요소의 CSS color 프로퍼티 값을 변경한다.
    [...$apples].forEach(elem => { elem.style.color = 'blue';});
  </script>
</body>
</html>
```

getElementsByTagName 메서드와 마찬가지로 getElementsByClassName 메서드는 Document.prototype에 정의된 메서드와 Element.prototype에 정의된 메서드가 있다. Document.prototype.getElementByClassName 메서드는 DOM의 루트 노드인 문서 노드, 즉 document를 통해 호출하며 DOM 전체에서 요소 노드를 탐색하여 반환하고 Element.prototype.getElementsByClassName 메서드는 특정 요소 노드를 통해 호출하며 특정 요소 노드의 자손 노드 중에서 요소 노드를 탐색하여 반환한다.

```HTML
<!DOCTYPE html>
<html>
<body>
  <ul>
    <li class="apple">Apple</li>
    <li class="banana">Banana</li>
    <li class="orange">Orange</li>
  </ul>
  <div class="banana">Banana</div>
  <script>

    // DOM 전체에서 class 값이 'banana'인 요소 노드를 모두 탐색하여 반환한다.
    const $bananasFromDocument = document.getElementsByClassName('banana');
    console.log($bananasFromDocument);
    // HTMLCollection(2) [li.banana, div.banana]

    // fruits 요소의 자손 노드 중에서 class 값이 'banana' 인 요소 노드를 모두 탐색하여 반환한다.
    const $fruits = document.getElementsById('fruits');
    const $bananaFromFruits = $fruits.getElementsByName('banana');

    console.log($bananaFromFruits); // HTMLCollection [li.banana]
  </script>
</body>
</html>
```

만약 인수로 전달된 class 값을 갖는 요소가 존재하지 않는 경우 getElementsByClassName 메서드는 빈 HTMLCollection 객체를 반환한다.

-----

#### CSS 선택자를 이용한 요소 노드 취득

CSS 선택자는 스타일을 적용하고자 하는 HTML 요소를 특정할 때 사용하는 문법이다.

```JavaScript
/* 전체 선택자 : 모든 요소를 선택*/
* {... }
/* 태그 선택자 : 모든 p 태그 요소를 모두 선택 */
p {...}
/* id 선택자 : id 값이 'foo'인 요소를 모두 선택*/
#foo { ... }
/* class 선택자 : class 값이 'foo'인 요소를 모두 선택*/
#foo { ... }
/* 어트리뷰트 선택자: input 요소 중에 type 어트리뷰트 값이 text인 요소를 모두 선택 */
input[type=text] { ... }
/* 자식 선택자: div 요소의 자식 요소 중 p 요소를 모두 선택 */
div p { ... }
/* 자식 선택자: div 요소의 바로 자식 요소 중 p 요소를 모두 선택 */
div > p { ... }
/* 인접 형제 선택자: p 요소의 형제 요소 중에 p 요소 바로 뒤에 위치하는 ul 요소를 선택 */
p + ul { ... }
/* 일반 형제 선택자: p 요소의 형제 요소 중에 p 요소 뒤에 위치하는 ul 요소를 모두 선택 */
p ~ ul { ... }
/* 가상 클래스 선택자: hover 상태인 a 요소를 모두 선택 */
a:hover { ... }
/* 가상 요소 선택자: p 요소의 콘텐츠의 앞에 위치하는 공간을 선택 */
/* 일반적으로 content 프로퍼티와 함께 사용한다. */
p::before { ... }
```

Document.prototype/Element.prototype.querySelector 메서드는 인수로 전달한 CSS 선택자를 만족시키
는 하나의 요소 노드를 탐색하여 반환한다.

- 인수로 전달한 CSS 선택자를 만족시키는 요소 노드가 여러 개인 경우 첫 번째 요소 노드만 반환한다.
- 인수로 전달된 CSS 선택자를 만족시키는 요소 노드가 존재하지 않는 경우 null을 반환한다.
- 인수로 전달한 CSS 선택자가 문법에 맞지 않는 경우 DOMException 에러가 발생한다.

```HTML
<!DOCTYPE html>
<html>
<body>
<ul>
<li class="apple">Apple</li>
<li class="banana">Banana</li>
<li class="orange">Orange</i>
</ul>
<script>
// class 어트리뷰트 값이 bananal인 첫 번째 요소 노드를 탐색하여 반환한다.
const $elem = document.querySelector('.banana');

// 현재 요소 노드의 style.color 어트리뷰트 값을 변경한다.
$elem.style.color = 'red';
</script>
</body>
</html>
```



Document.prototype/Element.prototype.querySelectorAll 메서드는 인수로 전달한 CSS 선택자를 만족
시키는 모든 요소 노드를 탐색하여 반환한다. querySelectorAll 메서드는 여러 개의 요소 노드 객체를 갖는
DOM 컬렉션 객체인 NodeList 객체를 반환한다. NodeList 객체는 유사 배열 객체이면서 이터러블이다.

* 인수로 전달된 CSS 선택자를 만족시키는 요소가 존재하지 않는 경우 빈 NodeList 객체를 반환한다.

* 인수로 전달한 CSS 선택자가 문법에 맞지 않는 경우 DOMException 에러가 발생한다.

```HTML
<!DOCTYPE html>
<html>
<body>
<ul>
<li class="apple">Apple</li>
<li class="banana">Banana</li>
<li class="orange">Orange</li>
</ul>
<script>
const $elems = document.querySelectorAll('ul > li');
console.log($elems);
$elems.forEach(elem => { elem.style.color = red'; });
</script>
</body>
</html>
```

HTML 문서의 모든 요소 노드를 취득하려면 querySelectorAll 메서드의 인수로 전체 선택자 '*'를 전달한다.

```JavaScript
// 모든 요소 노드를 탐색하여 반환한다.

const $all = document.querySelectorAll('*');
// NodeList(8) [html, head, body, ul, Li#banana, Li#orange, script]
```

getElementsByTagName, getElementsByClassName 메서드와 마찬가지로 querySelector, querySelectorAll
메서드는 Document.prototype에 정의된 메서드와 Element.prototype에 정의된 메서드가 있다. Document.
prototype에 정의된 메서드는 DOM의 루트 노드인 문서 노드, 즉 document를 통해 호출하며, DOM 전체에
서 요소 노드를 탐색하여 반환한다. Element.prototype에 정의된 메서드는 특정 요소 노드를 통해 호출하며
특정 요소 노드의 자손 노드 중에서 요소 노드를 탐색하여 반환한다.



CSS 선택자 문법을 사용하는 querySelector, querySelectorAll 메서드는 getElementById,
getElementsBy*** 메서드보다 다소 느린 것으로 알려져 있다. 하지만 CSS 선택자 문법을 사용하여 좀 더 구
체적인 조건으로 요소 노드를 취득할 수 있고 일관된 방식으로 요소 노드를 취득할 수 있다는 장점이 있다.
따라서 id 어트리뷰트가 있는 요소 노드를 취득하는 경우에는 getElementById 메서드를 사용하고 그 외의
경우에는 querySelector, querySelectorAll 메서드를 사용하는 것을 권장한다.

-----


#### 특정 요소 노드를 취득할 수 있는지 확인

Element.prototype.matches 메서드는 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는
지 확인한다.

```HTML
<!DOCTYPE html>
<html>
<body>
<ul id="fruits">
<li class="apple">Apple</li>
<li class="banana">Banana</li>
<li class="orange">Orange</li>

</body>
<script>
const $apple = document.querySelector('.apple');
// $apple 노드는 '#fruits > li.apple'로 취득할 수 있다.
console.log($apple.matches('#fruits > li.apple')); 
// $apple 노드는 #fruit > Li.banana'로 취득할 수 없다.
console.log($apple.matches('#fruits > li.banana')); // false
</script>
</html>
```

Element.prototype.matches 메서드는 이벤트 위임을 사용할 때 유용하다. 

-----


#### HTMLCollection과 NodeList

DOM 컬렉션 객체인 HTMLCollection과 NodeList는 DOM API가 여러 개의 결과값을 반환하기 위한 DOM
컬렉션 객체다. HTMLCollection과 NodeList는 모두 유사 배열 객체이면서 이터러블이다. 따라서 for... of
문으로 순회할 수 있으며 스프레드 문법"을 사용하여 간단히 배열로 변환할 수 있다.


HTML Collection과 NodeList의 중요한 특징은 노드 객체의 상태 변화를 실시간으로 반영하는 살아 있는 객
체라는 것이다. HTML Collection은 언제나 live 객체로 동작한다. 단. NodeList는 대부분의 경우 노드 객체의
상태 변화를 실시간으로 반영하지 않고 과거의 정적 상태를 유지하는 non-live 객체로 동작하지만 경우에
따라 live 객체로 동작할 때가 있다.


- HTMLCollection
getElementsByTagName, getElementsByClassName 메서드가 반환하는 HTML Collection 객체는 노드 객체의
상태 변화를 실시간으로 반영하는 살아 있는 DOM 컬렉션 객체다. 따라서 HTMLCollection 객체를 살아
있는 객체라고 부르기도 한다.
다음 예제를 살펴보자.

```HTML
<!DOCTYPE html>
<head>
<style>
red { color: red; }
.blue { color: blue; }
</style>
</head>
<html>
<body>>
<ul id="fruits">
<li class="red">Apple</li>
<li class="red">Banana</li>
<li class="red">Orange</li>
</ul>
<script>

// class 값이 'red'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
const $elems = document.getElem
console.log($elems);

// HTMLCollection 객체의 모든 요소의 class 값을 'blue'로 변경한다.
for (let i = 0; i < $elems.length; i++) {
$elems[i].className = 'blue';
}

// HTMLCollection 객체의 요소가 3개에서 1개로 변경되었다.
console.log($elems); // HTMLCollection(1) [li.red]
</script>
</body>
</html>
```

위 예제는 getElementsByClassName 메서드로 class 값이 'red'인 요소 노드를 모두 취득하고, 취득된 모든
요소 노드를 담고 있는 HTMLCollection 객체를 for 문으로 순회하며 className 프로퍼티 "를 사용하여 모든
요소의 class 값을 'red'에서 'blue'로 변경한다.


따라서 위 예제가 에러 없이 실행되면 모든 li 요소의 class 값이 'blue'로 변경되어 모든 li 요소는 CSS에
의해 파란색으로 렌더링될 것이다. 하지만 위 예제를 실행해 보면 예상대로 동작하지 않는다. 다음 그림처럼
두 번째 li 요소만 class 값이 변경되지 않는다.

이처럼 HTMLCollection 객체는 실시간으로 노드 객체의 상태 변경을 반영하기 때문에 for 문 때문에 HTMLCollection 객체를 for 문으로 순회하면서 노드 객체의 상태를 변경해야 할 때 주의해야 한다. 이 문 제는 for 문을 역방향으로 순회하는 방법으로 회피할 수 있다.

```JavaScript
// for 문을 역방향으로 순회
for (let i = $elems.length - 1; i >= 0; i--){
  $elems[i].className = 'blue';
}
```

또는 while 문을 사용하여 HTMLCollection 객체에 노드 객체가 남아 있지 않을 때까지 반복하는 방법으로 회피할 수도 있다.

```JavaScript
// while 문으로 HTMLCollection에 요소가 남아 있지 않을 때까지 반복 처리
let i = 0;
while ($elems.length > i) {
  $elems[i].className = 'blue';
}
```


더 간단한 해결책은 부작용을 발생시키는 원인인 HTML Collection 객체를 사용하지 않는 것이다. 유사 배열
객체이면서 이터러블인 HTMLCollection 객체를 배열로 변환하면 부작용을 발생시키는 HTMLCollection 객체
를 사용할 필요가 없고 유용한 배열의 고차 함수(forEach, map, filter, reduce 등)를 사용할 수 있다.

```JavaScript
// 유사 배열 객체이면서 이더러들인 HTML Collec
[... $elems].forEach(elem => elem.className = 'blue);
```

- NodeList

HTML Collection 객체의 부작용을 해결하기 위해 getElementsByTagName, getElementsByClassName 메서드
대신 querySelectorAll 메서드를 사용하는 방법도 있다. querySelectorAll 메서드는 DOM 컬렉션 객체인
실시간으로 노드 객체의 상태 변경을 반영하지 않는NodeList 객체를 반환한다. 이때 NodeList 객체는 실시간으로
객체다.

```JavaScript
// querySelectorAll은 DOM 컬렉션 객체인 NodeList를 반환한다.
const $elems = document.querySelectorAll('.red');
// NodeList 객체는 NodeList.proto
$elems.forEach(elem => elem.className = 'blue');
```


querySelectorAll이 반환하는 NodeList 객체는 NodeList.prototype.forEach 메서드를 상속받아 사용할
수 있다. NodeList.prototype.forEach 메서드는 Array.prototype.forEach 메서드와 사용방법이 동일하다.
NodeList.prototype은 forEach 외에도 item, entries, keys, values 메서드를 제공한다.
NodeList 객체는 대부분의 경우 노드 객체의 상태 변경을 실시간으로 반영하지 않고 과거의 정적 상태
를 유지하는 non-live 객체로 동작한다. **하지만 childNodes 프로퍼티가 반환하는 NodeList 객체는
HTMLCollection 객체와 같이 실시간으로 노드 객체의 상태 변경을 반영하는 live 객체로 동작하므로 주의가
필요하다.**

```HTML
<!DOCTYPE html>
<body>
<ul id="fruits">
<li>Apple</li>
<li>Banana</li>
</ul
</body>
<script>
const $fruits = document.getElementById('fruits');

// childNodes 프로퍼티는 NodeList 객체(Live)를 반환한다.
const { childNodes } = $fruits;
console.log(childNodes instanceof NodeList); // true

// $fruits 요소의 자식 노드는 공격 텍스트 노드(39.3.1절 "공백 텍스트 노드" 참고)를
// 포함해 모두 5개다.
console.log(childNodes); // NodeList(5) [text, li, text, li, text]

for (let i = 0; i < childNodes.length; i++) {
// removeChild 메서드는 $fruits 요소의 자식 노드를 DOM에서 삭제한다.
// (39.6.9절 "노드 삭제" 참고)
// removeChild 메서드가 호출될 때마다 NodeList 객체인 childNodes가 실시간으로 변경된다.
// 따라서 첫 번째, 세 번째, 다섯 번째 요소만 삭제된다.
$fruits.removeChild(childNodes[i]);
}

// 예상과 다르게 $fruits 요소의 모든 자식 노드가 삭제되지 않는다.
console.log(childNodes); // NodeList(2) [li, li]
</script>
</html>
```

이처럼 HTMLCollection이나 NodeList 객체는 예상과 다르게 동작할 때가 있어 다루기 까다롭고 실수하기 쉽
다. 따라서 노드 객체의 상태 변경과 상관없이 안전하게 DOM 컬렉션을 사용하려면 HTMLCollection이나
NodeList 객체를 배열로 변환하여 사용하는 것을 권장한다. HTMLCollection과 NodeList 객체가 메서드를
제공하기는 하지만 배열의 고차 함수만큼 다양한 기능을 제공하지는 않는다. HTMLCollection이나 NodeList
객체를 배열로 변환하면 배열의 유용한 고차 함수(forEach, map, filter, reduce 등)를 사용할 수 있다는 장
점도 있다.

HTMLCollection과 NodeList 객체는 모두 유사 배열 객체이면서 이터러블이다. 따라서 스프레드 문법이나
Array.from 메서드를 사용하여 간단히 배열로 변환할 수 있다.

------------------

```HTML
<!DOCTYPE html>
<html>
<body>>
<ul id="fruits">
<li>Apple</li>
<li>Banana</li>
</ul>
</body>
<script>
const $fruits = document.getElementById('fruits');
// childNodes 프로퍼티는 NodeList 객체(live)를 반환한다.
const { childNodes } = $fruits;
console.log(childNodes instanceof NodeList); //true

// $fruits 요소의 자식 노드는 공백 텍스트 노드를 포함해 모두 5개다.
console.log(childNodes); // NodeList(5) [text, li, text, li , text]

for (let i = 0 , i < childNodes.length; i++) {
  //removesChild 메서드는 $fruits 요소의 자식 노드를 DOM 에서 삭제한다.
  // removeChild 메서드가 호출될 대마다 NodeList 객체인 childNodes가 실시간으로 변경된다.
  // 따라서 첫 번째, 세 번째, 다섯 번째 요소만 삭제된다.
}

$fruits.removeChild(childNode[i]);
});
// $fruits 요소의 모든 자식 노드가 삭제된 상태이다.
console.log(childNodes); // NodeList(2) [li, lis]
</script>
</html>
```

### 노드 탐색
요소 노드를 취득한 다음, 취득한 요소 노드를 기점으로 DOM 트리의 노드를 옮겨 다니며 부모, 형제, 자식
노드 등을 탐색raversing node waking해야 할 때가 있다.

```HTML
<ul id="fruits">
<li class="apple">Apple</li>
<li class="banana">Banana</li>
<li class="orange">Orange</li>
</ul>
```

ul#fruits 요소는 3개의 자식 요소를 갖는다. 이때 먼저 ul#fruits 요소 노드를 취득한 다음, 자식 노드를
모두 탐색하거나 자식 노드 중 하나만 탐색할 수 있다. li.banana 요소는 2개의 형제 요소와 부모 요소를 갖
는다. 이때 먼저 li.banana 요소 노드를 취득한 다음, 형제 노드를 탐색하거나 부모 노드를 탐색할 수 있다.



이처럼 DOM 트리 상의 노드를 탐색할 수 있도록 Node, Element 인터페이스는 트리 탐색 프로퍼티를 제공
한다.
parentNode, previousSibling, firstChild, childNodes 프로퍼티는 Node.prototype이 제공하고, 프로퍼티
키에 Element가 포함된 previousElementSibling, nextElementSibling과 children 프로퍼티는 Element.
prototype이 제공한다.
노드 탐색 프로퍼티는 모두 접근자 프로퍼티 "다. 단, 노드 탐색 프로퍼티는 setter없이 getter만 존재하여 참
조만 가능한 읽기 전용 접근자 프로퍼티다. 읽기 전용 접근자 프로퍼티에 값을 할당하면 아무런 에러 없이 무
시된다.


#### 공백 텍스트 노드

 HTML 요소 사이의 스페이스, 탭, 줄바꿈(개행) 등의 공백white space 문자는 텍스트 노드를 생성한다. 이를 공백 텍스트 노드라 한다. 

```HTML
<!DOCTYPE html>
<html>
<body>
<ul id="fruits">
<li class="apple">Apple</li>
<li class="banana">Banana</li>
<li class="orange">Orange</li>
</ul>
</body>
</html>
```

텍스트 에디터에서 HTML 문서에 스페이스 키, 탭키. 엔터 키 등을 입력하면 공백 문자가 추가된다. 위
HTML 문서에도 공백 문자가 포함되어 있다. 위 HTML 문서는 파싱되어 다음과 같은 DOM을 생성한다.

이처럼 HTML 문서의 공백 문자는 공백 텍스트 노드를 생성한다. 따라서 노드를 탐색할 때는 공백 문자가 생
성한 공백 텍스트 노드에 주의해야 한다. 다음과 같이 인위적으로 HTML 문서의 공백 문자를 제거하면 공백
텍스트 노드를 생성하지 않는다. 하지만 가독성이 좋지 않으므로 권장하지 않는다.

```HTML
<ul id="fruits"><li
class="apple">Apple</li><li
class= "banana">Banana</li><li
class="orange">Orange</li></ul>
```
#### 자식 노드 탐색


#### 자식 노드 존재 확인

자식 노드가 존재하는지 확인하려면 Node.prototype.hasChildNodes 메서드를 사용한다. hasChildNodes 메
서드는 자식 노드가 존재하면 true, 자식 노드가 존재하지 않으면 false를 반환한다. 단, hasChildNodes 메
서드는 childNodes 프로퍼티와 마찬가지로 텍스트 노드를 포함하여 자식 노드의 존재를 확인한다.


```HTML
<!DOCTYPE html>
<html>
<body>
<ul id="fruits">
</ul>
</body>
<script>
// 노드 탐색의 기점이 되는 #fruits 요소 노드를 취득한다.
const $fruits = document.getElementById('fruits');
// #fruits 요소에 자식노드가 존재하는 지 확인한다.
// hasChildNodes 메서드는 테스트 노드를 포함하여 자식 노드의 존재를 확인한다.
console.log($fruits.hasChildNodes()); // true
</script>
</html>
```

자식 노드 중에 텍스트 노드가 아닌 요소 노드가 존재하는지는 확인하려면 hasChildNodes 메서드 대신
children.length 또는 Element 인터페이스의 childElementCount 프로퍼티를 사용한다.

```HTML
<!DOCTYPE html>
<html>
<body>
<ul id="fruits">
</ul>
</body>
<script>
// 노드 탐색의 기점
// #fruits 요소 노드를 취득한다.
const $fruits = document.getElementById('fruits');
// 자식 노드의 존재를 확인한다.
console.log($fruits.hasChildNodes()); // true
// 요소 노드가 아닌 텍스트 노드가 존재하는지는 확인한다.
console.log(!!$fruits.children.length); // 0 false
// 요소 노드가 존재하는지는 확인한다.
console.log(!!$fruits.childElementCount); // 0 false
</script>
</html>
```

#### 요소 노드의 텍스트 노드 탐색

요소 노드의 텍스트 노드는 요소 노드의 자식 노드다. 따라서 요소 노드의 텍스트 노드는 firstChild 프로퍼티
로 접근할 수 있다. firstChild 프로퍼티는 첫 번째 자식 노드를 반환한다. firstChild 프로퍼티가 반환한
노드는 텍스트 노드이거나 요소 노드다.

```HTML
<!DOCTYPE html>
<html>
<body>
<div id="foo">Hello</div>
<script>
// 요소 노드의 텍스트 노드는 firstChild 프로퍼티로 접근할 수 있다.
console.log(document.getElementById('foo').firstChild); // #text
</script>
</body>
</html>
```

---------

### 부모 노드 탐색
부모 노드를 탐색하려면 Node.prototype.parentNode 프로퍼티를 사용한다. 텍스트 노드는 DOM 트리의 최
종단 노드인 리프 노드keer node이므로 부모 노드가 텍스트 노드인 경우는 없다.

```HTML
<!DOCTYPE html>
<html>
<body>
<ul id="fruits">
<li class="apple">Apple</li>
<li class="banana">Banana</li>
<li class="orange">Orange</li>
</body>
<script>
const $banana = document.querySelector('.banana");
// .banana 요스노
console.log($banana.parentNode);
</script>
</html>
```

#### 형제 노드 탐색

부모 노드가 같은 형제 노드를 탐색하려면 다음과 같은 노드 탐색 프로퍼티를 사용한다. 단, 어트리뷰트 노드
는 요소 노드와 연결되어 있지만 부모 노드가 같은 형제 노드가 아니기 때문에 반환되지 않는다. 즉, 아래 프
로퍼티는 텍스트 노드 또는 요소 노드만 반환한다.

- 프로퍼티

1. Node.prototype.previousSibling :  부모 노드가 같은 형제 노드 중에서 자신의 이전 형제 노드를
탐색하여 반환한다. previousSibling 프로퍼티가 반환하는 형제 노드는 요소 노드뿐만 아니라 텍스트 노드일 수도 있다.
2. Node.prototype.nextSibling : 부모 노드가 같은 형제 노드 중에서 자신의 다음 형제 노드를
탐색하여 반환한다. nextSibling 프로퍼티가 반환하는 형제노드는 요소 노드뿐만 아니라 텍스트 노드일 수도 있다.

3. Element.prototype.previousElementSiblin : 부모 노드가 같은 형제 요소 노드 중에서 자신의 이전 형제 요소 노드를 탐색하여 반환한다. previous ElementSibling 프로퍼티는 요소 노드만 반환한다.

4. Element.prototype.nextElementSibling : 부모 노드가 같은 형제 요소 노드 중에서 자신의 다음 형제 요소
노드를 탐색하여 반환한다. nextElementSibling 프로퍼티는 요소 노드만 반환한다.

