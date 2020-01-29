---
title: '[Jenkins] PipeLine Command'
date: 2020-01-28 13:26:00 -0400
categories: infra
tags: jenkins infra pipeline command
---

## Git CheckOut

```
pipleline {
  environment {

  }
  stage("Git CheckOut", {
          checkout(
                  [
                          $class                           : 'GitSCM',
                          branches                         : [[name: '${BRANCH_SELECTOR}']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions                       : [],
                          submoduleCfg                     : [],
                          userRemoteConfigs                : [[url: '${GIT_URL}']]
                  ]
          )
          println "Git CheckOut End"
  })
}
```

### 설명

#### extensions

\$class : "WipeWorkspace"

    빌드를 실행하기 전에 워크 스페이스의 파일들을 모두 삭제

\$class : "CleanBeforeCheckout"

    체크아웃 실행 전에 untracked files, directories, .gitignore에 해당하는 파일들을 삭제한다. -> 이전 빌드에서 생성된 artifacts가 모두 삭제됨.

#### userRemoteConfigs

credentialsId

    젠킨스 저장소 Credential ID 입력
