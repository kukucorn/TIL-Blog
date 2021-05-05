---
layout: post
title: "[20210506] 잘못 보낸 커밋(reset, revert)"
date: 2021-05-06 01:36 +0900
last_modified_at: 2021-05-06 01:36 +0900
tags: [git]
toc: true
---

잘못 보낸 커밋을 되돌리는 방법에는 reset과 revert가 있다.

reset은 나의 위치를 되돌리고 싶은 커밋의 위치로 초기화 시키는 것이다.

    git reset <option> <commit hash>

옵션에는 3가지가 있다.

1. hard : 최근의 커밋을 완전히 버리고 이전의 상태로 되돌리고 싶을 때
2. mixed : 변경한 인덱스의 상태를 원래대로 되돌리고 싶을 때
3. soft : 커밋만 되돌리고 싶을 때

revert는 특정커밋의 내용을 삭제하는 것에 대한 커밋을 만든다.  
특정커밋을 이력에서 삭제하는 reset과는 달리 revert는 삭제한 커밋이 이력에 남아있다.

    git revert <commit hash>

reset은 이력을 단순하게 만들어 주지만 삭제하는 이력의 존재를 다른사람이 알 수 없다.  
그렇기에 다른사람과 협업하는 경우라면 revert로 삭제 이력을 남겨서 다른사람이 커밋의 삭제 여부를 알 수 있도록 해야한다.
