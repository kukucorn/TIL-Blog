---
layout: post
title: "[20210714] ECMAScript"
date: 2021-07-14 22:42
last_modified_at: 2021-07-14 22:42
tags: [javascript]
toc: true
---

> javascript가 준수하는 사양인 ECMAScript에 대해 설명한다.

### ECMAScript가 생긴 이유

자바스크립트가 Netscape 브라우저 뿐만 아니라 다른 웹 브라우저들의 지원까지 받기 시작하면서 다양한 웹 브라우저에서 자바스크립트가 공토오디게 잘 작동하기 위해서 표준 규격이 필요해졌다.
이 때문에 ECMA 국제 기구에서 ECMAScript Standard라 불리는 스크립트 표준이 만들어지게 된다.

### ECMAScript란?

Javascript와 ECMAScript를 혼용해서 사용하는 경우가 많다. 엄밀히 말하자면 둘은 다르다.
위에서도 설명 했듯이 ECMAScript는 언어가 아니라 규약, 표준이다. 
Javascript는 ECMAScript의 표준을 만족하는 스크립트 언어일 뿐이다. 
버전은 보통 ES(숫자)의 방식으로 많이 사용한다.
ES5는 2009년에 만들어졌고 ES6는 2015년에 만들어졌다.
점차 ES6로 변화하고 있지만 아직까지 ES5를 사용하는 곳이 많으며, ES6를 지원하지 않는 브라우저도 존재한다.

### Babel

그렇다면 ES6로 웹사이트를 구현하게 되면 호환성 문제가 발생하는 브라우저가 있을 수 있다.
그럴 때는 바벨이라는 기술을 사용하여 ES6로 작성된 코드를 ES5의 코드로 바꿀 수 있다. 

---

### 출처

[https://wormwlrm.github.io/2018/10/03/What-is-the-difference-between-javascript-and-ecmascript.html](https://wormwlrm.github.io/2018/10/03/What-is-the-difference-between-javascript-and-ecmascript.html)
[https://takeuu.tistory.com/93](https://takeuu.tistory.com/93)
