---
layout: post
title: "[20220517] ShardingTest 객체 생성 에러"
date: 2022-05-18 00:20
last_modified_at: 2022-05-18 00:20
tags: [k8s]
toc: true
---

> ShardingTest 객체를 생성할 때, mongo 기본 폴더(/data/db)가 없어 발생한 문제를 해결합니다.

샤딩을 테스트하기 위해서 ShardingTest 객체를 사용할 수 있다.

이 때, ShardingTest 객체는 데이터 폴더로 mongo의 기본 폴더인 /data/db를 사용하게 된다.

하지만, 나는 mongo shell에 접속할 때, 기본 폴더 위치인 /data/db 폴더를 사용하지 않고 다른 위치에 존재하는 /{otherPath}/data/db를 사용하고 있었는데, 이게 문제를 발생시켰다.  

> 기본 폴더 위치를 사용하지 않았던 이유는 접근 권한 문제 때문이다.. 해결하지 못해서 권한이 있는 폴더를 사요하고 있었다.

```shell
// terminal에서 mongo shell에 접속
-> mongo --nodb --norc

// mongo shell에 접속 후, ShardingTest 객체 생성
> st = ShardingTest({
... name:"one-min-shards",
... chunkSize:1,
... shards:2,
... rs:{
...   nodes:3,
...   oplogSize:10
... },
... other:{
...   enableBalancer:true
... }});
// Error: Caught std::exception of type boost::filesystem::filesystem_error: boost::filesystem::create_directory: No such file or directory: "/data/db/one-min-shards-rs0-0"
```

발생한 에러를 살펴보면 /data/db/{shard 폴더}를 찾을 수 없다고 한다.

/data/db는 mongo가 사용하는 기본 폴더로 ShardingTest 객체를 생성할 때 기본 폴더를 참고하고 있었다.

그래서 현재 기본폴더로 /data/db가 설정되어 있는 값을 변경해주면 된다.

```tsx
> MongoRunner.dataPath = '/{myDataPath}/data/db'
```

그러면 에러 없이 샤딩이 구성되는 과정을 터미널에서 볼 수 있게 된다.  
