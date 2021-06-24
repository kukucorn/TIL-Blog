---
layout: post
title: "[20210624] spring MVC 구조"
date: 2021-06-24 22:01
last_modified_at: 2021-06-24 22:01
tags: [spring]
toc: true
---

> Spring MVC 프레임워크의 구조에 대해서 알아보자.

우선, Spring MVC 프레임워크의 이미지를 기준으로 하나하나 살펴보자.
![SpringMVC](../image/spring_mvc_structure.png)

### Dispatcher Servlet

- HttpServlet을 상속받았다.
- 스프링 부트는 내장 WAS(tomcat)를 띄울 때, DispatcherServlet을 자동으로 등록한다.
- urlPatterns = "/" 로 설정되어 있어 모든 요청이 DispatcherServlet이 받도록 한다.(FrontController Pattern)

### HandlerMapping

- 요청에 알맞은 컨트롤러를 찾는다.
- 다양한 방법으로 컨트롤러를 빈으로 등록하고 이를 사용한다.

### HandlerAdapter

- Adapter Pattern을 적용한 것으로 HandlerAdapter를 통해 컨트롤러의 메소드를 실행한다.

### ViewResolver

- View의 논리 주소를 물리 주소로 변환한다.
- 순차적으로 적절한 ViewResolver를 찾는다.

### View

- 컨트롤러를 통해 만들어진 데이터를 템플릿에 넣고 html파일을 생성하기 위해 렌더링한다.
- 템플릿 엔진에 따라 문서를 만들어내는 문법이 다르기 때문에 해당 view template이 있어야 한다.

#### 템플릿 엔진

지정된 템플릿 양식에 데이터를 포함하여 결과 문서(HTML)를 생성하는 소프트웨어 혹은 모듈

1. server side

- 서버 측에서 DB, API로 부터 가져온 정보를 미리 정의된 템플릿에 넣어서, 서버 측에서 html을 렌더링해서 클라이언트에 보냄
- JSP, Freemarker, mustache

2. client side

- 클라이언트는 서버에서 필요한 데이터만 받은 후, 데이터(json 형태)를 템플릿의 적절한 위치에 replace하고 다시 DOM 객체에 동적으로 그림
- react, Vue
