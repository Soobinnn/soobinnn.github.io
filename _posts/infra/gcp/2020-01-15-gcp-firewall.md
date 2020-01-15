---
title: '[GCP] 방화벽 설정'
date: 2020-01-15 09:22:00 -0400
categories: infra
tags: gcp infra firewall
---

## 방화벽 설정

메뉴 - Compute Engine - VM 인스턴스 - 인스턴스 메뉴 - 네트워크 세부정보 보기 ![firewall_start](/assets/img/post/gcp/firewall_start.PNG)

메뉴 - 방화벽 규칙 - 방화벽 규칙 만들기 선택 ![firewall_1](/assets/img/post/gcp/firewall_1.PNG)

해당 정보 입력

"대상" 의 경우는 모든 사람이 접근을 허용 하고 싶을땐 **네트워크의 모든 인스턴스** 를 선택하고 "소스 IP 범위" 는 **0.0.0.0/0** 을 한다.

특정 IP 대역만 접근 하도록 설정도 가능하다. ![firewall_2](/assets/img/post/gcp/firewall_2.PNG)

만들기를 누르고 조금 기다리면 방화벽이 설정된 것을 확인 할 수 있다. ![firewall_3](/assets/img/post/gcp/firewall_3.PNG)

### 확인

설정한 해당 포트로 어플리케이션을 실행 시킨 후 접속이 되는지 확인한다.

어플리케이션 실행 후 netstat -nat 명령어로도 확인 할 수 있다.
