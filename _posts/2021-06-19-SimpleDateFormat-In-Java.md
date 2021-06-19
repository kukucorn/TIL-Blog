---
layout: post
title: "[20210619] SimpleDateFormat in java"
date: 2021-06-19 20:54
last_modified_at: 2021-06-19 20:54
tags: [java]
toc: true
---

> SimpleDateFormat.parse()를 사용함에 있어서 발생한 실수에 대해 알아보자.

어떤 알고리즘 문제를 풀면서 겪게된 문제였다.

해당 문제에서는 날짜 정보를 "19 Jun 2021" 이런식으로 "일 월 년" 형식으로 제공하였다.

제공된 날짜 정보를 서로 비교해야 하는 문제여서, String 문자열을 java.util.Date 클래스로 변환하기 위해서 java.lang.SimpleDateFormat 클래스를 사용하려 했다.

사용법은 간단했다.

    SimpleDateFormat sdf = new SimpleDateFormat("dd MMM yyyy");
    sdf.parse("19 Jun 2021");

그런데 계속 ParseException이 발생하였다.
마땅한 예외 정보가 나오지 못해서 명확한 이유를 바로 알지 못했다.

그래서 검색을 하다가 SimpleDateFormat 생성자에서 Locale 정보를 입력해야 영어로 표현한 month가 제대로 파싱 된다는 것이었다.

그래서 해결방법은 이렇다.

    SimpleDateFormat sdf = new SimpleDateFormat("dd MMM yyyy", Locale.US);
    sdf.parse("19 Jun 2021");

굉장히 간단한 문제였는데, 예외에서 정확한 이유를 제대로 제시해주지 못해서 오류에대한 감을 잡기가 어려웠던 것 같다...

역시 이래서 예외처리를 자세히 해주어야 하는 것인가...

Locale에도 여러 가지가 존재한다. English, Italy 등등 각 나라별 표시법이 조금씩 차이를 보이는듯 하다.

---

### 출처

[https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html#SimpleDateFormat-java.lang.String-java.util.Locale-](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html#SimpleDateFormat-java.lang.String-java.util.Locale-)
[https://www.baeldung.com/java-string-to-date](https://www.baeldung.com/java-string-to-date)
