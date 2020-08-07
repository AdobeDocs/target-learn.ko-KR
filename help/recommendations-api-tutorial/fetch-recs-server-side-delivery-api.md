---
title: 배달 API를 사용하여 Recommendations 가져오기
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations에는 추천 제품 및/또는 컨텐츠 카탈로그를 관리할 수 있는 전용 API 세트가 포함되어 있습니다. 추천 알고리즘 및 캠페인 관리 웹, 모바일, 이메일, IOT 및 기타 채널에 표시될 JSON, HTML 또는 XML 객체에 대한 권장 사항을 전달할 수 있습니다.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 7265fd8611aacc94d1a66c10cd641c0644f2d43f
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 0%

---


# 배달 API [!DNL Recommendations] 로 가져오기

Adobe Target 및 Adobe Target [!DNL Recommendations] API를 사용하여 웹 페이지에 대한 응답을 제공할 수 있지만 앱, 스크린, 콘솔, 이메일, 키오스크 및 기타 디스플레이 장치 등 비 HTML 기반 경험에서도 사용할 수 있습니다. 즉, 라이브러리와 JavaScript를 [!DNL Target] 사용할 수 없는 경우에도 **[!DNL Target]전달 API **기능을 통해 개인화된 경험을 전달하는[!DNL Target]데 필요한 모든 기능을 이용할 수 있습니다.

>[!NOTE]
>
> 실제 권장 사항이 포함된 컨텐츠(권장 제품 또는 항목)를 요청하는 경우 [!DNL Target] 배달 API를 사용하십시오.

권장 사항을 검색하려면 사용자 ID(사용자가 최근에 본 항목과 같은 프로필 관련 권장 사항과 함께 사용하기 위해)를 포함하는 적절한 컨텍스트 정보와 함께 Adobe Target 배달 API POST 호출을 전송하십시오. 이 호출에는 사용자 ID, 관련 mbox 이름, mbox 매개 변수, 프로필 매개 변수 또는 기타 속성이 포함될 수 있습니다. 응답에는 JSON 또는 HTML 형식으로 권장된 entity.ids(및 기타 엔티티 데이터를 포함할 수 있음)가 포함되며, 이러한 데이터는 장치에 표시될 수 있습니다.

