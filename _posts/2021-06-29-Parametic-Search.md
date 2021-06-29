---
layout: post
title: "[20210629] Binary Search와 Parametic Search"
date: 2021-06-29 21:53
last_modified_at: 2021-06-29 21:53
tags: [algorithm]
toc: true
---

> Binary Search와 Parametic Search를 비교한다.

### Binary Search

이분 탐색으로 정렬된 배열에서 원하는 값의 유무를 O(logN) 시간 복잡도 만에 찾을 수 있다.
여기서 중요한 개념은 원하는 값의 유무이다.

### Parametic Search

이분 탐색의 응용한 것으로 봐도 무방하다.
Parametic Search를 사용하여 정렬된 배열에서 원하는 값의 대략적인 위치를 찾을 수 있다.
여기서 대략적인 위치란 만약 원하는 값이 배열에 중복으로 존재한다면 중복되는 값 중 가장 먼저 나오는 위치 혹은 가장 나중에 나오는 위치를 찾을 수 있다.
또한, 배열에 원하는 값이 존재하지 않더라도 원하는 값이 위치할 수 있는 범위 안의 인덱스 값을 반환할 수도 있다.
이분 탐색은 원하는 값과 동등한지만 비교한다면, Parametic Search에서는 비교함수를 문제에 맞춰서 정의해 주어야 한다.
그래서 비교함수의 복잡도에 따라 다를 수는 있지만, 이분 탐색과 마찬가지로 O(logN) 시간 복잡도를 갖는다.

### 백준 1654번 랜선 자르기

K개의 랜선이 있고, 이를 N개의 랜선으로 자르려고 한다. 이 때, 랜선을 최대 몇 센티미터로 잘라야 N개의 랜선을 만들 수 있는지에 관한 문제이다.

이 문제에서 랜선을 N개로 자를 수 있는 경우의 수는 여러 개가 존재할 수 있다. 그렇기에 최대로 자를 수 있는 길이를 찾는게 핵심이다.

이를 Binary Search로 풀면 최대 값을 찾을 수 없기에 Parametic Search를 이용하여 풀어야 한다.

    private static long parameticSearch(int[] lengthOfString, int numOfString) {

    	long mid = 0;
    	long left = 1;
    	long right = max(lengthOfString);

    	while(left <= right) {
    		mid = (left + right) >>> 1;

                    // 비교 함수
    		if(cutString(lengthOfString, mid) >= (long)numOfString) {
    			left = mid + 1;
    		} else {
    			right = mid - 1;
    		}
    	}

    	return right;
    }

비교 함수로 줄을 특정 높이(mid)에서 잘랐을 때, 나오는 줄의 갯수와 내가 필요로하는 줄의 갯수를 비교하는 것으로 사용하였다.

특정 높이(mid)에서 필요로 하는 갯수보다 많이 만들어 졌거나 같다면 높이를 더 높이고(left = mid + 1)
적게 만들어 졌다면 높이를 낮춘다(right = mid - 1)

while문의 마지막은 항상 left와 right가 같은 상황이다.
left와 right가 같은 상황에서 비교 함수를 만족한다면 right가 최대값이 되고,
비교 함수를 만족하지 않는다면 높이를 하나 낮춘 값이 최대값이 될 것이다.

---

### 출처

[https://www.acmicpc.net/problem/1654](https://www.acmicpc.net/problem/1654)
