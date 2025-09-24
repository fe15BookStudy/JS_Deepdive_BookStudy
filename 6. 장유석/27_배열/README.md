# 배열

1. 배열이란?
   배열은 여러 개의 값을 순차적으로 나열한 자료 구조이다. 배열은 사용빈도가 매우 높은 기본적인 자료 구조이다.

```
const arr = ['apple','banana','orange'];
```

배열 리터럴을 통하여 생성한 것이다.
배열이 가지고 있는 값은 요소라고 부른다. js의 모든 값은 배열의 요고사 될 수 있다.
즉, 원시 값은 물론 객체, 함수 배열 등 자바 스크립트에서 값으로 인정하는 모든 것은 배열의 요소가 될 수 있다.
배열의 요소는 재열에서 자신의 위치를 나태내는 0이상의 정수인 인덱스를 갖는다.
요소의 인덱스는 0부터 시작된다. apple이 0번 banana가 1번 orange가 2번이다.

```
arr[0] // apple
arr[1] // banana
arr[2] // orange
```

요소에 접근할 때는 대괄호 표기법을 사용한다. 대괄호 내에는 접근하고 싶은 요소의 인덱스를 지정한다.

```
arr.length // 3
```

배열은 요소의 개수, 배열의 길이를 나타내는 length 프로퍼티를 갖는다.

배열은 인덱스와 length프로퍼티를 갖기 때문에 for문을 통해 순차적으로 접근할 수 있다.

```
for (let i = 0; i < arr.length; i++){
  console.log(arr[i]); // 'apple' 'banana' 'orange'
}
```

js에 배열이라는 타입은 존재하지 않는다. 배열은 객체 타입이다.

```
typeof arr // object
```

배열은 배열 리터럴, Array생성자 함수, Array.of, Array.form 메서드로 생성할수 있다.
배열의 생성자 함수는 Array이며, 배열의 프로토타입 객체는 Array.Prototype이다.
Array.Prototype은 배열을 위한 빌트인 메서드를 제공한다.

```
const arr = [1,2,3];
arr.constructur === array // true
Object.getPrototypeOf(arr) === Array.Prototype // true
```

배열은 객체지만 일반 객체와는 구별되는 독특한 특징이 있다.

| 구조            | 프로퍼티 키와 프로퍼티 값 | 인덱스와 요소 |
| :-------------- | :------------------------ | :------------ |
| 값의 참조       | 프로퍼티 키               | 인덱스        |
| 값의 순서       | X                         | O             |
| length 프로퍼티 | X                         | O             |

일반 객체롸 배열을 구분 하는 가장 면확한 차이는 `값의 순서` 와 `length 프로퍼티`이다.

배열의 장점은 처음부터 순차적으로 요소에 접근 할 수도 있고, 마지막부터 역순으로 요소에 접근 할 수도 있으며,
특정 위치부터 순차적으로 접근 할 수도 있다는 것이다. 이는 배열이 인덱스, 즉 값의 순서와 length 프로퍼티를 갖기 때문이다.

2. 자바스트립트 배열은 배열이 아니다.
   자료 구조에서 말하는 배열은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조를 말한다.
   즉, 배열의 요소는 하나의 데이터 타입으로 통일되어 있으며 서로 연속적으로 인접해 있다.
   이러한 배열을 `밀집 배열`이라 한다.
   이렇게 빈틈없이 연속적으로 이어져 있으면 인덱스를 통해 단 한번의 연산으로 임의의 요소에 접근 할 수 있다.
   이는 매우 효율적이며, 고속으로 동작한다.

`검색 대상 요소의 메모리 주소 = 배열의 시작 메모리 주소 + 인덱스 *요소의 바이트 수`

- 인덱스가 0인 요소의 메모리 주소 : 1000+0\*8 = 1000
  이처럼 배열은 인덱스를 통해 효율적으로 요소에 접근 할 수 있다는 장접이 있다. 하지만 정렬되지 않은 배열에서 특정한 요소를 검색하는 경우
  요소를 처음부터 특정 요소를 발견할 때까지 차례대로 검색 해야 한다.
  또한 배열에 요소를 삽임하거나 삭제하는 경우 배열의 요소를 연속적으로 유지하기 위해 요소를 이동시켜야 하는 단점도 있다.

js의 배열은 위의 자료구조에서 말하는 일반적인 의미의 배열과 다르다.
즉, 배열의요소를 위한 각각의 메모리 공간은 동일한 크기를 갖지 않아도 되며, 연속적으로 이어져 있지 않을수도 있다.
배열의 요소가 연속적으로 이어져 있지 않는 배열을 `희소 배열`이라고 한다.

4. 배열 생성

