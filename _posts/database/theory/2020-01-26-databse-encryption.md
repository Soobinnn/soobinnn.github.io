---
title: '[database] encryption'
date: 2020-01-26 10:02:00 -0400
categories: database
tags: database devlog encryption
---
# 암호화 종류
- 양방향
    - 대칭형
        - DES
        - 3-DES
        - AES
        - SEED
        - ARIA
        - MASK
    - 비대칭형
        - RSA
        - DSA

- 단방향

## DES
DB 암호화를 위해 DES 알고리즘이 많이 사용되고는 있지만, 다소 보안성이 약한 것으로 여겨진다.

## 3DES
속도면에서 뒤떨어지기는 하나 보안성 측면에서 강한면으로 인해 널리 사용되고 있다.

# DB 암호화 구축
DB 암호화를 위해 고려해야 할 중요한 3가지
1. 어떻게 암호화를 수행 할 것인가?
2. 기업의 IT인프라에서 데이터 흐름이 어떻게 되는가?
3. DB 암호화가 어떻게 보안 규칙과 연동되는가?


# DB 암호화 종류
## Plug-In 방식

## API 방식


