---
layout: post
title: "[20220519] ESLint 에러(TypeError: this.cliEngine is not a constructor)"
date: 2022-05-19 23:20
last_modified_at: 2022-05-19 23:20
tags: [eslint]
toc: true
---

> WebStorm에서 ESLint를 설정하면서 발생한 에러를 해결하는 방법(간단함 주의)을 포스팅한다.

WebStorm 버전마다 ESLint를 지원하는 버전이 다르다고 한다.

[https://youtrack.jetbrains.com/issue/WEB-52236](https://youtrack.jetbrains.com/issue/WEB-52236)

내가 지금 사용하고 있는 WebStorm의 버전은 2021.1.3이고 사용하려 했던 ESLint 버전은 현재 가장 최근 버전인 major 8 이었다.

위 링크를 따라가보면 ESLint major 8버전은 WebStorm 버전 2021.2.2부터 가능하기 때문에 제목에 적혀있는 에러를 해결하기 위해서는 두 가지 방법이 있었다.

1. WebStorm 버전을 2021.2.2 이상으로 업그레이드
2. ESLint를 WebStorm이 지원하는 버전까지 다운그레이드

문제는 WebStorm이 회사에서 지원해주고 있기 때문에 WebStorm 버전을 내 맘대로 업그레이드 할 수 없었다. 그렇기 때문에 나 같은 경우에는 ESLint를 다운그레이드 함으로써 해결하였다.
