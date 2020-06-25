---
title: 데이터 제공업체를 사용하여 타사 데이터를 Adobe Target에 통합
seo-title: 데이터 제공업체를 사용하여 타사 데이터를 Adobe Target에 통합
description: 데이터 공급자는 타사의 데이터를 Target에 쉽게 전달할 수 있는 기능입니다.  타사는 기상 서비스, DMP 또는 자체 웹 서비스일 수 있습니다. 그런 다음, 이 데이터를 사용하여 대상, Target 콘텐츠를 작성하고 방문자 프로필을 보강할 수 있습니다.
audience: marketer
difficulty: 5
author: Daniel Wright
doc-type: use
activity-type: feature-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 40%

---


# 데이터 제공업체를 사용하여 타사 데이터를 Adobe Target에 통합

[!UICONTROL 데이터 공급자는 타사의 데이터를 Target에 쉽게 전달할 수 있는 기능입니다.  ]  타사는 기상 서비스, DMP 또는 자체 웹 서비스일 수 있습니다. 그런 다음, 이 데이터를 사용하여 대상, Target 콘텐츠를 작성하고 방문자 프로필을 보강할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 데이터 공급자 사용 방법

1. 구현 전문가는 API를 서드 파티에 호출하고, 응답을 구문 분석하고, 전송할 응답의 이름/값 쌍을 포함하는 at.js(또는 at.js의 라이브러리 헤더 섹션) 앞에 코드를 추가합니다 [!DNL Target].
1. at.js는 flicker를 관리하고 전역 Target 요청에 사용자 지정 매개 변수로 이름/값 쌍을 포함합니다.
1. 마케터는 이러한 사용자 지정 매개 변수를 기반으로 [!DNL Target] 인터페이스에서 대상을 구성합니다.
1. 마케터는 이러한 고객을 사용하여 고객 경험, 활동 및 지표뿐만 아니라 보고 대상을 타깃팅합니다.

>[!NOTE]
>
>[!UICONTROL 데이터 제공자는] at.js 1.3 이상이 필요합니다.

## 지원 자료

* [at.js 및 Adobe Target에서 데이터 공급자 구현](implement-data-providers-to-integrate-third-party-data.md)
* [데이터 제공업체 설명서](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)