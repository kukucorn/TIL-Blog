---
layout: post
title: "[20210708] java.util.ConcurrentModificationException"
date: 2021-07-08 23:24
last_modified_at: 2021-07-08 23:24
tags: [java]
toc: true
---

알고리즘 문제를 풀다가 이런 예외가 발생했다. 처음 봤을 때는 동시성문제 때문에 발생한 예외같은데 단일 쓰레드만 사용하고 있던 필자로서는 뭐가 문제인지 1도 예측이 가지 않았다.
그래서 결국 구글 선생님께 여쭈어 보았다...

결론적으론 for-each문 이나 Iterator를 사용할 때 발생할 수 있다고 했다.
결국에는 Iterator를 사용할 때 발생할 수 있는 예외였다. 왜냐면, for-each문도 결국 컴파일 하게되면 Iterator로 변환되기 때문이다.

그렇다면 언제 발생하는 것일까??
Collection 객체들은 모두 Iterator를 제공하는데, 이 때 Iterator로 변환한 Collection을 Iterator를 사용하는 도중에 변화가 생기면 발생하는 예외이다.

    Iterator<Integer> iter = list.iterator();
    while(iter.hasNext()) {
        int num = iter.next();
        if(num == 0) list.remove(num);
    }

좀더 자세히 말하면, Collection들은 모두 modCount라는 지역변수를 가지고, Iterator 또한 modCount를 가진다.
Collection으로 Iterator을 만들면 해당 Collection의 modCount를 Iterator에서는 똑같이 초기화한다.
Iterator는 next()를 호출할 때마다 자신의 modCount와 변환된 Collection의 modCount를 비교하고 다르다면 예외를 발생시킨다.

---

### 출처

[https://jistol.github.io/java/2019/11/24/concurrentmodificationexception-with-ehcache/](https://jistol.github.io/java/2019/11/24/concurrentmodificationexception-with-ehcache/)
