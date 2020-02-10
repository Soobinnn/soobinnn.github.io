---
title: '[Docker] DockerFile/Docker-Compose '
date: 2019-12-30 10:37:00 -0400
categories: infra
tags: docker infra command
---

# Docker File

```
vi Dockerfile

FROM

ENV SPRING_HOME /



```

## Info

### FROM

어떤 이미지를 기반으로 할지 설정함. Docker 이미지는 기존에 만들어진 이미지를 기반으로 생성함. <이미지 이름>:<태그> 형식으로 설정

### ENV

해당 이미지의 환경변수를 지정해주는 옵션

### MAINTAINER

메인테이너 정보

### RUN

셀 스크립트 혹은 명령

실행베이스 이미지에 있는 /bin/sh 실행 파일을 사용하여 명령어를 실행한다.

### VOLUME

호스트와 공유할 디렉토리 목록

host어디에 저장될 것인지는 설정 불가능 host의 특정 디렉터리와 연결하려면

```
docker run -v {host directory}}:{container directory} dockerfile
```

### ENTRYPOINT

컨테이너가 시작되었을 때 첫번 째로 실행되는 명령어 (CMD와 동일)

```
exec 형식 : ENTRYPOINT ["executable", "param1", "param2", ...]
shell 형식 : ENTRYPOINT {command} {param1} {param2} ...

shell 형식은 /bin/sh 를 거친 후에 실행된다.
반면에 exec 형식은 script를 바로 실행하기 때문에 exec 형식을 추천한다.

# example
#  yum install -y rdate

ENTYPOINT ["yum","install","-y","rdate"]
```

### COPY / ADD

호스트 내부에 있는 파일을 이미지 내부로 복사. Dockerfile 파일이 존재하는 경로에서 하위에 있는 파일만 복사 가능. 따라서 Dockerfile을 작성할 때 별도의 폴더를 생성하고, 그 안에 이미지 생성에 필요한 파일들을 넣어둔다.

- ADD 압축 파일은 압축을 해제하여 복사한다.(Auto-extraction) URL을 통해 파일을 복사할 수 있다. (Remote-URL) ADD 보다 COPY가 직관성이 높다.

### USER

컨테이너 내에서 명령어를 실행시키는 사용자를 설정한다.

### CMD

컨테이너가 시작되었을 때 실행할 실행 파일 또는 셸 스크립트

### WORKDIR

CMD에서 설정한 파일이 실행될 디렉터리명령어 RUN, CMD, ENTRYPOINT, COPY 등이 실행될 Directory를 지정

### EXPOSE

호스트와 연결할 포트 번호

# docker-compose 설치

```
curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose

# chmod +x /usr/bin/docker-compose
# ls -l /usr/bin/docker-compose
# docker-compose --version
```
