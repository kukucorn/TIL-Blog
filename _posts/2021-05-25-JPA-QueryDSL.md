---
layout: post
title: "[20210525] SQL JOIN"
date: 2021-05-25 23:49
last_modified_at: 2021-05-25 23:49
tags: [jpa, querydsl]
toc: true
---

> JPA와 QueryDSL에 대한 전반적인 소개를 한다.

### JPA

지루하게 반복되는 CRUD 문제를 세련된 방법으로 해결할 수 있도록 고안된 방법이다. 개발자는 interface를 작성하기만 하면 스프링 Data JPA가 구현 객체를 동적으로 생성해서 주입해준다. Repository 구현체는 스프링 로딩 시점에 만들어진다. CRUD는 JPA에서 자동으로 생성해준다는데, CRUD가 아닌 쿼리는 어떻게 처리할까? @Query 어노테이션으로 직접 정의하거나, 메서드 이름으로 쿼리를 생성할 수 있다. 둘 다 정렬, 페이징 기능을 지원한다.

하지만, JPA에서 쿼리를 직접 정의할 때, SQL이나 JPQL을 사용하면 문자열로 선언해야 하기 때문에 type-check가 불가능하다. 그래서 해당 쿼리를 실행하기 전까지는 오류를 발견할 수 없는 단점이 있다.

### QueryDSL

QueryDSL을 사용하면 컴파일 시점에 문법적인 오류를 찾을 수 있다. Builder api를 사용하기 때문에 java 코드로 query를 작성하기 때문이다. 또한 JPQL과 다르게 BooleanBuilder를 사용해서 동적 쿼리를 사용할 수도 있다. Database에서 조회한 entity 객체에서 원하는 필드만 뽑아서 dto로 뽑아내는 기능도 지원을 한다.  
QueryDSL로 query를 작성하는데 Q-type class가 필요한데, 몇가지 세팅만 해주면 @Entity로 명시한 클래스들의 Q-type class를 자동으로 만들어준다. 또한 query를 만들기 위해서는 JPAQueryFactory가 필요하다. (JDBC는 SQLQueryFactory를 사용) Q-type class의 인스턴스를 사용하는 방법에는 직접 생성해서 사용하거나 이미 생성된 인스턴스를 사용하면 된다.

---

### 출처

https://ict-nroo.tistory.com/117
