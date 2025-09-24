## 27.1 배열이란?
- 배열은 여러 개의 값을 순차적으로 나열한 자료구조
- 인덱스(index)를 통해 각 요소에 접근
- 배열 리터럴 `[]`을 사용해 생성

## 27.2 자바스크립트 배열은 전통적 배열이 아니다
- 일반적인 배열과 달리 희소 배열(sparse array) 형태
- 연속적이지 않은 메모리 공간에 저장
- 해시 테이블로 구현되어 접근 속도가 상대적으로 느림

## 27.3 length 프로퍼티와 희소 배열
- `length` = 요소 개수
- `length` 프로퍼티는 배열의 길이를 나타냄
- 늘리면 빈 슬롯만 생김, 줄이면 배열 잘림.
- 희소 배열에서는 실제 요소 개수와 다를 수 있음, 일부 인덱스가 비어있음 → 성능 비효율.
- length 값을 직접 변경 가능

## 27.4 배열 생성
## 27.4.1 배열 리터럴
- const arr = [1, 2 ,3]; 형태로 생성

## 27.4.2 Array 생성자 함수
- new Array() 또는 Array() 사용
- 인수에 따라 동작이 달라짐

## 27.5 배열 요소의 참조
- 대괄호 표기법 arr[0] 사용
- 존재하지 않는 인덱스는 undefined 반환

## 27.6 배열 요소의 추가와 갱신
- 인덱스로 직접 할당하여 요소 추가/수정
- length 프로퍼티 자동 갱신

## 27.7 배열 요소의 삭제
- delete 연산자 사용 시 희소 배열이 됨
- Array.prototype.splice() 메서드 권장

## 27.8 배열 메서드
배열 조작을 위한 다양한 메서드들
- 변경 메서드(mutator): 원본 배열 수정
  - push() : 마지막에 요소 추가
  - pop() : 마지막 요소 제거
  - splice() : 중간 요소 추가/삭제
-접근 메서드 (accessor): 원본 변경 X
  - concat(), slice(), includes(), indexOf()

## 27.8.1 Array.isArray
- 배열 여부를 판별하는 정적 메서드
- `Array.isArray([])` → true
- `Array.isArray({})` → false

## 27.8.2 Array.prototype.indexOf/ includes
- indexOf(): 특정 요소의 인덱스를 반환, 없으면 -1
- includes() : 요소 존재 여부(boolean 반환, ES7 도입)


## 27.8.3 Array.prototype.push
- 배열 끝에 요소 추가, 변경된 length 반환.
- 원본 배열 수정.
- 하나만 추가할 때는 arr[arr.length] = 값 도 가능.
- ES6부터는 스프레드 문법([...arr, 새요소]) 권장 → 부수 효과 없음.

## 27.8.4 Array.prototype.pop
- 배열 끝 요소 제거, 제거된 요소 반환.
- 원본 배열 수정.

## 27.9 스택 구현
- LIFO (후입 선출) 구조.
- `push`(데이터 삽입), `pop`(데이터 제거)으로 쉽게 구현 가능.

## 27.10 큐
- FIFO(선입 선출) 구조.
- `push`, `shift`
- 생성자 함수나 클래스 기반으로 구현 가능.



## forEach메서드의 주요 특징

- `this`바인딩 문제: 콜백 함수 내부에서 `this`가 `undefined`가 됨
- 해결책: 화살표 함수 사용하거나 `bind()`메서드로 `this` 바인딩
- 반환값 없음: `undefined`만 반환하므로 체이닝 불가
- 원본 배열 수정 가능: 콜백 함수에서 원본 배열 요소 변경 가능

# 배열 고차 함수

프로그래밍에서 순수 함수(pure function)와 보조 함수(helper function)의 조합을 통해 로직 내에 존재하는 조건문과 반복문을 제거하여 복잡성을 해결하고 변수 사용을 억제하여 상태 변경을 피하려는 프로그래밍 패러다임

## Array.prototype.sort

- 배열의 요소를 직접 변경하여 정렬된 배열 반환
- 기본 정렬 순서: 오름차순, 문자열로 변환 후 정렬
- 문제점: 숫자 정렬시 `'10'`이 `'2'`보다 앞에 옴(문자열 비교)
- 해결책: 비교 함수 전달

```javascript
numbers.sort((a, b) => a - b); // 오름차순
numbers.sort((a, b) => b - a); // 내림차순
```

- 한글 정렬도 올바른 순서로 정렬됨
- reverse() 메서드와 함께 사용하여 역순 정렬 가능

## Array.prototype.unshift/shift
- unshift(value) : 맨 앞에 추가, length 반환.
- shift() : 맨 앞 요소 제거 및 반환.
- → 큐(FIFO) 구조 구현 가능.

## Array.prototype.splice
- 원본 배열 수정, 요소 추가/삭제/교체 가능.
- `splice(start, deleteCount, ...items)`
- start: 시작 인덱스
- deleteCount: 삭제할 개수
- items: 삽입할 요소
- 특정 값 제거 시: `indexOf` + `splice`
- 모든 값 제거 시: `filter`

