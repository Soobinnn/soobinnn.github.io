---
title: '[React] ChangeLog Auto'
date: 2020-05-25 08:40:00 -0400
categories: devlog
tags: react devlog changelog auto
---

# ChangeLog 자동화

[standard-version](https://github.com/conventional-changelog/standard-version) 를 통해 통해 versioning 과 CHANGELOG.md 를 자동으로 생성할 수 있다.

기본적인 원리는 git commit의 로그에서 기록된 package.json 에 새로운 버전을 명시하고 CHANGELOG.md에 해당 내용을 추가하는 방식

## standard-version 

위 라이브러리가 하는 작업

- git 의 commit 로그를 확인하여 새로운 version을 생성하고 packet.json 에 version 필드를 갱신.

- Conventional Commits 에 해당하는 내용을 CHANGELOG.md 파일에 추가합니다.

- 두가지 내용을 묶어서 한번에 chore(release): 버전명(예: 1.1.2) 형태의 메시지로 커밋합니다.

- 버전명을 Tag로 만들어서 git에 추가합니다.

## Get Start
### Install
```
npm install standard-version -D
```

### package.json에 스크립트 추가
```
{
  ...
  "scripts": {
    "release": "standard-version"
  }
}
```
```
// 최초에 한번: CHANGELOG.md 파일을 생성함
yarn release --first-release

// 새로운 버전을 생성하고 CHANGELOG.md 버전 내용을 추가 및 커밋
yarn release
```

\* `standard-version`를 사용하기 위해서는 Conventinal Commit이 필요함.

### Coventional Commits

#### Get Start
##### Install
```
npm install @commitlint/cli @commitlint/config-conventional -D
```

##### Example
```
<type>[optional scope]: <description>


# Examples

fix: allow login without uid
feat: add chat function
BREAKING CHANGE: 'extend' > 'inherit', must fix all the codes

fix(chat): broken emoji
feat(auth): add Google Play Auth

// 설명
feat: add hat wobble
^--^  ^------------^
|     |
|     +-> Summary in present tense.
|
+-------> Type: chore, docs, feat, fix, refactor, style, or test.


```


##### Description
커밋 Type 설명

| Type | SemVer | Description |
| ----- | ----- | ------ |
| fix | PATCH | Bug Fix, API 변경 사항 없이 내부 수정 |
| feat | MINOR| 새로운 기능 추가, API 변경(하위 호환) |
| BREAKING CHANGE | MAGER | API 큰 변경 |
| refactor | |리팩토링 코드, 변수 명등 변경 |
| docs | | 문서 수정/추가 |
| test | | 테스트 코드 추가/수정 |
| chore | | 그 외 자잘한 수정 사항들 |

# 참고 문서
https://velog.io/@hax0r/Node-%ED%94%84%EB%A1%9C%EB%8D%95%ED%8A%B8-%ED%80%84%EB%A6%AC%ED%8B%B0%EB%A5%BC-%EB%86%92%EC%9D%B4%EB%8A%94-%ED%98%91%EC%97%85-%EB%B0%A9%EB%B2%95-q29zo12w