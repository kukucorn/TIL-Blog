---
layout: post
title: "[20220406] in operator in TypeScript(Mapped types)"
date: 2022-04-06 23:26
last_modified_at: 2022-04-06 23:26
tags: [TypeScript]
toc: true
---

in 연산자는 JavaScript에서 객체가 특정 속성을 가지고 있는지 확인하는데 사용한다.

```js
propertyName in objectVariable;
```

객체가 in 연산자 앞에 명시한 속성을 가지고 있다면 true, 아니면 false를 반환한다.  
이러한 특성을 이용해서 TypeScript에서는 type guard로도 사용할 수 있다.  
하지만, 이번 포스팅에서는 type guard로의 in이 아닌 index signature에서 mapped types로 사용된 in을 다루려 한다.

### mapped types

기존의 타입으로 새로운 타입을 생성하는 방법을 mapped types라고 한다.

```ts
interface Person {
  name: string;
  age: number;
}
```

Person 타입이 선언되어 있다.  
Person 타입의 모든 속성이 readonly인 타입을 사용하고 싶을 때,

```ts
interface ReadonlyPerson {
  readonly name: string;
  readonly age: number;
}
```

처럼, 새롭게 타입을 선언할 수 있다.  
하지만, 만약 Person의 name이 string이 아닌 다른 타입으로 변경된다면? Person과 ReadonlyPerson을 둘 다 변경해주어야 한다.  
그렇기 때문에 위의 방법보다는 기존의 Person을 활용하여 ReadonlyPerson을 생성해주면 좋다.  
물론 [Readonly\<T\>](https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlytype) Utility type을 사용하면 된다.  
하지만, Readonly\<T>를 사용하지 않는다면?

```
type ReadonlyPerson = {
    readonly [key in keyof Person]: Person[key];
}
```

처럼 구현할 수 있을 것이다.  
이 때, in 연산자는 뭘까?

### index signature에서의 in 연산자

index signature에서의 in 연산자는 주어진 union type을 하나씩 순회한다.

```
type ReadonlyPerson = {
    readonly [K in keyof Person]: Person[K];
}
```

그래서 방금전 작성한 코드를 다시 보면,  
keyof Person이 Person의 키 값의 union 값을 반환하고,  
반환된 union 값을 하나씩 순회하여 K에 할당한다.  
그렇게 할당된 K는 Person[K]의 타입과 동일하게 할당되고,  
readonly도 함께 추가된다.  
결국 위의 코드는 Person의 key 값을 순회하면서 Person key 값에 매칭되는 타입을 모두 readonly로 변환하라는 의도가 담겨 있음을 알 수 있다.  
이처럼 index signature에서의 in 연산자는 mapped types를 구현할 때 유용하게 사용할 수 있다.
