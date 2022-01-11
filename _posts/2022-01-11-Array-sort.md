---
layout: post
title: "[20220111] Array.prototype.sort 기본 정렬시 주의점"
date: 2022-01-11 23:55
last_modified_at: 2022-01-11 23:55
tags: [javascript]
toc: true
---

Array.prototype.sort 사용 시, 인자로 비교 함수를 전달할 수 있다.  
하지만, 이는 옵션으로 비교 함수를 전달하지 않고 사용할 수 있다.  
이 때, 주의해야 할 점이 있다.

비교 함수를 전달하지 않으면 오름차순으로 정렬되는 줄 알았지만, 그렇지 않다.

> The default sort order is ascending, built upon converting the elements into strings, then comparing their sequences of UTF-16 code units values. - MDN Web Docs

sort의 기본 정렬은 오름차순이지만, 배열의 원소들을 string으로 변환하고 오름차순으로 정렬한다.  
그렇기 때문에 숫자 배열을 정렬하면 원치않는 결과를 얻을 수 있다.

```js
const arr = [1, 10, 20, 2];

// default sort
arr.sort(); // [1, 10, 2, 20]

// with compare function
arr.sort((a, b) => a - b); // [1, 2, 10, 20]
```

이렇게 숫자를 오름차순 정렬하기 위해서는 비교 함수를 함께 사용해야한다.

---

### 출처

[MDN Web Docs - Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
