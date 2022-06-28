---
title: 배달 API를 사용하여 Recommendations을 가져오는 방법
description: 이 자습서 부분에서는 개발자가 Adobe Target 배달 API를 사용하여 권장 사항 콘텐츠를 가져오는 데 필요한 단계를 안내합니다.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 553d1208-647f-479d-acc7-d7760469d642
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 1%

---

# 가져오기 [!DNL Recommendations] 배달 API 사용

Adobe Target 및 Adobe Target [!DNL Recommendations] API는 웹 페이지에 대한 응답을 전달하는 데 사용할 수 있지만 앱, 스크린, 콘솔, 이메일, 키오스크 및 기타 디스플레이 장치를 포함한 HTML을 기반으로 하지 않는 환경에서도 사용할 수 있습니다. 즉, [!DNL Target] 라이브러리와 JavaScript는 사용할 수 없습니다. **[!DNL Target]배달 API** 여전히 [!DNL Target] 개인화된 경험을 제공하는 기능입니다.

>[!NOTE]
>
> 실제 권장 사항(권장 제품 또는 항목)이 포함된 콘텐츠를 요청할 때는 [!DNL Target] 배달 API.

권장 사항을 검색하려면 적절한 컨텍스트 정보를 사용하여 Adobe Target 배달 API POST 호출을 전송하십시오. 여기에는 사용자 ID(사용자가 최근에 본 항목과 같은 프로필 관련 권장 사항과 함께 사용), 관련 mbox 이름, mbox 매개 변수, 프로필 매개 변수 또는 기타 속성이 포함될 수 있습니다. 응답에는 JSON 또는 HTML 형식으로 권장 entity.ids(및 다른 엔티티 데이터를 포함할 수 있음)가 포함되며, 그런 다음 장치에 표시할 수 있습니다.

