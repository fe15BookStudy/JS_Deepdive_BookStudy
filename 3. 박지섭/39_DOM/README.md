# 39장 DOM

## 39.1 DOM

**DOM은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조이다.**

## 39.2 노드

### 39.2.1 HTML 요소와 노드 객체

- HTML 요소는 HTM 문서를 구성하는 개별적인 요소를 의미한다. 이 요소는 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 요소 노드 객체로 변환된다.
- **노드 객체들로 구성된 트리 자료구조를 DOM이라 한다.**

### 39.1.2 노드 객체의 타입

```html
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <ul>
      <li id="apple">Apple</li>
      <li id="banana">Banana</li>
      <li id="Orange">Orange</li>
    </ul>
  </body>
</html>
```

- DOM은 노드 객체의 **계층적인 구조**로 구성된다. 노드 객체는 종류가 있고 **상속 구조**를 갖는다. 노드 객체는 총 12개의 종류(노드 타입)가 있다. 이 중 중요한 노드 타입은 다음과 같이 4가지다.
  - **문서 노드**
    - 문서 노드는 DOM 트리의 최상위에 존재하는 루트 노드로서 document 객체를 가리킨다.
    - HTML 문서당 document 객체는 유일하고 DOM 트리의 루트 노드이므로 다른 노드들(요소, 속성, 텍스트)에 접근하려면 문서 노드를 통해야 한다.
  - **요소노드**
    - 요소 노드는 HTML 요소를 가리키는 객체다.
    - 요소 노드는 HTML 요소 간의 중첩에 의해 부자 관계를 가지며, 이 부자 관계를 통해 정보를 구조화한다. 따라서 요소 노드는 문서의 구조를 표현한다고 할 수 있다.(ul 요소 밑에 li 요소는 부자 관계이다.)
  - **속성 노드**
    - 속성 노드는 HTML 요소의 속성을 가리키는 객체다.
    - 속성 노드는 속성이 지정된 HTML 요소의 요소 노드와 연결되어 있다. 단, 요소 노드는 부모 노드와 연결되어 있지만 속성 노드는 부모 노드와 연결되어 있지 않고 요소 노드에만 연결되어 있다.
    - 속성 노드에 접근하여 속성 노드를 참조하거나 변경하려면 요소 노드에 접근해야 한다.
    - 속성 노드는 요소 노드의 자식 노드가 아니다. 속성 노드는 부모 노드가 없으므로 요소 노드의 형제 노드도 아니다. 별도의 노드인데 요소 노드에 붙어 있는 정보로 이해하면 된다.
  - **텍스트 노드**
    - 텍스트 노드는 HTML 요소의 텍스트를 가리키는 객체다.
    - 요소 노드가 문서의 구조를 표현한다면 텍스트 노드는 문서의 정보를 표현한다고 볼 수 있다.
    - 텍스트 노드는 요소 노드의 자식 요소이며, **자식 노드를 가질 수 없는 리프 노드다.** 즉, 텍스트 노드는 DOM 트리의 최종단이다.
    - 텍스트 노드에 접근하려면 먼저 부모 노드인 요소 노드에 접근해야 한다.

## 39.2 요소 노드 취득

- HTML의 구조나 내용 또는 스타일 등을 동적으로 조작하려면 먼저 요소 노드를 취득해야 한다. 요소 노드의 취득은 HTML 요소를 조작하는 시작점이다. 이를 위해 아래와 같이 DOM은 요소 노드를 취득할 수 있는 다양한 메서드가 있다.

### 39.2.1 id를 이용한 요소 노드 취득

- Document.prototype.getElementById
  - 이 메서드는 **인수로 전달한 id 속성 값을 갖는 하나의 요소 노드를 탐색하여 반환한다.** getElementById 메서드는 Document.prototype의 프로퍼티다. 따라서 반드시 문서 노드인 document를 통해 호출해야 한다.
  - id 값은 HTML 문서 내에서 유일한 값이여야 하지만 만약에 id 값을 갖는 요소가 여러 개 존재한다면 getElementById 메서드는 인수로 전달된 id 값을 갖는 첫 번째 요소 노드만 반환한다.(단 하나의 요소 노드를 반환)
  - 인수로 전달된 id 값을 갖는 요소가 존재하지 않는 경우 null을 반환한다.
    ```html
    <!DOCTYPE html>
    <html lang="ko-KR">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <ul>
          <li id="apple">Apple</li>
          <li id="banana">Banana</li>
          <li id="Orange">Orange</li>
        </ul>

        <script>
          // id 값이 'banana'인 요소 노드를 탐색하여 반환한다.
          // 두 번째 li 요소가 파싱되어 생성된 요소 노드가 반환된다.

          const elem = document.getElementById("banana");

          // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
          elem.style.color = "red";
        </script>
      </body>
    </html>
    ```

