---
layout: post
title: "[20210630] Priority Queue로 중간값 구하기 최적화"
date: 2021-06-30 21:09
last_modified_at: 2021-06-30 21:09
tags: [algorithm]
toc: true
---

> 백준 1655번 가운데를 말해요를 풀이한다.

### 문제 설명

입력 값으로 숫자가 N번 입력된다.
입력 값을 하나씩 입력 받을 때 마다, 이떄까지 불렸던 숫자 중 중간 값을 출력하는 문제이다.

### 첫 시도

처음에는 입력된 숫자를 배열에 정렬된 상태로 유지하면서 중간 값을 구하려고 하였다.
정렬 중에 삽입 정렬이 제한된 조건(배열이 이미 정렬 되어 있다면)에서 빠르다고 알고 있어서 이렇게 접근 했던 것이다.

삽입 정렬처럼 정렬된 상태의 배열에서 새로 들어갈 숫자의 위치를 binary search로 찾고, 삽입된 위치 뒤에 존재하던 배열의 요소들을 한 칸씩 뒤로 밀었다.
binary Search(O(lonN)) \* 배열의 요소 한 칸씩 뒤로 밀기(O(logN))으로 결국 O(NlogN) 시간 복잡도 이기에, 이를 모든 입력마다 적용하니 O(N^2logN)이 되어 시간 초과를 받았다.

### 두번째 시도

한참 고민을 하다가, 힌트를 받은 것이 해당 문제를 Priority Queue로 풀 수 있다는 것이다.
Priority Queue는 저장되는 요소들을 정렬된 상태로 유지하지는 않지만, 저장된 요소들의 최대 값과 최소 값은 Min Heap과 Max Heap으로 알 수 있다.

그래서 생각해낸 아이디어가 Min Heap과 Max Heap 두 개를 사용해서 구하는 것이었다.
두 Heap을 합쳐서 사용하면 중간 값을 유지할 수 있었다.
(Max Heap) 중간 값 (Min Heap)

중간 값을 기준으로 작은 값은 Max Heap으로, 큰 값은 Min Heap에 삽입한다.
하지만, 두 Heap의 크기를 같거나 한쪽에 비해 하나만 부족하도록 유지를 해야한다.

Heap의 insert는 O(logN)이므로, Priority Queue를 두 개 사용해서 O(NlogN)으로 풀 수 있었다.

---

### 출처

[https://www.acmicpc.net/problem/1655](https://www.acmicpc.net/problem/1655)
