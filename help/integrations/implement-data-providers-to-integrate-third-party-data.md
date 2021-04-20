---
title: 데이터 제공업체를 구현하여 제3자 데이터를 통합하는 방법
description: 이 자습서에서는 Adobe Target의 데이터 공급자 기능을 사용하여 타사 데이터 공급자의 데이터를 검색하고 Target 요청에 전달하는 방법에 대한 구현 세부 사항과 예제를 제공합니다.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# [!UICONTROL 데이터 공급자]를 구현하여 타사 데이터를 Adobe Target에 통합합니다.

구현 세부 사항 및 Adobe Target의 [!UICONTROL 데이터 공급자] 기능을 사용하여 타사 데이터 공급자로부터 데이터를 검색하고 Target 요청에 전달하는 방법에 대한 예입니다.

>[!NOTE]
>
>[!UICONTROL 데이터 ] 제공자에게  `at.js` 1.3 이상 필요

## 데이터 공급자의 기본 구성 요소 구현

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

`dataProvider`의 기본 구성 요소 및 올바른 순서로 코드를 가져오는 방법에 대한 간단한 개요입니다.\
비디오에 사용된 코드에 대한 작업 예는 다음과 같습니다.
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 타사 API와 통합

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

날씨 API를 통합하는 보다 현실적인 예.\
비디오에 사용된 코드에 대한 작업 예는 다음과 같습니다.
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 여러 제공업체와 통합

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

여러 공급자의 데이터를 전역 [!DNL Target] 요청에 통합하는 방법입니다.\
비디오에 사용된 코드에 대한 작업 예는 다음과 같습니다.
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 페이지 로드 영향 최소화

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

세션 저장소 개체에 데이터를 저장하여 페이지 로드 시간에 대한 영향을 최소화할 수 있습니다. 또는 `profile.` 접두어를 사용하여 값을 프로필 매개 변수로 전달하고 세션의 첫 번째 [!DNL Target] 요청에서 전달할 수도 있습니다. 그러나 요청당 50개의 프로필 매개 변수를 전달하도록 제한됩니다.

비디오에 사용된 코드에 대한 작업 예는 다음과 같습니다.[https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 지원 자료

* [Adobe Target에서 데이터 공급자 사용](use-data-providers-to-integrate-third-party-data.md)

* [데이터 공급자 설명서](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)