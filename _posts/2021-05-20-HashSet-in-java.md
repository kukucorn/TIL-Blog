---
layout: post
title: "[20210520] HashSet in java"
date: 2021-05-20 18:07
last_modified_at: 2021-05-20 18:07
tags: [java]
toc: true
---

### Set

Set은 자바 컬렉션 중 하나인데 순서가 없으며 중복된 값을 저장하지 않는다.

### HashSet

HashSet은 Set의 구현체 중 하나인데 Hash알고리즘을 이용해서 Set을 구현하였다.  
HashSet의 java 코드를 살펴보면 사실 HashSet은 HashMap으로 구현되어 있다. 자세하게는 HashSet에 저장하는 값은 HashMap의 key로 유지되며 value에는 더미 값이 들어가 있다. 그래서 생각보다 HashSet은 간단하게 구현되어 있다.

### HashMap

HashMap은 key-value의 자료구조이며, get과 put에 상수시간(O(1))이 걸린다. HashMap은 hash table 구조로 구현되어 있다. HashMap에 저장되는 각 노드들은 key값의 해시 값에 의해 index가 정해지며, 하나의 index에는 여러 노드들이 존재 할 수 있으며, 이 노드들은 LinkedList 로 구현되어 있다. 그렇기 때문에 HashMap에 저장되는 노드의 키는 hashCode()와 equals()가 구현되어 있어야 중복을 배제할 수 있다. hash값으로 table의 인덱스 값을 찾으며, table의 인덱스에 존재하는 노드들 중 중복된 값이 존재하는지 equals()로 비교한다.

---

### 출처
