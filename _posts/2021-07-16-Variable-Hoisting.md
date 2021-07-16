---
layout: post
title: "[20210716] 변수 호이스팅"
date: 2021-07-16 20:27
last_modified_at: 2021-07-16 20:27
tags: [javascript]
toc: true
---

> 변수 호이스팅에 대해 알아보자.

### 호이스팅의 발생

    console.log(score);

    var score;

자바스크립트는 인터프리터로 코드를 해석하기 때문에 문을 하나씩 해석해 나간다.
해당 코드를 실행시키면 score변수는 아직 선언되기 전이기 때문에 console에는 참조 에러가 발생할 것 같지만, 에러는 발생하지 않고 undefined가 출력된다.
그 이유는 변수 선언이 런타임이 아니라 그 이전 단계에서 먼저 실행되기 때문이다.

### 호이스팅 발생 원인

    console.log(score);

    var score = 100;

    console.log(score);

그렇다면 위에 얘기 대로라면 console에는 100이 두 번 출력 되어야 한다.
하지만, undefined와 100이 한 번씩 출력 된다.
그 이유는 런타임 이전에 변수 선언만 되지 값이 할당하지는 않기 때문이다.
값이 할당되는 시점은 런타임이다.

그렇기 때문에 처음 score는 변수 선언만 되고 아직 값이 할당되지 않은 상태이기 때문에 undefined를 출력한다.
두 번째 score는 100으로 값이 할당된 후에 출력하기 때문에 100을 출력한다.

### 호이스팅 예방

ES5까지는 변수를 선언하는 방법이 var 하나였지만,
ES6부터는 let, const가 추가 되었다.
var는 호이스팅이 발생하는 반면, let과 const는 호이스팅이 발생하지 않는다.

    console.log(score);

    let score;

이렇게 사용하게 되면 ReferrenceError: score is not defined 에러를 발생시킨다.
애초에 let과 const는 호이스팅이 발생하지 않도록 선언 전에 사용하게되면 에러가 발생한다.

호이스팅을 발생시키지 않고 안전하게 사용하기 위해서는 var보다 let, const를 사용하자.

---

### 출처

'이웅모 지음, 모던 자바스크립트 Deep Dive'
