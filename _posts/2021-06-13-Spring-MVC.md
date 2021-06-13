---
layout: post
title: "[20210613] Spirng MVC"
date: 2021-06-13 21:33
last_modified_at: 2021-06-13 21:33
tags: [spring]
toc: true
---

> Spring MVC 프레임워크에 대해 공부한다.

Spring MVC 프레임워크는 말 그대로 우리에게 MVC 구조를 제공해주는 프레임워크이다. 그래서 우리는 MVC 구조를 간편하게 사용할 수 있게 된다.

### 구성요소

- DispatcherServlet
- HandlerMapping
- HandlerAdapter
- Controller
- ViewResolver
- View
- View template

Spring MVC를 구성하고 있는 요소들이다. 많은 수에 놀랄수도 있지만 여기서 우리가 구현해야 하는 요소는 Controller와 View template 뿐이다. 하나씩 알아보도록 하자.

### DispatcherServlet

DispatcherServlet은 가장 중요한 요소이다. 해당 요소는 Front Controller 패턴이 적용되어 있다. Spring 서버로 전송되는 모든 요청은 DispatcherServlet으로 오게되며, 각 요청을 처리하기 위해서 위에서 언급한 각 요소들로 위임을 한다.

### HandlerMapping

요청 URL과 매칭되는 컨트롤러를 검색한다.

### HandlerAdapter

매칭된 컨트롤러 객체를 이용해서 요청을 처리한다. DispatcherServlet에는 컨트롤러에서 처리한 ModelAndView를 반환한다. Controller가 여러 방식으로 선언될 수 있기에 동일한 방식으로 처리하기 위해 Adapter Pattern이 적용되어 있다.

### Controller

우리의 비즈니스 로직을 구현하는 곳이다. 주로 @Controller 어노테이션을 이용해서 구현한다.

### ViewResolver

뷰의 논리 주소를 물리 주소로 변환한다.

### View

템플릿에 데이터를 넣고 html파일 생성을 위해 rendering 수행

### View template

server side rendering 방식에는 jsp, Freemarker, mustache 등이 있으며, 지금까지 만들어진 ModelAndView에 포함된 데이터와 템플릿으로 html을 생성할 수 있게 한다.

### @EnableWebMvc 와 WebMvcConfigurer

MVC를 구성하는 요소들은 기본적으로 Spring boot를 사용하게 되면 자동으로 추가해 주지만, 기본으로 제공해주는 인터페이스가 아닌 다른 인터페이스를 사용하려면 @EnableWebMvc와 WebMvcConfigurer를 사용하면 된다. 해당 어노테이션을 사용하면 스프링부트가 제공하는 기본 설정을 무시하게 된다. WebMvcConfigurer 인터페이스에서 새로운 설정이 필요한 요소들만 구현한 다음 해당 클래스를 @Configuration을 사용해 등록하면 된다. WebMvcConfigurer 인터페이스에서 필요한 메소드만 구현할 수 있는 이유는 인터페이스에서 제공하는 모든 메서드가 디폴트 메서드(java8부터 지원)이기 때문이다.

---

### 출처

최범균 저, 스프링 5 프로그래밍 입문