## Array.prototype.includes

- 배열 내에 특정 요소가 포함되어 있는지 확인
- `true` 또는 `false` 반환
- 두번째 인수로 검색 시작 인덱스 지정 가능

## Array.prototype.flat

- **ES10(2019)**에서 도입
- 인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화
- 기본값 :`1`(1단계만 평탄화)
- `Infinity` 전달 시 모든 중첩 배열 평탄화

## Array.prototype.fill

- 인수로 전달받을 값으로 배열의 처음부터 끝까지 요소 채움
- 원본 배열 직접 변경
- 두번쨰, 세번째 인수로 채울 번위 지정 가능

## Array.from

- 유사 배열 객체나 이터러블을 얕은 복사하여 새로운 배열 생성
- 두 번째 인수로 콜백 함수 전달하여 요소 변환 가능

## Array.prototype.join

- 원본 배열의 모든 요소를 문자열로 변환 후, 인수로 전달받은 구분자로 연결한 문자열 반환
- 기본 구분자: 콤마(`,`)

## Array.prototype.reverse

- 원본 배열의 순서를 반대로 뒤집음
- 원본 배열 직접 변경

## Array.prototype.slice

- 인수로 전달된 범위의 요소들을 복사하여 새 배열로 반환
- 원본 배열 변경하지 않음
- `slice(start, end)`: start부터 end-1까지 복사
- 음수 인덱스 사용 가능

## Array.prototype.concat

- 인수로 전달된 값들을 원본 배열의 마지막 요소로 추가한 새 배열 반환
- 원본 배열 변경하지 않음
- ES6에서는 스프레드(...) 문법으로 대체 가능

## Array.prototype.flatMap

- 배열의 각 요소에 함수를 적용한 후 결과를 평탄화(flatten)
- `map()` + `flat()`을 한 번에 수행
- 중첩 배열을 1단계 평탄화하며 새로운 배열 반환

## Array.prototype.findIndex

- 조건을 만족하는 첫 번째 요소의 인덱스 반환
- 조건에 맞는 요소가 없으면 `-1` 반환
- `find()`와 유사하지만 값 대신 인덱스 반환

## Array.prototype.find

- 조건을 만족하는 첫 번째 요소의 값 반환
- 조건에 맞는 요소가 없으면 `undefined` 반환
- `filter()`와 달리 첫 번째 일치 요소만 반환

## Array.prototype.some

- 배열의 하나 이상 요소가 조건을 만족하면 `true`
- 모든 요소가 조건을 만족하지 않으면 `false`
- 빈 배열에서는 항상 `false` 반환

## Array.prototype.every

- 모든 요소가 조건을 만족하면 `true`
- 하나라도 조건을 만족하지 않으면 `false`
- 빈 배열에서는 항상 `true` 반환

## Array.prototype.reduce

- 배열의 모든 요소를 순회하며 하나의 값으로 축약
- 누적값(accumulator)과 현재값(currentValue) 사용
- 초기값 설정 가능, 설정하지 않으면 첫 번째 요소가 초기값
- 합계, 평균, 최댓값, 배열 평탄화, 중복 제거 등에 활용
```javascript
arr.reduce((accumulator, currentValue, index, array) => { ... }, initialValue);
```
- accumulator: 누적값
- currentValue: 현재 요소 값
- index: 현재 인덱스
- array: reduce를 호출한 배열
- initialValue: 최초 누적값 (없으면 첫 번째 요소가 사용됨)

초기값의 중요성

- 초기값이 없으면 배열 첫 번째 요소가 accumulator로 설정됨.
- 빈 배열에서 초기값 없이 reduce 호출 시 → 에러 발생.
- 객체의 프로퍼티 합산 등에서는 초기값 반드시 필요.
```javascript
[1, 2, 3].reduce((acc, cur) => acc + cur, 0); // 6
```

## Array.prototype.filter

- 조건을 만족하는 모든 요소로 새로운 배열 생성
- 조건에 맞지 않는 요소는 제외
- 원본 배열 변경하지 않음
```javascript
const numbers = [1, 2, 3, 4, 5];
const odds = numbers.filter(item => item % 2); // [1, 3, 5]
```

## Array.prototype.map

- 각 요소에 함수를 적용하여 새로운 배열 생성
- 원본 배열과 같은 길이의 새 배열 반환
- 원본 배열 변경하지 않음
```javascript
const numbers = [1, 4, 9];
const roots = numbers.map(Math.sqrt); // [1, 2, 3]
```

## Array.prototype.forEach

- 각 요소에 대해 함수 실행 (반복문 역할)
- 반환값 없음 (`undefined` 반환)
- 배열 수정이나 부수 효과를 위해 사용
- `break`나 `continue` 사용 불가
```javascript
[1, 2, 3].forEach((item, index, arr) => {
  console.log(item, index, arr);
});
```