Adobe Target [용](https://developers.adobetarget.com/api/delivery-api/) 배달 API는 표준 [!DNL Target] 요청에서 제공하는 모든 기존 기능을 노출합니다.

>[!NOTE]
>배달 API:
>* 위치 및 대상에 대한 경험이나 오퍼를 RESTful 방식으로 검색할 수 있습니다.
>* 인증이 필요 없습니다.
>* POST만.
>* 쿠키 또는 리디렉션 호출을 처리하지 않습니다.
>* &quot;사용자 역할&quot;이 필요하거나 인식되지 않습니다. 컨텐츠 또는 보고서 이벤트를 Edge Server에 간단하게 [!DNL Target] 가져옵니다.


배달 API를 사용하여 권장 사항을 포함한 [!DNL Target] 경험을 전달하려면 다음 단계를 수행하십시오.

1. Visual Experience Composer가 아닌 양식 기반 컴포저를 사용하여 [!DNL Target] 활동(A/B, XT, AP 또는 [!DNL Recommendations])을 만듭니다.
2. 배달 API를 사용하여 방금 만든 활동에 의해 생성된 요청에 대한 응답을 [!DNL Target] 얻습니다.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## 양식 기반 Experience Composer를 사용하여 권장 사항 만들기

전달 API와 함께 사용할 수 있는 권장 사항을 만들려면 [양식 기반 작성기를 사용하십시오](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html).

1. 먼저 권장 사항에 사용할 JSON 기반 디자인을 만들어 저장합니다. 샘플 JSON과 양식 기반 활동을 구성할 때 JSON 응답을 반환할 수 있는 방법에 대한 배경 정보는 권장 사항 디자인 [만들기에 대한 설명서를 참조하십시오](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html). 이 예에서 디자인 이름은 *Simple JSON입니다.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. 활동 [!DNL Target]> 활동 **[!UICONTROL 만들기]>[!UICONTROL Recommendations]으로 이동한 다음****** Form을 선택합니다.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. 속성을 선택하고 다음을 **[!UICONTROL 클릭합니다]**.
4. 사용자가 권장 사항의 응답을 받을 위치를 정의합니다. 아래 예제는 *api_charter라는 위치를 사용합니다*. 앞서 만든 JSON 기반의 디자인을 *간단한 JSON이라고 합니다.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. 권장 사항을 저장하고 활성화합니다. 결과가 나올 것입니다. [결과가 준비되면](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html)배달 API를 사용하여 결과를 검색할 수 있습니다.

## 배달 API 사용

The syntax for the [Delivery API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) is:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 클라이언트 코드가 필요합니다. 다시 말해, 클라이언트 코드는 **[!UICONTROL Recommendations]>[!UICONTROL 설정으로 이동하여 Adobe Target에서 찾을 수 있습니다]**. 권장 사항 **[!UICONTROL API 토큰]** 섹션의 **[!UICONTROL 클라이언트 코드]** 값을확인하십시오.
   ![client-code.png](assets/client-code.png)
1. 클라이언트 코드가 있으면 배달 API 호출을 구성합니다. 아래 예제는 **[!UICONTROL 배달 API Postman 컬렉션]** 에서 제공되는 [웹 일괄적인 Mbox 배달 API 호출로](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)시작하여 관련 사항을 수정합니다. 예:
   * HTML이 아닌 **경우** **브라우저** 및 **주소**&#x200B;개체가 필요하지 않으므로본문에서제거되었습니다.
   * *이 예에서는 api_charter* 이름이 위치 이름으로 나열됩니다.
   * 이 권장 사항은 현재 항목 키를 전달해야 하는 컨텐트 유사성을 기반으로 하므로 entity.id가 지정됩니다 [!DNL Target].
      ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)쿼리 매개 변수를 올바르게 구성해야 합니다. 예를 들어 필요에 따라 지정해야`{{CLIENT_CODE}}` 합니다. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. 요청 전송 이 작업은 권장 개체 목록을 출력할 JSON 디자인으로 정의된 활성 권장 사항이 *있는 api_charter* 위치에 대해 실행됩니다.
1. JSON 디자인에 따라 응답을 받을 수 있습니다.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)이 응답에는 권장 개체의 개체 ID와 키 ID가 포함됩니다.

이 방법 [!DNL Recommendations] 으로 배달 API를 사용하면 HTML이 아닌 장치에서 방문자에게 권장 사항을 표시하기 전에 추가 단계를 수행할 수 있습니다. 예를 들어, 최종 결과를 표시하기 전에 배달 API의 응답을 가져와 다른 시스템(예: CMS, PIM 또는 전자 상거래 플랫폼)에서 엔티티 속성 세부 사항(재고, 가격, 등급 등)에 대한 추가적인 실시간 조회를 수행할 수 있습니다.

이 튜토리얼에서 설명한 방법을 사용하면 모든 애플리케이션에서 응답을 활용하여 개인화된 권장 사항을 제공할 수 [!DNL Target] 있습니다.

## 구현 예제

다음 리소스는 HTML이 아닌 다양한 구현의 예를 제공합니다. 관련된 시스템 및 디바이스로 인해 모든 구현이 고유해야 한다는 점을 명심하십시오.

