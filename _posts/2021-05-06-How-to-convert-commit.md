---
layout: post
title: "[20210506] 잘못 보낸 커밋(reset, revert)"
date: 2021-05-06 01:36
last_modified_at: 2021-12-21 00:39
tags: [git]
toc: true
---

잘못 보낸 커밋을 되돌리는 방법에는 reset과 revert가 있다.

## reset

reset은 현재 HEAD와 HEAD가 가리키고 있는 Branch의 위치를 되돌리고 싶은 커밋의 위치로 이동 시키는 명령어.  
되돌아간 커밋 이후에 생성되었던 커밋 메시지들은 모두 삭제됨(완전히 삭제된다기 보다는 참조가 사라져서 log에서 사라진다고 보는게 맞을듯).

    git reset <option> <commit hash or commit ref>

옵션에 따라 Staging Area와 Working Directory의 상태가 변경됨.

### option

- --hard : Staging Area와 Working Directory의 상태가 지정한 커밋과 같아진다. 즉, HEAD의 상태가 사라짐.
- --mixed : Staging Area 만 지정한 커밋과 같아진다.
- --soft : reset 전 HEAD의 Staging Area와 Working Directory가 유지된다.

### commit

- 해시는 커밋 해시의 일부만 지정해도 유일함이 보장되면 가능
- 참조는 ~ 혹은 ^ 로 HEAD를 기준으로 상대 참조가 가능

## revert

revert는 특정커밋의 내용을 삭제하는 것에 대한 커밋을 만든다.  
특정커밋을 이력에서 삭제하는 reset과는 달리 revert는 삭제한 커밋이 이력에 남아있다.

    git revert <commit hash>

reset은 이력을 단순하게 만들어 주지만 삭제하는 이력의 존재를 다른사람이 알 수 없다.  
그렇기에 다른사람과 협업하는 경우라면 revert로 삭제 이력을 남겨서 다른사람이 커밋의 삭제 여부를 알 수 있도록 해야한다.
