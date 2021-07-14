---
layout: post
title: "[20210606] 추적하고 있는 파일/폴더 더이상 추적하지 않게 in git"
date: 2021-06-06 23:47
last_modified_at: 2021-06-06 23:47
tags: [git]
toc: true
---

> 추적 중인 파일이나 폴더를 더이상 추적하지 않게 하는 방법에 대한 내용을 다룬다.

git을 사용하면서 추적하고 싶지 않은 파일이나 폴더는 .gitignore이라는 파일에 해당 파일이나 폴더의 경로를 추가하면 된다.  
하지만, .gitignore 파일이 추가되기 전부터 이미 git에서 추적중인 파일이나 폴더는 .gitignore파일에서 설정하더라도 추적을 계속 하게 된다.  
이 경우에, rm 명령어를 사용하면 된다.

    git rm --cached [filename]
            or
    git rm -r --cached [foldername]

이후, 커밋을 하게되면 다음부터는 더이상 추적하지 않게된다.