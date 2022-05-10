---
layout: post
title: "[20220510] Docker 로그인 여부 확인"
date: 2022-05-10 23:25
last_modified_at: 2022-05-10 23:25
tags: [docker]
toc: true
---

> DockerHub에 로그인 되어 있는지 확인하는 과정을 포스팅한다.

### docker info에 존재하지 않는 Username

"도커, 컨테이너 빌드업!" 이라는 책을 보고 공부하면서 터미널에서 DockerHub에 로그인 되어 있는지 확인하는 과정에서 도커 버전이 업그레이드 되면서 로그인 상태를 확인할 수 있는 방법이 바뀐 것으로 보인다.~~(책을 따라 했을 때 원하는 결과를 얻지 못했기 때문에...)~~  
[docker info docs](https://docs.docker.com/engine/reference/commandline/info/)를 살펴보면 Username 필드를 확인할 수 있는데, 내가 찾은 [stackoverflow](https://stackoverflow.com/questions/29326721/is-there-a-way-to-get-the-docker-hub-username-of-the-current-user)에서 docker info 에서 더이상 Username을 제공해주지 않는다고 한다.  
docs와 한 가지 다른점은 docs에서의 환경이 Redhat의 linux환경이라는 점이다. 혹시 linux에서만 Username이 보이는 것일까..  
여튼, MacOS에서는 책에서 제안한 명령어로는 로그인 여부를 알 수 없었다.  
```zsh
> docker info | grep Username
(empty)
```  

### 로그인 여부 확인 방법

그래서 알아낸 방법은 config.json에서 auths 속성을 확인하는 것이다.  
```zsh
> cat ~/.docker/config.json
// 로그인 상태
{
	"auths": {
		"https://index.docker.io/v1/": {}
	},
	"credsStore": "desktop"
}

// 로그아웃 상태
{
	"auths": {},
	"credsStore": "desktop"
}
```
로그인 상태라면 위의 경우처럼 auths에 값이 채워져 있다.  
docker 로그인은 docker login 명령어를 사용하면 된다.  
로그인이 성공적으로 되면 docker hub에 존재하는 이미지를 pull 하거나 로컨의 이미지를 push 할 수 있게 된다.  

### (추가) 로그인 방법
1. ID와 PWD
2. [PAT(Personal Access Token)](https://docs.docker.com/docker-hub/access-tokens/) - 권장
로그인하는 과정에서 PWD나 PAT가 노출되는 상황이 발생할 수 있다. 이 때, 상대적으로 PAT를 사용함으로써 위험성을 낮출 수 있다.  
또한, PAT마다 권한을 달리 부여하여 여러 사용자에게 제한된 권한을 부여할 수도 있다.
