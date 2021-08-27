---
title: Adobe Recommendations API란?
description: 이 자습서에서는 Adobe Target Recommendations API를 사용하여 Recommendations 카탈로그 및 사용자 지정 기준을 구성 및 관리하고 게재 API를 사용하여 권장 사항 콘텐츠를 검색하는 실습 방법을 개발자에게 설명합니다.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Recommendations API 개요

[!DNL Recommendations]에 관련된 API에는 다음 작업을 수행할 수 있는 [관리 API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en)가 포함됩니다.

* 추천 제품 또는 컨텐츠 카탈로그를 관리합니다
* [!DNL Recommendations] 알고리즘 및 활동을 관리합니다

Recommendations에서 [!DNL Target] [배달 API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en)를 사용하여 다음을 수행할 수도 있습니다.

* 웹, 모바일, 이메일, IOT(Internet of Things) 및 기타 채널에 표시할 수 있도록 JSON, HTML 또는 XML 개체에서 권장 사항을 검색합니다.

## 자습서 설명

이 자습서에서는 [!DNL Recommendations] API를 사용하여 [!DNL Recommendations] 카탈로그 및 사용자 지정 기준을 구성 및 관리하고 배달 API를 사용하여 권장 사항 콘텐츠를 검색하는 실습 방법을 개발자에게 설명합니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* Recommendations API를 사용하여 엔티티 구성 및 관리
* Recommendations API를 사용하여 사용자 지정 기준 구성 및 관리
* 배달 API와 함께 Recommendations을 사용하여 HTML이 아닌 장치에서 권장 사항 결과를 사용하는 방법을 이해합니다

## 대상자

이 자습서는 API 또는 Recommendations API를 처음 사용하는 개발자를 위한 것입니다.

## 사전 요구 사항

Target 관리 API를 사용하려면 [Adobe 인증 설정](../apis/configure-io-target-integration.md)이 필요합니다. 이 자습서를 시작하기 전에 이 구성이 있는지 확인하십시오.

## 리소스

이 자습서를 이해하고 이를 성공적으로 따르는 데 필요한 다음 리소스를 확인합니다.

| 리소스 | 세부 사항 |
| --- | --- |
| 포스트맨 | 운영 체제에 대한 [Postman app](https://www.postman.com/downloads/)을 가져옵니다. Postman Basic은 계정 생성과 함께 무료입니다. 일반적으로 Adobe Target API를 사용하기 위해 필요하지 않지만 Postman을 사용하면 API 워크플로우를 보다 쉽게 만들 수 있고 Adobe Target에서는 API를 실행하고 작동 방법을 학습하는 데 도움이 되는 여러 Postman 컬렉션을 제공합니다. 이 자습서의 나머지 부분에서는 Postman에 대한 작업 지식을 가정합니다. 도움이 필요하면 [Postman 설명서](https://learning.getpostman.com/)를 참조하십시오. |
| 참조 | 이 자습서의 나머지 부분에서 다음 리소스에 익숙하다고 가정합니다.<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Target Adobe I/O 설명서](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API 설명서](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[다음 &quot;Recommendations 카탈로그 관리&quot; >](manage-catalog.md)
