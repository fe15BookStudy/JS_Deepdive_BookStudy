# 주요 배열 메서드 정리

## 1. Array.prototype.flatMap

- 배열의 각 요소에 함수를 적용한 후 결과를 평탄화(flatten)
- `map()` + `flat()`을 한 번에 수행
- 중첩 배열을 1단계 평탄화하며 새로운 배열 반환

## 2. Array.prototype.findIndex

- 조건을 만족하는 첫 번째 요소의 인덱스 반환
- 조건에 맞는 요소가 없으면 `-1` 반환
- `find()`와 유사하지만 값 대신 인덱스 반환

## 3. Array.prototype.find

- 조건을 만족하는 첫 번째 요소의 값 반환
- 조건에 맞는 요소가 없으면 `undefined` 반환
- `filter()`와 달리 첫 번째 일치 요소만 반환

## 4. Array.prototype.some

- 배열의 하나 이상 요소가 조건을 만족하면 `true`
- 모든 요소가 조건을 만족하지 않으면 `false`
- 빈 배열에서는 항상 `false` 반환

## 5. Array.prototype.every

- 모든 요소가 조건을 만족하면 `true`
- 하나라도 조건을 만족하지 않으면 `false`
- 빈 배열에서는 항상 `true` 반환

## 6. Array.prototype.reduce

- 배열의 모든 요소를 순회하며 하나의 값으로 축약
- 누적값(accumulator)과 현재값(currentValue) 사용
- 초기값 설정 가능, 설정하지 않으면 첫 번째 요소가 초기값
- 합계, 평균, 최댓값, 배열 평탄화, 중복 제거 등에 활용

## 7. Array.prototype.filter

- 조건을 만족하는 모든 요소로 새로운 배열 생성
- 조건에 맞지 않는 요소는 제외
- 원본 배열 변경하지 않음

## 8. Array.prototype.map

- 각 요소에 함수를 적용하여 새로운 배열 생성
- 원본 배열과 같은 길이의 새 배열 반환
- 원본 배열 변경하지 않음

## 9. Array.prototype.forEach

- 각 요소에 대해 함수 실행 (반복문 역할)
- 반환값 없음 (`undefined` 반환)
- 배열 수정이나 부수 효과를 위해 사용
- `break`나 `continue` 사용 불가
