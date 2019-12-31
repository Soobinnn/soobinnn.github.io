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
docker pull jenkins

docker run --restart=always -d -p 9090:8080 -p 50000:50000 -v /home/jenkins:/var/jenkins_home:z --name jenkins -u root jenkins

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
