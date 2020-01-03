---
title: '[SonaQube Install SonaQube ?'
date: 2020-01-02 22:13:00 -0400
categories: infra
tags: sonaQube infra install
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

# 참고 문서
