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

** 접속 시 만약, 유지보수중이라는 창이뜬다면
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


sonar.log-기본 프로세스에 대한 로그입니다. 시작 및 종료에 대한 일반 정보를 보유합니다. 여기에는 전반적인 상태가 표시되지만 세부 정보는 표시되지 않습니다. 다른 로그를 살펴보십시오.
web.log-데이터베이스에 대한 초기 연결, 데이터베이스 마이그레이션 및 재 인덱싱 및 HTTP 요청 처리에 대한 정보 여기에는 해당 요청과 관련된 데이터베이스 및 검색 엔진 로그가 포함됩니다.
ce.log-백그라운드 작업 처리 및 해당 작업과 관련된 데이터베이스 및 검색 엔진 로그에 대한 정보
es.log-Elasticsearch 시작, 상태 변경, 클러스터, 노드 및 인덱스 수준 작업 등과 같은 검색 엔진의 운영 정보

//그림

위와 같은 순서로 진행하면 login-token이 생성됩니다.
그리고 login-token을 maven, gradle에 설정을 하면 ID, Password 필요없이 SonarQube에 소스코드를 올릴 수 있습니다.
SVN, Git 같은 형상관리에 ID, Password 가 commit 되는 상황을 방지할 수 있습니다.

property "sonar.login", "cc7876988f5e0fwejd69875b360b42ed34db4215"

# 참고 문서
