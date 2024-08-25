---
title: Adobe Target에서 대상 및 오퍼 만들기
description: 이 단원에서는 이전 단원에서 구현한 세 위치에 대한 Adobe Target의 대상과 오퍼를 빌드합니다. 다음 단원에서는 개인화된 경험을 표시하는 데 사용됩니다.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 4b153e4f-a979-49a8-8c26-f7ac95162a2f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 1%

---

# Adobe Target에서 대상 및 오퍼 만들기

이 단원에서는 [!DNL Target] 인터페이스로 이동하여 이전 단원에서 구현한 세 위치에 대한 대상 및 오퍼를 빌드합니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* Adobe Target에서 대상자 만들기
* Adobe Target에서 오퍼 만들기

보다 구체적으로, 이 단원에서는 자습서 시작 부분에 정의된 개인화 사용 사례를 완수하는 데 필요한 대상과 오퍼를 만듭니다. 앱 사용자가 여행을 예약하는 데 도움이 되도록 홈 및 검색 화면을 사용하고, 감사 화면을 사용하여 사용자 대상에 따라 관련된 프로모션을 표시하려고 합니다. 다음은 각 위치에 대해 이 단원에서 빌드할 내용을 나타내는 표입니다.

| 위치 | 대상자 | 오퍼 |
| --- | --- | --- |
| wetravel_engage_home | 새 모바일 앱 사용자 | &quot;이용 가능한 버스 노선을 검색하려면 출발 및 도착지를 선택하십시오.&quot; |
| wetravel_engage_search | 새 모바일 앱 사용자 | &quot;필터를 사용하여 검색 결과 좁히기&quot; |
| wetravel_engage_home | 모바일 앱 사용자 반환 | &quot;돌아오신 것을 환영합니다! 체크아웃 중에 프로모션 코드 BACK30을 사용하여 10% 할인을 받으세요.&quot; |
| wetravel_engage_search | 모바일 앱 사용자 반환 | 기본 컨텐츠 |
| wetravel_context_dest | 목적지: 샌디에이고 | &quot;DJ&quot; |
| wetravel_context_dest | 목적지: 로스앤젤레스 | &quot;범용&quot; |

## Workspace 선택

회사에서 속성 및 작업 영역을 사용하여 앱 및 웹 사이트를 개인화하기 위한 경계를 설정하는 경우(마지막 단원에서 at_property 매개 변수를 구현한 경우) 이 단원을 진행하기 전에 먼저 올바른 Workspace에 있는지 확인해야 합니다. 속성 및 작업 영역을 사용하지 않는 경우에는 이 단계를 무시하면 됩니다. 이전 단원에서 사용한 Workspace을 선택하여 at_property 값을 복사합니다.

![Workspace 예](assets/workspace.jpg)

## 대상자 만들기

이제 앱을 개인화하는 데 사용할 대상을 만들어 보겠습니다.

### 새 사용자를 위한 대상 만들기

Adobe Target 대상은 특정 방문자 그룹을 식별하는 데 사용됩니다. 그런 다음 오퍼를 해당 특정 그룹에 타기팅할 수 있습니다. 처음 두 지역에서는 &quot;새 사용자&quot; 대상을 사용합니다.

1. 위쪽 탐색에서 **[!UICONTROL Audiences]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL Create Audience]** 단추를 클릭합니다.
   ![새 사용자 대상 만들기](assets/audience_new_mobile_app_users_1.jpg)

1. 대상 이름으로 **[!UICONTROL New Mobile App Users]**&#x200B;을(를) 입력하십시오.
1. **[!UICONTROL Add Rule]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL Custom]** 규칙을 선택하십시오.
   ![새 사용자 대상 만들기](assets/audience_new_mobile_app_users_2.jpg)

1. **[!UICONTROL a.Launches]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL is less than]**&#x200B;을(를) 선택합니다.
1. **5** 입력.
1. 새 대상을 저장합니다.
   ![새 사용자 대상 만들기](assets/audience_new_mobile_app_users_3.jpg)

### 재방문자를 위한 대상 만들기

위에 나열된 동일한 단계에 따라 재방문자를 위한 대상자를 만듭니다.

