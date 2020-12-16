---
title: Adobe Target에서 응답 토큰 및 at.js 사용자 지정 이벤트 사용
seo-title: Adobe Target에서 응답 토큰 및 at.js 사용자 지정 이벤트 사용
description: 응답 토큰 및 at.js 사용자 지정 이벤트를 사용하면 Target에서 제3자 시스템으로 프로필 정보를 공유할 수 있습니다. 사용자 지정 프로필 속성, 지리적 정보, 활동 세부 사항 및 내장 프로필을 비롯한 Target 방문자 프로필의 모든 개체를 Target 응답에 추가할 수 있습니다. 응답에서 사용자 지정 JavaScript를 사용하여 제3자와 통합할 수 있습니다.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---


# Adobe Target에서 응답 토큰 및 at.js 사용자 지정 이벤트 사용

응답 토큰 및 `at.js` 사용자 지정 이벤트를 사용하면 [!DNL Target]의 프로필 정보를 타사 시스템에 공유할 수 있습니다. 사용자 지정 프로필 속성, 지리적 정보, 활동 세부 사항 및 내장 프로필을 포함한 [!DNL Target] 방문자 프로필의 모든 개체를 [!DNL Target] 응답에 추가할 수 있습니다. 이 응답에서는 사용자 지정 JavaScript를 사용하여 제3자와 통합할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 응답 토큰 및 at.js 사용자 지정 이벤트를 사용하는 방법

1. [!DNL Target]에서 필요한 데이터를 결정합니다.
1. Setup->Response Token 화면에서 토글을 전환하여 필요한 데이터에 대한 응답 토큰 켜기
1. 사용해야 하는 이벤트 리스너를 결정합니다.
1. Adobe Target 이벤트를 수신하고, 응답 토큰을 읽고, 통합에 필요한 작업을 하는 데 필요한 JavaScript를 작성합니다
1. &quot;Target 로드&quot; 액션 후 Launch에서 사용자 정의 코드 작업을 사용하여 이벤트 리스너 JavaScript를 배포하거나 Setup->Implementation 화면에서 at.js의 라이브러리 바닥글 섹션에 추가하고 새 at.js 파일을 저장합니다.
1. QA 및 통합 게시

## 추가 리소스

* [Adobe Target에서 Experience Cloud Debugger 사용](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [응답 토큰 설명서](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [At.js 사용자 지정 이벤트 설명서](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [Adobe Target에서 데이터 공급자 사용](use-data-providers-to-integrate-third-party-data.md)