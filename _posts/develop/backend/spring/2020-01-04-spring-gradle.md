---
title: '[Spring] Gradle'
date: 2020-01-04 21:05:00 -0400
categories: devlog
tags: spring devlog gradle
---

# Gradle 이란?

# Gradle 설치

## For Window

1. [gralde.org/gradle-download/](https://gradle.org/gradle-download/) 접속

2. Complete 클릭하여 gradle-version-all.zip 다운로드

3. gradle-version-all.zip 압축해제
4. gradle-version 폴더명 gradle로 변경
5. gradle 폴더 d:\ 로 이동

### Path설정

내 PC -> 속성 -> 고급 시스템 설정 -> 환경 변수 -> Path 선택 -> D:\gradle\bin 추가

### 확인

cmd창 열어서 gradle -v

## Linux

# Gradle로 Spring 시작하기

```
gradle init

1. application 선택
2. java 선택
3. groovy 선택
4. JUnit 4 선택
5. project name 입력
6. package 입력
```

## Description

implementation	compile	
수정 시 사용하는 모듈까지만 재빌드를 한다. 

종속된 모듈의 하위 dependency를 패키지에 포함되지않는다. 

api	compile	
수정 시 연관된 모든 모듈을 재빌드 한다.

종속된 하위 모듈 모두를 패키지에 포함한다. 

compileOnly	provided	

Gradle이 컴파일 클래스 경로에만 종속성을 추가합니다(빌드 출력에 추가되지 않음). 

runtimeOnly	apk	

Gradle이 런타임 시에 사용하도록 빌드 출력에만 종속성을 추가합니다. 

annotationProcessor	compile	

주석 프로세서인 라이브러리에 종속성을 추가하려면 반드시 annotationProcessor구성을 
사용하여 주석 프로세서 클래스 경로에 추가해야 합니다. 그 이유는 이 구성을 사용하면 컴파일 
클래스 경로를 주석 프로세서 클래스 경로와 분리하여 빌드 성능을 향상할 수 있기 때문입니다. 