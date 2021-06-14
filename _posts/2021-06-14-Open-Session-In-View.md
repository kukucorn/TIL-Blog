---
layout: post
title: "[20210614] Open Session In View In Spring"
date: 2021-06-14 15:31
last_modified_at: 2021-06-14 15:31
tags: [spring]
toc: true
---

> Open Session In View 에 대해 알아보자.

원래 영속성 컨텍스트는 트랜잭션과 생명주기를 같이한다. 그렇게 되면 트랜잭션이 종료되면 영속성 컨텍스트도 함께 사라진다.

### Open Session In View

- Session은 영속성 컨텍스트를 의미(예전에 영속성 컨텍스트를 session이라 불렀음)
- 영속성 컨텍스트를 View까지 열어둔다는 뜻

### 왜 열어둘까?

- 일반적으로 트랜잭션은 Service와 Repository 단에서 시작되고 종료됨
- 만약 트랜잭션이 종료되는 시점에 영속성 컨텍스트도 사라진다면 View 단에서 dirty checking이랑 lazy loading이 불가능해짐
- 스프링부트에서는 spring.jpa.open-in-view 속성을 기본적으로 true로 설정

### OSIV On 장&단점

장점

- Controller나 View 에서도 지연로딩이 가능해짐

단점

- DB Connection resource를 오래 잡고 있으므로 자원 낭비
- 극단적으로 모든 커넥션이 사용중이라면 장애 발생 가능

### OSIV Off 장&단점

장점

- DB와의 커넥션 리소스 절약

단점

- 모든 지연로딩을 트랜잭션 안에서 처리해야함
- 트랜잭션이 끝나기 전에 지연 로딩을 강제로 호출해 두어야 한다.
- 이를 위한 별도 메소드를 추가로 정의해야 함.

### 정리

- 서비스 서버에서는 일반적으로 OSIV를 끄고, 관리자 페이지와 같이 동시 접속이 많지 않은 상황에서는 편의를 위해 켤 수 있음.
