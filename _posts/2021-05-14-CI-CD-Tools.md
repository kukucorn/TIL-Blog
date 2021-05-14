---
layout: post
title: "[20210514] CI & CD"
date: 2021-05-14 21:55
last_modified_at: 2021-05-14 21:55
tags: [CI, CD]
toc: true
---

> CI 와 CD를 설명하며, 관련된 Tool들을 소개한다.

## CI(Continuous Integration)

하나의 프로젝트에 여러 개발자들이 투입되어 개발을 하면 각자 개발자들이 개발한 소스코드들을 한 군데 모아서 합치는 과정이 필요한데 이를 통합이라고 한다. CI를 직역해보면 계속된 통합이다. 말 그대로 하루에도 수십번 통합하는 행위를 뜻한다.

## CD(Continuous Deployment)

CD도 말 그대로 계속된 배포이다. 자세히 말하자면 소프트웨어 배포 과정인데 자동화된 테스트로 바뀐 코드들의 유효성과 안전성을 판단한다.

## Tools

CI와 CD를 개발자가 직접 하려면 매번 반복되는 일이기에 번거러우면서도 실수하기 쉬운 부분들이 많다. 그래서 이를 자동으로 처리해주는 Tool들이 존재한다.  
그 중에서 현재 프로젝트에서 사용 중인 Travis CI에 대해 소개하려 한다.

## Travis CI

Travis는 Github과 Bitbucket에 저장된 소스코드를 CI해주는 기능을 가진 도구이다. 그래서 필자의 경우에는 Github을 사용하였고, 소스코드를 추가하거나 변경하고 Github repository에 push하거나 pull request가 제출되면 Travis에서는 이를 감지하고 자동으로 배포 파일을 만들어준다.(필자의 경우에는 java 이므로 jar 파일이 만들어짐) 감지하는 branch는 여러개를 지정할 수도 있다.  
배포가 완료되면 기재해놓은 이메일로 통합 결과를 알려주기도 한다.  
설정 파일은 .travis.yml 으로 이름 지어야 하며, repository의 root directory에 위치해야 하며, 빌드와 테스트 환경을 위해 사용된 프로그래밍 언어를 명시해야한다.

---

### 출처

[Continuous Integration](https://en.wikipedia.org/wiki/Continuous_integration)  
[Continuous Deployment](<https://www.atlassian.com/continuous-delivery/continuous-deployment#:~:text=Continuous%20Deployment%20(CD)%20is%20a,cycle%20has%20evolved%20over%20time.>)  
[Travis CI](https://en.wikipedia.org/wiki/Travis_CI)
