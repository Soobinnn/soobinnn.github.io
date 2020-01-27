---
title: '[git] Git Command'
date: 2020-01-07 16:43:00 -0400
categories: devlog
tags: git devlog
---

# Git 명령어

### pull

```
git pull <remote Repository> <branch name>

// 이미 존재하는 두 프로젝트의 기록(history)을 저장하는 드문 상황에 사용된다고 한다. 즉, git에서는 서로 관련 기록이 없는 이질적인 두 프로젝트를 병합할 때 기본적으로 거부하는데, 이것을 허용해 주는 것이다.
git pull origin 브런치명 --allow-unrelated-histories
```

### tag
```
# 태그 생성
git tag <tag name>


# 태그 목록 보기
git tag

# 태그명 포함 로그 보기
git log --decorate 
```

### checkout

```
git checout <branch name>

# 옵션
-b

ex) 원격에 있는 브랜치를 가져올 수 있다.
git checkout -b feature/TESTAUTO-7049 develop

```

### branch

```
git branch <branch name>

git branch : 현재 작업하고 있는 브랜치 확인
```
