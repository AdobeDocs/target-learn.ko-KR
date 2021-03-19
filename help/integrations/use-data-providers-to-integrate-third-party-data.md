---
title: 데이터 공급자를 사용하여 제3자 데이터를 통합하는 방법
description: 이 자습서에서는 데이터 공급자를 사용하는 사용자를 소개합니다. 데이터 공급자 기능을 사용하여 제3자의 데이터를 Adobe Target으로 쉽게 전달하는 방법을 알아봅니다.
role: 비즈니스 전문가, 개발자
level: 경험
topic: 개인화, 통합
feature: 구현, 통합, API/SDK
doc-type: feature video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 22%

---


# 데이터 공급자를 사용하여 제3자 데이터를 Adobe Target에 통합

[!UICONTROL 데이터 공급자는 타사의 데이터를 Target에 쉽게 전달할 수 있는 기능입니다.  ]  타사는 기상 서비스, DMP 또는 자체 웹 서비스일 수 있습니다. 그런 다음, 이 데이터를 사용하여 대상, Target 콘텐츠를 작성하고 방문자 프로필을 보강할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 데이터 공급자 사용 방법

1. 구현 전문가는 API를 제3자에 호출하고 응답을 구문 분석하여 응답에서 [!DNL Target]으로 보낼 이름/값 쌍으로 지정하는 at.js(또는 at.js의 라이브러리 헤더 섹션) 앞에 코드를 추가합니다.
1. at.js는 깜박임을 관리하고 글로벌 Target 요청에 이름/값 쌍을 사용자 정의 매개 변수로 포함합니다.
1. 마케터는 이러한 사용자 지정 매개 변수를 기반으로 [!DNL Target] 인터페이스에서 대상을 만듭니다.
1. 마케터는 이러한 대상을 보고 대상뿐만 아니라 경험, 활동 및 지표를 타깃팅하기 위해 사용합니다.

>[!NOTE]
>
>[!UICONTROL 데이터 ] 제공자에게 at.js 1.3 이상이 필요합니다.

## 지원 자료

* [at.js 및 Adobe Target에서 데이터 공급자 구현](implement-data-providers-to-integrate-third-party-data.md)
* [데이터 공급자 설명서](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)