1. 대상 이름을 _다시 방문하는 모바일 앱 사용자_&#x200B;로 지정합니다.
1. **[!UICONTROL a.Launches is greater than or equal to 5]**&#x200B;을(를) 사용자 지정 규칙으로 사용합니다.
1. 새 대상을 저장합니다.

   ![재방문 사용자 대상 만들기](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>[!DNL Target] 모바일 SDK에서 수집된 모든 라이프사이클 지표 및 차원은 앞에 &quot;a&quot;(예: a.Launches)가 추가되며 드롭다운 메뉴의 &quot;사용자 지정&quot; 옵션에서 사용할 수 있으며 대상을 빌드하는 데 사용할 수 있습니다.

### 샌디에이고 여행을 예약하는 사용자를 위한 대상 만들기

다음으로 We.Travel 앱에서 제공하는 일부 대상에 대한 몇 가지 대상을 만듭니다. 마지막 단원에서는 wetravel_context_dest 위치 요청에서 대상을 위치 매개 변수로 전달했습니다. 이 매개 변수는 드롭다운 메뉴의 &quot;사용자 지정&quot; 옵션에서 사용할 수 있습니다.

>[!NOTE]
>
>사용자 지정 드롭다운에 표시되어야 하는 매개 변수가 [!DNL Target] 인터페이스에 표시되지 않으면 요청에서 실제로 전달되고 있는지 다시 확인하십시오. 이 요청에 있지만 [!DNL Target] 인터페이스에 지연 로드되지 않은 경우 매개 변수 이름을 입력하고 Enter 키를 눌러 대상을 계속 정의할 수 있습니다

1. 대상 이름을 _대상: 샌디에이고_&#x200B;로 지정합니다.
1. _locationDest에 San Diego가 포함되어 있음_&#x200B;을 정의하는 사용자 지정 규칙을 사용합니다.
1. 새 대상을 저장합니다.

   ![샌디에이고 대상자 만들기](assets/audience_locationDest_san_diego.jpg)

### Los Angeles 여행을 예약하는 사용자를 위한 대상 만들기

1. 대상자의 이름을 _대상: 로스앤젤레스_(으)로 지정합니다.
1. _locationDest에 Los Angeles 포함_ 정의가 있는 사용자 지정 규칙 사용
1. 새 대상을 저장합니다.

![로스앤젤레스 대상 만들기](assets/audience_locationDest_los_angeles.jpg)

## 오퍼 만들기

이제 이러한 메시지를 표시할 오퍼를 만들어 보겠습니다. 다시 말해서 오퍼는 [!DNL Target] 응답으로 제공되는 코드/콘텐츠 조각입니다. 가장 자주 [!DNL Target] 사용자 인터페이스에서 만들어지지만 API를 통해 또는 Adobe Experience Manager과의 경험 조각 통합을 사용하여 만들 수도 있습니다. 모바일 앱에서는 JSON 오퍼가 일반적입니다. 이 자습서에서는 모든 일반 텍스트 콘텐츠(JSON 포함)를 앱에 전달하는 데 사용할 수 있는 HTML 오퍼를 사용합니다.

### 새 사용자를 위한 오퍼 만들기

먼저 새 사용자에게 보낼 메시지에 대한 오퍼를 만들어 보겠습니다.

1. 위쪽 탐색에서 **[!UICONTROL Offers]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL Create]** 아이콘을 클릭합니다.
1. **[!UICONTROL HTML Offer]**&#x200B;을(를) 선택합니다.

   ![홈 오퍼 만들기](assets/offer_home_1.jpg)

1. 오퍼 이름을 _Home으로 지정합니다. 새 사용자 참여_.
1. 코드로 _사용 가능한 버스를 검색하려면 Source 및 대상 선택_&#x200B;을 입력하십시오.
1. 새 오퍼를 저장합니다.

   ![홈 HTML 오퍼 만들기](assets/offer_home_2.jpg)

### 재방문 사용자를 위한 오퍼 만들기

이제 재방문자를 위한 하나의 오퍼를 만들어 보겠습니다(두 번째 오퍼는 기본 콘텐츠이며, 이는 nothing으로 표시됨).

1. 오퍼 이름을 _Home: 재방문 사용자_&#x200B;로 지정합니다.
1. _돌아오신 것을 환영합니다! 체크아웃 중에 프로모션 코드 BACK30을 사용하여 10% 할인 혜택을 받으십시오.HTML 코드로_&#x200B;을(를) 사용합니다.
1. 새 오퍼를 저장합니다.

   ![홈 HTML 오퍼 만들기](assets/offer_home_returning_users.jpg)

### 샌디에이고 오퍼 만들기

ThankYou 활동으로 &quot;DJ&quot;가 반환되면 filterRecommendationBasedOnOffer() 함수 의 로직에 &quot;DJ SAM과 함께하는 락 나이트&quot;에 대한 배너가 표시됩니다.

1. 오퍼 이름을 _샌디에이고 프로모션_&#x200B;으로 지정합니다.
1. HTML 코드로 _DJ_&#x200B;을(를) 입력하십시오.
1. 새 오퍼를 저장합니다.

![샌디에이고 오퍼 만들기](assets/offer_san_diego.jpg)

### Los Angeles로 이동하는 사용자를 위한 오퍼 만들기

ThankYou 활동으로 &quot;Universal&quot;이 반환되면 filterRecommendationBasedOnOffer() 함수 의 로직에 &quot;Universal Studios&quot;에 대한 배너가 표시됩니다.

1. 오퍼 이름을 _Promotion for Los Angeles_&#x200B;로 지정합니다.
1. HTML 코드로 _Universal_&#x200B;을(를) 입력하십시오.
1. 새 오퍼를 저장합니다.

![Los Angeles 오퍼 만들기](assets/offer_los_angeles.jpg)

## 결론

이제 대상 및 오퍼가 있습니다. 다음 단원에서는 위치, 대상 및 오퍼를 함께 연결하여 개인화된 경험을 만드는 활동을 빌드합니다!

**[다음 : &quot;레이아웃 개인화&quot; >](personalize-layouts.md)**
