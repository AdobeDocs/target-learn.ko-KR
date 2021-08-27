---
title: 데이터 공급자를 사용하여 타사 데이터를 통합하는 방법
description: 이 자습서에서는 사용자를 데이터 공급자에 대해 소개합니다. 데이터 공급자 기능을 사용하여 타사의 데이터를 Adobe Target에 쉽게 전달하는 방법을 알아봅니다.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
thumbnail: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 데이터 공급자를 사용하여 Adobe Target에 타사 데이터 통합

[!UICONTROL 데이터 공급자는 타사의 데이터를 Target에 쉽게 전달할 수 있는 기능입니다.  ]  타사는 기상 서비스, DMP 또는 자체 웹 서비스일 수 있습니다. 그런 다음, 이 데이터를 사용하여 대상, Target 콘텐츠를 작성하고 방문자 프로필을 보강할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 데이터 공급자 사용 방법

1. 구현 전문가는 타사에 API를 호출하는 at.js(또는 at.js의 라이브러리 헤더) 앞에 코드를 추가하고, 응답을 구문 분석하고, [!DNL Target]로 전송할 응답의 이름/값 쌍으로 지정합니다.
1. at.js는 플리커를 관리하고 글로벌 Target 요청에 이름/값 쌍을 사용자 지정 매개 변수로 포함합니다.
1. 마케터는 이러한 사용자 지정 매개 변수를 기반으로 하여 [!DNL Target] 인터페이스에서 대상을 만듭니다.
1. 마케터는 이러한 대상을 사용하여 보고 대상뿐만 아니라 경험, 활동 및 지표를 타깃팅합니다.

>[!NOTE]
>
>[!UICONTROL 데이터 ] 공급자는 at.js 1.3 이상이 필요합니다

## 지지 자료

* [at.js 및 Adobe Target에서 데이터 공급자 구현](implement-data-providers-to-integrate-third-party-data.md)
* [데이터 공급자 설명서](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en#data-providers)
