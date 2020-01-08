---
title: '[Jenkins] PipeLine'
date: 2020-01-08 10:17:00 -0400
categories: infra
tags: jenkins infra whatis
---

# Jenkins Pipeline

연속적인 이벤트, Job의 그룹

Jenkins을 사용하여 연속적인 전달 파이프 라인의 통합 및 구현을 지원하는 플러그인의 조합

파이프라인 DSL(Domain-Specific Language)를 통해 간단하거나 복잡한 전달 파이프 라인을 코드로 생성할 수 있는 확장 가능한 자동화 서버

## 특징

젠킨스 파이프라인은 2가지 문법을 지원함

1. Scripted
2. Declarative

Scripted 문법의 경우 Groovy로 빌드되기 때문에 일반적으로 파이프라인을 생성하는데 Declarative보다 훨씬 유연한 방법이다.

반면, Declarative의 경우 Scripted보다 훨씬 더 간단하게 작성 할 수 있다. 대신 고정된 방식으로만 사용해야한다.

2가지문법은 서로 호환되지 않는다. 같이 쓸수 없음.

\* Scripted Pipeline 이 먼저 생겼고 그 후 특정 버전 이후 부터 Declarative Pipeline 이 추가됨

```
# Declarative Pipeline 형태
pipeline {
    agent any
    stages ('Example') {
        steps {
            echo "Hello World"
        }
    }
}

# Scripted Pipeline
node {
    stage('Example') {
        if (env.BRANCH_NAME == 'master') {
            echo 'I only execute on the master branch'
        } else {
            echo 'I execute elsewhere'
        }
    }
}
```

### Scripted

쉘 스크립트를 짜듯이 자유롭게 파이프라인을 구성할 수 있도록 지원함. Scripted 문법은 Groovy문법을 사용함.

#### 장점

- 더 많은 절차적 코드 작성 가능
- 프로그램과 흡사
- 기존 파이프 라인 문법이라 친숙하고 이전 버전과 호환가능
- 필요한 경우 커스텀한 작업 생성이 가능하기 때문에 유연성이 좋다.
- 보다 복잡한 워크 플로우 및 파이프 라인 모델링 가능

#### 단점

- 일반적으로 더 많은 프로그래밍 필요
- Groovy 언어 및 환경으로 제한된 구문 검사
- 전통적인 젠킨스 모델과는 맞지 않음
- 같은 작업이라면 Declarative 문법보다 잠재적으로 더 복잡

더 다양한 작업을 생성할 수 있지만, 복잡하고, 유지보수하기 힘든 단점

#### 문법

**Directive**

<table>
<th>Directive</th>
<th>설명</th>
<tr>
  <td>node</td>
  <td>
    Scripted 파이프라인을 실행하는 젠킨스 에이전트<br/>
    최상단 선언 필요<br/>
    Jenkins Master-Slave 구조에서는 파라미터로 Master-Slave 정의 가능
  </td>
</tr>
<tr>
  <td>dir</td>
  <td>명령을 수행할 디렉터리 / 폴더 정의</td>
</tr>
<tr>
  <td>stage</td>
  <td>파이프라인의 각 단계를 얘기하며, 이 단계에서 어떤 작업을 실행할지 선언하는 곳</td>
</tr>
<tr>
  <td>git</td>
  <td>git 원격 저장소에서 프로젝트 Clone</td>
</tr>
<tr>
  <td>sh</td>
  <td>Unix환경에서 실행할 명령어 실행 (window는 bat)</td>
</tr>
<tr>
  <td>def</td>
  <td>Groovy 변수 혹은 함수 선언</td>
</tr>
</table>

** 예외 흐름** try/catch/finally로 별도의 처리를 할 수 있음.

**예제**

```
# 전체적인 구성
pipeline {
    agent {}
    triggers {}
    tools {}
    environment {}
    options {}
    parameters {}
    stages {
        stage('stage1') {}
        stage('stage2') {}

        parallel { // 병렬 처리
            stage('parallel_1') {}
            stage('parallel_2') {}
        }
    }

    // stages 완료 후 실행
    post {
      always {}
      changed {}
      fixed {}
      regression {}
      aborted {}
      failure {}
      success {}
      unstable {}
      cleanup {}
    }
}
```

