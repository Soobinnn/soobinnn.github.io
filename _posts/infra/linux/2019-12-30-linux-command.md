---
title: '[linux] linux Command'
date: 2019-12-30 10:58:00 -0400
categories: infra
tags: linux infra command
---

# 리눅스 명령어

## 초기 설정

### root 계정 패스워드 설정

```
sudo passwd root
```

### 포트 확인

```
netstat

# 옵션
-n : ip 주소를 문자형(localhost)가 아닌 숫자형태로 보여줌.
-a : all
-t : tcp 정보 확인
```

### 사용자 그룹 추가

```
사용자를 생성하고 그룹에 추가
useradd -G <그룹> <사용자 이름>

기존 사용자를 그룹에 추가
usermod -aG <그룹> <사용자 이름>
```

# 쉘스크립트

#!/bin/bash를 기제하는 이유스크립트 파일이 bash쉘로 실행시킨다는 의미.
