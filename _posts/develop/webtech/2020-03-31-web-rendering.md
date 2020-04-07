---
title: '[Web] Rendering'
date: 2020-03-31 15:38:00 -0400
categories: devlog
tags: web devlog rendering
---

# 렌더링

## Process

5단계로 이뤄짐

1. DOM 트리 생성
2. 스타일 구조체 생성
3. 렌더 트리 생성
4. 레이아웃 처리
5. 페인트

1. DOM 트리 생성

노드를 트리형태로 나타냄

2. 스타일 구조체 생성

브라우저의 자체 스타일 -> 사용자 정의 스타일 -> html태그의 style 속성 단계로 처리됨

3. 렌더 트리 생성

첫번째로 만든 DOM 트리와 그다음 스타일 구조를 더해 렌더 트리를 만든다.

렌더 트리는 노드에 스타일 정보가 설정돼 있고 화면에 표시되는 노드

4. 레이아웃 처리

노드의 크기 계산과 해당 위치에 배치

5. 페인트

스타일, 크기, 배치가 끝났으니 화면에 노드를 표현하는 작업


## Reflow

변경이 생긴 렌더 트리에 대해 유효성 확일을 하고 노드의 크기와 위치를 다시 계산하는 작업


## Repaint

변경된 노드를 화면에 업데이트 하여 표시해주는 것을 의미
리플로가 발생 했을 때, 색 변경등 단순 스타일 변경이 일어날 시 발생

다시 계산되고 뿌려주는 작업이니 처리 비용이 발생되고 많이 발생할 시 웹 페이지를 표시하는데 오래 걸려 사용자가 불편함을 느낄 수 있다.

(비용크기 : Reflow > repaint )

## 비용 줄이는 방법
1. 작업 그루핑
2. 실행 사이클
3. 노출 제어를 통한 리플로 최소화 방법
4. 캐싱
5. css 규칙


# 참고 자료
https://do-dam.tistory.com/entry/%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80%EC%9D%98-%EB%9E%9C%EB%8D%94%EB%A7%81-%EA%B3%BC%EC%A0%95-2%ED%8E%B8?category=765639

https://d2.naver.com/helloworld/59361

https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction?hl=ko