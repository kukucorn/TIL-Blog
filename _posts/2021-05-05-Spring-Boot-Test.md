---
layout: post
title: "[20210505] Spring Boot Test"
date: 2021-05-05 20:39
last_modified_at: 2021-05-05 20:39
tags: [spring-boot-test, test]
toc: true
---

스프링에서 JUnit을 이용한 테스트를 공부하였다.  
테스트는 단위 테스트와 통합 테스트로 나뉘는데,  
단위 테스트에는 MockMVC를 사용하고  
통합 테스트에는 RestTemplate을 사용하였다.  
통합 테스트에서는 테스트 환경을 @SpringBootTest를 선언하여  
Application Context를 모두 구성하기 때문에 시간이 오래걸린다.

참고 : [How to test a controller in Spring Boot](https://thepracticaldeveloper.com/guide-spring-boot-controller-tests/)
