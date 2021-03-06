---
layout: post
title: "[20210601] Stream in Java"
date: 2021-06-01 18:18
last_modified_at: 2021-06-01 18:18
tags: [java]
toc: true
---

> java.util의 추가된 API인 stream에 대해서 공부한다.

컬렉션은 자바에서 가장 많이 사용하는 기능 중 하나이다. 거의 모든 자바 애플리케이션은 컬렉션을 만들고 처리하는 과정을 포함한다.
SQL 질의에서는 조건에 대해서 어떻게 필터링 할 것인지 구현할 필요가 없다.(반복자, 누적자 등을 이용할 필요가 없다.) 그저 우리가 기대하는 것이 무엇인지 표현하기만 하면 된다.
많은 요소를 포함하는 커다란 컬렉션을 처리하는데 성능을 높이려면 멀티코어 아키텍처를 활용해서 병렬로 컬렉션의 요소를 처리해야 한다. 하지만, 병렬 처리 코드를 구현하는 것은 복잡하고 어렵다.

### 스트림이란 무엇인가?

스트림은 소스에서 추출된 연속 요소로, 데이터 처리 연산을 지원한다.
스트림을 이용하면 선언형(즉, 데이터를 처리하는 임시 구현 코드 대신 질의로 표현할 수 있다)으로 컬렉션 데이터를 처리할 수 있다.
스트림으로 멀티 스레드 코드를 구현하지 않아도 데이터를 투명하게 병렬로 처리할 수 있다.

#### 스트림을 쓰면서 생기는 이득

- 선언형으로 코드를 구현할 수 있다.
- filter, sorted, map, collect 같은 여러 빌딩 블록 연산을 연결해서 복잡한 데이터 처리 파이프라인을 만들 수 있으며, 여러 연산을 파이프라인으로 연결해도 여전히 가독성과 명확성이 유지된다.

### 스트림 시작하기

컬렉션의 주제는 데이터고 스트림의 주제는 계산이다.

### 스트림과 컬렉션

컬렉션은 컬렉션의 모든 데이터를 메모리에 모두 저장해놓고 사용하지만 스트림은 현재 처리하는데 필요한 데이터만 로드해서 사용하면서 소비해 버린다.
컬렉션은 DVD와 같고, 스트림은 스트리밍과 같다.
스트림은 딱 한 번만 탐색할 수 있다. 즉, 탐색된 스트림의 요소는 소비된다.
스트림은 내부반복(스트림 내부적으로 로직이 구현되어 있다.)이고, 컬렉션은 외부 반복(컬렉션의 요소 하나하나에 직접 접근)이다.

### 스트림 연산

스트림의 연산은 크게 중간 연산과 최종 연산으로 구분한다.

중간 연산은 다른 스트림을 반환한다. 중간 연산의 중요한 특징은 단말 연산을 스트림 파이프라인에 실행하기 전까지는 아무 연산도 수행하지 않는다는 것이다.(lazy)
스트림의 게으른 특성 덕분에 몇 가지 최적화 효과를 얻을 수 있다.

1. limit 연산, 쇼트서킷 기법 덕분에 모든 요소에 접근하지 않아도 된다.
2. filter와 map은 서로 다른 연산이지만 한 과정으로 병합되었다.(루트 퓨전)

최종 연산은 스트림 파이프라인에서 결과를 도출한다.

스트림 파이프라인의 개념은 빌더 패턴과 비슷하다. 호출을 연결해서 설정을 만듬(중간 연산을 연결), 준비된 설정에 build 메서드를 호출(최종 연산에 해당)

---

### 출처

Java 8 in Action by Alan Mycroft and Mario Fusco 참고
