---
title: Adobe Recommendations API 소개
description: 이 자습서에서는 Adobe Target Recommendations API를 사용하여 Recommendations 카탈로그 및 사용자 지정 기준을 구성 및 관리하고 배달 API를 사용하여 추천 컨텐츠를 검색하는 실습 연습을 안내합니다.
role: Developer
level: 중간
topic: 개인화, 관리, 통합, 개발
feature: API/SDK, Recommendations, 관리 및 구성, 개요
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 1%

---


# Adobe Recommendations API 개요

[!DNL Recommendations]과(와) 관련된 API에는 다음과 같은 작업을 할 수 있는 [관리 API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)가 포함됩니다.

* 추천 제품 또는 컨텐츠 카탈로그 관리
* [!DNL Recommendations] 알고리즘 및 활동 관리

Recommendations과 함께 [!DNL Target] [배달 API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)를 사용하면 다음 작업을 수행할 수도 있습니다.

* 웹, 모바일, 이메일, IOT(Internet of Things) 및 기타 채널에 표시될 수 있도록 JSON, HTML 또는 XML 개체에서 추천을 검색할 수 있습니다.

## 자습서 설명

이 자습서에서는 개발자가 [!DNL Recommendations] API를 사용하여 [!DNL Recommendations] 카탈로그 및 사용자 지정 기준을 구성 및 관리하고 배달 API를 사용하여 추천 컨텐츠를 검색하는 실습 연습을 안내합니다. 이 튜토리얼을 통해 다음과 같은 작업을 수행할 수 있습니다.

* Recommendations API를 사용하여 엔티티 구성 및 관리
* Recommendations API를 사용하여 사용자 지정 기준 구성 및 관리
* 배달 API와 함께 Recommendations을 사용하여 HTML 이외의 장치에서 권장 사항 결과를 사용하는 방법에 대해 알아봅니다.

## 대상자

이 자습서는 Target API 또는 Recommendations API를 처음 사용하는 개발자를 위해 제작되었습니다.

## 전제 조건

Target 관리 API를 사용하려면 [Adobe 인증 설정](../apis/configure-io-target-integration.md)이 필요합니다. 이 튜토리얼을 시작하기 전에 이 설정을 구성해야 합니다.

## 리소스

이 튜토리얼을 이해하고 이를 성공적으로 따르는 데 필요한 다음 리소스를 참조하십시오.

| 리소스 | 세부 사항 |
| --- | --- |
| Postman | 운영 체제용 [Postman 앱](https://www.postman.com/downloads/)을 가져옵니다. Postman basic은 계정 생성으로 무료입니다. 일반적으로 Adobe Target API를 사용하기 위해 필요하지 않지만, Postman은 API 워크플로우를 보다 쉽게 만들고, Adobe Target은 API를 실행하고 작동 방식을 배우는 데 도움이 되는 여러 Postman 컬렉션을 제공합니다. 이 자습서의 나머지 부분에서는 Postman에 대한 작업 지식을 가정합니다. 도움이 필요한 경우 [포스트맨 설명서](https://learning.getpostman.com/)를 참조하십시오. |
| 참조 | 이 자습서의 나머지 부분에서는 다음 리소스에 대해 잘 알고 있다고 가정합니다.<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Target Adobe I/O 설명서](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API 설명서](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[다음 &quot;Recommendations 카탈로그 관리&quot; >](manage-catalog.md)
