---
layout: post
title: "[20220407] Getting started Docker"
date: 2022-04-07 21:33
last_modified_at: 2022-04-07 21:33
tags: [Docker]
toc: true
---

Docker [Getting Started](http://localhost/tutorial/what-next/)를 전부 살펴보았다.  
우선, Docker의 Getting Started는 신박했다.  
처음에 Getting Started를 보고 싶은데 자꾸 다른 것부터 따라하라고 하길래 일단 따라했었다.  
그게 알고보니 Getting Started의 image를 다운받고 container를 생성해서 Getting Started를 제공하는 서버를 실행하는 것이었다.  
그렇기 때문에 아마도 위에서 제공한 링크를 따라가면 Not Found를 발견할 수 있다.(실행 된다면 Getting Started 서버를 실행중인 container가 있다는 뜻...)  
필자도 처음부터 알아 차렸던 것은 아니고 Getting Started를 따라하다보니 많이 생긴 container를 정리하면서 Getting Started 사이트에 갑자기 접근할 수 없게 되었다.  
그러다가 사이트 주소가 localhost였고..? 내가 지운 container 중에 하나가 Getting Started image를 실행 중인 container였다.  
여하튼, 앞으로 Docker에 관한 개념이나 활용한 내용들을 정리해볼 생각이다.

Getting Started에서 배운 내용을 간단히 정리해보자면,  
독립된 실행 환경을 제공하는 container,  
각 container마다 실행되는 image,  
container는 독립된 환경에 있지만 container끼리 공유할 수 있는 file system 공간인 named volume, bind mounts,  
여러 container를 하나의 네트워크 공간에 두어 통신할 수 있도록 제공하는 network,  
보통 container에는 하나의 layer(하나의 image)를 기반으로 동작하며 하나의 application을 구성하기 위해 여러 layer(image)가 연관되어 동작한다.  
그렇기에 하나의 application을 구성하기 위해서 해야하는 일련의 동작들이 있는데, 이를 한 번에 실행할 수 있도록 하는 compose,  
아직 배우지는 않았지만, Container Orchestration 혹은 k8s 등을 공부하고 정리해보려 한다.
