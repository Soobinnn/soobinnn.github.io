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

```

## 시작하기

### 플러그인

플러그인에 **pipeline** 이 설치되어 있는지 확인

새로운 item -> item name 입력 -> pipeline 선택

# 참고문서

[scripted 공식문서](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline)
