---
title: 배달 API를 사용하여 Recommendations 가져오기
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations에는 추천 제품 및/또는 컨텐츠 카탈로그를 관리할 수 있는 전용 API 세트가 포함되어 있습니다.추천 알고리즘 및 캠페인 관리;웹, 모바일, 이메일, IOT 및 기타 채널에 표시될 JSON, HTML 또는 XML 객체로 권장 사항을 전달할 수 있습니다.
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
source-wordcount: '1473'
ht-degree: 0%

---


# 배달 API를 사용하여 [!DNL Recommendations]을(를) 가져오는 중

Adobe Target 및 Adobe Target [!DNL Recommendations] API를 사용하여 웹 페이지에 대한 응답을 제공할 수 있지만 앱, 스크린, 콘솔, 이메일, 키오스크 및 기타 디스플레이 장치를 포함한 비 HTML 기반 경험에서도 사용할 수 있습니다. 즉, [!DNL Target] 라이브러리 및 JavaScript를 사용할 수 없는 경우에도 **[!DNL Target]배달 API**&#x200B;을 사용하면 [!DNL Target] 기능의 전체 범위에 액세스하여 개인화된 경험을 제공할 수 있습니다.

>[!NOTE]
>
> 실제 권장 사항이 포함된 컨텐트(권장 제품 또는 항목)를 요청하는 경우 [!DNL Target] 배달 API를 사용하십시오.

권장 사항을 검색하려면 적절한 컨텍스트 정보를 사용하여 Adobe Target 배달 API POST 호출을 전송하십시오. 이 정보에는 사용자 ID(사용자가 최근에 본 항목과 같은 프로필별 권장 사항과 함께 사용), 관련 mbox 이름, mbox 매개 변수, 프로필 매개 변수 또는 기타 속성이 포함될 수 있습니다. 응답에는 JSON 또는 HTML 형식으로 권장 entity.ids(및 다른 엔티티 데이터를 포함할 수 있음)가 포함되며, 이렇게 된 후 장치에 표시할 수 있습니다.

