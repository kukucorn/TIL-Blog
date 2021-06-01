---
layout: post
title: "[20210513] Emoji😊와 Emoji 호환 Encoding"
date: 2021-05-13 23:52
last_modified_at: 2021-05-13 23:52
tags: [mysql, encoding]
toc: true
---

> Emoji의 단축키는 (윈도우키) + (마침표) or (윈도우키) + (세미콜론) 이다.

## Emoji란?

이모지는 그림 형태의 문자인데 이모티콘과 유사하지만 좀더 작은 느낌이다.  
일본의 휴대전화 문자 메시지에서 시작되어 지금은 대부분의 스마트폰 및 PC 등 다양한 환경에서 사용되는 그림 문자이다.  
나는 이모지가 이모티콘의 간결한 버전이라서 이모지라고 하는줄 알았는데, 일본에서 시작된 만큼 일본어 えもじ(에모지)가 영어식 발음인 emoji로 한글식 발음인 이모지로 변형되면서 이모지가 보편적으로 사용되었다고 한다

## Emoji 호환 Encoding in mysql

Emoji를 호환하기 위해서는 utf-8 인코딩이 글자당 4bytes까지 필요하다.  
하지만, mysql에서는 utf-8 인코딩이 3bytes까지만 지원하기 때문에 mysql에 Emoji를 저장하려면 다른 인코딩 방식을 사용해야한다.  
mysql에서 이모지를 지원하는 인코딩은 utf-8mb4이다. bm4는 multi-bytes4라는 의미이다.

---

### 출처

[MySQL utf8에서 utf8mb4로 마이그레이션 하기](https://www.letmecompile.com/mysql-utf8-utf8mb4-migration/)