다음 [배달 API](https://developer.adobe.com/target/implement/delivery-api/)Adobe Target에 대한 {target=_blank} 표준 [!DNL Target] 요청 제공.

>[!NOTE]
>배달 API:
>* 위치 및 대상에 대한 경험이나 오퍼를 RESTful 방식으로 검색할 수 있습니다.
>* 인증이 필요하지 않습니다.
>* POST만
>* 쿠키나 리디렉션 호출을 처리하지 않습니다.
>* &quot;사용자 역할&quot;이 필요하거나 인식되지 않습니다. 콘텐츠나 보고서 이벤트를 [!DNL Target] edge server.


배달 API를 사용하여 전달하려면 [!DNL Target] 경험—권장 사항 포함—다음 단계를 수행합니다.

1. 만들기 [!DNL Target] 활동(A/B, XT, AP 또는 [!DNL Recommendations]) 양식 기반 작성기(시각적 경험 작성기가 아님)를 사용하여 다음을 수행합니다.
2. 배달 API를 사용하여 [!DNL Target] 방금 만든 활동입니다.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## 양식 기반 경험 작성기를 사용하여 권장 사항 만들기

배달 API와 함께 사용할 수 있는 권장 사항을 만들려면 [양식 기반 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

1. 먼저 추천에 사용할 JSON 기반 디자인을 만들어 저장합니다. 샘플 JSON과 양식 기반 활동을 구성할 때 JSON 응답을 반환할 수 있는 방법에 대한 배경 정보가 필요하면 설명서를 참조하십시오. [권장 사항 디자인 만들기](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=en). 이 예제에서 디자인 이름은 입니다 *단순 JSON.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. in [!DNL Target], 다음 위치로 이동합니다. **[!UICONTROL 활동] > [!UICONTROL 활동 만들기] > [!UICONTROL Recommendations]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 양식]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. 속성을 선택하고 **[!UICONTROL 다음]**.
4. 사용자가 권장 사항의 응답을 받을 위치를 정의합니다. 아래 예에서는 라는 위치를 사용합니다 *api_charter*. 앞에서 만든, 이름이 인 JSON 기반 디자인을 선택합니다 *단순 JSON.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. 권장 사항을 저장하고 활성화합니다. 결과가 생성됩니다. [결과가 준비되면](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html?lang=en), 배달 API를 사용하여 검색할 수 있습니다.

## 배달 API 사용

의 구문 [배달 API](https://developer.adobe.com/target/implement/delivery-api/#tag/Delivery-API){target=_blank}:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 클라이언트 코드가 필요합니다. 미리 알림으로 클라이언트 코드는 다음 위치로 이동하여 Adobe Target에서 찾을 수 있습니다 **[!UICONTROL Recommendations] > [!UICONTROL 설정]**. 참고 사항 **[!UICONTROL 클라이언트 코드]** 값에서 **[!UICONTROL 권장 사항 API 토큰]** 섹션을 참조하십시오.
   ![client-code.png](assets/client-code.png)
1. 클라이언트 코드가 있으면 배달 API 호출을 구성합니다. 아래 예제는 **[!UICONTROL 웹 일괄 처리 Mbox 배달 API 호출]** 에서 제공 [배달 API Postman 컬렉션](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection), 관련 수정 사항 만들기 예:
   * a **브라우저** 및 **주소** 객체가 **본문** HTML 이외의 사용 사례에는 필요하지 않으므로
   * *api_charter* 이 예제에서는 위치 이름으로 나열됩니다
   * 이 권장 사항은 현재 항목 키를 전달해야 하는 콘텐츠 유사성을 기반으로 하므로 entity.id가 지정됩니다. [!DNL Target].
      ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
쿼리 매개 변수를 올바르게 구성해야 합니다. 예를 들어 
`{{CLIENT_CODE}}` 필요한 경우. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. 요청을 보냅니다. 이 실행은 *api_charter* 에서 실행 중인 활성 권장 사항이 있는 위치는 JSON 디자인에서 정의되며, 권장 엔티티 목록을 출력합니다.
1. JSON 디자인을 기반으로 응답을 수신합니다.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
응답에는 키 ID와 권장 엔티티의 엔티티 ID가 포함됩니다.

배달 API 사용 [!DNL Recommendations] 이 방법을 사용하면 비HTML 장치에서 방문자에게 권장 사항을 표시하기 전에 추가 단계를 수행할 수 있습니다. 예를 들어, 최종 결과를 표시하기 전에 배달 API의 응답을 받아 다른 시스템(예: CMS, PIM 또는 전자 상거래 플랫폼)에서 엔티티 속성 세부 사항(재고, 가격, 등급 등)에 대한 추가적인 실시간 조회를 수행할 수 있습니다.

이 자습서에 요약된 접근 방식을 사용하여 모든 애플리케이션에서 응답을 활용할 수 있습니다. [!DNL Target] 개인화된 추천을 제공합니다.

## 구현 예제

다음 리소스는 다양한 비HTML 구현의 예를 제공합니다. 관련된 시스템 및 장치 때문에 모든 구현은 고유합니다.

| 리소스 | 세부 사항 |
| --- | --- |
| [Adobe Target 어디에서나 - 서버 측 또는 IoT에서 구현](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Target 서버측 API를 활용하는 React 애플리케이션에 대한 실습 경험을 제공하는 Adobe Summit 2019 Lab |
| [Adobe SDK가 없는 모바일 앱의 Adobe Target](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 이 안내서에서는 Adobe SDK를 설치하지 않고 모바일 앱에서 Adobe Target을 설정하는 방법을 보여줍니다. 이 솔루션은 Telium SDK 웹 보기 및 원격 명령 모듈을 사용하여 Adobe 방문자 API(Experience Cloud) 및 Adobe Target API에 요청을 보내고 받습니다. |
| [모바일 앱에서의 Adobe Target 작동 방식](https://experienceleague.adobe.com/docs/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html?lang=en) | 방법 [!DNL Target] mobile SDK를 사용한 작업 |
| [구성 [!DNL Target] 확장 및 구현 [!DNL Target] API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | 구성 단계 [!DNL Target] 확장, Experience Platform Launch 추가 [!DNL Target] 앱으로 확장 및 구현 [!DNL Target] 활동을 요청하고, 오퍼를 미리 가져오며, 시각적 미리 보기 모드로 전환하기 위한 API입니다. |
| [Adobe Target 노드 클라이언트](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 오픈 소스 [!DNL Target] Node.js SDK v1.0 |
| [서버 측 개요](https://experienceleague.adobe.com/docs/target/using/implement-target/server-side/api-and-sdk-overview.html?lang=en) | Adobe Target 서버 측 배달 API, 서버 측 배치 배달 API, Node.js SDK 및 Adobe Target에 대한 정보입니다 [!DNL Recommendations] API. |
| [이메일의 Adobe Campaign 컨텐츠 Recommendations](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Adobe Campaign에서 Adobe Target 및 Adobe I/O Runtime을 통해 이메일에서 콘텐츠 권장 사항을 활용하는 방법을 설명하는 블로그입니다. |

## 관리 [!DNL Recommendations] API를 사용하여 설정

대부분의 경우 권장 사항은 Adobe Target UI에서 구성한 다음 를 통해 사용하거나 액세스합니다 [!DNL Target] API(위의 섹션에서 언급된 이유 등)입니다. 이 UI-API 조정은 일반적입니다. 하지만 경우에 따라 사용자가 API를 통해 설정뿐 아니라 결과의 사용과 같은 모든 작업을 수행하려고 할 수 있습니다. 덜 일반적이긴 하지만, 사용자는 절대적으로 구성, 실행, *및* api를 완전히 사용하여 권장 사항의 결과를 활용하십시오.

우리는 [이전 섹션](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=_blank} Adobe Target Recommendations 엔터티를 관리하고 서버 측에서 제공하는 방법. 마찬가지로 Adobe I/O을 사용하면 Adobe Target에 로그인하지 않고도 기준, 프로모션, 컬렉션 및 디자인 템플릿을 관리할 수 있습니다. 전체 목록 [!DNL Recommendations] API를 찾을 수 있습니다. [여기](https://developers.adobetarget.com/api/recommendations/), 하지만 여기에 참조에 대한 요약이 있습니다.

| 리소스 | 세부 사항 |
| --- | --- |
| [컬렉션](https://developers.adobetarget.com/api/recommendations/#tag/Collections) | 컬렉션을 나열하고, 만들고, 가져오고, 편집하고, 삭제합니다. |
| [기준](https://developers.adobetarget.com/api/recommendations/#tag/Criteria) | 기준을 나열하고 가져옵니다. |
| [디자인](https://developers.adobetarget.com/api/recommendations/#tag/Designs) | 디자인을 목록 작성, 가져오기, 편집, 삭제 및 검증합니다. |
| [엔티티](https://developers.adobetarget.com/api/recommendations/#tag/Entities) | 엔티티를 저장, 삭제 및 가져옵니다. |
| [프로모션](https://developers.adobetarget.com/api/recommendations/#tag/Promotions) | 프로모션을 나열, 생성, 가져오기, 편집 및 삭제합니다. |
| [카테고리 기준](https://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | 카테고리 기준을 나열하고, 만들고, 가져오고, 편집하고, 삭제합니다. |
| [사용자 지정 기준](https://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | 사용자 지정 기준을 나열하고, 만들고, 가져오고, 편집하고, 삭제합니다. |
| [항목 기준](https://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | 항목 기준을 나열하고, 만들고, 가져오고, 편집하고, 삭제합니다. |
| [인기도 기준](https://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | 인기도 기준을 나열, 만들기, 가져오기, 편집 및 삭제합니다. |
| [프로필 속성 기준](https://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | 프로필 속성 기준을 나열하고, 만들고, 가져오고, 편집하고, 삭제합니다. |
| [최근 기준](https://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | 최근 기준을 나열하고, 만들고, 가져오고, 편집하고, 삭제합니다. |
| [시퀀스 기준](https://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | 시퀀스 기준을 나열하고, 만들고, 가져오고, 편집하고, 삭제합니다. |

## 참조 설명서

* [Adobe Target 관리 API 설명서](https://developer.adobe.com/target/administer/admin-api/){target=_blank}
* [Adobe Target 배달 API](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}
* [ [!DNL Recommendations] 를 이메일과 통합](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## 요약 및 검토

축하합니다! 이 자습서를 완료하면 다음 방법을 배울 수 있습니다.
* [Recommendations API를 사용하여 카탈로그를 관리합니다](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=_blank}
* [Recommendations API를 사용하여 사용자 지정 기준 관리](https://developer.adobe.com/target/before-administer/recs-api/manage-custom-criteria/){target=_blank}
* [Recommendations에서 배달 API 사용](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=_blank}