Adobe Target용 [배달 API](https://developers.adobetarget.com/api/delivery-api/)은 표준 [!DNL Target] 요청이 제공하는 모든 기존 기능을 표시합니다.

>[!NOTE]
>배달 API:
>* 위치 및 고객에 대한 경험이나 오퍼를 RESTful 방식으로 검색할 수 있습니다.
>* 인증이 필요하지 않습니다.
>* 게시물만.
>* 쿠키 또는 리디렉션 호출을 처리하지 않습니다.
>* &quot;사용자 역할&quot;이 필요하거나 인식되지 않습니다. 컨텐트나 이벤트를 [!DNL Target] Edge Server에 간단하게 보고합니다.


배달 API를 사용하여 권장 사항을 포함한 [!DNL Target] 경험을 제공하려면 다음 단계를 수행합니다.

1. 양식 기반 컴포저(Visual Experience Composer 아님)를 사용하여 [!DNL Target] 활동(A/B, XT, AP 또는 [!DNL Recommendations])을 만듭니다.
2. 배달 API를 사용하여 방금 만든 [!DNL Target] 활동에 의해 생성된 요청에 대한 응답을 가져옵니다.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## 양식 기반 Experience Composer를 사용하여 권장 사항 만들기

배달 API와 함께 사용할 수 있는 권장 사항을 만들려면 [양식 기반 컴포저](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)를 사용하십시오.

1. 먼저 권장 사항에 사용할 JSON 기반 디자인을 만들어 저장합니다. 샘플 JSON 및 양식 기반 활동을 구성할 때 JSON 응답을 반환할 수 있는 방법에 대한 배경 정보가 필요하면 [권장 사항 디자인 만들기](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html)의 설명서를 참조하십시오. 이 예에서 디자인 이름은 *단순 JSON입니다.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. [!DNL Target]에서 **[!UICONTROL 활동] > [!UICONTROL 활동 만들기] > [!UICONTROL Recommendations]**&#x200B;으로 이동한 다음 **[!UICONTROL 양식]**&#x200B;을 선택합니다.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. 속성을 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
4. 사용자에게 권장 사항의 응답을 받을 위치를 정의합니다. 아래 예제는 *api_charter*&#x200B;라는 위치를 사용합니다. 앞에서 만든 JSON 기반 디자인을 *간단한 JSON이라고 합니다.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. 권장 사항을 저장하고 활성화합니다. 결과가 생성됩니다. [결과가 준비되면](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html) 배달 API를 사용하여 결과를 검색할 수 있습니다.

## 배달 API 사용

[배달 API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API)의 구문은 다음과 같습니다.

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 클라이언트 코드가 필요합니다. 다시 말해서 클라이언트 코드는 **[!UICONTROL Recommendations] > [!UICONTROL 설정]**&#x200B;으로 이동하여 Adobe Target에서 찾을 수 있습니다. **[!UICONTROL 권장 사항 API 토큰]** 섹션의 **[!UICONTROL 클라이언트 코드]** 값을 확인하십시오.
   ![client-code.png](assets/client-code.png)
1. 클라이언트 코드가 있으면 배달 API 호출을 구성합니다. 아래 예제는 [배달 API 포스트만 컬렉션](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)에 제공된 **[!UICONTROL 웹 일괄 처리된 Mbox 배달 API 호출]**&#x200B;으로 시작하여 관련 수정을 수행합니다. 예:
   * 비HTML 사용 사례에는 필요하지 않으므로 **browser** 및 **address** 개체가 **Body**&#x200B;에서 제거되었습니다.
   * *api_* charteris가 이 예제에서 위치 이름으로 나열됩니다.
   * 이 권장 사항은 현재 항목 키를 [!DNL Target]으로 전달해야 하는 컨텐트 유사성을 기반으로 하므로 entity.id가 지정됩니다.
      ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
쿼리 매개 변수를 올바르게 구성해야 합니다. 예를 들어 
필요한 경우 `{{CLIENT_CODE}}`.<!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. 요청을 전송합니다. 이 작업은 권장 개체 목록을 출력할 JSON 디자인에 정의된 활성 권장 사항이 있는 *api_charter* 위치에 대해 실행됩니다.
1. JSON 디자인을 기반으로 응답을 받을 수 있습니다.
   ![server-side-create-recs-json-response2.](assets/server-side-create-recs-json-response2.png)
png 응답에는 권장 개체의 개체 ID와 키 ID가 포함됩니다.

이 방식으로 [!DNL Recommendations]과 함께 배달 API를 사용하면 HTML이 아닌 장치에서 방문자에게 권장 사항을 표시하기 전에 추가 단계를 수행할 수 있습니다. 예를 들어 최종 결과를 표시하기 전에 배달 API에서 응답을 가져와 다른 시스템(예: CMS, PIM 또는 전자 상거래 플랫폼)에서 엔티티 속성 세부 사항(재고, 가격, 등급 등)을 실시간으로 추가로 조회할 수 있습니다.

이 튜토리얼에서 설명한 접근 방법을 사용하여 [!DNL Target]의 응답을 활용하여 개인화된 권장 사항을 제공할 수 있습니다.

## 구현 예제

다음 리소스는 HTML이 아닌 다양한 구현의 예를 제공합니다. 관련된 시스템 및 디바이스 때문에 모든 구현이 고유해야 합니다.

| 리소스 | 세부 사항 |
| --- | --- |
| [AEM에서 RESTful API 사용](https://helpx.adobe.com/experience-manager/using/restful-services.html) | 제3자 RESTful 웹 서비스의 데이터를 사용하는 Adobe Experience Manager OSGi 번들을 만들고 배포하는 방법 |
| [Adobe Target Everywhere - 서버 측 또는 IoT에서 구현](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Target 서버측 API를 활용하는 React 애플리케이션에 대한 실습 경험을 제공하는 Adobe Summit 2019 Lab |
| [Adobe SDK가 없는 모바일 앱의 Adobe Target](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 이 안내서에서는 Adobe SDK를 설치하지 않고 모바일 앱에서 Adobe Target을 설정하는 방법을 보여 줍니다. 이 솔루션은 Telium SDK 웹 뷰와 원격 명령 모듈을 사용하여 Adobe 방문자 API(Experience Cloud) 및 Adobe Target API에 요청을 보내고 받습니다. |
| [모바일 앱에서 Adobe Target 작동 방식](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Mobile SDK에서 [!DNL Target]이(가) 작동하는 방식 |
| [API  [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] 구성](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Experience Platform Launch에서 [!DNL Target] 확장을 구성하고, 앱에 [!DNL Target] 확장을 추가하고, [!DNL Target] API를 구현하여 활동 요청, 프리페치 오퍼 및 시각적 미리 보기 모드 시작을 위한 단계입니다. |
| [Adobe Target 노드 클라이언트](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 오픈 소스 [!DNL Target] Node.js SDK v1.0 |
| [서버측 개요](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Adobe Target Server Side Delivery API, Server Side Batch Delivery API, Node.js SDK 및 Adobe Target [!DNL Recommendations] API에 대한 정보입니다. |
| [이메일의 Adobe Campaign 컨텐츠 Recommendations](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Adobe Campaign에서 Adobe Target 및 Adobe I/O Runtime을 통해 이메일에서 컨텐츠 권장 사항을 활용하는 방법을 설명하는 블로그입니다. |

## API를 사용하여 [!DNL Recommendations] 설정 관리

대부분의 경우, 권장 사항은 Adobe Target UI에서 구성한 다음, 위의 섹션에 언급된 것과 같은 이유로 [!DNL Target] API를 통해 사용되거나 액세스됩니다. 이 UI-API 조정은 일반적입니다. 하지만 사용자는 API를 통해 모든 작업(설정 및 결과 사용 모두)을 수행할 수 있습니다. 일반적이지 않지만, 사용자는 API를 사용하여 완전히 권장 사항의 결과를 구성 및 실행할 수 있습니다. *및*

Adobe Target Recommendations 개체를 관리하고 서버측을 제공하는 방법을 [이전 섹션](manage-catalog.md)에서 알아보았습니다. 마찬가지로 Adobe I/O을 사용하면 Adobe Target에 로그인하지 않고도 기준, 프로모션, 컬렉션 및 디자인 템플릿을 관리할 수 있습니다. 모든 [!DNL Recommendations] API의 전체 목록은 [여기](http://developers.adobetarget.com/api/recommendations/)에 있지만 여기에 참조 요약이 있습니다.

| 리소스 | 세부 사항 |
| --- | --- |
| [컬렉션](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | 컬렉션을 목록 작성, 만들기, 가져오기, 편집 및 삭제합니다. |
| [기준](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | 기준을 나열하고 가져옵니다. |
| [디자인](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | 디자인을 목록 작성, 생성, 가져오기, 편집, 삭제 및 확인할 수 있습니다. |
| [엔티티](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | 엔티티를 저장, 삭제 및 가져올 수 있습니다. |
| [프로모션](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | 프로모션을 목록 작성, 가져오기, 편집 및 삭제할 수 있습니다. |
| [카테고리 기준](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | 범주 기준을 목록, 만들기, 가져오기, 편집 및 삭제합니다. |
| [사용자 지정 기준](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | 사용자 지정 기준을 목록 작성, 생성, 가져오기, 편집 및 삭제합니다. |
| [품목 기준](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | 항목 기준을 나열, 만들기, 가져오기, 편집 및 삭제합니다. |
| [인기도 기준](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | 인기 기준을 목록 작성, 생성, 가져오기, 편집 및 삭제합니다. |
| [프로필 속성 기준](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | 프로필 속성 기준을 목록, 만들기, 가져오기, 편집 및 삭제합니다. |
| [최근 기준](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | 최근 기준을 목록 작성, 생성, 가져오기, 편집 및 삭제합니다. |
| [시퀀스 기준](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | 시퀀스 기준을 나열, 만들기, 가져오기, 편집 및 삭제할 수 있습니다. |

## 참조 설명서

* [Adobe Target API 설명서](https://developers.adobetarget.com/api/#getting-started)
* [Adobe Target 배달 API](https://developers.adobetarget.com/api/delivery-api/)
* [이메일 [!DNL Recommendations] 과 통합](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## 요약 및 검토

축하합니다! 이 튜토리얼을 완료하면 다음 방법을 배울 수 있습니다.
* [Recommendations API를 사용하여 카탈로그 관리](manage-catalog.md)
* [Recommendations API를 사용하여 사용자 지정 기준 관리](manage-custom-criteria.md)
* [Recommendations에서 배달 API 사용](fetch-recs-server-side-delivery-api.md)
