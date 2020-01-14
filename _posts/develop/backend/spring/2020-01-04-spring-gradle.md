---
title: '[Spring] Gradle'
date: 2020-01-04 21:05:00 -0400
categories: devlog
tags: spring devlog gradle
comments: true
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

내 PC -> 속성 -> 고급 시스템 설정 -> 환경 변수 -> Path 선택 ->  D:\gradle\bin 추가

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