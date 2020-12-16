---
title: Adobe Target에서 대상 및 오퍼 만들기
seo-title: Adobe Target에서 대상 및 오퍼 만들기
description: '이 단원에서 Adobe Target에서 이전 단원에서 구현한 3개의 위치에 대한 대상과 혜택을 제작할 예정입니다. 다음 단원에서 개인화된 경험을 표시하는 데 사용됩니다.   '
seo-description: 이 단원에서 Adobe Target에서 이전 단원에서 구현한 3개의 위치에 대한 대상과 혜택을 제작할 예정입니다. 다음 단원에서 개인화된 경험을 표시하는 데 사용됩니다.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: 199fbde58696a0511623c5500cc6afbbcfdd67a3
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---


# Adobe Target에서 대상 및 오퍼 만들기

이 단원에서 [!DNL Target] 인터페이스로 이동하여 이전 단원에서 구현한 3개의 위치에 대한 대상 및 오퍼를 만듭니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* Adobe Target에서 대상 만들기
* Adobe Target에서 오퍼 만들기

보다 구체적으로 설명하면 튜토리얼을 시작할 때 정의된 개인화 사용 사례를 달성하는 데 필요한 고객과 오퍼를 만듭니다. 앱 사용자가 여행 예약을 할 수 있도록 홈 및 검색 화면을 사용하고 싶은 경우, 감사 화면을 사용하여 사용자의 대상에 따라 일부 관련 프로모션을 표시하고자 합니다. 다음은 각 위치에 대해 이 단원에서 작성할 내용을 나타내는 표입니다.

| 위치 | 대상자 | 오퍼 |
| --- | --- | --- |
| wetravel_engage_home | 새 모바일 앱 사용자 | &quot;사용 가능한 버스 경로를 검색하려면 원본 및 대상 선택&quot; |
| wetravel_engage_search | 새 모바일 앱 사용자 | &quot;필터를 사용하여 검색 결과 좁히기&quot; |
| wetravel_engage_home | 재방문 모바일 앱 사용자 | &quot;돌아온 걸 환영합니다! 체크아웃 중에 프로모션 코드 BACK30을 사용하여 10% 할인 혜택을 받을 수 있습니다.&quot; |
| wetravel_engage_search | 재방문 모바일 앱 사용자 | 기본 콘텐츠 |
| wetravel_context_dest | 대상:샌디에이고 | &quot;DJ&quot; |
| wetravel_context_dest | 대상:로스앤젤레스 | &quot;범용&quot; |

## 작업 영역 선택

회사에서 속성 및 작업 영역을 사용하여 앱 및 웹 사이트를 개인화하기 위한 경계를 설정하고 마지막 단원에서 at_property 매개 변수를 구현한 경우 이 단원을 진행하기 전에 먼저 올바른 작업 영역에 있는지 확인해야 합니다. 속성 및 작업 영역을 사용하지 않는 경우 이 단계를 무시하십시오. 이전 단원에서 사용한 작업 영역을 선택하여 at_property 값을 복사합니다.

![작업 영역 예](assets/workspace.jpg)

## 대상자 만들기

이제 앱을 개인화하는 데 사용할 고객을 만들어 보겠습니다.

### 새 사용자용 대상 만들기

Adobe Target 대상은 특정 방문자 그룹을 식별하는 데 사용됩니다. 그런 다음 오퍼를 특정 그룹으로 타깃팅할 수 있습니다. 처음 두 위치에 대해 &quot;새 사용자&quot; 대상을 사용합니다.

1. 위쪽 탐색에서 **[!UICONTROL 대상]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 대상자 만들기]** 단추를 클릭합니다.
   ![새 사용자 대상 만들기](assets/audience_new_mobile_app_users_1.jpg)

1. 대상 이름으로 **[!UICONTROL 새 모바일 앱 사용자]**&#x200B;를 입력합니다.
1. **[!UICONTROL 규칙 추가]**&#x200B;를 선택합니다.
1. **[!UICONTROL 사용자 지정]** 규칙을 선택합니다.
   ![새 사용자 대상 만들기](assets/audience_new_mobile_app_users_2.jpg)

1. **[!UICONTROL a.Launches]**&#x200B;를 선택합니다.
1. **[!UICONTROL 이(가)]**&#x200B;보다 작음을 선택합니다.
1. **5**&#x200B;을 입력합니다.
1. 새 대상을 저장합니다.
   ![새 사용자 대상 만들기](assets/audience_new_mobile_app_users_3.jpg)

### 돌아온 사용자를 위한 대상 만들기

위에 나열된 동일한 단계를 따라 돌아온 사용자를 위한 대상자를 만듭니다.

