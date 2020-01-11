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

### run
컨테이너 생성과 함께 컨테이너 시작
```
docker run <옵션> <이미지 이름><실행할 파일>

# 옵션

-i : (interactive)
-t : (Pseudo-tty)
--name : 컨테이너의 이름을 지정 (default 자동지정)
-d : 컨테이너를 백그라운드로 실행시키는 옵션
-p : 호스트 포트와 컨테이너 포트를 연결한다. (여러개 가능)
```

### login

Docker Registry에 로그인하는 명령어

```
docker login <옵션> <Docker Registry URL>

# 옵션
-e : (--email="") 로그인할 때 사용할 이메일 설정
-p : (--password="") 로그인할 때 사용할 비밀번호를 설정
-u : (--username="") 로그인할 때 사용할 Docker Registry 계정을 설정

# 로그인 확인방법
// 로그인이 되어있다면 Username 출력, 로그인 안되어 있으면 아무것도 출력되지 않음.
docker info | grep Username
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

### push
Docker Hub / Registry에 이미지를 올리는 명령어.

Docker Hub에 이미지를 올리려면 이미지 이름을 <Docker Hub 사용자 계정>/<이미지 이름>:<태그> 형식으로 생성해야 합니다. 

아무 사용자 이름이나 사용할 수 있지만 내 계정 이름과 일치해야 이미지를 올릴 수 있습니다. 태그를 지정하지 않으면 latest가 됩니다.

```
docker push <이미지 이름>

# 예제
docker push webatoz/jenkins
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
