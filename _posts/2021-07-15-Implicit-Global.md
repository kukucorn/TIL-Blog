---
layout: post
title: "[20210715] 암묵적 전역 in Javascript"
date: 2021-07-15 22:02
last_modified_at: 2021-07-15 22:02
tags: [javascript]
toc: true
---

> Javascript의 암묵적 전역에 대해 알아보자.

    var x = 10; // 전역 변수

    function foo() {
        y = 20;
    }
    foo();

    console.log(x + y);

해당 코드를 실행시켜보면 어떤 값이 출력될까??
ReferenceError: y is not defined ?
아니다. 30이 출력된다.

결론적으로 y는 함수 내에서 선언하였지만, 함수의 스코프가 아닌 <U>전역 객체</U>에 저장이 된다.

이를 이해하기 위해서는 y가 할당되는 과정을 알아야 한다.

foo함수가 호출되면 자바스크립트 엔진은 y변수에 값을 할당하기 위해 먼저 스코프 체인을 통해 선언된 변수인지 확인한다.
먼저 함수 스코프를 확인하고 찾을 수 없다면 전역 스코프를 확인한다.
전역 스코프에서도 발견하지 못하면 자바스크립트 엔진은 참조에러를 방생시키는 것이 아니라 전역 객체에 프로퍼티를 동적 생성한다.(window.y = 20)
그래서 y를 전역 변수처럼 사용할 수 있었던 것이다.
이를 암묵적 전역(Implicit global)이라 한다.

y는 변수가 아니므로 변수 호이스팅도 발생하지 않는다.

    console.log(x); // undefined
    console.log(y); // ReferenceError: y is not defined

    var x = 10;

    function foo() {
        y = 20;
    }
    foo();

    console.log(x + y) // 30

또한 y는 변수가 아니라 프로퍼티이기 때문에 delete 연산자로 삭제할 수도 있다.

---

### 참고

'이웅모 지음, 모던 자바스크립트 Deep Dive'