| 리소스 | 세부 사항 |
| --- | --- |
| [AEM에서 RESTful API 사용](https://helpx.adobe.com/experience-manager/using/restful-services.html) | 타사 RESTful 웹 서비스의 데이터를 사용하는 Adobe Experience Manager OSGi 번들을 만들고 배포하는 방법 |
| [Adobe Target 어디서나 - 서버 쪽 또는 IoT에서 구현](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Target 서버측 API를 활용하는 React 애플리케이션에 대한 실습 경험을 제공하는 Adobe Summit 2019 Lab |
| [Adobe SDK가 없는 모바일 앱의 Adobe Target](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 이 안내서에서는 Adobe SDK를 설치하지 않고 모바일 앱에서 Adobe Target을 설정하는 방법을 보여 줍니다. 이 솔루션은 Telium SDK 웹 뷰와 원격 명령 모듈을 사용하여 Adobe 방문자 API(Experience Cloud) 및 Adobe Target API에 요청을 보내고 받습니다. |
| [모바일 앱의 Adobe Target 작동 방식](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Mobile SDK [!DNL Target] 사용 방법 |
| [API [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] 구성](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Experience Platform Launch에서 확장 [!DNL Target] 기능을 구성하고, 앱에 [!DNL Target] 익스텐션을 추가하고, 작업 요청, 프리페치 오퍼 및 시각적 미리 보기 모드 시작을 위한 [!DNL Target] API를 구현하는 단계입니다. |
| [Adobe Target 노드 클라이언트](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 오픈 소스 [!DNL Target] Node.js SDK v1.0 |
| [서버측 개요](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Adobe Target 서버측 배달 API, 서버측 배치 배달 API, Node.js SDK 및 Adobe Target API에 대한 [!DNL Recommendations] 정보입니다. |
| [Adobe Campaign 콘텐츠 Recommendations(이메일)](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Adobe Campaign의 Adobe Target과 Adobe I/O Runtime을 통해 이메일에서 컨텐츠 추천을 활용하는 방법을 설명하는 블로그입니다. |

## API를 [!DNL Recommendations] 사용하여 설정 관리

대부분의 경우, 권장 사항은 위의 섹션에 언급된 것과 같은 이유로 Adobe Target UI에서 구성한 다음 [!DNL Target] API를 통해 사용되거나 액세스됩니다. 이 UI-API 조정은 일반적으로 사용됩니다. 하지만 사용자는 API를 통해 설정뿐만 아니라 결과의 사용 모두 모든 작업을 수행할 수 있습니다. 일반적으로 사용되지 않지만, 사용자는 API를 사용하여 권장 사항 *의 결과를 절대적으로 구성, 실행 및* 활용할 수 있습니다.

Adobe Target Recommendations 개체를 관리하고 서버측에서 제공하는 방법을 [이전 섹션](manage-catalog.md) 에서 배웠습니다. 마찬가지로 Adobe I/O를 사용하면 Adobe Target에 로그인하지 않고도 조건, 프로모션, 컬렉션 및 디자인 템플릿을 관리할 수 있습니다. 모든 API의 전체 목록은 [!DNL Recommendations] 여기에서 [](http://developers.adobetarget.com/api/recommendations/)찾을 수 있지만 여기에 참조 요약이 있습니다.

| 리소스 | 세부 사항 |
| --- | --- |
| [컬렉션](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | 컬렉션 목록 작성, 가져오기, 편집 및 삭제 |
| [기준](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | 목록 작성 및 기준 가져오기 |
| [디자인](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | 디자인을 목록 작성, 가져오기, 편집, 삭제 및 확인할 수 있습니다. |
| [엔티티](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | 엔티티를 저장, 삭제 및 가져옵니다. |
| [프로모션](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | 홍보 목록 작성, 가져오기, 편집 및 삭제 |
| [범주 기준](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | 범주 기준을 목록 작성, 가져오기, 편집 및 삭제합니다. |
| [사용자 지정 기준](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | 사용자 지정 기준을 목록 작성, 가져오기, 편집 및 삭제합니다. |
| [품목 기준](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | 항목 기준을 목록 작성, 가져오기, 편집 및 삭제합니다. |
| [인기 기준](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | 인기 기준을 목록 작성, 가져오기, 편집 및 삭제합니다. |
| [프로필 속성 기준](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | 프로필 속성 기준을 목록, 만들기, 가져오기, 편집 및 삭제합니다. |
| [최근 기준](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | 최근 기준을 목록 작성, 가져오기, 편집 및 삭제합니다. |
| [시퀀스 기준](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | 시퀀스 기준을 목록 작성, 가져오기, 편집 및 삭제합니다. |

## 참조 설명서

* [Adobe Target API 설명서](https://developers.adobetarget.com/api/#getting-started)
* [Adobe Target 배달 API](https://developers.adobetarget.com/api/delivery-api/)
* [이메일과 [!DNL Recommendations] 통합](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## 요약 및 검토

축하합니다! 이 튜토리얼을 완료하면 다음과 같은 방법을 배울 수 있습니다.
* [Recommendations API를 사용하여 카탈로그 관리](manage-catalog.md)
* [Recommendations API를 사용하여 사용자 지정 기준 관리](manage-custom-criteria.md)
* [Delivery API와 Recommendations 사용](fetch-recs-server-side-delivery-api.md)
