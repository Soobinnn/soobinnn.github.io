# Infra 기본 이론


### Bare Metal
어떤 소프트웨어도 담겨 있지 않은 하드웨어
운영체제가 설치되어 있지 않은 하드웨어

#### 가상화 아키텍쳐
1. 호스트형 가상화
2. 베어메탈 가상화

##### 1. 호스트형 가상화

하드웨어 상에 호스트 운영체제가 있고, 그 위에서 가상머신을 구현하는 방식

보통 호스트 운영체제가 커널 수준에서 가상화 기술을 지원함.

##### 2. 베어메탈 가상화
- 베어메탈 하이퍼 바이저
- 베어메탈 스위치
- 베어메탈 클라우드 서비스

__베어메탈 하이퍼바이저__

호스트 운영체제 없이 하드웨어 상에 하이퍼바이저가 바로 설치되고, 이 위에 가상머신을 구현하는 것

하이퍼바이저를 베어메탈 하이퍼바이저라 부름.

\* 현재 서버용 하이퍼바이저의 대부분은 베어메탈 하이퍼바이저이며,
데스크톱용 하이퍼바이저의 다수가 호스트형 하이퍼바이저이다.

\* 하이퍼바이저 (hypervisor)
호스트 컴퓨터에서 다수의 운영체제를 동시에 실행하기 위한 논리적 플랫폼.

__베어메탈 스위치__

네트워크 분야에서 SDN (Soft Defined Network)개념

> SDN
>> 네트워킹 하드웨어와 소프트웨어를 분리하는 것.
기존 네트워크 장비는 하드웨어부터 운영체제, 관리 소프트웨어까지 네트워크 장비 업체가 일체형으로 제공해옴. -> 가격이 매우 비쌈

네트워크 장비를 범용적으로 사용할 수 있는 하드웨어와 소프트웨어를 분리.

여기서 운영체제와 어플리케이션을 기업이 필요한 대로 설치할 수 있도록 만들어진 순수 하드웨어 만의 스위치장비

__베어메탈 클라우드 서비스__

클라우드 서비스는 일반적으로 가상머신을 제공하는데, 베어메탈 서버에 클라우드의 특징인 빠른 프로비저닝을 적용한 매니지드 호스팅 서비스


__VIP__


# 참고 자료
https://run-it.tistory.com/44
