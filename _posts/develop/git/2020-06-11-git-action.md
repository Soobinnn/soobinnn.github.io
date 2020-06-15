---
title: '[Git Lab] Git Action'
date: 2020-06-05 19:54:00 -0400
categories: devlog
tags: git devlog git action
---

# Git Aciton

Github 저장소를 기반으로 소프트웨어 개발 Workflow를 자동화 할 수 있는 도구이다. 간단하게 말하자면 Github에서 직접 제공하는 CI/CD 도구

## 비용
Workflow는 저장소마다 최대 20개

Workflow 안에 존재하는 Job이라는 단위마다 최대 6시간 동안 실행될 수 있고, 초과하게 되면 자동으로 중지

Github 계정 플랜에 따라 전체 Git 저장소를 통틀어 동시 실행할 수 있는 Job 개수가 정해져 있다.

Job 안에서 Github API를 호출한다면 1시간 동안 최대 1,000번까지만 가능

공개 저장소는 무료

비공개 저장소를 기준으로 한달에 500MB 스토리지와 실행 시간 2,000분(minute)까지 제공된다.

## 개념

#### Workflow

프로젝트를 빌드, 테스트, 패키지, 릴리즈/배포하기 위한 전체적인 프로세스

Workflow는 여러 개의 `Job`으로 구성되며 `event`에 의해 실행됨.

GitHub에게 workflow file을 전달하면 Github Actions가 실행함.

#### Job

하나의 인스턴스에서 여러 Step으로 그룹시켜 실행하는 역할

#### Step

순차적으로 명령어를 수행
`Uses`는 이미 다른 사람들이 정의한 명령어를 가져와 실행

`Run`은 가상환경 내에서 실행할 수 있는 스크립트

#### Event

Workflow를 실행시키는 조건을 설정


# 참고자료
https://velog.io/@adam2/Github-Action-%EC%A3%BC%EC%9A%94-%EB%AC%B8%EB%B2%95