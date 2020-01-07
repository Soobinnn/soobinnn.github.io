---
title: '[Jenkins] Git 연동'
date: 2019-12-30 10:30:00 -0400
categories: infra
tags: jenkins infra whatis
---

# GitHub 연동

## GitHub

### Access Token 발급

로그인 -> Setting -> Developer settings -> Personal access tokens

생성 -> Note 입력 -> repo, admin:repo_hook 체크

## Jenkins

### Configure

Jenkins -> Jenkins 관리 -> 시스템 설정 -> GitHub -> GitHub Servers

Name 입력 - Credentials -> Add -> Secret text 선택 -> secret입력 ID gitID입력

Credentials 선택 후 Test Connection

Test connection Credentials verified for user ID, rate limit: 4983 가 나오면 인증됨.

Manage hooks 체크 -> Apply -> Save

### Item

#### 소스 코드 관리

소스 코드 관리 - Git - Repo URL 입력 - Credentials ID/PW 입력

## Git Push 트리거 설정 방법

코드가 푸쉬되면 빌드 트리거링 하도록 설정

### Jenkins

```
jenkins 와 github.com - webhook 을 연동하기 위해서는 GitHub Integration Plugin 플러그인이 설치되있어야한다.
```

Jenkins Item -> Build Trigger -> GitHub hook trigger for GITScm polling 선택

### GitHub

GitHub에서 코드가 푸쉬 될 때마다 WebHook을 jenkins에 보내도록 설정해야함.

프로젝트 - Settings - Webhooks -> Add webhook -> url : http:/{jenkins url}/github-webhook/

- 연결이 잘됬는지 왼쪽 아이콘이 보임. Jenkins에서는 GitHub Hook Log가 생김

# GitLab