- 배열 리터럴
  배열 리터럴은 가장 일반적이고도 간편한 배열 생성 방식이다.
  배열 리터럴은 0개 이상의 요소를 쉼표로 구분하여 대괄호로 묶는다. 객체 리터럴과 달리 프로퍼티 키가 없고 값만 존재한다.

  ```
  const arr = [1,2,3];
  console.log(arr.length); //3
  ```

  배열 리터럴에 요소를하나도 추가하지 않으면 배열의 길이, length 프로퍼티 값이 0인 빈 배열이 된다.

  ```
  const arr = [];
  console.log(arr.length); //0
  ```

  배열 리터럴에 요소를 생략하면 희소 배열이 생성된다.

  ```
  const arr = [1, ,3];

  console.log(arr.length); //3
  console.log(arr); // [1, empty , 3]
  console.log(arr[1]); // undefined
  ```

  위 예제의 arr는 인덱스가 1인 요소를 갖지 않는 희소 배열이다.
  arr[1]이 undefined인 이유는 객체 인 arr에 프로퍼티의 키가 1인 프로퍼티가 존재 하지 않기 때문이다.
  만약 `console.log(arr[2]);`이라면 3을 출력할 것이다.

- Array 생성자 함수
  Object 생성자 함수를 통해 객체를 생성할 수 있듯이 Array 생성자 함수를 통해 배열을 생성할 수도 있다.
  Array 생성자 함수는 전달된 인수의 개수에 따라 다르게 동작하므로 주의가 필요하다.

  - 전달된 인숙가 1개 이고 숫자인경우 length 프로퍼티 값이 인수인 배열을 생성한다.

    ```
    const arr = new Array(10);

    console.log(arr); //[empty * 10]
    console.log(arr.length); //10
    ```

    이때 생성된 배열은 희소 배열이다. length 프로퍼티의 값은 0이 아니지만 실제로 배열의 요소는 존재 하지 않는다. ?

    ```
    console.log(Object.getOwnProprepertyDescriptors(arr));
    ```

    배열은 요소를 최대 2의 32승 - 1(1,294,967,295)개 가질 수 있다.
    따라서 Array 생성자 함수에 전달할 인수는 0또는 2의 32승 - 1(1,294,967,295) 이하인 양의 정수 이어야 한다.
    전달된 인수가 범위를 벗어나면 RangError가 발생한다.

  - 전달된 인수가 없는 경우 빈 배열을 생성한다. 즉 배열 리터럴 []과 같다.

  - 전달된 인수가 2개 이상이거나 숫자가 아닌 경우 인수를 요소로 갖는 배열을 생성한다.

    ```
    new Array(1,2,3); //[1,2,3]

    new Array({}); //[{ }]
    ```

    Array 생성자 함수는 new 연산자와 함께 호출 하지 않더라도 배열을 생성하는 생성자 함수로 동작한다.
    이는 Array 생성자 함수 내부에서 new.target을 확인하기 때문이다.

  - Array.of
    Array.of 메서드는 전달된 인수를 요소로 갖는 배열을 생성한다. Array.of는 Array 생성자 함수와 다르게 전달된 인수가 1개이고
    숫자이더라도 인수를 요소로 갖는 배열을 생성한다.

    ```
    Array.of(1); //[1]

    Array.of(1,2,3); //[1,2,3]

    Array.of('strang'); //['strang']

    ```

  - Array.from
    Array.from 메서드는 유사 배열 객체 또는 이터러블 객체를 인수로 전달 받아 배열로 변환하여 반환한다.

    ```
    Array.from({ length: 2,0: 'a',1:'b'}); //['a','b']

    Array.from('Hello'); //['H','e','l','l','o']
    ```

    이터러블을 변환하여 배열을 생성한다. 문자열은 이터러블이다.

    Array.from을 사용하면 두번째 인수로 전달한 콜백 함수를 통해 값을 만들면서 요소를 채울 수 있다.
    Array.from메서드는 두번째 인수로 전달한 콜백 함수에 첫번째 인수에 의해 생성된 배열의 요소 값과 요소 값의 인덱스를 순차적으로 전달하면서 호출하고
    콜백 함수의 반환값으로 구성된 배열을 생성한다.

    ```
    Array.from({ length : 3}); [undefined,undefined,undefined]

    Array.from({ length : 3},(_, i) => i); [0,1,2]
    ```

