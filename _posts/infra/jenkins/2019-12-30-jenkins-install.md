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

docker run -d -p 9090:8080 -v /jenkins:/home/jenkins --name jenkins -u root jenkins

# 실행 확인
docker ps -a
```

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
