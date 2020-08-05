---
title: Adobe Target API 개요
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations에는 추천 제품 및/또는 컨텐츠 카탈로그를 관리할 수 있는 전용 API 세트가 포함되어 있습니다. 추천 알고리즘 및 캠페인 관리 웹, 모바일, 이메일, IOT 및 기타 채널에 표시될 JSON, HTML 또는 XML 객체에 대한 권장 사항을 전달할 수 있습니다.
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: b66dbae616c9559f5d1b7bbedf2d9b383840973b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# Adobe Target API 개요

Adobe Target API는 유형에 따라 그룹화할 수 있습니다.

| API 유형 | 이 기능을 통해 얻을 수 있는 이점 | 다운로드 링크 |
| --- | --- | --- |
| 관리 | 활동, 대상, 오퍼 및 기타 객체(엔티티, 기준, 디자인 등 포함 [!DNL Recommendations] )를 생성, 수정 및 삭제합니다. API [!DNL Recommendations] 는 관리자 API의 유형입니다.) | <UL><li>[Target 관리 API Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman Collection](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul> |
| 배달 | 최종 사용자에게 전달할 최적화된 개인화된 컨텐츠 [!DNL Target] 를 검색할 수 있습니다. | [Target 배달 API Postman 컬렉션](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection) |
| 보고 | 활동 결과 및 기타 보고 결과를 내보낼 수 있습니다. | 보고 API는 [Target Admin API Postman 컬렉션 내에 포함되어 있습니다](https://developers.adobetarget.com/api/#admin-postman-collection). |
| 프로필 | Adobe Target에 저장된 사용자 프로필 검색 및 수정 | [Target 프로필 API Postman Collection](https://developers.adobetarget.com/api/#profiles) |

Adobe Target의 다양한 측면을 구성할 수 있는 **관리 API** ( [!DNL Recommendations] API 포함)와 컨텐츠를 검색할 수 있는 **배달 API**&#x200B;를구별할 수 있습니다. 관리 API는 인증이 필요한 반면 배달 API는 인증이 필요하지 않습니다.

Adobe Target 관리 API를 사용하려면 먼저 Adobe I/O를 사용하여 인증을 구성해야 합니다.

[다음 &quot;인증 구성&quot; >](configure-io-target-integration.md)