5. 배열 요소의 참조

   배열의 요소를 참조 할때는 대괄호 표기법을 사용한다. 대괄호 안에는 인덱스가 와야 한다.
   정수로 평가되는 표현식이라면 인덱스 대신 사용할 수 있다.
   인덱스는 값을 참조할 숭 있다는 의미에서 객체의 프로퍼티 키와 같은 역할을 한다.

   ```
   const arr = [1,2];
   // 인덱스가 0인 요소를 참조
   console.log(arr[0]); //1
   // 인덱스가 1인 요소를 참조
   console.log(arr[1]); //2
   ```

   존재 하지 않는 요소에 접근하면 undefined가 반환된다.

   ```
   const arr = [1,2];
   // 인덱스가 2인 요소를 참조. 배열 arr에는 인덱스가 2인 요소가 없다.
   console.log(arr[2]); //undefined
   ```

   배열은 인덱스를 나차내는 문자열을 프로퍼티 키로 갖는 객체이다.
   따라서 존재하지 않는 프로퍼티 키로 객체의 프로퍼티에 접근했을때 undefined를 반환하는 것처럼 배열도 존재 하지 않는 요소를 참조하면 undefined를 반환한다. 희소 배열도 같다.

   ```
   const arr = [1, ,3];

   console.log(Object.getOwnProprepertyDescriptors(arr));

   console.log(arr[1]); //undefined
   console.log(arr[3]); //undefined
   ```

6. 배열 요소의 추가와 갱신

   객체에 프로퍼티를 동적으로 추가할 수 있는 것처럼 배열에도 요소를 동적으로 추가 할 수 있다.
   존재 하지 않는 인덱스를 사용해 값을 할당 하면 새로운 요소가 추가된다.
   이때 length 프로퍼티 값은 자동 갱신된다.

   ```
   const arr = [0];

   arr[1] = 1;

   console.log(arr); //[0,1]
   console.log(arr,length); //2
   ```

   만약 현재 배열의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 희소배열이 된다.

   ```
   const arr = [0];

   arr[100] = 100;
   console.log(arr); //[0,1,empty * 98, 100]
   console.log(arr,length); //101
   ```

   이때 인덱스로 요소에 접근하여 명시적으로 값을 할당하지 않은 요소는 생성되지 않는다는 것에 주의하자.

   이미 요소가 존재하는 요소에 값을 재할당하면 요소 값이 갱신된다.

   ```
   const arr = [0];

   arr[1] = 10;
   console.log(arr); //[0,10,empty * 98, 100]
   ```

7. 배열 요소의 삭제
   배열은 사실 객체이기 때문에 배열의 특정 요소를 삭제 하기 위해 delete연산자를 사용할 수 있다.

   ```
   const arr = [1,2,3];

   delete arr[1];
   console.log(arr); //[1,empty,3]

   console.log(arr,length); //3
   ```

   delete 연산자는 객체의 프로퍼티를 삭제한다. 따라서 위 예제의 delete arr[1]는 arr에서 프로퍼티키가 `1`인 프로퍼티를 삭제한다.
   이때 배열은 희소 배열이 되며 length 값은 변하지 않는다. 따라서 희소 배열을 만드는 delete연산자는 사용하지 않는것이 좋다.

   희소배열을 만들지 않으면서 배열의 특정 요소를 완전히 삭제하려면 Array.prototype.splice 메서드를 사용한다.

   ```
   const arr = [1,2,3];

   arr.splice(1,1);
   console.log(arr); //[1,3]

   console.log(arr,length); //2
   ```

