---
title: '[Docker] Command'
date: 2019-12-30 10:37:00 -0400
categories: infra
tags: docker infra command
---

# Docker 명령어

### exec

```
docker exec -ti

# 옵션
-i : (interactive mode) , /bin/bash 프로세스와 입력&출력 가능
-t : (Pseudo-tty), root@151c498ae0f0 형식의 프롬프트 제공
```

### build

```
# Dockerfile Build
docker build -t <이미지명> <Dockerfile가 있는 경로>

# 옵션
-t : (--tag) 저장소 이름/이미지이름:태그 설정
--rm=true : 이미지 생성에 성공했을 때 임시 컨테이너를 삭제함.
-q : (--quiet=false) : Dockerfile의 RUN이 실행한 출력 결과를 표시하지 않는다.
--no-cache=false: 이전 빌드에서 생성된 캐시를 사용하지 않는다. Docker는 이미지 생성 시간을 줄이기 위해서 Dockerfile의 각 과정을 캐시하는데, 이 캐시를 사용하지 않고 다시만듬.
--force-rm=false : 이미지 생성에 실패했을 때도 임시 컨테이너를 삭제함.

# 예제
docker build -t hello .
docker build -t hello /opt/hello

cat Dockerfile | sudo docker build -t hello -
echo -e "FROM ubuntu:14.04\nRUN yum update" | sudo docker build -t hello -
sudo docker build -t hello - < Dockerfile
```

### commit

컨테이너에서 작업을 한 후 그 컨테이너를 다시 이미지로 생성하는 명령어

```
docker commit [options] <container name> [image name[:tag name]]

# 옵션
-a : (--author="") 생성자 정보
-m : (--message="") 이미지 메시지
-p : (--pause=true/false) 이미지를 생성할 때 컨테이너를 중지한 뒤 커밋 여부

# 예제
docker commit -a "sbim" -m "update" jenkins jenkins:1.0
```

# 현재 postgres와 superset 컨테이너를 각각 만들어 놓은 상태이다.

```
docker network create dataviz # network 생성
docker network connect dataviz postgres # postgresql 컨테이너를 네트워크에 연결
docker network connect dataviz superset # superset 컨테이너를 네트워크에 연결
docker network inspect dataviz # network 정보 확인
```

```
docker network ls
```
