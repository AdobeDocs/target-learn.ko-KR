---
title: Adobe Recommendations API 개요
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations에는 추천 제품 및/또는 컨텐츠 카탈로그를 관리할 수 있는 전용 API 세트가 포함되어 있습니다.추천 알고리즘 및 캠페인 관리웹, 모바일, 이메일, IOT 및 기타 채널에 표시될 JSON, HTML 또는 XML 객체에 대한 권장 사항을 전달할 수 있습니다.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---


# Adobe Recommendations API 개요

귀하를 허용하는 [!DNL Recommendations] 관리 [API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) 포함 관련 API:

* 추천 제품 또는 컨텐츠 카탈로그 관리
* 알고리즘 및 [!DNL Recommendations] 활동 관리

Recommendations과 함께 [!DNL Target] 배달 [API를](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) 사용하면 다음을 수행할 수 있습니다.

* 웹, 모바일, 이메일, IOT(Internet of Things) 및 기타 채널에 표시될 수 있도록 JSON, HTML 또는 XML 개체에서 추천을 검색할 수 있습니다.

## 자습서 설명

이 자습서에서는 개발자가 API를 사용하여 카탈로그 및 사용자 지정 기준을 구성 및 관리하고, 전달 API를 사용하여 추천 컨텐츠를 검색하는 실습 과정을 안내합니다. [!DNL Recommendations] [!DNL Recommendations] 이 튜토리얼을 종료하면 다음 작업을 수행할 수 있습니다.

* Recommendations API를 사용하여 엔티티 구성 및 관리
* Recommendations API를 사용하여 사용자 지정 기준 구성 및 관리
* 배달 API와 함께 Recommendations을 사용하여 HTML이 아닌 장치에서 추천 결과를 사용하는 방법을 이해합니다

## 대상자

이 자습서는 Target API 또는 Recommendations API를 처음 사용하는 개발자를 위해 마련되었습니다.

## 전제 조건

Target 관리 API를 사용하려면 [Adobe 인증 설정이 필요합니다](../apis/configure-io-target-integration.md). 이 튜토리얼을 시작하기 전에 이 설정을 구성해야 합니다.

## 리소스

이 튜토리얼을 이해하고 이 튜토리얼을 성공적으로 따르는 데 필요한 다음 리소스를 참조하십시오.

| 리소스 | 세부 사항 |
| --- | --- |
| 포스트맨 | 운영 체제용 [Postman 앱](https://www.postman.com/downloads/) 다운로드 Postman basic은 계정 생성으로 무료입니다. 일반적으로 Adobe Target API를 사용하기 위해 필요하지 않지만, Postman은 API 워크플로우를 보다 쉽게 만들고, Adobe Target은 API를 실행하고 작동 방식을 학습하는 데 도움이 되는 여러 Postman 컬렉션을 제공합니다. 이 자습서의 나머지 부분에서는 Postman에 대한 작업 지식을 가정합니다. 도움이 필요한 경우 [포스트맨 문서를 참조하십시오](https://learning.getpostman.com/). |
| 참조 | 이 자습서의 나머지 부분에서는 다음 리소스에 대해 잘 알고 있다고 가정합니다.<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Target Adobe I/O 설명서](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API 설명서](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[다음 &quot;Recommendations 카탈로그 관리&quot; >](manage-catalog.md)
