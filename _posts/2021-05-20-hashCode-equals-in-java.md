---
layout: post
title: "[20210520] hashCode() & equals() in java"
date: 2021-05-20 22:07
last_modified_at: 2021-05-20 22:07
tags: [Java]
toc: true
---

### equals()

equals()는 객체라면 모두 사용할 수 있다. 그런데 내가 선언한 클래스를 같은 값으로 초기화 시킨 후 equals()로 비교해보면 항상 false를 반환한다. 왜냐하면 Object의 equals()는 두 객체를 == 으로 비교하기 때문이다. 그래서 equals()로 객체를 비교하려면 equals()를 override 시켜야 한다.

### hashCode()

그런데, equals()만 구현해서는 hashMap에서는 객체를 구분할 수 없다. 왜냐하면 hashMap에서는 key를 결정할 때, hashCode()를 이용하기 때문이다. 그래서 hashMap의 key값을 동일하게 인식하기 위해서는 hashCode()를 override 시켜야 한다.

### hashCode에서 31을 곱하는 이유

대부분의 hashCode의 경우 클래스의 변수 해시 값에 31을 곱하는 경우를 본 적이 있을 것이다. (String의 hashCode의 경우도 그렇다.) 그러면 왜 31을 곱하는 것일까??  
첫 번째 이유는 소수 값을 사용 했을 때 다른 수를 사용했을 때 보다 hashing 한 결과에 대한 충돌이 덜하다는 것이다. 즉, hash algorithm을 사용했을 때 다른 input에 같은 output이 나올 확률이 적다는 뜻이다.
두 번째 이유는 hash 알고리즘에 특정 숫자의 곱셈을 사용하게 되는데 31을 곱하는 것은 왼쪽으로 5번 shift하고 자기 자신을 빼는것과 같기 때문에 곱셈보다 쉬프트가 속도적인 측면에서 더 좋기 때문에 최적화가 되기 때문이다.

    31 * i == (i << 5) - i

그렇기 때문에 꼭 31만이 정답은 아니다. 위의 특성을 만족하는 수 중 하나가 31이기 때문에 31을 쓰는 것이지 다른 숫자를 사용해도 문제가 되지는 않는다.

---

### 출처

[Why is 31 used in Hashcode?](https://www.quora.com/Why-is-31-used-in-Hashcode)
