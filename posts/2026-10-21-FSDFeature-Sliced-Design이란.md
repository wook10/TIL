---
title: "FSD(Feature-Sliced Design)이란?"
date: 2026-10-21
tags: []
velog_url: https://velog.io/@s26011-cloud/FSDFeature-Sliced-Design%EC%9D%B4%EB%9E%80
---

~~![](images/2026-10-21-FSDFeature-Sliced-Design%EC%9D%B4%EB%9E%80/1.png)
# 📌 FSD 아키텍쳐란?
---
FSD는 대규모 프론트엔드 애플리케이션을 기능 중심(Feature-Driven)으로 구조화 하는 아키텍쳐 방법론이다. FSD의 계층 구조는 크게 레이어, 슬라이스, 세그먼트로 나뉜다.

## 📌 레이어 (Layers)
---
레이어란 FSD에서 프로젝트 코드를 책임 범위와 의존 방향에 따라 수직으로 나눈 취상위 구분 단위이다. FSD의 레이어는 app, processes, pages, widgets, features, entities, shared로 구성된다.

- App 레이어란
  - 애플리케이션의 로직이 초기화되는 곳이다. 여기에는 Providers, router, global styles, global type declarations 등이 정의된다.

- Processes 레이어란
  - 여러 페이지에 걸친 프로세스을 처리하는 레이어이다. 현재는 사용이 권장되지 않는다.

- Pages 레이어란
  - 애플리케이션의 각 페이지가 포함된 레이어이다.

- Widgets 레이어란
  - 페이지에서 사용되는 독립적인 UI 컴포넌트이다. 보통 여러 features 또는 entities를 조합한 구성 요소로 페이지 단위에서 활용된다.

- Features 레이어란
  - 사용자 시나리오와 비즈니스 가치를 가지는 기능을 다루는 레이어이다.

- Entities 레이어란
  - 비즈니스 도메인을 나타내는 엔티티를 구성하는 레이어이다.
  
- Shared 레이어란
  - 특정 비즈니스 로직에 종속되지 않는 재사용 가능한 요소들을 담는 레이어이다.

## 📌 슬라이스 (Slives)
---
대부분의 레이어에는 슬라이스라는 하위 디렉토리가 있으며, 이는 애플리케이션을 두 번째 수준으로 분해한 것이다. 슬라이스는 코드를 비즈니스 도메인 기준으로 묶는 단위이며, 같은 레이어의 슬라이스끼리는 서로 의존할 수 없다.

## 📌 세그먼트 (Segments)
---
각 슬라이스는 세그먼트로 구성된다. 세그먼트는 슬라이스 내부의 코드를 역할에 따라 구분하는 데 도움을 준다.

- api
  - 서버 요청 등 필요한 API 관련 코드
- UI
  - 해당 슬라이스의 UI 컴포넌트
- model
  - 비즈니스 로직, 즉 상태와의 상호작용
- lib
  - 슬라이스 내부에서 사용되는 보조 기능
- config
  - 슬라이스에 필요한 설정
- consts
  - 필요한 상수 정의
  
## 📌 Public API
---
 각 슬라이스에는 Public API가 존재한다. Public API는 index.js 또는 index.ts 파일로 표현되며, 이를 통해 외부에 필요한 기능만 노출하고 나머지는 내부 구현으로 격리할 수 있다. 

