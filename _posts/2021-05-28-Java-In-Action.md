---
layout: post
title: "[20210528] Java 8"
date: 2021-05-28 22:34
last_modified_at: 2021-05-28 22:34
tags: [java]
toc: true
---

> Java in action 을 읽고 전체적인 java version 8 의 기능들을 소개한다.

java 8 에서 많은 변화가 있었다. 그 중 가장 큰 변화는 단일 코어만 사용(그래서 다중 처리를 위해서 멀티 쓰레드 기법을 사용해야만 했다.)하던 전과 달리 멀티 코어를 사용할 수 있다.
그리고 간결한 코드를 위한 기법들(스트림, 람다)이 추가 되었다.  

### 자바 함수
- 메서드와 람다를 이급 시민에서 일급 시민으로 만들었다. 그래서 함수의 파라미터로 메서드를 제공할 수도 있다.

### 스트림
- 스트림을 사용하면 컬렉션을 활용했을 때와 비교해서 간결하게 코드를 작성할 수 있다.
- 외부 반복이 아닌 내부 반복으로 처리할 수 있다.
- 컬렉션을 사용할 때는 단일 코어를 사용하는 반면, 스트림은 멀티 코어로 병렬로 작업을 수행할 수 있다.
- 스트림을 병렬로 실행하게 되면 처리해야 하는 리스트를 CPU의 갯수 만큼 나누고 각자 처리(forking step)해서 나온 여러 결과를 합치는 식으로 진행한다.
- 컬렉션은 데이터를 어떻게 저장하고 접근할지에 중점을 두는 반면, 스트림은 데이터에 어떤 계산을 할 것인지 묘사하는 것에 중점을 둔다는 점이 다르다.(그래서 가독성이 좋다 짧기도 하고)
- 컬렉션을 기존의 방식으로 처리하는 것 보다 컬렉션을 스트림으로 바꾸고, 병렬로 처리한 다음, 리스트로 다시 복원하는 것이 더 빠르다.

### 디폴트 메서드
- 인터페이스를 변경하는 것은 쉽지 않다. 왜냐면 인터페이스를 구현하는 모든 클래스는 인터페이스에서 변경된 점을 적용해야 하기 
때문
- default 예약어를 사용하면 인터페이스에서 메서드를 정의할 수 있게 된다.
- 라이브러리 설계자가 더 쉽게 변화할 수 있는 인터페이스를 만들 수 있다.
- 하지만 다중 상속과 유사한 문제가 발생할 수 있다.(다이아몬드 상속 문제)

### Optional
- NullPointer 예외를 피할 수 있도록 도와주는 Optional<T> 클래스를 제공한다.
- Optional은 값을 갖거나 갖지 않을 수 있는 컨테이너 객체이다.
- 값의 여부에 따라 처리할 수 있는 로직을 가진다.

### 패턴매칭
- switch를 확장한 구조를 사용할 수 있다. 
- 데이터 형식 분류와 분석을 한 번에 수행할 수 있다.

---
### 출처
java in action(서적)