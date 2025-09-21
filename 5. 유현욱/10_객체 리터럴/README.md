# 모던 자바스크립트 Deep Dive

## 10장 객체 리터럴

### 객체란?

자바스크립트는 객체 기반의 프로그래밍 언어이며, 자바스크립트를 구성하는 거의 모든것이 객체다. 객체는 0개이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키와 값으로 구성된다. 자바스크립트에서 사용할 수 있는 모든 값은 프로퍼티 값으로 사용할 수 있다.

```jsx
var counter = {
  num: 0,
  increase: function () {
    this.num;
  }
};
```
이처럼 객체는 객체의 상태를 나타내는 값과 프로퍼티를 참조하고 조작할 수 있는 동작을 모두 포함할 수 있기 때문에 상태와 동작을 하나의 단위로 구조화할 수 있어서 유용하다.

### 객체 리터럴에 의한 객체 생성
자바스크립트는 프로토타입 기반 객체지향 언어로서 클래스 기반 객체지향 언어와는 달리 다양한 객체 생성 방법을 지원한다
- 객체리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스(ES6)

가장 일반적이고 간단한 방법은 객체 리터럴을 사용하는 방법이다
```jsx
var person={
  name:'Lee',
  sayHello : function(){
    console.log(`Hello! My name is ${this.name}.`);
  }
};
console.log(typeof person); // object
console.log(person); //{name:'Lee, sayHello : f}

var empty={}; //빈 객체도 가능
console.log(typeof empty); // object
```

### 프로퍼티
객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.
```jsx
var person={
  name:'Lee',
  age:20
};
//키는 name과 age 값은 'Lee',20 이다.
```
프로퍼티를 나열할 때는 쉼표로 구분된다. 일반적으로 마지막 프로퍼티 뒤에는 쉼표를 사용하지 않으나 사용해도 괜찮다. 프로퍼티 키는 프로퍼티 값에 접근할 수 있는 이름으로서 식별자 역할을 한다. 

식별자네이밍 규칙을 준수하는 이름은 따옴표를 생략할 수 있지만, 식별자 네이밍 규칙을 따르지 않으면 따움표를 사용해야 한다.
```jsx
var person={
  firsrName:'hyun',
  'last-name':'wook'
};
// last-name을 그냥 사용하면 -연산자가 있는 표현식으로 해석해서 에러가 난다
```
문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수 있다.
```jsx
var obj={};
var key='hello';
obj[key]='world'; //프로퍼티키로 사용할 표현식을 대괄호로 묶어야한다.

console.log(obj);//{hello:"world"}
```
프로퍼티 키로 숫자 리터럴을 사용하면 따옴표는 붙지않지만 내부적으로 문자열을 반환한다.
```jsx
var foo={
  0:1,
  1:2,
  2:3
};
console.log(foo); // {0:1,1:2,2:3}
```
이미 존재하는 프로퍼티 키를 중복선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다
```jsx
var foo={
  name:"hyun",
  name:"wook"
};
console.log(foo); // {name: "wook"}
```

### 메서드
자바스크립트에서 사용할 수 있는 모든 값은 프로퍼티 값으로 사용할 수 있다. 함수는 값으로 취급할 수 있기 때문에 프로퍼티 값으로 사용 가능하다. 프로퍼티값이 함수일 경우 일반 함수와 구분하기 위해 메서드라고 불린다. 즉, 메서드는 객체에 묶여있는 함수이다.
```jsx
var circle={
  radius : 5,
  getDiameter: function(){
    return 2 * this.radius;
  }
};

console.log(circel.getDiameter()); //10
```
### 프로퍼티 접근
프로퍼티에 접근하는 방법은 두가지가 있다.
- 마침표 프로퍼티 접근 연산자(.)를 사용하는 마침표 표기법
- 대괄호 프로퍼티 접근연산자([...])를 사용하는 대괄호 표기법
```jsx
var person={
  name:'wook'
};
console.log(person.name); //wook
console.log(person['name']); //wook
//대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 함. 안그러면 에러난다.

console.log(person.age.); //undefined
// 객체에 존재하지 않는 프로퍼티에 접근하면 undefined를 반환한다.
```


### 프로퍼티 값 갱신
이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티값이 갱신된다.
```jsx
var person={
  name :'hyun';
};
person.name = 'wook';
console.log(person); //{name:"wook"}
```

### 프로퍼티 동적 생성
존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당 된다.
```jsx
var person={
  name :'wook';
};
person.age = 26;
console.log(person); //{name:"wook", age : 26}
```

### 프로퍼티삭제
delete 연산자는 객체의 프로퍼티를 삭제한다. 이때 delete연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다. 만약 존재하지 않는 프로퍼티를 삭제하면 아무런 에러없이 무시된다.
```jsx
var person={
  name :'wook';
};
person.age = 26;
delete person.age; //동적으로 생성된 age가 삭제된다.
delete person.address; //없으므로 무시된다.

console.log(person); //{name:"wook"}
```

### ES6에서 추가된 객체 리터털의 확장 기능

#### 프로퍼티 축약 표현
프로퍼티값은 변수에 할당된 값, 즉 식별자 표현식일 수도 있다.
```jsx
//ES5
var x=1;
var y=2;

var obj={
  x:x;
  y:y;
};
console.log(obj); // {x:1,y:2}
```

ES6에서는 프로퍼티값으로 변수를 사용하는 경우 변수이름과 프로퍼티 키가 동일한 이름일때 생략하여 쓸 수 있다. 프로퍼티 키는 변수이름으로 자동생성된다.
```jsx
//ES6
let x=1;
let y=2;

const obj={
 x, y;
};
console.log(obj); // {x:1,y:2}
```

---

#### 계산된 프로퍼티 이름
문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 주의할 점은 프로퍼티 키로 사용할 표현식을 대괄호로 묶어야 한다!

```jsx
//ES5
var prefix='prop';
var i=0;
var obj={};

obj[prefix + '-'+ ++i] = i;
obj[prefix + '-'+ ++i] = i;
obj[prefix + '-'+ ++i] = i;

console.log(obj); //{prop-1: 1, prop-2: 2, prop-3: 3}
```

ES6에서는 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.

```jsx
//ES6
const prefix='prop';
let i = 0;
const obj = {
  [`${prefix} - ${++i}`] : i,
  [`${prefix} - ${++i}`] : i,
  [`${prefix} - ${++i}`] : i
};
console.log(obj); //{prop-1: 1, prop-2: 2, prop-3: 3}
```

---

#### 메서드 축약표현
```jsx
//ES5
var obj={
  name : 'wook',
  sayHi: function(){
    console.log('Hi! ' + this.name);
  }
}
obj.sayHi();//Hi! wook
```

ES6에서는 메서드를 정의할때 function 키워드를 생략한 축약 표현을 사용할 수 있다.
```jsx
//ES6
const obj={
  name : 'wook',
  sayHi(){
    console.log('Hi! ' + this.name);
  }
}
obj.sayHi();//Hi! wook
```