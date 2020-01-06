---
title: '[SonaQube] Sonarqube 자동화'
date: 2020-01-06 10:31:00 -0400
categories: infra
tags: sonaQube infra jenkins auto devops
---

# Sonarqube Jenkins 연동

Sonarqube를 Jenkins와 연동 하여 정적분석 자동화 / 리포트 자동화에 대한 문서이다.

# 준비

## Sonarqube

admin 로그인 -> 설정 -> security -> Generate Token -> **발급된 토큰 복사**

Projects -> Create new project -> Projectkey 생성한 토큰 붙여넣기 -> Display Name 작성

Provider a token 생성

## Jenkins

### 플러그인 설치

Jenkins 관리 -> 플러그인 관리 -> Sonarqube Scanner 설치

### Sonarqube Scanner 플러그인 설정

#### 환경설정

Jenkins 관리 -> 시스템 설정 -> SonarQube Servers

Environment variables 체크 SonarQube installations name : 원하는 명 작성 ServerURL : 소나서버 URL 작성

#### Global Tool Config

Jenkins 관리 -> Global Tool Configuration -> SonarQube Scanner

\*만약 SonarQube Scanner가 안보일 경우, 아래 확인 후 진행 Jenkins 관리 > 플러그인 관리 > 고급 탭 > 맨 아래 “지금 확인” 버튼 클릭

SonarQube Scanner -> "SonarQube Scanner installations..." 클릭 -> Name 입력 -> Install automatically 체크 -> install from Maven Central Version 선택

### Jenkins Item 설정

#### Build

Execute SonarQube Scanner

**Analysis properties**

```
sonar.host.url = 자신의 sonar url
sonar.login = loginkey값입력
sonar.projectKey= projectKey값입력
sonar.projectName= projectName입력
sonar.projectVersion= 1.0

# path to source directiories (required)
sonar.sources=src
sonar.tests=
sonar.sourceEncoding=UTF-8
sonar.exclusions=src/public/**/*
```

\* 보다 자세한 Analysis Properties 파라미터 정보

[A nalysis Param](https://docs.sonarqube.org/latest/analysis/analysis-parameters/)

[Source Param](https://docs.sonarqube.org/latest/project-administration/narrowing-the-focus/)

# 참고 자료

[공식문서](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-jenkins/)

https://brunch.co.kr/@joypinkgom/45

https://taetaetae.github.io/2018/02/08/jenkins-sonar-github-integration/

https://okky.kr/article/439198

https://daddyprogrammer.org/post/817/sonarqube-analysis-intergrated-intellij/
