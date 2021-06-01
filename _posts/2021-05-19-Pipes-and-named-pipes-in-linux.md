---
layout: post
title: "[20210519] Pipes and named pipes in linux"
date: 2021-05-19 21:38
last_modified_at: 2021-05-19 21:38
tags: [linux]
toc: true
---

### Pipes or unnamed pipe

리눅스에서 pipe라는 명령어는 한 명령어의 출력을 다른 명령어에게 보낼 수 있도록 한다. piping는 말그대로 하나의 프로세스의 표준 출력, 입력, 에러를 다른 프로세스에 다시 보낼 수 있게 한다.  
pipe혹은 unnamed pipe의 문법은 명령어 사이에 | 를 사용하는 것이다.

    Command-1 | Command-2 | ... | Command-N

pipe는 다른 세션 간에는 접근 할 수 없다. pipe의 왼쪽 명령어가 실행 되는 동안 생성된 출력 값은 잠시 동안 저장되다가 표준 출력(오른쪽 명령어의 입력)으로 내보내진다. 그 후 생성된 출력 값은 삭제된다.

### Named pipe

잠시동안 데이터가 유지되는 unnamed pipe와는 다르게 named pipe는 시스템이 살아있고 지워질 때까지 유지된다. FIFO 방식을 따르는 특별한 파일이지만 평범한 파일 처럼 사용할 수도 있다.
named pipe를 만들기 위한 명령어는

    mkfifo <pipe-name>

혹은,

    mknod p <pipe-name>

어떤 명령어의 표준 출력을 다른 프로세스에 내보내기 위해서는 > symbol을 사용한다.

    ls -al > contents.txt

혹은 어떤 명령어의 표준 입력으로 보내기 위해서는 < symbol을 사용한다.

    tail -n 2 < contents.txt

---

### 출처

[An introduction to pipes and named pipes in Linux](https://opensource.com/article/18/8/introduction-pipes-linux#:~:text=In%20Linux%2C%20the%20pipe%20command,to%20another%20for%20further%20processing.)
