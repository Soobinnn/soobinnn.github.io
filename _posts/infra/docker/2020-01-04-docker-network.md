---
title: '[Docker] Docker Network '
date: 2020-01-04 18:51:00 -0400
categories: infra
tags: docker infra network
---

# Docker Network

도커는 기본으로 세 개의 네트워크를 제공한다.

1. bridge network
2. host network
3. none network

### Bridge Network

컨테이너 간 연결을 제공하며 컨테이너를 구동하는 호스트 네트워크가 구분 된다.

### Host Network

컨테이너를 위한 별도 네트워크 없이 호스트와 동일한 네트워크를 사용한다.

### None Network

네트워크 연결을 갖지 않는다.

## Network Scope

네트워크의 범위.

1. local
2. global
3. swarm

### local

컨테이너 간 연결은 네트워크가 존재하는 호스트로 제한됨.

### global

클러스터의 모든 노드에 네트워크가 존재하지만 호스트 간 라우팅은 지원하지 않는다.

### swarm

도커 스웜에 참여하는 모든 호스트로 연결을 확장한다.

# 예제

## 컨테이너 간 연결 : Bridge Network

```
docker run --rm --name dbadmin --link mysqldb:db -p 8080:8080 adminer
```

--link 옵션이 중요하다. --link containe_name:identify --link 명령어의 첫번째 파라미터는 컨에티너의 이름이며, 그 다음은 컨테이너 내부에서 사용할 식별다.

즉 dbadmin 컨테이너 내부에서 db라는 이름으로 mysqldb컨테이너에 접근할 수 있다는 것을 의미한다.

```

### 직접 생성해서 연결
```

docker network create \
--driver bridge \
--attachable \
--scope local \
--subnet 10.0.7.0/24 \
--ip-range 10.0.7.0/24 \
mynet

```
mynet라는 이름으로 driver는 bridge 로,

--attachable 옵션은 컨테이너가 언제든지 네트워크에 연결하거나 떨어질 수 있게 설정한다.

--subnet과 --ip-range는 서브넷과 할당 가능한 IP 범위를 지정한다.

네트워크를 생성했다면 컨테이너를 네트워크에 붙일 수 있다. 컨테이너를 실행할 때 --network 옵션을 사용하면 된다.
```

docker run --name mysqldb \
--network mynet \
-e MYSQL_ROOT_PASSWORD=rootpw \
-d mysql:5.7

```

# 관련 명령어
```

docker network ls

```

```
