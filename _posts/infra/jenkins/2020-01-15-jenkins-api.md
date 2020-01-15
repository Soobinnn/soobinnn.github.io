---
title: '[Jenkins] Jenkins API'
date: 2020-01-15 09:01:00 -0400
categories: infra
tags: jenkins infra api
---

# Jenkins API

## Job 정보 확인

GET /job/{jenkinsJobName}/api/json

## Job 특정 빌드번호의 정보 확인

GET /job/{jenkinsJobName}/{buildNumber}/api/json

## Job의 마지막 빌드 정보 확인

GET /job/{jenkinsJobName}/lastBuild/api/json

## Job빌드 수행

GET /job/{jenkinsJobName}/build?token={token}

# 참고 자료

// 파이썬에서 사용하는 API

https://jenkinsapi.readthedocs.io/en/latest/using_jenkinsapi.html

// Java API

https://github.com/jenkinsci/java-client-api
