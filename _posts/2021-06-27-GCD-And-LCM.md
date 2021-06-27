---
layout: post
title: "[20210627] 최대공약수와 최소공배수"
date: 2021-06-27 20:44
last_modified_at: 2021-06-27 20:44
tags: [algorithm]
toc: true
---

> 유클리드 호제법을 이용하여 최대공약수와 최소공배수를 찾아보자.

### 기존의 최대공약수 구하는 방법

중등 교육을 받았다면 최대공약수는 누구나 다 구할 수 있을 것이다.
최대공약수는 두 수의 공통된 약수들을 모두 곱한 값이다.

이를 알고리즘으로 풀이해보면,

    int a, b; // a, b는 임의의 두 수
    int aliquot = 2; // 최소 약수
    int gcd = 1;

    while(a > 1 || b > 1) {
        if(a % aliquot && b % aliquot) {
            gcd *= aliquot;
            a /= aliquot;
            b /= aliquot;
        } else if(a % aliquot) {
            a /= aliquot;
        } else if(b % aliquot) {
            b /= aliquot;
        } else {
            aliquot++;
        }
    }

위의 알고리즘은 약수의 크기가 클 수록 많은 시간이 소모된다.
하지만, 이를 유클리드 호제법을 사용하면 최적화 할 수 있다.

### 유클리드 호제법을 활용한 최대공약수 구하기

유클리드 호제법은 2개의 자연수 a, b에 대해서 a를 b로 나눈 나머지를 r이라 하면(단, a>b), a와 b의 최대공약수는 b와 r의 최대공약수와 같다는 성질을 이용한 알고리즘이다.

> (a, b의 최대공약수) = (b, r의 최대공약수)

이를 코드로 작성하면

     public int gcd(int p, int q) {
        if (q == 0) return p;
        return gcd(q, p%q);
    }

굉장히 코드의 양도 줄고 걸리는 시간도 단축된다.

### 최소 공배수 구하기

> (a, b의 최소공배수) = (a, b의 최대공약수(gcd)) x (a / gcd) x (b / gcd)

---

### 출처

[https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C\_%ED%98%B8%EC%A0%9C%EB%B2%95](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)
