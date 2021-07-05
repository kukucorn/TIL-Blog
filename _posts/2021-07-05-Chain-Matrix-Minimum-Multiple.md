---
layout: post
title: "[20210705] DP를 이용한 연쇄 행렬 최소 곱셈"
date: 2021-07-05 20:24
last_modified_at: 2021-07-05 20:24
tags: [algorithm]
toc: true
---

> DP를 이용한 연쇄 행렬 곱셈의 최소 곱의 수를 구해보자.

### 행렬의 곱셈에 관한 이야기

행렬의 곱셈은 결합 법칙이 성립한다.
A \* (B \* C) = (A \* B) \* C

하지만, 행렬을 곱하는 순서에 따라서 곱하는 횟수는 달라진다.

연쇄 행렬 최소 곱셈이란? 행렬을 모두 곱하게 될 때 곱하는 횟수의 최소값을 의미한다.

주어진 행렬의 수가 작다면 bruth force를 이용하여 풀어도 괜찮지만, 행렬의 수가 많아진다면 매우 많은 비용이 들 수 있다.

이를 최적화하기 위한 방법으로 DP를 이용해 볼 것이다.

### DP에 사용되는 점화식

(i ≤ k ≤ j-1)일 때, M[i][j] = min(M[i][k] + M[k + 1][j] + d[i-1] \* d[k] \* d[j])
(i == j)일 때, M[i][j] = 0

M[i][j]는 행렬 i에서 j까지의 곱의 횟수를 의미한다.
d[k]는 연쇄 행렬 중 k번 째 행렬의 크기이다.

예로, A = 30 X 10 행렬, B = 10 X 5 행렬이라고 하자.
d[0] = 30,
d[1] = 10,
d[2] = 5 이다.

행렬 A를 1, B를 2이라 하면,
1 ≤ k ≤ 1 이므로, k == 1일 때 M[1][2] 값이 최소가 된다.(유일한 값이기 때문)
M[1][2] = M[1][1] + M[2][2] + d[0] \* d[1] \* d[2]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= 0 + 0 + 30 \* 10 \* 5
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= 1500

### java 코드

    for(int diagonal = 0; diagonal < matrixSize; diagonal++) {
        for(int i = 1; i <= matrixSize - diagonal; i++) {
            int j = i + diagonal;
            if (j == i) {
                M[i][j] = 0;
                continue;
            }
            M[i][j] = Integer.MAX_VALUE;
            for (int k = i; k <= j - 1; k++)
                M[i][j] = Math.min(M[i][j], M[i][k] + M[k + 1][j] + d[i - 1] * d[k] * d[j]);
        }
    }

해당 로직을 거치게 되면 M[i][j]는 i에서 j까지 행렬을 곱하는 많은 경우의 수 중 최소 곱의 횟수를 의미하게 된다.

---

### 출처

[https://huiyu.tistory.com/entry/DP-연쇄행렬-최소곱셈-알고리즘](https://huiyu.tistory.com/entry/DP-연쇄행렬-최소곱셈-알고리즘)
