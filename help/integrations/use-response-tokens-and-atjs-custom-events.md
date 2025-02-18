---
title: 응답 토큰 및 at.js 사용자 지정 이벤트 사용 방법
description: 응답 토큰 및 at.js 사용자 지정 이벤트를 사용하여 Target에서 타사 시스템으로 프로필 정보를 공유하는 방법을 알아봅니다.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 3%

---

# Adobe Target에서 응답 토큰 및 at.js 사용자 지정 이벤트 사용

응답 토큰 및 `at.js` 사용자 지정 이벤트를 사용하면 [!DNL Target]에서 타사 시스템으로 프로필 정보를 공유할 수 있습니다. 사용자 지정 프로필 특성, 지리적 정보, 활동 세부 정보 및 기본 제공 프로필을 포함한 [!DNL Target] 방문자 프로필의 모든 개체를 사용자 지정 JavaScript을 사용하여 서드파티와 통합할 수 있는 [!DNL Target] 응답에 추가할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 응답 토큰 및 at.js 사용자 지정 이벤트 사용 방법

1. [!DNL Target]에서 필요한 데이터 확인
1. 설정->응답 토큰 화면의 토글을 전환하여 필요한 데이터에 대한 응답 토큰을 켭니다
1. 사용해야 하는 이벤트 리스너 결정
1. Adobe Target 이벤트를 수신하는 데 필요한 JavaScript을 작성하고, 응답 토큰을 읽고, 통합에 필요한 작업을 수행합니다
1. Target 로드 작업 후 Launch의 사용자 지정 코드 작업을 사용하여 이벤트 리스너 JavaScript을 배포하거나 설정->구현 화면에서 at.js의 라이브러리 바닥글 섹션에 추가하고 새 at.js 파일을 저장합니다
1. QA 및 통합 게시

## 추가 리소스

* [Adobe Target에서 Experience Cloud Debugger 사용](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [응답 토큰 설명서](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Adobe Target에서 데이터 공급자 사용](use-data-providers-to-integrate-third-party-data.md)
