---
layout: post
title: "[20210526] N+1 Problem with JPA & Hibernate"
date: 2021-05-26 16:08
last_modified_at: 2021-05-27 13:30
tags: [jpa]
toc: true
---

> JPA를 사용하다 보면 자주 마주하는 문제인 N+1 query 문제에 대해 알아보자!

### N+1 query 문제란?

조회하려는 엔티티에 연관된 하위 엔티티가 존재할 때, 조회한 엔티티의 데이터(1개) 뿐만 아니라 하위 엔티티의 데이터(N개)까지 조회를 하기 위해서 1개의 쿼리문 뿐만 아니라 N개의 추가적인 쿼리문이 실행되어서 총 N+1개의 쿼리문이 실행되는 것을 말한다.
하위 엔티티의 수(N)가 작다면 차이를 못 느낄 수 있지만, N의 크기가 클 수록 더 많은 쿼리가 실행되면서 성능에 영향을 주게 된다.
slow query log로 느린 쿼리를 찾을 수도 있지만, N+1 이슈를 발생시키는 각각의 쿼리들은 잘게 쪼개어 지기 때문에 slow query log에 남을만큼 느린 쿼리가 되지 못하기에 발견하기 어렵다.

### N+1 query 문제 발생 원인

1. FetchType.EAGER
   엔티티 간에 관계를 설정하면서 FetchType을 설정할 수 있다. 이때, FetchType으로 Eager를 설정한다면 주 객체가 조회될 때 연관된 객체들도 모두 조회하게 된다.
   그렇게 되면 내가 필요하지 않은 데이터도 모두 가져오기 때문에 좋지 않은 방법이다.
   안타깝게도 기본 값으로 해당 속성값이 주어지기 때문에 이를 피하기 위해서는 명시적으로 다른값(LAZY)을 설정해주어야 한다.
   만약 해당 엔티티를 불러올 때 JOIN FETCH를 사용하는 것을 잊어버린다면 항상 N+1 문제가 발생한다.
   만약 연관 객체들 모두가 필요하지 않다면, 기본 값으로 FetchType.LAZY를 쓰는 것이 좋다.

2. FetchType.LAZY
   하지만, FetchType.LAZY를 사용한다고 N+1이 해결되는 것은 아니다.
   연관객체가 모두 프록시 객체로 선언될 뿐 연관객체를 사용하게 될 때는 N+1문제가 발생한다.
   그렇기 때문에 연관객체를 사용해야 한다면 JOIN FETCH를 사용하여야 한다.

3. Second-level cache
   쿼리 결과를 second-level cache에 가져 올 때도 N+1문제가 발생할 수 있다.
   만약 second-level cache에 저장되지 않은 데이터를 사용하려면 N개의 쿼리가 발생한다.

### 해결 방법

1. join fetch
   JPQL의 문법인 join fetch를 사용하는 것이다. 그러면 Subject의 하위 entity까지 한번의 쿼리로 모두 조회할 수 있다.
   하지만, 단점으로는 불필요한 쿼리문이 추가된다는 점이다.

2. @EntityGraph
   쿼리 수행시 바로 가져올 필드명을 지정하면 Lazy가 아닌 Eager 조회로 가져오게 된다.

> 1,2번의 공통점은 둘 다 join을 사용하기 때문에 카테시안 곱(Cartesian Product)이 발생하여 하위 엔티티의 수만큼 상위 엔티티가 중복으로 발생하게 된다. 이런 중복을 제거하기 위해서 하위 엔티티를 Set으로 선언할 수도 있고, query에 distinct를 추가해주어야 한다.  
둘의 차이점은 join fetch는 inner join인 반면 entityGraph는 outer join을 발생시킨다.

3. batch size
   hibernate에서는 default batch size를 지정할 수 있다.  
   하위 엔티티를 조회하게 될 때 기존의 하나의 엔티티에 하나의 쿼리를 보내는 방법이 아닌 하나의 쿼리에 batch size만큼의 엔티티를 조회하는 방법을 사용한다.