### 39.2.2 태그 이름을 이용한 요소 노드 취득

- document.getElementsByTagName
  - 이 메서드는 인수로 전달한 태그 이름을 갖는 **모든 요소들**을 탐색하여 반환한다.
  - 메서드 이름에 포함된 Elements가 복수형인 것에서 알 수 있듯이 이 메서드는 여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체를 반환한다.
    ```html
    <!DOCTYPE html>
    <html lang="ko-KR">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <ul>
          <li id="apple">Apple</li>
          <li id="banana">Banana</li>
          <li id="Orange">Orange</li>
        </ul>

        <script>
          // 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
          // 탐색된 요소 노드들은 HTMLCollection 객체(유사 배열 객체)에 담겨 반환된다.

          const elem = document.getElementsByTagName("li");

          // 취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
          // HTMLCollection 객체를 배열로 변환하여 순회하며 color 프로퍼티 값을 변경한다.
          [...elem].forEach((elem) => {
            elem.style.color = "red";
          });
        </script>
      </body>
    </html>
    ```
  - 이 메서드는 Document.prototype에 정의된 메서드와 Element.prototype에 정의된 메서드가 있다. Document.prototype.getElementsByTagName 메서드는 루트 노드인 문서 노드를 통해 호출하며 DOM 전체에서 요소 노드를 탐색하여 반환한다. 하지만 Element.prototype은 특정 요소 노드를 통해 호출하며, 특정 요소 노드의 자손 노드 중에서 요소 노드를 탐색하여 반환한다.
    ```html
    <!DOCTYPE html>
    <html lang="ko-KR">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <ul>
          <li id="apple">Apple</li>
          <li id="banana">Banana</li>
          <li id="Orange">Orange</li>
        </ul>

        <ul>
          <li>HTML</li>
        </ul>

        <script>
          // 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
          // 탐색된 요소 노드들은 HTMLCollection 객체(유사 배열 객체)에 담겨 반환된다.

          const lisFromDocument = document.getElementsByTagName("li");
          console.log(lisFromDocument); // HTMLCollection(4) [li, li, li, li]

          // id가 fruits인 ul 요소의 자손 노드 중에서 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
          const fruits = document.getElementById("fruits");
          const lisFromFruits = fruits.getElementsByTagName("li");
          console.log(lisFromFruits); // HTMLCollection(3) [li, li, li]
        </script>
      </body>
    </html>
    ```

### 39.2.3 class를 이용한 요소 노드 취득

- document.getElementByClassName
  - 이 메서드는 인수로 전달한 class 속성 값을 갖는 **모든 요소 노드들을** 탐색하여 반환한다.
  - getElementsByTagName 메서드와 마찬가지로 여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체를 반환한다. 그리고 이 메서드도 Document.prototype에 정의된 메서드와 Element.prototype에 정의된 메서드가 있다.
    ```html
    <!DOCTYPE html>
    <html lang="ko-KR">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <ul>
          <li class="fruit apple">Apple</li>
          <li class="fruit banana">Banana</li>
          <li class="fruit Orange">Orange</li>
        </ul>

        <script>
          // class 값이 'fruit'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
          const elem = document.getElementsByClassName("fruit");

          // 취득한 모든 요소의 CSS color 프로퍼티 값을 변경한다.
          [...elem].forEach((elem) => {
            elem.style.color = "red";
          });

          // class 값이 'fruit apple'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
          const apples = document.getElementsByClassName("fruit apple");

          // 취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
          [...apples].forEach((appelsElem) => {
            appelsElem.style.color = "blue";
          });
        </script>
      </body>
    </html>
    ```

### 39.2.4 CSS 선택자를 이용한 요소 노드 취득

- document.querySelector

  - 이 메서드는 인수로 전달한 CSS 선택자를 만족시키는 **하나의 요소 노드**를 탐색하여 반환한다.
  - 인수로 전달한 CSS 선택자를 만족시키는 요소 노드가 여러 개인 경우 첫 번째 요소 노드만 반환한다.
  - 만족시키는 요소 노드가 존재하지 않는 경우 null을 반환한다.
    ```html
    <!DOCTYPE html>
    <html lang="ko-KR">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <ul>
          <li class="apple">Apple</li>
          <li class="banana">Banana</li>
          <li class="Orange">Orange</li>
        </ul>

        <script>
          // class 속성 값이 'banana'인 첫 번째 요소 노드를 탐색하여 반환한다.
          const elem = document.querySelector(".banana");

          // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
          elem.style.color = "red";
        </script>
      </body>
    </html>
    ```

