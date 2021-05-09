---
layout: post
title: "[20210509] MySQL Spatial data"
date: 2021-05-09 22:49
last_modified_at: 2021-05-09 22:49
tags: [MySQL]
toc: true
---
## MySQL의 지리정보 Spatial data   
   
MySQL에서는 지리정보(위도, 경도)를 double이나 float으로 표현하지 않고 특정 데이터 타입을 지원한다.   
이를 이용하면 MySQL에서 지리 관련 함수를 제공해 준다.   
가령 내가 오늘 사용한 함수는 두 위치 사이의 거리를 계산해주는 함수를 사용했는데,   
왜 이 함수를 사용해야 하냐면 우리가 흔히 계산하는 두 점 사이의 거리는 평면에서의 거리이다.   
하지만 현실세계에서 두 위치 사이의 거리는 그렇게 계산하면 오차가 발생한다. 왜냐하면 우리가 살고 있는 지구는 둥구느깐...   
그래서 위도 경도를 이용하여 거리를 계산하려면 다른 공식을 사용해야 하는데 이를 MySQL에서는 지원해주는 것이다!   
다음에는 이를 최적화 하기 위해서는 DB에 저장된 모든 위치와 비교하는 것이 아니라 현재 위치에서 근처에 위치한 가계들만 가져올 수 있도록
 index를 설정하는 것을 공부 해보겠다!   
   
***   
   
### 출처   
MySQL Spatial Function : <https://dev.mysql.com/doc/refman/8.0/en/spatial-function-reference.html>   
최적화 : <https://purumae.tistory.com/198>
 