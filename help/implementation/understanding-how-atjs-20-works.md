---
title: at.js 2.0은 어떻게 작동합니까?
description: at.js 2.0은 SPA(단일 페이지 애플리케이션)에 대한 Adobe Target의 지원을 개선하고 다른 Experience Cloud 솔루션과 통합됩니다. 이 비디오와 함께 제공되는 다이어그램은 모든 것이 어떻게 합쳐지는지 설명합니다.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 22%

---

# Adobe Target at.js 2.0 작동 방식 이해

`at.js` 2.0은 단일 페이지 애플리케이션(SPA)에 대한 Adobe Target의 지원을 개선하고 다른 Experience Cloud 솔루션과 통합됩니다. 이 비디오와 함께 제공되는 다이어그램은 모든 것이 어떻게 합쳐지는지 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 아키텍처 다이어그램

![페이지 로드 시 at.js 2.0 동작](assets/pageload.png)

1. 호출이 ECID(Experience Cloud ID)를 반환합니다. 사용자가 인증되면 다른 호출이 고객 ID를 동기화합니다.

1. `at.js` 라이브러리가 동기적으로 로드되며 문서 본문(`at.js` 는 페이지에 구현된 사전에 숨기는 코드 조각 선택 사항을 사용하여 비동기식으로 로드할 수도 있습니다.

1. 모든 구성된 매개 변수, ECID, SDID 및 고객 ID를 포함하는 페이지 로드 요청이 이루어집니다.

1. 프로필 스크립트가 실행되며에 전달됩니다. [!UICONTROL 프로필 저장소]. 스토어는 의 적격 대상자를 요청합니다. [!UICONTROL 대상 라이브러리] (예: 다음에서 공유된 대상) [!DNL Analytics], Audience Manager 등). [!UICONTROL 고객 속성] (으)로 전송됨 [!UICONTROL 프로필 저장소] 배치 프로세스.
1. URL, 요청 매개 변수 및 프로필 데이터를 기반으로 [!DNL Target] 현재 페이지 및 미래 보기를 위해 방문자에게 반환할 활동 및 경험을 결정합니다

1. 타깃팅된 컨텐츠를 다시 페이지로 전송하며, 원할 경우 추가적인 개인화를 위한 프로필 값을 포함할 수 있습니다.

   현재 페이지의 타기팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.

   단일 페이지 애플리케이션의 향후 보기를 위한 타깃팅된 콘텐츠는 브라우저에 캐시되므로 보기가 트리거될 때 추가적인 서버 호출 없이 즉시 적용할 수 있습니다. ( 다음에 대한 다이어그램 참조: `triggerView()` behavior).

1. [!DNL Analytics] 페이지에서 로 전송된 데이터 [!UICONTROL 데이터 수집] 서버
1. [!DNL Target] 데이터는 SDID를 통해 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. [!DNL Analytics] [!DNL Analytics] 그런 다음 두 위치에서 데이터를 볼 수 있습니다 [!DNL Analytics] 및 [!DNL Target] A4T 보고서를 통해

![triggerView() 함수를 사용할 때 at.js 2.0 동작](assets/triggerview.png)

1. `adobe.target.triggerView()` 단일 페이지 애플리케이션에서 호출됨
1. 보기용으로 타기팅된 콘텐츠를 캐시에서 읽습니다

1. 타기팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다

1. 활동 및 증분 지표에서 방문자를 계산하기 위해 알림 요청이 [!DNL Target] 프로필 스토어에 전송됩니다
1. [!DNL Analytics] SPA에서 로 데이터가 전송됩니다. [!UICONTROL 데이터 수집] 서버

1. [!DNL Target] 에서 데이터가 전송됩니다. [!DNL Target] 로 백엔드 [!UICONTROL 데이터 수집] 서버. [!DNL Target] 데이터는 SDID를 통해 [!DNL Analytics] 데이터에 대응되며 [!DNL Analytics] 보고 저장소로 처리됩니다. [!DNL Analytics] 그런 다음 두 위치에서 데이터를 볼 수 있습니다 [!DNL Analytics] 및 [!DNL Target] A4T 보고서를 통해

## 추가 리소스

* [단일 페이지 애플리케이션에서 at.js 2.0 구현](implement-atjs-20-in-a-single-page-application.md)
* [단일 페이지 애플리케이션용 Adobe Target 시각적 경험 작성기 사용(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
