---
layout: post
title: "[20210620] Map을 선언할 때 초기화하는 방법"
date: 2021-06-20 21:59
last_modified_at: 2021-06-20 21:59
tags: [java]
toc: true
---

java.util.Map을 초기화 할 때 보통 선언을 하고 값을 초기화 하여서 사용하였다.

    Map<String, Integer> monthMap = new HashMap<String, Integer>();
    monthMap.put("Jan", 1);
    ...

하지만, 선언과 동시에 초기화 하는 방법이 여러가지 있다.

#### 변경 가능한 Map

##### 익명 하위클래스의 이니셜라이저를 이용한 방식(가끔 알 수 없는 오류가 발생하기도함)

    Map<String, Integer> monthMap = new HashMap<String, Integer>(){
        {
            put("Jan" ,1);
            ...
        }
    }

#### 변경 불가능한 Map

##### 1) 인스턴스 갯수에 제한이 없다.

    Map<String, Integer> monthMap = Collections.unmodifiableMap(new HashMap<String, Integer>) {
        {
            put("Jan", 1);
            ...
        }
    }

##### 2) Java 9에서 지원, 인스턴스 갯수가 10개로 제한

    Map<String, Integer> monthMap = Map.of("Jan", 1, ...);

##### 3) Java 9에서 지원, 인스턴스 갯수 제한 없음

    Map<String, Integer> monthMap = Map.ofEntries(
        entry("Jan", 1),
        ...
    )

---

### 출처

[https://junho85.pe.kr/1784](https://junho85.pe.kr/1784)
