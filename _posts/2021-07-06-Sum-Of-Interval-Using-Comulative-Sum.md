---
layout: post
title: "[20210706] 누적 합을 이용한 구간 합 구하기"
date: 2021-07-06 22:12
last_modified_at: 2021-07-06 22:12
tags: [algorithm]
toc: true
---

> 누적 합을 이용한 구간 합을 구하는 방법에 대해 알아보자.

### 기초

누적 합(Cumulative Sum) : 처음 값부터 N번째 까지의 수를 모두 더한 값
구간 합(Sum Of Intervals) : N번째 부터 M번째 까지의 수를 모두 더한 값

1, 2, 3, 4, 5 가 순서대로 존재할 때,
3번째 까지의 누적 합은 1+2+3으로 6이다.
2번째 부터 4번째 까지의 구간 합은 2+3+4로 9이다.

### 내가 겪었던 문제

[https://www.acmicpc.net/problem/11659](https://www.acmicpc.net/problem/11659)
해당 문제를 풀다가 겼은 문제는 아니지만 백준에 알맞은 문제가 존재해서 해당 문제를 참고해서 다뤄보겠슴다!

1. 처음 접근 방법

처음애 접근한 방법은 모든 구간 합을 구하기 위해서 문제에서 N개의 수가 주어진다면 N X N 배열로 구간 합을 구하려고 했었다.

N X N 배열의 이름을 DP라고 하자.

DP[i][j] 는 i부터 j까지의 구간 합을 의미한다.
그리고 다음과 같은 점화식도 사용할 수 있다.
DP[i][j] = DP[i][k] + DP[k + 1][j] (if, i < k < j)

처음 DP배열을 초기화 하는데에 O(N^2^) 이지만, 한 번 초기화하고 여러번 사용할 때 용이하다.
하지만, 문제가 존재하는데 N의 크기가 커진다면 메모리를 엄청나게 잡아먹게된다 N^2^...

2. 메모리 문제를 해결하는 방법(누적 합 이용)

메모리 문제를 최적화하기 위한 방법으로 누적 합을 이용해서 구간 합을 구하는 방법이 있다.

해당 방법에서는 다음과 같은 점화식을 이용한다.
(i ~ j 구간 합) = (j 까지의 누적 합) - (i-1 까지의 누적 합)

메모리 공간은 N^2^에서 N으로 크게 줄어 들게 된다.
하지만, 구간 합이 필요할 때마다 1번의 연산(minus)이 필요하다.

3. 당연한 소리(잔소리)

당연한 소리일수도 있지만 구간 합이 단 한번만 필요하다면 위에서 나왔던 방법으로 하게되면 메모리 낭비, CPU 낭비가 될 수 있다.
단 한 번의 구간 합은 그냥 무지성으로다가 해당 구간의 값을 모두 더해버리자!!

---

### 출처

백준 11066번 맞은 사람 suy427님의 코드를 보고나서...
(위의 링크와는 다른 문제임)
[https://www.acmicpc.net/problem/11066](https://www.acmicpc.net/problem/11066)