- querySelectorAll
  - 메서드는 인수로 전달한 CSS 선택자를 만족 시키는 **모든 요소 노드**를 탐색하여 반환한다.
    ```html
    <!DOCTYPE html>
    <html lang="ko-KR">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <ul>
          <li class="apple">Apple</li>
          <li class="banana">Banana</li>
          <li class="orange">Orange</li>
        </ul>

        <script>
          // ul 요소의 자식 요소인 li 요소를 모두 탐색하여 반환한다.
          const elems = document.querySelectorAll("ul > li");

          // 취득한 요소 노드들은 NodeList 객체에 담겨 반환된다.
          console.log(elems); // NodeList(3) [li.apple, li.banana, li.orange]

          // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
          // NodeList는 forEach 메서드를 제공한다.
          elems.forEach((elem) => {
            elem.style.color = "red";
          });
        </script>
      </body>
    </html>
    ```
- querySelector, querySelectorAll 메서드는 getElementById, getElementsBy\*\*\* 메서드보다 다소 느리다. id 속성이 있는 요소 노드를 취득할 땐 getElementId 메서드를 사용하고 그 외의 경우에는 querySelector, querySelectorAll 메서드를 사용하는 것이 낫다.

### 39.2.5 특정 요소 노드를 취득할 수 있는지 확인

- Element.prototype.matches 메서드는 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인한다.
- 이 메서드는 이벤트 위임을 사용할 때 유용하다.

### 39.2.6 HTMLCollection 과 NodeList

- DOM 컬렉션 객체인 HTMLCollection 과 NodeList는 DOM API가 여러 개의 결과 값을 반환하기 위한 DOM 컬렉션 객체다.
- 이 두 개 모두 유사 배열 객체이면서 이터러블이다. 따라서 for…of문으로 순회할 수 있으며 스프레드 문법을 사용하여 간단히 배열로 변환할 수 있다.
- HTMLCollection은 노드 객체의 **상태 변화를 실시간으로 반영하는 살아있는 객체다.** NodeList는 대부분의 경우 노드 객체의 상태 변화를 실시간으로 반영하지 않고 과거의 정적 상태를 유지하는 non-live 객체로 동작하지만 경우에 따라 live 객체로 동작할 때가 있다.
- HTMLCollection 객체는 실시간으로 노드 객체의 상태 변경을 반영하여 요소를 제거할 수 있기 때문에 for문으로 순회하면서 노드 객체의 상태를 변경해야 할 때 주의해야 한다. 이 문제는 for문을 역방향으로 순회하는 방법으로 회피할 수 있다.
- **노드 객체의 상태 변경과 상관없이 안전하게 DOM 컬렉션을 사용하려면 HTMLCollection이나 NodeList 객체를 배열로 변환하여 사용하는 것이 좋다.** 객체를 배열로 변환하면 배열의 유용한 고차 함수(forEach, map, filter, reduce 등)를 사용할 수 있다. **→ 스프레드 문법[…]이나 Array.from 메서드를 사용하면 간단히 배열로 변경 가능!**

## 39.3 노드 탐색

- 요소 노드를 취득한 다음 취득한 요소 노드를 기점으로 DOM 트리의 노드를 옮겨 다니며 부모, 형제, 자식 노드 등을 탐색해야 할 때가 있다. 다음 예시를 살펴보자.
  ```html
  <ul id="fruits">
    <li class="apple">Apple</li>
    <li class="banana">Banana</li>
    <li class="orange">Orange</li>
  </ul>
  ```
- ul#fruits 요소는 3개의 자식 요소를 갖는다. 이때 먼저 ul#fruits 요소 노드를 취득한 다음, 자식 노드를 모두 탐색하거나 자식 노드 중 하나만 탐색할 수 있다.
- li.banana 요소는 2개의 형제 요소와 부모 요소를 갖는다. 이때 먼저 li.banana 요소 노드를 취득한 다음, 형제 노드를 탐색하거나 부모 노드를 탐색할 수 있다.

### 39.3.1 공백 텍스트 노드

- HTML 요소 사이의 스페이스, 탭, 줄바꿈(개행) 등의 공백 문자는 텍스트 노드를 생성한다. 이를 공백 텍스트 노드라 한다.

### 39.3.2 자식 노드 탐색

