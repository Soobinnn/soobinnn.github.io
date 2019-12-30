---
title: '[Docker] Install Docker ?'
date: 2019-12-30 10:37:00 -0400
categories: infra
tags: docker infra install
---

# 설치

## Linux

\*\* RedHat 8은 docker 지원이 안됨.

### 공통 스크립트

```
sudo wget -qO- http://get.docker.com/ | sh
```

### Ubuntu

```
sudo apt-get update
sudo apt-get install docker.io
sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker
```

### CentOS (RedHat, Fedora)

```
#Install
sudo yum install docker

#Docker 서비스 실행
sudo service docker start

#부팅시 자동 실행 설정
sudo chkconfig docker on
```

## Window
