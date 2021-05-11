---
layout: post
title: "[20210511] Circular Dependencies in Spring"
date: 2021-05-11 21:06
last_modified_at: 2021-05-11 21:06
tags: [Spring]
toc: true
---

## Circular Dependency

> Circular Dependency란 bean A와 bean B가 서로 의존하는 관계인 상태이다.

### 언제 예외가 발생하는가?

dependency를 선언하는 방법에는 여러가지가 있는데, 그 중 constructor injection을 이용하면서 Circular Dependency 상태라면 BeanCurrentlyInCreationException가 발생한다고 한다.

### 왜 예외가 발생하는가?

다른 의존 관계 설정 방법은 그들이 필요할 때 의존 관계를 설정하지만, constructor injection은 context loading 때 의존 관계를 설정하기 때문에 예외가 발생한다.

### 해결책은 무엇인가?

1. Redesign - circular dependency가 발생하지 않도록 한다.
2. @Lazy - lazy를 설정하면 context loading 때는 proxy 객체를 만들어 두었다가 필요로 할 때 생성한다.
3. Setter/Field injection
4. @PostConstruct - 만약 A, B가 Circular Dependency 상태라면 A의 dependency injection이 끝나고 나서 B에서 A로의 dependency를 설정한다.
5. Implement ApplicationContextAware and InitializingBean - 설정이 끝난 ApplicationContext에서 의존하기 위한 bean을 가져와서 설정한다.

### 무엇이 최선인가??

내가 참고한 자료에서는 우선적으로 circular dependency가 발생한다면 해당 bean들을 redesign하는 것을 추천하고 있다.  
하지만, 불가피하게 사용해야 한다면 선호하는 방법은 setter injection이라고 한다.  
하지만, 여러 다른 방법들도 있으니 상황에 맞춰 사용하면 된다고 말하고 있다.

---

### 출처

[Circular Dependencies in Spring](https://www.baeldung.com/circular-dependencies-in-spring)
