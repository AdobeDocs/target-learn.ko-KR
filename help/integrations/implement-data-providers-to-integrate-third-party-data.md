---
title: 데이터 제공업체를 구현하여 타사 데이터를 Adobe Target에 통합
seo-title: 데이터 제공업체를 구현하여 타사 데이터를 Adobe Target에 통합
description: 구현 세부 사항 및 Adobe Target 데이터 공급자 기능을 사용하여 타사 데이터 공급자로부터 데이터를 검색하고 Target 요청에 전달하는 방법에 대한 예입니다.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# 데이터 [!UICONTROL 제공업체] 구현 - 타사 데이터를 Adobe Target에 통합

Implementation details and examples of how to use Adobe Target&#39;s [!UICONTROL Data Providers] feature to retrieve data from third-party data providers and pass it in the Target request.

>[!NOTE]
>
>[!UICONTROL 데이터 제공업체는] 1.3 `at.js` 이상이 필요합니다.

## 데이터 제공자의 기본 구성 요소 구현

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

A의 기본 구성 요소 `dataProvider` 와 올바른 순서로 코드를 얻는 방법에 대한 간략한 개요입니다.\
비디오에 사용된 코드의 작업 예는 다음 사이트에서 찾을 수 있습니다.
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 타사 API와 통합

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

날씨 API를 통합하는 보다 현실적인 예.\
비디오에 사용된 코드의 작업 예는 다음 사이트에서 찾을 수 있습니다.
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 여러 제공업체와 통합

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

여러 공급자의 데이터를 글로벌 [!DNL Target] 요청에 통합하는 방법\
비디오에 사용된 코드의 작업 예는 다음 사이트에서 찾을 수 있습니다.
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 페이지 로드 영향 최소화

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

세션 저장소 개체에 데이터를 저장하여 페이지 로드 시간에 대한 영향을 최소화합니다. 또는 접두사를 사용하여 값을 프로필 매개 변수로 전달하여 세션의 첫 번째 요청에 전달하기만 하면 `profile.` [!DNL Target] 됩니다. 그러나 요청당 50개의 프로필 매개 변수를 전달하도록 제한됩니다.

비디오에 사용된 코드의 작업 예는 다음 사이트에서 찾을 수 있습니다. [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 지원 자료

* [Adobe Target과 함께 데이터 공급자 사용](use-data-providers-to-integrate-third-party-data.md)

* [데이터 제공업체 설명서](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)