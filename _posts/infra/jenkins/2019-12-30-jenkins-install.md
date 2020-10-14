---
title: '[Jenkins] Install Jenkins on Docker'
date: 2019-12-30 10:32:00 -0400
categories: infra
tags: jenkins infra docker install
---

# 도커로 Jenkins 설치

## 준비

## 설치

```

docker run --restart=always -d -p 9090:8080 -p 50000:50000 -v /home/jenkins:/var/jenkins_home:z -v /var/run/docker.sock:/var/run/docker.sock --name jenkins -e TZ=Asia/Seoul -u root jenkins/jenkins:2.249.2-lts-jdk11


# 실행 확인
docker ps -a
```

-v /home/jenkins:/var/jenkins_home:z 의 경우는 일종의 백업 기능으로, 격리된 운영 공간인 컨테이너의 /var/jenkins_home의 젠킨스 운영 공간의 정보를 내 호스트 PC의 /jenkins로 공유하겠다는 의미

해당 설정으로 인해 jenkins 컨테이너를 누군가 갑자기 지우더라도 내 호스트 pc의 /home/jenkins 디렉토리 안에 운영되던 jenkins 데이터가 남아있게 됨

### 접속확인

ip주소:9090/

//그림1

### Admin Passowrd 등록

```
# jenkins 접속
docker exec -ti jenkins /bin/bash

cat /var/jenkins_home/secrets/initialAdminPassword
```

cat으로 나온 패스워드를 복사해서 입력

### Getting Started

//그림2

//그림3

//그림4

## 추가 설정

### 추천 플러그인

- Build Name and Description Setter <br/>: 빌드 이름 세팅 플러그인
- Parameterized Trigger <br/> : 트리거 시 파라미터값 전달 플러그인

### Host docker 소켓을 jenkins 컨테이너와 연동

```
# 기존 구동중인 Jenkins 컨테이너 중지 및 삭제
docker stop jenkins
docker rm jenkins

#host의 docker.sock과 container의 연동
docker run --restart=always -d -p 9090:8080 -p 50000:50000 -v /home/jenkins:/var/jenkins_home:z -v /var/run/docker.sock:/var/run/docker.sock --name jenkins -e TZ=Asia/Seoul -u root jenkins/jenkins:2.249.2-lts-jdk11

#jenkins 컨테이너에서 docker binary 설치
wget https://get.docker.com/builds/Linux/x86_64/docker-17.05.0-ce.tgz
tar xvfz docker-17.05.0-ce.tgz
cp ./docker/docker /usr/bin/
docker -v

exit

# 권한 설정 (Docker in Docker)
도커 컨테이너 내부에서 Jenkins는 jenkins 유저로 실행됩니다. 이제 jenkins 유저가 docker.sock에 접근할 수 있도록 퍼미션을 잡아줘야 합니다.

cat /etc/group | grep docker

docker exec -it jenkins /bin/bash

groupadd -g 999 docker
cat /etc/group | grep docker
usermod -aG docker jenkins

exit

docker restart jenkins
```

## Jenkins Time 설정

### TimeZone 확인방법

jenkins경로/systemInfo에서 user.timezone 확인

```
cd /var/lib/jenkins
JENKINS_JAVA_OPTIONS="-Dorg.apache.commons.jelly.tags.fmt.timeZone=Asia/Seoul" 입력
http://[jenkins-server]/restart
```

# 참고 문서

// docker in docker, docker out docker

https://aidanbae.github.io/code/docker/dinddood/
