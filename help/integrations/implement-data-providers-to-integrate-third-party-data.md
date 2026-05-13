---
title: 데이터 공급자를 구현하여 타사 데이터를 통합하는 방법
description: 이 자습서에서는 Adobe Target의 데이터 공급자 기능을 사용하여 타사 데이터 공급자로부터 데이터를 검색하고 이를 Target 요청에 전달하는 방법에 대한 자세한 구현과 예를 제공합니다.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
TQID: https://experienceleague.adobe.com/Oh0ngUGA-ZfpPHnQnN0VRgUG1ta4yqg8Pfm8mhCZTN0
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 293
ht-degree: 0%

---

# [!UICONTROL Data Providers]을(를) 구현하여 Adobe Target에 타사 데이터 통합

Adobe Target의 [!UICONTROL Data Providers] 기능을 사용하여 타사 데이터 공급자로부터 데이터를 검색하고 이를 Target 요청에 전달하는 방법에 대한 자세한 내용과 예입니다.

>[!NOTE]
>
>[!UICONTROL Data Providers]에는 `at.js` 1.3 이상이 필요합니다.

## 데이터 공급자의 기본 구성 요소 구현

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

`dataProvider`의 기본 구성 요소와 올바른 순서로 코드를 얻는 방법에 대한 간략한 개요입니다.\
비디오에 사용된 코드가 있는 작업 예는 여기에서 찾을 수 있습니다.
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 타사 API와 통합

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

보다 현실적인 예, 날씨 API 통합.\
비디오에 사용된 코드가 있는 작업 예는 여기에서 찾을 수 있습니다.
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 여러 공급자와 통합

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

여러 공급자의 데이터를 전역 [!DNL Target] 요청에 통합하는 방법입니다.\
비디오에 사용된 코드가 있는 작업 예는 여기에서 찾을 수 있습니다.
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 페이지 로드 영향 최소화

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

세션 저장소 개체에 데이터를 저장하여 페이지 로드 시간에 미치는 영향을 최소화합니다. 또는 `profile.` 접두사를 사용하여 값을 프로필 매개 변수로 전달하고 세션의 첫 번째 [!DNL Target] 요청에만 전달할 수 있습니다. 그러나 요청당 50개의 프로필 매개 변수를 전달하는 것으로 제한됩니다.

비디오에 사용된 코드가 있는 작업 예는 [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)에서 찾을 수 있습니다.

## 지원 자료

* [Adobe Target에서 데이터 공급자 사용](use-data-providers-to-integrate-third-party-data.md)
