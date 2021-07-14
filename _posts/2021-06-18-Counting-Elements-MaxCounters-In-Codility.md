---
layout: post
title: "[20210618] Counting Elements - MaxCounters (in Codility)"
date: 2021-06-18 21:30
last_modified_at: 2021-06-18 21:30
tags: [algorithm]
toc: true
---

### 문제 정보

N개의 counter가 존재하며, 해당 counter들은 순서가 존재한다.
M개의 counter 위치 정보가 저장된 배열(A)이 있으며, 이를 순회하며 위치 정보와 일치하는 counter의 값을 증가시킨다. 만약 N+1의 값이 나오면 counter의 모든 값을 counter에서 가장 큰 값으로 통일한다.

[https://app.codility.com/programmers/lessons/4-counting_elements/max_counters/](https://app.codility.com/programmers/lessons/4-counting_elements/max_counters/)

### 직면한 문제

효율성에서 O(N \* M)이 나왔으며, 효율성을 통과하지 못했다.

처음 제출한 코드는

    for(int num : A) {
        if(num == N + 1) {
            max = findMax(counters);
            Arrays.fill(counters, max);
        } else {
            counters[num]++;
        }
    }

이었다.

처음 for문에서 O(M)의 복잡도,
Arrays.fill에서 O(N)의 복잡도가 나오므로,
결론적으로 이는 O(N \* M) 복잡도였던 것이다.

### 해결 방법

여기서 최적화를 하기위해서는 Arrays.fill()을 사용하지 않아야 했다.

그래서 나온 코드가

    for(int num : A) {
        if(num == N + 1) {
            boundary = max;
        } else {
            if(counters[num] < boundary) counters[num] = boundary;
            counters[num]++;
            max = Math.max(max, counters);
        }
    }

    for(int i = 0; i < counters.length; i++) {
        if(counters[i] < boundary) counters[num] = boundary;
    }

boundary라는 변수를 사용하여 전체 변수의 기준 값을 저장하였고,
전체의 값이 최대값으로 변경해야 하더라도 즉시 배열 전체를 초기화 하지 않고, 필요 시에만 초기화 해주면서,
처음 for문에서 O(M)의 복잡도,
두 번째 for문에서 O(N)의 복잡도로
전체 시간복잡도는 O(M + N)으로 줄일 수 있었다.