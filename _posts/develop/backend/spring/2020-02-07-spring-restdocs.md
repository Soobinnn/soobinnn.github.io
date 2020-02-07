---
title: '[Spring] Spring Rest Docs '
date: 2020-02-07 17:36:00 -0400
categories: devlog
tags: spring devlog docs
---

# Spring Rest Docs

## Install

```java
// 1. ascii doctor 플러그인 설정
plugins {
  id 'org.asciidoctor.convert' version "1.5.6"
}

// 2. asciidoctor Task 설정
asciidoctor {
    dependsOn test
}

// 3. bootJar Task 설정
bootJar {
    dependsOn asciidoctor
    from ("${asciidoctor.outputDir}/html5") {
        into "static/docs"
    }
}

// 4. mockMVC에 rest docs 추가하기
testImplementation('org.springframework.restdocs:spring-restdocs-mockmvc')

// 5. *.adoc 파일의 {snippets}를 자동으로 설정 - 아래에서 자세히 설명
asciidoctor 'org.springframework.restdocs:spring-restdocs-asciidoctor:2.0.3.RELEASE'
```

# 참고 문서

https://lannstark.tistory.com/9

https://spring.io/guides/gs/testing-restdocs/