- 자식 노드를 탐색하기 위해선 다음과 같은 노드 탐색 프로퍼티를 사용한다.

| 프로퍼티                            | 설명                                                                                                                                                                              |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Node.prototype.childNodes           | **자식 노드를 모두 탐색**하여 DOM 컬렉션 객체인 NodeList에 담아 반환한다. **childNodes 프로퍼티가 반환한 NodeList에는 요소 노드뿐만 아니라 텍스트 노드도 포함되어 있을 수 있다.** |
| Element.prototype.children          | **자식 노드 중에서 요소 노드만 모두 탐색**하여 DOM 컬렉션 객체인 HTMLCollection에 담아 반환한다. **children 프로퍼티가 반환한 HTMLCollection에는 텍스트 노드가 포함되지 않는다.** |
| Node.prototype.firstChild           | 첫 번째 자식 노드를 반환한다. firstChild 프로퍼티가 반환한 노드는 텍스트 노드이거나 요소 노드이다.                                                                                |
| Node.prototype.lastChild            | 마지막 자식 노드를 반환한다. firstChild 프로퍼티가 반환한 노드는 텍스트 노드이거나 요소 노드이다                                                                                  |
| Element.prototype.firstElementChild | 첫 번째 자식 요소 노드를 반환한다. firstElementChild 프로퍼티는 요소 노드만 반환한다.                                                                                             |
| Element.prototype.lastElementChild  | 마지막 자식 요소 노드를 반환한다. lastElementChild 프로퍼티는 요소 노드만 반환한다.                                                                                               |

```html
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <ul id="fruits">
      <li class="apple">Apple</li>
      <li class="banana">Banana</li>
      <li class="orange">Orange</li>
    </ul>

    <script>
      const fruits = document.getElementById("fruits");

      console.log(fruits.childNodes); // NodeList(7) [text, li.apple, text, li.banana, text, li.orange, text]

      console.log(fruits.children); // HTMLCollection(3)[li.apple, li.banana, li.orange]

      console.log(fruits.firstChild); // #text

      console.log(fruits.lastChild); // #text

      console.log(fruits.firstElementChild); // li.apple

      console.log(fruits.lastElementChild); // li.orange
    </script>
  </body>
</html>
```

### 39.3.3 자식 노드 존재 확인

- 자식 노드가 존재하는지 확인하려면 Node.prototype.hasChildNodes 메서드를 사용한다.
- hasChildNodes 메서드는 자식 노드가 존재하면 true를 자식 노드가 존재하지 않으면 false를 반환한다. 단, hasChildNodes 메서드는 childNodes와 마찬가지로 **텍스트 노드를 포함하여 자식 노드의 존재를 확인한다.**

### 39.3.4 요소 노드의 텍스트 노드 탐색

- 요소 노드의 텍스트 노드는 요소 노드의 자식 노드다. 따라서 요소 노드의 텍스트 노드는 firstChild 프로퍼티로 접근할 수 있고 이는 첫 번째 자식 노드를 반환한다. firstChild 프로퍼티가 반환한 노드는 텍스트 노드이거나 요소 노드다.

### 39.3.5 부모 노드 탐색

- 부모 노드를 탐색하려면 Node.prototype.parentNode 프로퍼티를 사용한다. **텍스트 노드는 DOM 트리의 최종단 노드인 리프 노드 이므로 부모 노드가 텍스트 노드인 경우는 없다.**
  ```html
  <!DOCTYPE html>
  <html lang="ko-KR">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>
    </head>
    <body>
      <ul id="fruits">
        <li class="apple">Apple</li>
        <li class="banana">Banana</li>
        <li class="orange">Orange</li>
      </ul>

      <script>
        // 노드 탐색의 기점이 되는 .banana 요소 노드를 취득한다.
        const banana = document.querySelector(".banana");

        // .banana 요소 노드의 부모 노드를 탐색한다.
        console.log(banana.parentNode); // ul#fruits
      </script>
    </body>
  </html>
  ```

### 39.3.6 형제 노드 탐색

- 부모 노드가 같은 형제 노드를 탐색하려면 다음과 같은 노드 탐색 프로퍼티를 사용한다. 단, 속성 노드는 요소 노드와 연결되어 있지만 부모 노드가 같은 형제 노드가 아니기 때문에 반환되지 않는다. **즉, 아래 프로퍼티는 텍스트 노드 또는 요소 노드만 반환한다.**