8. 배열 메서드

   배열 메서드는 결과물을 반환하는 패턴이 두가지이므로 주의가 필요하다.
   배열에는 원본 배열 (배열 메서드를 호출한 배열, 즉 배열 메서드의 구현체 내부에서 this가 가르키는 객체)을 직접 변경하는 메서드와
   원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메서드가 있다.
   27-41

   - Array.isArray
     Array.isArray는 Array 생성자힘수의 정적 메서드다
     전달된 인수가 배열이면 true, 배열이 아니면 false를 반환한다.

     ```
     // true
     Array.isArray([]);
     Array.isArray([1, 2]);
     Array.isArray(new Array());

     // false
     Array.isArray();
     Array.isArray({});
     Array.isArray(null);
     Array.isArray(undefined);
     Array.isArray(1);
     Array.isArray("Array");
     Array.isArray(true);
     Array.isArray(false);
     Array.isArray({ 0: 1, length: 1 });

     ```

   - Array.prototype.indexOf
     indexOf 메서드는 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.

     - 원본 배열에서 인수로 전달한 요소와 중복되는 요소가 여러개 있다면 첫번째로 검색된 인덱스를 반환한다.
     - 원본 배열에서 인수로 전달항 요소가 존재 하지 않으면 -1을 반환한다.

     ```
     const arr = [1, 2, 2, 3];
     arr.indexOf(2); // 1
     arr.indexOf(4); // -1
     arr.indexOf(2, 2); // 2
     ```

   - Array.prototype.push
     push 메서드는 인수로 전달 받은 모든 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.
     push 메서드는 원본 배열을 직접 변경한다.

     ```
     const arr = [1, 2];

     let result = arr.push(3, 4);
     console.log(result); // 4

     console.log(arr); // [1, 2, 3, 4]
     ```

   - Array.prototype.pop
     pop 메서드는 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.
     원본이 빈 배열이면 undifined를 반환한다.

     ```
     const arr = [1, 2, 3];
     console.log(arr.pop()); // 3
     console.log(arr); // [1, 2]
     ```

     pop 메서드와 push 메서드를 사용하면 스택을 쉽게 구현 가능하다.
     스택은 후입선출 방식이다. 데이터를 밀어넣는 것을 push 스택에서 데이터를 꺼내는것을 pop 이라고 한다.

   - Array.prototype.unshift
     unshift 메서드는 인수로 전달 받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.

     ```
     const arr = [1, 2];

     let result = arr.unshift(3, 4);

     console.log(arr); // [3, 4, 1, 2]
     ```

   - Array.prototype.shift
     shift 메서드는 원본 배열에서 첫번째 요소를 제거하고 제거하 ㄴ요소를 반환한다.
     원본이 빈 배열이면 undifined를 반환한다.

     ```
     const arr = [1, 2];

     let result = arr.shift();
     console.log(result); // 1

     console.log(arr); // [2]
     ```

   - Array.prototype.concat
     concat 메서드는 인수로 전달된 값들을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다.

     ```
     const arr1 = [1, 2];
     const arr2 = [3, 4];

     let result = arr1.concat(arr2);
     console.log(result); // [1, 2, 3, 4]

     let result = arr1.concat(3);
     console.log(result); // [1, 2, 3]
     ```

   - Array.prototype.splice
     원본 배열의 중간에 요소를 추가 하거나 둥간에 있는 요소를 제거하는 경우 splice 메서드를 사용한다.
     splice 메서드는 3개의 매개변수가 있다

     ```
     const arr = [1, 2, 3, 4];

     // 원본 배열의 인덱스 1부터 2개를 제거하고 새로운 요소 20, 30 을 삽입
     const result = arr.splice(1, 2, 20, 30);


     //제거한 요소 배열로 반환
     console.log(result); //[2, 3]
     //원본 배열이 변경됨
     console.log(arr); // [1, 20, 30, 4]
     ```

   - Array.prototype.slice
     인수로 전달된 범위의 요소들을 볷사하여 배열로 반환한다.
     원본 배열은 변경되지 않는다.

     ```
     const arr = [1, 2, 3];

     arr.slice(0, 1); // [1]
     arr.slice(1, 2); // [2]

     console.log(arr); //[1,2,3]
     ```

   - Array.prototype.join
     원본 배열의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 문자열, 즉 구분자로 연결한 문자열은 반환한다.
     구분자는 생략 가능하며 기분 구분자는 콤마이다.

     ```
     const arr = [1, 2, 3, 4];

     arr.join(); // '1,2,3,4';
     arr.join(""); // '1234'
     arr.join(":"); // '1:2:3:4'
     ```

   - Array.prototype.reverse
     원본 배열의 순서를 반대로 뒤집는다. 이때 원본 배열이 변경된다. 반환값은 변경된 배열이다.

     ```
     const arr = [1, 2, 3];
     const result = arr.reverse();
     //원본 배열 변경
     console.log(arr); // [3, 2, 1]
     // 반환값
     console.log(result); // [3, 2, 1]
     ```

   - Array.prototype.fill
     인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채운다. 이때 원본 배열이 변경된다.

     ```
     const arr = [1, 2, 3];
     arr.fill(0);
     console.log(arr); // [0, 0, 0]
     ```

     ```
     const arr = [1, 2, 3];

     // 값 0을 인덱스1부터 끝까지 요소로 채운다.
     arr.fill(0, 1);
     console.log(arr); // [1, 0, 0]
     ```

     ```
     const arr = [1, 2, 3, 4, 5];

     // 값 0을 인덱스1부터 인덱스3 이전까지 요소로 채운다.
     arr.fill(0, 1, 3);
     console.log(arr); // [1, 0, 0, 4, 5]
     ```

   - Array.prototype.includes
     배열 내에 특정 요소가 포함되어 있는지 확인하여 true 또는 false를 반환한다.
     첫번째 인수로 검색할 대상을 지정한다.

     ```
     const arr = [1, 2, 3];

     // 배열에 요소 2가 포함 되어있는지 확인한다.
     arr.includes(2); // true

     // 배열에 요소 100이 포함 되어있는지 확인한다.
     arr.includes(100); // false
     ```

   - Array.prototype.flat
     인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화한다.
     중첩 배열을 평탄화할 깊이를 인수로 전달할 수 있다. 인수를 생략할 경우 기본 값은 -1이다.
