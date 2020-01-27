---
title: '[postgresql] What is PostgreSQL'
date: 2020-01-26 10:03:00 -0400
categories: database
tags: postgresql database pg
---

## Linux 명령어
```
# postgresql docker 접속
docker exec -it <postgresql명> bash

# postgres 접속
psql -U <계정명>

password

db

CREATE USER (사용자아이디) WITH SUPERUSER CREATEDB LOGIN ENCRYPTED PASSWORD '(사용자 암호)';

# Timezone 한국시간
set timezone='ROK';

# DB 목록
\l

# 접속 종료
\q

# DB 생성
CREATE DATABASE sentry WITH ENCODING='UTF8' OWNER=postgres;
```