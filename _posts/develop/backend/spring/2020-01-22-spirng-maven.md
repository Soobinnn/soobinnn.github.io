---
title: '[Spring] maven'
date: 2020-01-22 22:10:00 -0400
categories: devlog
tags: spring devlog maven
---

# Maven 이란? 
: Apache에서 개발한 Java기반 프로젝트의 라이프사이클 관리를 위한 빌드 도구

   컴파일과 빌드를 동시에 수행, 테스트를 병행하거나 서버 측 Deploy자원을 관리할 수 있는 환경을 제공

   라이브러리 관리 기능도 내포함.

   settings.xml/pom.xml 파일에 필요한 라이브러리만 적으면 Maven이 알아서 다운, 설치 및 경로지정을 해줌

## 기능
 

POM (Project Object Model)

 : 프로젝트 내 빌드 옵션을 설정하는 부분

 
1. 프로젝트 정보 
```
<modelVersion> : maven의 pom.xml의 모델 버전

 <groupId> : 프로젝트를 생성한 조직,그룹명 (URL 역순으로 지정)

 <artifactId> : 프로젝트에서 생성되는 기본 아티팩트의 고유 이름

   * Maven에 의해 생성되는 일반적인 default값은 <artifact><version><extention>임 

     EX) demo-0.0.1-SNAPSHOT.jar

 <version> : 애플리케이션의 버전. (SNAPSHOT이 붙으면 아직 개발단계라는 의미)

 <packaging> : jar, war, ear, pom등 패키지 유형을 나타냄

 <name> : 프로젝트 명

 <dscription> : 프로젝트 설명

 <url> : 프로젝트를 찾을 수 있는 URL

 <properties> : pom.xml에서 중복해서 사용되는 설정값들을 지정해놓는 부분.

                     다른 위치에서 ${...}로 표기해서 사용할 수 있다.

 <profiles> : dev, pro이런식으로 개발할 때, 릴리즈할 때를 나눠야할 필요가 있는 설정 값은 profiles로 설정할 수 있음
```
 
2. 의존성 라이브러리 정보

    

3. build 정보
```

  <finalName> : 빌드 결과물 이름 설정

  <resources> : 리소스(각종 설정 파일)의 위치를 지정 (default : src/main/resources)

  <testResources> : 테스트 리소스의 위치를 지정 (default : src/test/resources)

  <Repositories> : 빌드할 때 접근할 저장소의 위치를 지정할 수 있다. (default : http://repo1.maven.org/maven2) 

  <outputDirectory> : 컴파일한 결과물 위치 값 지정, (default : target/classes)

  <testOutputDirectory> : 테스트 소스를 컴파일한 결과물 위치 값 지정, (default : target/test-classes)

  <plugin> : 어떠한 액션 하나를 담당하는 것으로 가장 중요하지만 들어가는 옵션은 각각 다름

      <executions> : 플러그인 goal과 관련된 실행에 대한 설정

      <configuration> : 플러그인에서 필요한 설정 값 지정

``` 

 

4. 배포

   

## 장점
 1. 컴파일과 빌드를 동시에 수행할 수 있음.

 2. 서버의 Deploy 자원을 관리할 수 있는 환경 제공

 3. pom.xml파일을 통해 관리하므로 개발,유지보수 측면에서 오픈소스 라이브러리,프로젝트 등 관리 용이

 4. IDE에 종속된 부분들을 제거할 수 있음.

 5. Maven Profile기능을 통해 배포 설정 파일을 관리하고 배포 파일을 생성할 수 있다.

 

## 단점
 1. Maven에서 기본적으로 지원하지 않는 빌드 과정을 추가해야 하는 경우 상당히 고생이 따름.

 2. 특정 플러그인 설정이 약간만 달라도 해당 설정을 분리해서 중복 기술할 때가 발생함.

 

 * 이와 같은 단점을 해결하기 위해, Gradle이라는 새로운 빌드 툴이 등장함.

 

* Maven LifeCycle
   : Maven에서는 clean, build, site의 세 가지 Lifecycle을 제공하고 있다

     compile, test, package, deploy 등의 과정은 빌드 Lifecycle에 속한다

     Maven은 모든 빌드 단위에 대한 Lifecycle이 예약되어 있어서 개발자가 임의로 변경 할 수 없다

     

   - Phase

      : Build Lifecycle의 각각의 단계를 의미함.

        특정 순서에 따라서 goal이 실행되도록 구조를 제공함

        Phase간에는 의존 관계가 있다

   - Goal

      : Target과 같은 개념

   - Phase와 Goal의 관계
      : Maven에서 제공하는 모든 기능은 플러그인 기반으로 동작함

       기본으로 제공하는 Phase를 실행하면 해당 Phase와 연결된 플러그인의 Goal이 실행됨

   - 

## Maven 기본 명령어
```
 maven [options] [goals] [phase]
```

