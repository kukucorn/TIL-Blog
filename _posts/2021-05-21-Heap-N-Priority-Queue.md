---
layout: post
title: "[20210521] Heap & Priority Queue"
date: 2021-05-21 22:34
last_modified_at: 2021-05-21 22:34
tags: [data structure]
toc: true
---

> 자료구조인 Heap과 Heap으로 구현한 Prioriry Queue에 대해 소개한다.

## Heap

힙은 트리를 기반으로 한 자료 구조이다. 힙의 노드들은 부모 노드와 자식 노드 간에 특별한 관계에 있다. i.e, 부모 노드는 항상 자식 노드보다 크거나 같다 or 그 반대의 경우가 이에 해당한다. 힙의 자식 노드의 최대 수는 힙의 종류에 따라 다르겠지만, 일반적으로 말하는 힙은 최대 2개의 자식 만을 가지는 Binary Heap을 칭한다. 만약 그 힙이 N개의 노드를 가진 완전 이진 트리라면 이 트리의 높이는 log~2~N이다.

### Max(Min) Heap

max 힙 에서는 부모 노드의 값이 항상 자식 노드의 값보다 크거나 같아야 한다. 그리고 이 트리의 루트 노드는 이 트리에서 가장 큰 값을 가진 노드이다.  
정돈 되지 않은 배열로 max heap을 구성하려면 시간복잡도가 O(NlogN) 정도 걸린다. i.e tree에서 leaf nodes를 제외한 나머지 노드들을 bottum-up 방식으로 max_heapify를 진행해야 하기 때문이다. max_heapify는 O(logN) 이다.  
min heap은 max heap의 조건이 반대인 경우이다. i.e 부모 노드의 값이 항상 자식 노드의 값보다 작거나 같아야 한다.

## Applications

### Heap Sort

heap의 이러한 특성으로 정렬을 할 수도 있다.  
만약 heap을 이용하여 오름차순 정렬을 한다면 max heap을 이용하면 된다. max heap의 경우 루트 노드에 현재 트리에서 가장 큰 값을 가진 노드가 루트 노드일 것이다. 그러면 tree node의 갯수가 N이라고 한다면 루트 노드와 Arr[N]의 값과 swap한 후 N-1개의 노드를 가진 heap에서 다시 루트노드를 선정한다 O(logN). 이를 반복하면 결국 오름차순으로 정렬된 배열을 갖게됨.  
힙 정렬의 시간 복잡도는 O(NlogN)이다.

### Priority Queue

heap으로 우선순위 큐를 구현할 수도 있다.  
우선순위 큐는 우선 순위에 따라서 처리하는 큐로 주로 Job Scheduling 에서 사용한다. heap의 루트 노드에 항상 가장 큰 값이나 가장 작은 값을 유지하는 특성을 이용하여 구현한다.
만약 Max Priority Queue를 구현한다고 가정하면,  
해당 큐에서 가장 큰 값을 조회하는 시간 복잡도는 O(1)이다.  
가장 큰 값을 반환하고 제거하는 시간 복잡도는 O(logN)이다. -> 루트 노드를 Arr의 가장 마지막 노드로 채우고 max_heapify를 하기 때문.  
새로운 값을 queue에 삽입하는 시간 복잡도는 O(logN)이다. -> Arr의 (가장 마지막 노드의 index + 1) 위치에 새로운 값을 채우고 heap을 유지하기 위해 parent의 값과 계속해서 비교해 나가기 때문.

---

### 출처

[Heaps/Priority Queues](https://www.hackerearth.com/practice/data-structures/trees/heapspriority-queues/tutorial/#:~:text=A%20heap%20is%20a%20tree,be%20followed%20across%20the%20tree.)
