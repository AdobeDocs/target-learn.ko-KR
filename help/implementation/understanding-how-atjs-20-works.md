---
title: Adobe Target at.js 2.0의 작동 방식 이해
seo-title: Adobe Target at.js 2.0의 작동 방식 이해
description: at.js 2.0은 단일 페이지 애플리케이션(SPA)에 대한 Adobe Target의 지원을 향상시키고 다른 Experience Cloud 솔루션과 통합합니다. 이 비디오와 동봉된 다이어그램은 모든 것이 어떻게 함께 오는지 설명합니다.
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 20%

---


# Adobe Target at.js 2.0의 작동 방식 이해

`at.js` 2.0은 단일 페이지 애플리케이션(SPA)에 대한 Adobe Target의 지원을 향상시키고 다른 Experience Cloud 솔루션과 통합합니다. 이 비디오와 동봉된 다이어그램은 모든 것이 어떻게 함께 오는지 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 건축 다이어그램

![페이지 로드 시 at.js 2.0 동작](assets/pageload.png)

1. 호출은 Experience Cloud ID(ECID)를 반환합니다. 사용자가 인증된 경우 다른 호출이 고객 ID를 동기화합니다.

1. `at.js` 라이브러리는 동기식으로 로드되고 문서 본문을 숨깁니다(페이지에 구현된 선택적 사전 숨김 조각을 사용하여 비동기식으로 로드할`at.js` 수도 있습니다).

1. 페이지 로드 요청은 모든 구성된 매개 변수, ECID, SDID 및 고객 ID를 포함하여 수행됩니다.

1. Profile scripts execute and feed into the [!UICONTROL Profile Store]. The Store requests qualified audiences from the [!UICONTROL Audience Library] (e.g. audiences shared from [!DNL Analytics], Audience Manager, etc). [!UICONTROL 고객 속성] 은 [!UICONTROL 프로필 스토어로] 일괄 처리됩니다.
1. Based on URL, request parameters, and profile data, [!DNL Target] decides which Activities and Experiences to return to the visitor for the current page and future views

1. 추가적인 개인화를 위한 프로필 값을 포함하여, 선택적으로 페이지에 다시 전송된 타깃팅된 컨텐츠.

   현재 페이지의 타깃팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.

   단일 페이지 애플리케이션의 향후 보기에 대한 타깃팅된 컨텐츠는 브라우저에 캐시되므로 뷰가 트리거될 때 추가 서버 호출 없이 즉시 적용할 수 있습니다. 비헤이비어는 다음 다이어그램 `triggerView()` 을 참조하십시오.

1. [!DNL Analytics] 페이지에서 [!UICONTROL 데이터 수집 서버로 전송된] 데이터
1. [!DNL Target] 데이터는 SDID를 통해 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. [!DNL Analytics] [!DNL Analytics] 그런 다음 A4T 보고서 [!DNL Analytics] 와 [!DNL Target] A4T 보고서를 통해 데이터를 볼 수 있습니다.

![triggerView() 함수가 사용되는 경우 at.js 2.0 동작](assets/triggerview.png)

1. `adobe.target.triggerView()` 단일 페이지 애플리케이션에서 호출됩니다.
1. 보기용으로 타깃팅된 콘텐츠를 캐시에서 읽습니다

1. 타깃팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다

1. 활동 및 증분 지표에서 방문자를 계산하기 위해 알림 요청이 [!DNL Target] 프로필 스토어에 전송됩니다
1. [!DNL Analytics] 데이터는 SPA에서 [!UICONTROL 데이터 수집 서버로] 전송됩니다.

1. [!DNL Target] 데이터는 백엔드에서 [!DNL Target] 데이터 수집 [!UICONTROL 서버로] 전송됩니다. [!DNL Target] 데이터는 SDID를 통해 [!DNL Analytics] 데이터에 대응되며 [!DNL Analytics] 보고 저장소로 처리됩니다. [!DNL Analytics] 그런 다음 A4T 보고서 [!DNL Analytics] 와 [!DNL Target] A4T 보고서를 통해 데이터를 볼 수 있습니다.

## 추가 리소스

* [단일 페이지 애플리케이션에서 at.js 2.0 구현](implement-atjs-20-in-a-single-page-application.md)
* [단일 페이지 애플리케이션(SPA VEC)에 Adobe Target의 시각적 경험 컴포저 사용](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [at.js 작동 방식 설명서](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)