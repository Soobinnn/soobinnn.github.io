---
title: '[Jenkins] Deploy'
date: 2020-02-10 09:00:00 -0400
categories: infra
tags: jenkins infra pipeline deploy spring
---

# 젠킨슨으로 자동 배포하기

# Setting

## Jenkins - Github 연동

젠킨스와 Github 연동시 사용자명, 비밀번호 인증방식은 보안상 추천하지 않는 방식이다.

Jenkins - Github 간 SSH 연동 방식

### 1. 키 생성

```
su jenkins

mkdir /var/lib/jenkins/.ssh
cd /var/lib/jenkins/.ssh

# 만약 권한이없다면 관리자 계정으로 그룹설정
chown -R root:docker /var

ssh-keygen -t rsa -f /var/lib/jenkins/.ssh/github_spring-deploy

# 비밀번호 입력하지 않고 Enter

# 비밀키/공개키 생성 확인
ls -al

# 공개키 확인 후 복사
cat /var/lib/jenkins/.ssh/github_spring-deploy.pub
```

GIt hub deploy 설정공개키 등록

생성확인

-- 젠킨스비밀키등록

Kind 인증 방식을 선택합니다. 여기선 비밀키 방식을 선택해야 Github과 공개키/비밀키로 인증이 가능합니다. Username 각 젠킨스 Job에서 보여줄 인증키 이름 입니다. 전 키 이름 그대로 사용했습니다. Private Key 좀전에 복사한 비밀키를 그대로 붙여넣습니다.

# Start

## Spring Boot

```
pipeline {
    agent {
        label 'citech-gitlab'
    }

    environment {
        GIT_USERNAME=sh(returnStdout: true, script: 'cat /home/apps/gitlab/GIT_USERNAME').trim()
        GIT_PASSWORD=sh(returnStdout: true, script: 'cat /home/apps/gitlab/GIT_PASSWORD').trim()
        SOURCE_BRANCH="${env.gitlabSourceBranch}"
        TAG_NAME = "${env.gitlabSourceBranch}".replace("release/","")
    }

    stages {
        stage("Git checkout") {
            steps {
                echo "Fetching changes from the remote Git repository"
                echo "${env.gitlabSourceNamespace}/${env.gitlabSourceBranch}"
                echo "${SOURCE_BRANCH}"
                echo "${TAG_NAME}"
                checkout ([
                    $class: 'GitSCM',
                    branches: [[name: "CI_Tech/${env.gitlabSourceBranch}"]],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [
                        [
                            $class: 'RelativeTargetDirectory',
                            relativeTargetDir: "./${PROJECT_NAME}/${BRANCH_NAME}"
                        ],
                        [$class: 'PruneStaleBranch'],
                        [$class: 'CleanCheckout'],
                        [
                            $class: 'PreBuildMerge',
                            options: [
                                fastForwardMode: 'NO_FF',
                                mergeRemote: "CI_Tech",
                                mergeTarget: "${BRANCH_NAME}"
                            ]
                        ]
                    ],
                    gitTool: 'jgit',
                    submoduleCfg: [],
                    userRemoteConfigs: [
                        [
                            credentialsId: 'gitlab_root',
                            name: env.gitlabTargetNamespace,
                            url: "https://${GIT_PROJECT_URL}"
                        ],
                        [
                            credentialsId: 'gitlab_root',
                            name: env.gitlabSourceNamespace,
                            url: "https://${GIT_PROJECT_URL}"
                        ]
                    ]
                ])

                echo "dir -> ${PROJECT_NAME}/${BRANCH_NAME}"

                dir("./${PROJECT_NAME}/${BRANCH_NAME}") {
                    sh 'git status'
                    withCredentials([usernamePassword(credentialsId: 'gitlab_root', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh 'git commit --amend -m "Merge branch \'${SOURCE_BRANCH}\' into ${BRANCH_NAME} by jenkins"'
                        sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${GIT_PROJECT_URL} HEAD:${BRANCH_NAME}'
                    }
                }
            }
        }
    }
}

```

println "Test Started" try { sh "\${tool name: GRADLE_VERSION, type: 'hudson.plugins.gradle.GradleInstallation'}/bin/gradle test -Dorg.gradle.daemon=true" } finally { junit allowEmptyResults: true, keepLongStdio: true, testResults: 'build/test-results/\*.xml' }

```

```

# 참고자료

https://jenkins.io/doc/pipeline/steps/workflow-scm-step/