| 프로퍼티                                 | 설명                                                                                                                                                                       |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Node.prototype.previousSibling           | 부모 노드가 같은 형제 노드 중에서 자신의 이전 형제 노드를 탐색하여 반환한다. previousSibling 프로퍼티가 반환하는 형제 노드는 요소 노드뿐만 아니라 텍스트 노드일 수도 있다. |
| Node.prototype.nextSibling               | 부모 노드가 같은 형제 노드 중에서 자신의 다음 형제 노드를 탐색하여 반환하다. nextSibling 프로퍼티가 반환하는 형제 노드는 요소 노드뿐만 아니라 텍스트 노드일 수도 있다.     |
| Element.prototype.previousElementSibling | 부모 노드가 같은 형제 요소 노드 중에서 자신의 이전 형제 요소 노드를 탐색하여 반환한다. previousElementSibling 프로퍼티는 요소 노드만 반환한다                              |
| Element.prototype.nextElementSibling     | 부모 노드가 같은 형제 요소 노드 중에서 자신의 다음 형제 요소 노드를 탐색하여 반환한다. nextElementSibling 프로퍼티는 요소 노드만 반환한다.                                 |

## 39.4 요소 노드의 텍스트 조작

### 39.4.1 nodeValue

- Node.prototype.nodeValue 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티다. 따라서 nodeValue 프로퍼티는 참조와 할당 모두 가능하다.
- 텍스트 노드의 nodeValue 프로퍼티를 참조할 때만 텍스트 노드의 값, 즉 텍스트를 반환한다.
- 텍스트 노드의 nodeValue 프로퍼티에 값을 할당하면 텍스트를 변경할 수 있다. 따라서 요소 노드의 텍스트를 변경하려면 다음과 같은 순서의 처리가 필요하다.
  - 텍스트를 변경할 요소 노드를 취득한 다음, 취득한 요소 노드의 텍스트 노드를 탐색한다. 텍스트 노드는 요소 노드의 자식 노드이므로 firstChild 프로퍼티를 사용하여 탐색한다.
  - 탐색한 텍스트 노드의 nodeValue 프로퍼티를 사용하여 텍스트 노드의 값을 변경한다.

```html
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="foo">Hello</div>

    <script>
      // 1. #foo 요소 노드의 자식 노드인 텍스트 노드를 취득한다.
      const textNode = document.getElementById("foo").firstChild;

      // 2. nodeValue 프로퍼티를 사용하여 텍스트 노드의 값을 변경한다.
      textNode.nodeValue = "World";

      console.log(textNode.nodeValue); // World
    </script>
  </body>
</html>
```

### 39.5.2 textContent

- Node.prototype.textContent 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 텍스트와 모든 자손 노드의 텍스트를 모두 취득하거나 변경한다.
- 요소 노드의 textContent 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역(시작 태그와 종료 태그 사이) 내의 텍스트를 모두 반환한다. 다시 말해, 요소 노드의 childNodes 프로퍼티가 반환한 모든 노드들의 텍스트 노드의 값, 즉 텍스트를 모두 반환한다. 이때 HTML 마크업은 무시된다.

```html
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="foo">Hello <span>world!</span></div>

    <script>
      // #foo 요소 노드의 텍스트를 모두 취득한다 이때 HTML 마크업은 무시된다.

      console.log(document.getElementById("foo").textContent); // Hello world!
    </script>
  </body>
</html>
```

- nodeValue 프로퍼티를 참조하여도 텍스트를 취득할 수 있지만 텍스트 노드가 아닌 노드의 nodeValue 프로퍼티는 null을 반환하므로 의미가 없고 텍스트 노드의 nodeValue 프로퍼티를 참조할 때만 텍스트 노드의 값, 즉 텍스트를 반환한다.

```html
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="foo">Hello <span>world!</span></div>

    <script>
      // #foo 요소 노드는 텍스트 노드가 아니다.
      console.log(document.getElementById("foo").nodeValue); // null

      // #foo 요소 노드의 자식 노드인 텍스트 노드의 값을 취득한다.
      console.log(document.getElementById("foo").firstChild.nodeValue); // Hello

      // span 요소 노드의 자식 노드인 텍스트 노드의 값을 취득한다.
      console.log(
        document.getElementById("foo").lastChild.firstChild.nodeValue
      ); // world!
    </script>
  </body>
</html>
```

- 요소 노드의 콘텐츠 영역에 자식 요소 노드가 없고 텍스트만 존재한다면 textContent 프로퍼티를 사용하는 편이 코드가 더 간단하다. textContent 프로퍼티로 문자열을 추가할 때 HTML 마크업이 있더라도 문자열 그대로 인식되어 텍스트로 취급된다. 즉, HTML 마크업이 파싱되지 않는다.
