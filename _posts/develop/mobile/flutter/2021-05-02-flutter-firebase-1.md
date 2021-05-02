---
title: '[Flutter] Firebase Setting'
date: 2021-05-02 15:05:00 -0400
categories: devlog
tags: devlog flutter firebase setting
---

# Firebase Setting

## 개인 개발 환경 세팅
- google-services.json 파일 받기
- SHA 인증서 지문 등록

### google-services.json 파일 받기

Firebase 프로젝트 개요 - 프로젝트 설정으로 이동합니다.

![firebase-setting-1](/assets/img/post/flutter/firebase-setting-1.png)

`"내 앱"` 에서 google-services.json을 다운 받습니다.

![firebase-setting-2](/assets/img/post/flutter/firebase-setting-2.png)

`{project}/android/app/` 하위로 옮깁니다.

![firebase-setting-3](/assets/img/post/flutter/firebase-setting-3.png)

### SHA 인증서 지문 등록

Android Studio를 새로 열어, google-services.json을 넣은 프로젝트의 android folder를 엽니다.

![firebase-setting-4](/assets/img/post/flutter/firebase-setting-4.png)

android 폴더기준으로 열은 후 오른쪽 탭에 `gradle`을 클릭한 후,

android/Tasks/android/signingReport 를 클릭합니다.

![firebase-setting-5](/assets/img/post/flutter/firebase-setting-5.png)

아래와 같이 local debug key가 뜨는데 `SHA-1`의 Key를 복사합니다.

![firebase-setting-6](/assets/img/post/flutter/firebase-setting-6.png)

다시, firebase 프로젝트 설정 페이지에 가서 `SHA 인증서 지문`에 복사한 디지털 지문을 등록합니다.

![firebase-setting-7](/assets/img/post/flutter/firebase-setting-7.png)

테스트 하면 정상적으로 잘되는 것을 확인할 수 있습니다.


