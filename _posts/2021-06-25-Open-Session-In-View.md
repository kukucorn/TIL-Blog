---
layout: post
title: "[20210625] Open Session In View"
date: 2021-06-25 23:02
last_modified_at: 2021-06-25 23:02
tags: [spring]
toc: true
---

> JPA의 옵션 중 하나인 OSIV에 대해 알아보자.

JPA는 영속성 컨텍스트를 이용하여 동작한다.
하지만, 영속성 컨텍스트는 트랜잭션 단위로 존재하며, 트랜잭션이 종료되면 영속성 컨텍스트도 함께 종료된다.

### Open Session In View

- Session은 영속성 컨텍스트를 의미(예전에 영속성 컨텍스트를 session이라 불렀음)
- 즉, 영속성 컨텍스트를 View까지 열어둔다는 뜻

### 왜 View까지 열어둘까?

- 일반적으로 트랜잭션은 Service와 Repository 단에서 시작되고 종료됨
- 만약 트랜잭션이 종료되는 시점에 영속성 컨텍스트도 사라진다면 View 단에서는 dirty checking이랑 lazy loading이 불가능해짐

### 사용법

- spring.jpa.open-in-view 속성을 enabled로 설정하여 사용(spring boot에서는 기본 값으로 enabled로 설정해줌)

### OSIV On

장점

- Controller나 View 에서도 지연로딩이 가능해짐

단점

- DB Connection resource를 오래 잡고 있으므로 자원 낭비
- 극단적으로 모든 커넥션이 사용중이라면 장애 발생 가능

### OSIV Off

장점

- 커넥션 리소스 절약

단점

- 모든 지연로딩을 트랜잭션 안에서 처리해야함
- 트랜잭션이 끝나기 전에 지연 로딩을 강제로 호출해 두어야 한다.
- 이를 위한 별도 메소드를 추가로 정의해야 함.

### 정리

- 서비스 서버는 일반적으로 OSIV를 끄고, 관리자 페이지와 같이 동시 접속이 많지 않은 상황에서는 편의를 위해 켤 수 있음.
