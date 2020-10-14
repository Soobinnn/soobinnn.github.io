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
#### Centos 7
// sudo yum install docker 는 이전 버전이므로 하지 않음.
yum install -y yum-utils device-mapper-persistent-data lvm2

yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

yum install -y docker-ce

#Docker 서비스 실행
systemctl start docker

#부팅시 자동 실행 설정
sudo chkconfig docker on
```

/\* Centos에서 **install docker** 가 아닌 **install docker-ce** "최신버전"으로 설치해야하는 이유 -> docker in docker, docker out of docker 사용 시 보안 이슈

[docker공식문서](https://docs.docker.com/install/linux/docker-ce/centos/)

## Window

## Docker 삭제

docker container 를 모두 중지하고 삭제

```
docker stop $(docker ps -q)

docker rm $(docker ps -a -q)
```

docker service, containerd service 를 중지

```
systemctl stop docker.service
systemctl stop containerd.service
```

docker package(여기에서는 docker-ce package)를 삭제

```
yum list installed | grep docker

yum erase ~~~
```

/var/lib/docker 아래의 모든 파일, 디렉토리를 삭제

```
cd /var/lib/docker

rm -rf *
```

/var/run 아래에서 docker.sock, docker.pid 파일과 docker 디렉토리를 삭제

```
cd /var/run
rm docker.sock docker.pid

rm -rf docker
```

# 참고 문서

https://docs.docker.com/install/linux/docker-ce/centos/

http://cloudrain21.com/remove-docker-forcely-and-reinstall
