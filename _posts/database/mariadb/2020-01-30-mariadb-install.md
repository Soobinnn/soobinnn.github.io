---
title: '[MariaDB] Install'
date: 2020-01-30 21:41:28 -0400
categories: database
tags: mariadb database
---

본 환경은 Centos7에서 설치
# install on docker
```
mkdir /home/mariadb

docker pull mariadb

docker run -d -p 3306:3306 -v /home/mariadb:/var/lib/mysql \
--name mariadb \
-e MYSQL_ROOT_PASSWORD=패스워드
--restart=always mariadb

docker exec -ti mariadb bash

mysql -u root -p

//패스워드 입력



```