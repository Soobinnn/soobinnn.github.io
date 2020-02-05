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

# 태그 지우기
git tag -d <태그명>

# 원격에 있는 태그 지우기
git push origin :<태그명>
```

### checkout

```
git checkout <branch name>

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

### log

```
# 현재 브랜치에 대한 로그 커밋 출력
git log

# 모든 브랜치의 로그 출력
git log --branches

#모든 브랜치의 브랜치명 표시
git log --branches --decorate

git log --braches --decorate --graph

git log --branches --decorate --graph --online

# 최신 로그 5개까지만 출력해줌
git log -5

git log -p <branchname>
```

### rebase

```
# 과거의 커밋을 통합할 때
git rebase -i HEAD~~

```
