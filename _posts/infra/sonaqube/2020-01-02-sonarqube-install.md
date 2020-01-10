---
title: '[SonaQube] Install SonaQube'
date: 2020-01-02 22:13:00 -0400
categories: infra
tags: sonaqube infra install
---

# 준비사항

```
sysctl -w vm.max_map_count=262144
sysctl -w fs.file-max=65536
ulimit -n 65536
ulimit -u 4096
```

SonarQube7.9 설치 시 제약 조건 : https://docs.sonarqube.org/7.9/requirements/requirements/

\*\* 만약 사양이 안되면, sonarqube:7.5-community 버전으로

# 설치

## Install SonaQube on Docker

```
docker pull sonarqube

docker run --restart=always -d --name sonarqube -p 9000:9000 -p 9092:9092 -u root  sonarqube:7.5-community

# 9000 포트는 sonarqube , 9092 는 sonarqube 내부 h2 db
# sonarqube는 postgresSQL을 권장함

$ docker run -d --name sonarqube \
    -p 9000:9000 -p 9092:9092 \
    -e SONARQUBE_JDBC_USERNAME=sonar \
    -e SONARQUBE_JDBC_PASSWORD=sonar \
    -e SONARQUBE_JDBC_URL=jdbc:mysql://192.168.0.32:3306/sonar \
    sonarqube

# 접속 확인
# http://<본인의  ip>:9000/sonar
# 초기 ID/PW : admin / admin
```

\*\* 접속 시 만약, 유지보수중이라는 창이뜬다면

```
# sonarqube 로그를 확인한다.
docker logs sonarqube

# 로그내용 중 database를 upgrade를 해야된다라는 명령어가 뜬다면 아래와 같이 해결하면 된다.

# 로그 내용
...
2020.01.04 11:21:09 WARN  web[][o.s.s.p.DatabaseServerCompatibility] The database must be manually upgraded. Please
 backup the database and browse /setup. For more information: https://docs.sonarqube.org/latest/setup/upgrading
2020.01.04 11:21:09 WARN  app[][startup]
################################################################################
      The database must be manually upgraded. Please backup the database and browse /setup. For more information: h
ttps://docs.sonarqube.org/latest/setup/upgrading
################################################################################
...

# 해결방법
http://ip:9000/setup 접속하여 Database 업데이트를 하면 작동된다.

```

//그림위와 같이 뜨는 것을 확인 할 수 있다.

## SonarQube Setting

### 1. 로그인

Admin / Admin 접속

### 2. 플러그인 다운로드

Administration -> Marketplace -> 원하는 언어별 플러그인 설치

## Install Sonarqube Scanner

[Download Link](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)

# 참고 문서