```
pipeline {
    // ************
    // agent
    // *************
    agent any
    //agent none // 이 경우 stage에서 지정해야 함
    /*
    agent {
      docker {
        image 'maven:3-alpine',
        label 'my-defined-label',
        args '-v /tmp:/tmp'
      }
    }
    */
    /*
    agent {
        dockerfile {
            filename 'Dockerfile.build'
            dir 'build'
            label 'my-defined-label'
            additionalBuildArgs  '--build-arg version=1.0.2'
    	}
    }
    */

    // ************
    // triggers
    // *************
    triggers {
        cron('H */4 * * 1-5')
        pollSCM('H */4 * * 1-5')
        upstream(upstreamProjects: 'job1,job2', threshold: hudson.model.Result.SUCCESS)
    }

    // ************
    // tools
    // *************
    tools {
      // Jenkins 'Global Tool Configuration' 에 설정한 버전과 연동
      nodejs "node-latest"
      maven 'apache-maven-3.0.1'
      gradle 'gradle-latest'
    }

    // ************
    // environment
    // *************
    environment {
        PROJECT = 'webapp'
        PHASE = params.PHASE // 파라미터값을 받아올 경우
        JOB_NAME = env.JOB_NAME // 내부 변수를 가져올 경우 (https://wiki.jenkins.io/display/JENKINS/Building+a+software+project)
    }

    // ************
    // options
    // *************
    options {
        buildDiscarder(logRotator(numToKeepStr: '3', artifactNumToKeepStr: '3'))
      	checkoutToSubdirectory('foo')
      	disableConcurrentBuilds()
        newContainerPerStage
        overrideIndexTriggers(true)
        preserveStashes(5)
        retry(3)
        skipDefaultCheckout()
        skipStagesAfterUnstable()
        timeout(time: 1, unit: 'HOURS')
        timestamps()
    }

    // ************
    // parameters
    // *************
    parameters {
        string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
        text(name: 'DEPLOY_TEXT', defaultValue: 'One\nTwo\nThree\n', description: '')
        booleanParam(name: 'DEBUG_BUILD', defaultValue: true, description: '')
        choice(name: 'CHOICES', choices: 'one\ntwo\nthree', description: '')
        file(name: 'FILE', description: 'Some file to upload')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'A secret password')
    }

    stages {
        stage('stage 1') {
            // ************
		    // when
    		// *************
            when {
                branch 'master'
                buildingTag()
                changelog '.*^\\[DEPENDENCY\\] .+$'
                changeset "**/*.js"
                changeRequest()
                environment name: 'DEPLOY_TO', value: 'production'
                equals expected: 2, actual: currentBuild.number
                expression { return params.DEBUG_BUILD }
                tag "release-*"
                tag pattern: "release-\\d+", comparator: "REGEXP"
                not { branch 'master' }
                allOf { branch 'master'; environment name: 'DEPLOY_TO', value: 'production' }
                anyOf { branch 'master'; branch 'staging' }
                anyOf {
                    environment name: 'DEPLOY_TO', value: 'production'
                    environment name: 'DEPLOY_TO', value: 'staging'
                }
        	}

            // ************
		    // step
    		// *************
            step {
                echo "Hello ${params.PERSON}"
                echo "Biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"
                echo "Choice: ${params.CHOICE}"
                echo "Password: ${params.PASSWORD}"
                sh 'echo test..'
            }
        }

        parallel {
            stage('NPM Build') {
                steps {
                    sh """
                    	cd ${WORKSPACE}
                    	npm set progress=false
                    	yarn install
                    	yarn run stage
                    """
                }
            }
            stage('Gradle Build') {
                steps {
                    sh "gradle clean build"
                }
            }
        }
    }

    // ************
	// post
    // *************
    post {
        always {
            echo 'I will always say Hello again!'
        }
        success {
            archiveArtifacts artifacts: "**"
        }
    }
}
```

## 시작하기

### 플러그인

플러그인에 **pipeline** 이 설치되어 있는지 확인

새로운 item -> item name 입력 -> pipeline 선택

## 명령어를 만들어주는 플러그인&설정

- Blueocean 플러그인
- Pipeline Syntax -> Snippet Generator

# 참고문서

[scripted 공식문서](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline)