1. 대상 이름 _재계약 모바일 앱 사용자_.
1. **[!UICONTROL a.Launches가 사용자 지정 규칙으로 5]**&#x200B;보다 크거나 같습니다.
1. 새 대상을 저장합니다.

   ![돌아온 사용자 대상 만들기](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>[!DNL Target] 모바일 SDK에서 수집된 모든 라이프사이클 지표 및 차원은 &quot;a&quot;(예: a.Launches)로 프리펜드되며, 드롭다운 메뉴의 &quot;사용자 지정&quot; 옵션에서 사용할 수 있으며, 대상을 빌드하는 데 사용할 수 있습니다.

### 샌디에이고 여행 예약 사용자를 위한 타겟 만들기

다음으로 We.Travel 앱에서 제공되는 일부 대상에 대해 몇 명의 고객을 제작할 예정입니다. 마지막 수업에서 대상을 wetravel_context_dest 위치 요청에서 위치 매개 변수로 전달했습니다. 이 매개 변수는 드롭다운 메뉴의 &quot;사용자 지정&quot; 옵션에서 사용할 수 있습니다.

>[!NOTE]
>
>사용자 지정 드롭다운에서 보려는 매개 변수가 [!DNL Target] 인터페이스에 표시되지 않으면 요청에서 실제로 전달되고 있는지 다시 확인하십시오. 요청에 있지만 [!DNL Target] 인터페이스에 지연이 로드되지 않은 것으로 확인된 경우 매개 변수 이름과 Enter 키를 입력하여 대상을 계속 정의할 수 있습니다

1. 대상 이름 _대상:샌디에이고_.
1. 이 정의와 함께 사용자 지정 규칙을 사용합니다._locationDest contains San Diego_.
1. 새 대상을 저장합니다.

   ![&quot;샌디에이고&quot; 고객 만들기](assets/audience_locationDest_san_diego.jpg)

### 로스앤젤레스 여행을 예약하는 사용자를 위한 대상자 만들기

1. 대상 이름 _대상:로스앤젤레스_
1. 이 정의와 함께 사용자 지정 규칙을 사용합니다._locationDest contains Los Angeles_
1. 새 대상을 저장합니다.

![&quot;로스앤젤레스&quot; 대상 만들기](assets/audience_locationDest_los_angeles.jpg)

## 오퍼 만들기

이제 이러한 메시지를 표시하는 오퍼를 만듭니다. 다시 말해서 오퍼는 코드/컨텐츠의 코드 조각이며 [!DNL Target] 응답으로 전달됩니다. 이러한 지표는 대부분 [!DNL Target] 사용자 인터페이스에서 생성되지만 API를 사용하거나 Adobe Experience Manager과 경험 조각 통합을 사용하여 만들 수도 있습니다. 모바일 앱에서 JSON 오퍼는 일반적으로 사용됩니다. 이 튜토리얼에서는 HTML 오퍼를 사용하여 일반 텍스트 콘텐츠(JSON 포함)를 앱에 제공하는 데 사용할 수 있습니다.

### 새 사용자를 위한 오퍼 만들기

먼저, 새 사용자에게 메시지에 대한 오퍼를 만들어 보겠습니다.

1. 위쪽 탐색에서 **[!UICONTROL 오퍼]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. **[!UICONTROL HTML 오퍼]**&#x200B;를 선택합니다.

   ![홈 오퍼 만들기](assets/offer_home_1.jpg)

1. 오퍼 이름 _홈:새 사용자 참여_.
1. _소스 및 대상 선택을 입력하여 사용 가능한 버스_&#x200B;을 코드로 검색합니다.
1. 새 오퍼를 저장합니다.

   ![홈 HTML 오퍼 만들기](assets/offer_home_2.jpg)

### 돌아온 사용자를 위한 오퍼 만들기

이제 돌아온 사용자를 위한 단일 오퍼를 만듭니다(두 번째 오퍼는 기본 컨텐츠가 되며 아무 것도 표시되지 않습니다).

1. 오퍼 이름 _홈:재방문 사용자_.
1. _돌아온 것을 환영합니다! 체크아웃 동안 프로모션 코드 BACK30을 사용하여 10% 할인 혜택을 받을 수 있습니다._ 를 HTML 코드로 채웁니다.
1. 새 오퍼를 저장합니다.

   ![홈 HTML 오퍼 만들기](assets/offer_home_returning_users.jpg)

### 샌디에이고 오퍼 만들기

&quot;DJ&quot;가 ThankYou 활동으로 반환되면 filterRecommendationBasedOnOffer() 함수의 논리가 &quot;Rock Night with DJ SAM&quot;에 대한 배너를 표시합니다.

1. 오퍼 이름 _샌디에고에 대한 프로모션_&#x200B;을 지정합니다.
1. HTML 코드로 _DJ_&#x200B;를 입력합니다.
1. 새 오퍼를 저장합니다.

![&quot;샌디에이고&quot; 오퍼 만들기](assets/offer_san_diego.jpg)

### 로스앤젤레스로 가는 사용자를 위한 오퍼 만들기

&quot;Universal&quot;이 감사 인사 활동으로 반환되면 filterRecommendationBasedOnOffer() 함수의 논리가 &quot;Universal Studios&quot;에 대한 배너를 표시합니다.

1. 오퍼 이름 _Promotion for Los Angeles_.
1. _유니버설_&#x200B;을 HTML 코드로 입력합니다.
1. 새 오퍼를 저장합니다.

![&quot;로스앤젤레스&quot; 오퍼 만들기](assets/offer_los_angeles.jpg)

## 결론

이제 대상 및 오퍼가 있습니다. 다음 단원에서는 위치, 고객 및 오퍼를 연계하여 개인화된 경험을 만드는 활동을 만듭니다.

**[다음:&quot;레이아웃 개인화&quot; >](personalize-layouts.md)**
