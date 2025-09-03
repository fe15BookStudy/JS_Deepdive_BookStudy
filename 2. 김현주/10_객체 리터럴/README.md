# 객체란?

- 객체는 0개 이상의 프로퍼티로 구성된 집합체
- 프로퍼티는 key와 value로 구성
- JavaScript의 모든 값이 객체가 될 수 있음

# 객체 리터럴과 프로퍼티

- 객체 생성 방법 : {} 중괄호를 사용한 key: value형태의 객체 리터럴
- 프로퍼티 키 : 문자열 또는 심벌 값
- 프로퍼티 값 : 모든 JavaScript 값(문자열, 숫자, 함수 등) 가능

```javascript
var person = {
  name: 'Lee',
  sayHello: function () {
    console.log(`Hello! My name is ${this.name}.`);
  },
};

console.log(typeof person); // object
console.log(person); // {name: "Lee", sayHello: f}
```

- 빈 객체는 {}로 생성 가능

```javascript
var empty = {};
```

주의: {} 는 코드 블록이 아닌 객체 리터럴로 평가됨.

- 프로퍼티 접근 방법
  객체의 프로퍼티에 접근하는 방법은 두 가지가 있습니다.

  ```javascript
  let apple = {
    name: 'apple',
    'hello-bye': '🖐️',
    0: 1,
    ['hello-bye1']: '🖐️',
  };
  //속성, 데이터에 접근하기 위해서는
  console.log(apple.name); //마침표 표기법 dot notation
  console.log(apple['hello-bye1']); //대괄호 표기법 bracket notation
  console.log(apple['hello-bye']);
  apple['name'];
  ```

# 객체의 구성

- 객체는 프로퍼티와 메서드로 이루어진 집합체.
- 프로퍼티는 상태(값), 메서드는 동작을 표현.

```javascript
var counter = {
  num: 0,
  increase: function () {
    this.num++;
  },
};
```

# 객체 리터럴의 특징

- C++/Java 같은 클래스 기반 언어는 클래스를 정의하고 new 연산자로 인스턴스를 생성.
- 하지만 자바스크립트는 객체 리터럴만으로도 객체를 생성할 수 있어 훨씬 간단하다.

# 메서드와 this

- 프로퍼티 값이 함수인 경우를 메서드라고 함
- this 키워드로 자신이 속한 객체 참조
- ES5 방식

```javascript
sayHi: function() { console.log(this.name); }
```

- ES6방식

```javascript
sayHi() { console.log(this.name); }
```

단순 함수와 달리 메서드 축약 표현은 프로토타입에 붙고, constructor 속성이 없음.

# 프로퍼티 접근

두 가지 접근 방법:

- 마침표 표기법 : person.name
- 대괄호 표기법 : person['name']

# 프로퍼티 값 갱신

- 이미 존재하는 프로퍼티에 값을 할당하면 값이 갱신됨

# 프로퍼티 동적 생성

존재하지 않는 프로퍼티에 값을 할당하면 동적으로 생성됨

- 동적 추가: obj.newKey = value
- 삭제: delete obj.key
- 없는 키 삭제해도 에러 ❌ (그냥 무시됨)

# 프로퍼티 삭제

- delete연산자로 프로퍼티 삭제 가능
- 존재하지 않는 프로퍼티 삭제 시 에러 발생하지 않음

```javascript
const obj = {
  name: '현주',
  age: 20,
};
//코딩하는 시점에, 정적으로 접근이 확정됨
obj.name;
obj.age;

//동적으로 속성에 접근하고 싶을때 대괄호 표기법 사용!
function getValue(obj, key) {
  return obj[key];
}
console.log(getValue(obj, 'name'));

function addKey(obj, key, value) {
  obj[key] = value;
}
addKey(obj, 'job', 'engineer');
console.log(obj);

function deleteKey(obj, key) {
  delete obj[key];
}
deleteKey(obj, 'age', '20');
console.log(obj);
```

# ES6에서 추가된 객체 리터럴 확장 기능

- 프로퍼티 축약 표현

```javascript
//ES6
let x = 1,
  y = 2;
const obj = { x, y }; //{x: 1, y: 2}
```

- 계산된 프로퍼티 이름

```javascript
//ES6
const key = 'hello';
const obj = { [key]: 'world' }; // {hello: "world"}
```

- 메서드 축약 표현

```javascript
//ES6
const obj = {
  name: 'Lee',
  sayHi() {
    //function 키워드 생략
    console.log('Hi!' + this.name);
  },
};
```
