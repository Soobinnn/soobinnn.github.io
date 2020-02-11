---
title: '[Jenkins] Slack 연동'
date: 2020-02-11 17:36:00 -0400
categories: infra
tags: jenkins infra slack
---

## Slack

### Slack 채널 생성

### Jenkins App 설치

## Jenkins

### Slack Pluin 설치

### Global 설정

Jenkins 관리 - 시스템 설정 - Global Slack Notifier Setting

```
post {
        success {
            slackSend (channel: '#migrator', color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
        }
        failure {
            slackSend (channel: '#migrator', color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
        }
    }
```

# 참고자료

https://medium.com/hgmin/jenkins-slack-e20615c5f797

https://github.com/jenkinsci/slack-plugin
