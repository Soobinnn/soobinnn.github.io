---
title: '[Docker] Install Docker ?'
date: 2019-12-30 10:37:00 -0400
categories: infra
tags: docker infra command
---

docker exec -ti

-i : (interactive mode) , /bin/bash 프로세스와 입력&출력 가능

-t : (Pseudo-tty), root@151c498ae0f0 형식의 프롬프트 제공

# 현재 postgres와 superset 컨테이너를 각각 만들어 놓은 상태이다.

```
docker network create dataviz # network 생성
docker network connect dataviz postgres # postgresql 컨테이너를 네트워크에 연결
docker network connect dataviz superset # superset 컨테이너를 네트워크에 연결
docker network inspect dataviz # network 정보 확인
```
