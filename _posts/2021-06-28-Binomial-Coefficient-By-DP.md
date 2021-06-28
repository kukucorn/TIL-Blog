---
layout: post
title: "[20210628] DP를 이용한 이항계수"
date: 2021-06-28 21:51
last_modified_at: 2021-06-28 21:51
tags: [algorithm]
toc: true
---

> 다이나믹 프로그래밍 기법을 이용한 이항계수를 구해보자.

### 이항계수란?

쉽게 말해서 조합의 가짓수를 의미한다.

### 이항계수 정의

우리가 흔히 알고있는 정의 중 하나는
(1) nCk = n! / (k! \* (n - k)!) 이다.
하지만, (1)은 숫자가
또 다른 정의에 의해
(2) nCk = n-1Ck-1 + n-1Ck
로도 표현 가능하다.
(2)은 흔히 말하는 점화식과 굉장히 닮았으며, 이를 이용해서 다이나믹 프로그래밍 기법을 활용가능하다.

### 이항계수 코드

    public int bino_coef(int n, int k) {
        if(n == k || k == 0) return 1;
        return bino_coef(n - 1, k) + bino_coef(n - 1, k - 1);
    }

위 (2)번 정의의 점화식을 이용해서 표현한 코드이다.
하지만, 이는 Top-down 방식으로 풀어가는데 동일한 계산을 여러번 한다는 단점이 있다.
이러한 단점을 해결하기 위해 DP를 적용하면 된다.

### DP를 이용한 이항계수

    public int bino_coef_with_DP(int n, int k) {

        if(DP[n][k] > 0) return DP[n][k];
        if(n == k || k == 0) return DP[n][k] = 1;

        return DP[n][k] = (bino_coef(n - 1, k) + bino_coef(n - 1, k - 1));
    }

매 계산마다 DP 배열에 저장하며, 한 번 계산된 것은 계산된 값을 바로 사용하여 시간을 단축시킨다.

---

### 출처

[https://ko.wikipedia.org/wiki/%EC%9D%B4%ED%95%AD\_%EA%B3%84%EC%88%98](https://ko.wikipedia.org/wiki/%EC%9D%B4%ED%95%AD_%EA%B3%84%EC%88%98)
