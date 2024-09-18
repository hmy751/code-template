# Array
---
## 2차원 배열 만들기
```js
new Array(r).fill(0).map(() => new Array(c).fill(value));
```
new Array(r)은 요소가 빈 요소로 fill을 사용하지 않으면 map메서드 콜백이 제대로 실행되지 않는다.

