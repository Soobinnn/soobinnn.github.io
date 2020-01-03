---
title: '[Docker] DockerFile/Docker-Compose '
date: 2019-12-30 10:37:00 -0400
categories: infra
tags: docker infra command
---

# docker-compose 설치

```
curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose

# chmod +x /usr/bin/docker-compose
# ls -l /usr/bin/docker-compose
# docker-compose --version
```
