---
layout: post
title: "[20220101] worker(node.js) vs PM2"
date: 2022-01-01 16:43
last_modified_at: 2022-01-01 16:43
tags: [node.js]
toc: true
---

> 이번 포스팅 에서는 node.js의 다중 인스턴스를 다루는 방법에 대해 비교해 본다.

node.js는 하나의 프로세스에서 동작한다.
32bit에서는 512MB의 메모리, 64bit에서는 1.5GM 메모리를 사용하도록 제한되어 있다.
V8엔진의 제한이 그대로 반영된 것이다.
설정으로 메모리 사용량을 조절할 수 있지만, 이보다는 worker를 늘리는 것을 권장한다.

## node.js의 worker

node.js에서 worker를 생성하는 방법에는 child_process와 cluster가 있다.
프로세스를 단순히 병렬로 실행하려면 child_process를 사용하면 되지만, 추가로 로드밸런싱이나 포트 공유 등이 필요하다면 cluster를 선택하는게 좋다.

## node.js cluster 모듈

cluster를 사용하면 인스턴스가 마스터와 워커로 나뉜다.(하나의 마스터와 다수의 워커)
처음 JavaScript를 실행한 인스턴스가 마스터가 된다.
후에, 마스터에서 cluster.fork()를 통해서 워커들을 생성한다.
마스터와 워커는 isMaster, isWorker 메서드로 구분가능하다.
마스터는 되도록 워커들을 생성/관리하는 로직만 포함하고, 워커에서 서비스 로직을 다루는게 좋다.

하지만, cluster를 사용하면 비즈니스 로직과 인스턴스를 관리하는 코드가 섞여서 존재하게 된다.
node.js는 application 로직만 가지고 있는게 좋다.
인스턴스를 관리하는 로직은 application 로직보다는 devops에 가깝다.

## PM2

PM2를 이용하면 node.js의 인스턴스를 클러스터링하고 로드밸런싱해준다.
뿐만 아니라 로깅, 재시작(인스턴스가 의도치 않게 종료되었을 때), 무중단 배포도 가능하다.

---

## 출처
[Is it better to use the cluster module with Node.js servers or to place several Node.js servers behind a load balancer?](https://www.quora.com/Is-it-better-to-use-the-cluster-module-with-Node-js-servers-or-to-place-several-Node-js-servers-running-on-same-machine-behind-a-load-balancer)
