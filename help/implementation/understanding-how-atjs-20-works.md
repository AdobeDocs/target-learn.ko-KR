---
title: At.js 2.0은 어떻게 작동합니까?
description: at.js 2.0은 SPA(단일 페이지 애플리케이션)에 대한 Adobe Target의 지원을 향상시키고 다른 Experience Cloud 솔루션과 통합합니다. 이 비디오와 함께 제공되는 다이어그램은 모든 것이 어떻게 함께 오는지 설명해 준다.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 21%

---


# Adobe Target at.js 2.0의 작동 방식 이해

`at.js` 2.0은 SPA(단일 페이지 애플리케이션)에 대한 Adobe Target의 지원을 향상시키고 다른 Experience Cloud 솔루션과 통합합니다. 이 비디오와 함께 제공되는 다이어그램은 모든 것이 어떻게 함께 오는지 설명해 준다.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 아키텍처 다이어그램

![페이지 로드의 at.js 2.0 비헤이비어](assets/pageload.png)

1. 호출은 Experience Cloud ID(ECID)를 반환합니다. 사용자가 인증된 경우 다른 호출은 고객 ID를 동기화합니다.

1. `at.js` 라이브러리는 동기식으로 로드되고 문서 본문을 숨깁니다.(페이지에 구현된 선택적 사전 숨김 조각을 사용하여 비동기적으로 로드할 `at.js` 수도 있습니다.)

1. 페이지 로드 요청은 구성된 모든 매개 변수, ECID, SDID 및 고객 ID를 포함하여 수행됩니다.

1. 프로필 스크립트는 [!UICONTROL 프로필 저장소]에 실행되고 피드됩니다. 스토어는 [!UICONTROL 대상 라이브러리]에서 자격이 있는 대상을 요청합니다(예: [!DNL Analytics], Audience Manager 등에서 공유된 대상). [!UICONTROL 고객 ] 속성은  [!UICONTROL 일괄 처리] 에서 프로필 스토어로 전송됩니다.
1. URL, 요청 매개 변수 및 프로필 데이터를 기반으로, [!DNL Target]은 현재 페이지 및 향후 보기에 대해 방문자에게 돌아갈 활동 및 경험을 결정합니다

1. 추가적인 개인화를 위한 프로필 값을 선택적으로 포함하여, 페이지로 다시 전송된 타깃팅된 컨텐츠.

   현재 페이지의 타깃팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.

   단일 페이지 애플리케이션의 향후 보기에 대한 타깃팅된 컨텐츠는 브라우저에 캐시되므로 뷰가 트리거될 때 추가 서버 호출 없이 즉시 적용할 수 있습니다. ( `triggerView()` 비헤이비어는 다음 다이어그램을 참조하십시오.)

1. [!DNL Analytics] 페이지에서  [!UICONTROL 데이터 ] 수집 서버로 전송된 데이터
1. [!DNL Target] 데이터는 SDID를 통해 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. [!DNL Analytics] [!DNL Analytics] 그런 다음 A4T 보고서 [!DNL Analytics] 와  [!DNL Target] A4T 보고서를 통해 데이터를 볼 수 있습니다.

![triggerView() 함수가 사용되는 경우 at.js 2.0 비헤이비어](assets/triggerview.png)

1. `adobe.target.triggerView()` 단일 페이지 애플리케이션에서 호출됩니다.
1. 보기용으로 타깃팅된 콘텐츠를 캐시에서 읽습니다

1. 타깃팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다

1. 활동 및 증분 지표에서 방문자를 계산하기 위해 알림 요청이 [!DNL Target] 프로필 스토어에 전송됩니다
1. [!DNL Analytics] 데이터는 SPA에서  [!UICONTROL Data CollectionServers로 ] 전송됩니다.

1. [!DNL Target] 데이터는 백엔드 [!DNL Target] 에서  [!UICONTROL 데이터 ] 수집 서버로 전송됩니다. [!DNL Target] 데이터는 SDID를 통해 [!DNL Analytics] 데이터에 대응되며 [!DNL Analytics] 보고 저장소로 처리됩니다. [!DNL Analytics] 그런 다음 A4T 보고서 [!DNL Analytics] 와  [!DNL Target] A4T 보고서를 통해 데이터를 볼 수 있습니다.

## 추가 리소스

* [단일 페이지 애플리케이션에서 at.js 2.0 구현](implement-atjs-20-in-a-single-page-application.md)
* [SPA VEC(Visual Experience Composer for Single Page Applications) 사용](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [사용 방법 at.js 사용 설명서](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)