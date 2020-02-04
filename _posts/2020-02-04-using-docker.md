---
layout: post
title: "Etc-Docker를 조금 더 깔끔하게.."
description: ""
category:
tags: [etc, docker]
---


## Docker 사용 이력
Docker는 딥러닝하고 거의 비슷한 시기쯤 접했으니까...

2013년 정도 되나보다.

기존에 VM 쓰다가 집어던지기를 몇번하다가 docker를 접하면서 

`오오!!!`

하면서 썼다. 초기에는 여러 리눅스 version 테스트 때문에 시작을 했고,

Theano 설정하는거 머리 터지면서부터는 GPU 설정을 목적으로 사용하기 시작했다.

지금은 다양한 과제에서 대부분 사용하고 있고, 

CI까지 연동하면서 활용하고 있다.


## 지난 기업 미팅에서 Docker 추가 활용 방안 고민
지난번에 딥러닝 관련 회의를 기업과 하다가 docker를 꼭 이야기 한 것은 아니지만, 

학습을 클러스터에 좌라락 뿌려서 사용하는 이야기가 나왔다. 

딱 이것을 위한 도구는 잘 보이지 않는데, 

그래도 기반은 container를 가지고 가야하니까, 

결국은 다시 docker를 조금 더 살펴보게 되었다.

docker compose, docker swarm, kubernetes 등등

참으로 많았다. 그 이상으로도 쓸만한게 많고 말이다.


## Docker 조금 더 잘쓰기
docker도 계속 업그레이드 되면서 다양한 기능이 제공되고 있다. 

GPU도 임의할당 가능하고, 연계된 컨테이너를 하나의 스크립트로 뿌리는 것도 가능해지고 말이다.

다른 것보다, 다양한 도구보다 이번에 살펴보면서 느낀 점은, 

docker를 아주 깔끔하게 관리하고 사용하는 사람이 많이 있다는 것이다. 

이것만 잘 따라해도 보다 정리된 연구가 가능할 것 같았다.

dockerfile도 잘 관리하고.

개인 registry도 구성하고 활용하고,

github 내에 dockerfile을 연동하게끔 dockerfile을 구성하고.. 

등등..

생각보다 한번 잡아놓으면 쓸만한 것이 너무 많았다.

역시 능력자는 너무 많다.



## TODO

[ ] 개인 set-up을 포함하는 dockerfile 만들기
  [ ] ssh 설정
  [ ] 계정 추가
  [ ] vi 기본 설정 추가
  [ ] 기본 프로그램 추가
  [ ] requirements 파일 관리
[ ] github 내 관련 dockerfile 추가
  [ ] requirements 파일 관리
[ ] 추가 docker 도구 검색