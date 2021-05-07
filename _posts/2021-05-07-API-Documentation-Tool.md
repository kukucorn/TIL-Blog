---
layout: post
title: "[20210507] API 문서화 도구(Swagger)"
date: 2021-05-07 20:57
last_modified_at: 2021-05-07 20:57
tags: [tool]
toc: true
---
## API 문서 자동화 도구 Swagger   
   
   
Spring Boot에서 작성한 Controller 의 api들을 자동으로 문서화 해주는 도구가 있다.   
Swagger라고 하는 도구인데, 메모장으로 작성하여 프론트 담당에게 주던 나의 수고를 덜어주었다.(무식한 나...)   
   
## 사용법   
   
사용법은 간단했다. swagger와 swagger-ui의 dependency를 지정하고, Docket 객체를 bean 등록 해주면 되었다.   
   
## 오류 해결

그런데 현재 진행 중인 프로젝트에 적용하려고 하니 이런 저런 오류가 났다.(401, 404)   
401 오류는 Spring Boot Security를 적용 중이어서 swagger에서 사용하는 url들을 permitAll() 해주니 해결되었다.   
404 오류는 swagger-ui의 version을 3.0.0을 사용하다가 2.x.x version으로 변경하니 잘 동작하였다.   
알고보니 3.0.0에서는 swagger-ui.html이 아니라 /swagger-ui/index.html 을 주소로 사용한다고 한다...   
   
***   
   
### 출처   
사용법 : <https://www.baeldung.com/swagger-2-documentation-for-spring-rest-api>   
401 해결 : <https://stackoverflow.com/questions/37671125/how-to-configure-spring-security-to-allow-swagger-url-to-be-accessed-without-aut>