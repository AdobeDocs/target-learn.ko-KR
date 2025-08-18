---
title: ' [!DNL Analysis Workspace]  활동에 대해 [!UICONTROL Auto-Allocate]에서 A4T 보고서를 설정하는 방법'
description: '[!UICONTROL Analytics for Target] 활동을 실행할 때  [!DNL Adobe] [!DNL Analysis Workspace]에서 [!UICONTROL Auto-Allocate]​(A4T) 보고서를 구성하는 방법'
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 190a67832f378e15090115420bfaf8a4af4b9cb9
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%

---

# [!DNL Analysis Workspace] 활동에 대해 [!DNL Auto-Allocate]에서 A4T 보고서 설정

[[!UICONTROL Auto-Allocate]의 ](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html){target=_blank} 활동[!DNL Adobe Target]은(는) 둘 이상의 경험에서 승자를 식별하고, 테스트가 계속 실행되고 학습되는 동안 승자에게 방문자 트래픽을 자동으로 재할당합니다. [!UICONTROL Analytics for Target]에 대한 [!UICONTROL Auto-Allocate]&#x200B;(A4T) 통합을 통해 [!DNL Adobe Analytics]에서 보고 데이터를 볼 수 있으며 [!DNL Analytics]에 정의된 사용자 지정 이벤트 또는 지표에 대해 최적화할 수 있습니다.

[!DNL Adobe Analytics] [!DNL Analysis Workspace]에서 다양한 분석 기능을 사용할 수 있지만 [!UICONTROL Analytics for Target] 활동을 올바르게 해석하려면 기본 [!UICONTROL Auto-Allocate] 패널을 몇 가지 수정해야 할 수 있습니다. [최적화 지표 기준](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}의 뉘앙스로 인해 이러한 수정이 필요합니다.

각 유형의 최적화 지표는 다음과 같이 A4T에서 다른 보고서 구성을 필요로 합니다.

* [!DNL Analytics] 지표 사용

   * [!UICONTROL Maximize metric value per visitor]
   * [!UICONTROL Maximize unique visitor conversion rate]

* [!DNL Target] 정의 전환 지표 사용

이 튜토리얼에서는 전반적인 A4T 지침 및 기준별 보고서 구성 단계를 다룹니다.

## 최적화 기준이 &quot;[!UICONTROL Maximize Metric Value Per Visitor]&quot;인 분석 지표

**정의**: (전체 지표 값) / (방문자 수)

보고서를 구성하려면 A4T 보고서에서 다음과 같이 변경합니다.

| 변경 필요 | [!DNL Target] 트리거된 보고서 | A4T 패널 보고서 |
| --- | --- | --- |
| [!DNL Analytics] 지표에 대한 지표 값 최대화 | <ul><li>[!UICONTROL Confidence] 지표를 제거합니다.</li><li>[!UICONTROL Lift (Low)] 및 [!UICONTROL Lift (High)]을(를) 제거합니다. [!UICONTROL Lift (Med)] 유지</li><li>혼동을 방지하기 위해 [!UICONTROL Conversion Rate] 열에서 백분율 프레젠테이션의 선택을 취소하십시오. 아래의 [A4T에 대한 전체 지침](#guidance)을 참조하세요.</li><li>[!UICONTROL Conversion] 비율 지표의 이름을 &quot;지표/방문자&quot;로 바꿉니다.</li></ul> | <ul><li>[!UICONTROL Confidence] 지표를 제거합니다.</li><li>[!UICONTROL Lift (Low)]을(를) 제거하고 [!UICONTROL Lift (High)]을(를) 유지합니다. [!UICONTROL Lift (Med)] 유지</li><li>혼동을 방지하기 위해 [!UICONTROL Conversion Rate] 열에서 백분율 프레젠테이션의 선택을 취소하십시오. 아래의 [A4T에 대한 전체 지침](#guidance)을 참조하세요.</li><li>[!UICONTROL Conversion] 비율 지표의 이름을 &quot;지표/방문자&quot;로 바꿉니다.</li><li>날짜 및 시간 범위가 [!DNL Target] 보고서에 표시되는 값과 일치하는지 확인하십시오. 아래의 [A4T에 대한 전체 지침](#guidance)을 참조하세요.</li></ul> |

![매출에 대한 지표 값 최대화](/help/integrations/assets/maximize-metric-value-revenue.png)

## 최적화 기준이 &quot;[!DNL Analytics]&quot;인 [!UICONTROL Unique Visitor Conversion Rate] 지표

**정의**: (# of Unique Visitors with positive value of the metric) / (총 # of Unique Visitors)

예: 최적화 지표가 [!UICONTROL Revenue]이라고 가정합니다. 활동에는 5명의 고유 방문자가 있으며, 이 고유 방문자 중 3명이 구매합니다. 이 예에서 이 값은 = (0&rbrace;이(가) 양수인 방문자 3명) / (총 고유 방문자 수 5명) = 0.6 = 60%입니다.[!UICONTROL Revenue]

>[!NOTE]
>
>여기에서 참조한 전환율은 클릭, 노출 등과 같은 주문 이외의 작업을 의미할 수 있습니다. 이러한 경우 기준은 여전히 각각 페이지를 클릭하거나 본 방문자의 수를 최대화하는 것입니다.

보고서를 구성하려면 A4T 보고서에서 다음과 같이 변경합니다.

| 변경 필요 | Target에서 트리거된 보고서 | A4T 패널 보고서 |
| --- | --- | --- |
| [!DNL Analytics] 지표에 대한 전환 최대화 | <ul><li>[!UICONTROL Confidence] 지표를 제거합니다.</li><li>세 개의 [!UICONTROL Lift] 지표를 모두 제거합니다.</li><li>혼동을 방지하기 위해 [!UICONTROL Conversion Rate] 열에서 백분율 프레젠테이션의 선택을 취소하십시오. 아래의 [A4T에 대한 전체 지침](#guidance)을 참조하세요.</li></ul> | <ul><li>[!UICONTROL Confidence] 지표를 제거합니다.</li><li>세 개의 [!UICONTROL Lift] 지표를 모두 제거합니다.</li><li>분석된 활동을 본 방문자를 양의 지표 값으로 필터링하는 세그먼트를 만듭니다. 아래의 [세그먼트 만들기](#segment)를 참조하십시오.</li><li>자동으로 채워진 [!UICONTROL Conversion Rate] 지표를 양의 지표 값과 고유 방문자 수로 [!UICONTROL Unique visitors]을(를) 나누도록 바꿉니다. 아래의 [전환율 지표 업데이트](#update-conversion-metric)를 참조하십시오.</li><li>혼동을 방지하기 위해 [!UICONTROL Conversion Rate] 열에서 백분율 프레젠테이션의 선택을 취소하십시오. 아래의 [A4T에 대한 전체 지침](#guidance)을 참조하세요.</li><li>날짜 및 시간 범위가 [!DNL Target] 보고서에 표시되는 값과 일치하는지 확인하십시오. 아래의 [A4T에 대한 전체 지침](#guidance)을 참조하세요.</li></ul> |

### 기본 A4T 패널 보고서 - 추가 지침

다음 섹션에는 기본 A4T 패널 보고서를 설정할 때의 추가 지침에 대한 자세한 정보가 포함되어 있습니다.

#### 세그먼트 만들기 {#segment}

1. 왼쪽 레일에서 **옆에 있는**&quot;+&quot; 기호&#x200B;**[!UICONTROL Segments]**&#x200B;을(를) 클릭합니다.

   ![왼쪽 레일의 세그먼트 옆에 더하기 기호가 있습니다.](/help/integrations/assets/plus-sign.png)

1. 세그먼트 제목을 &quot;양의 지표 값을 가진 방문자&quot;로 지정합니다.
1. **[!UICONTROL Definition]**&#x200B;에서 **[!UICONTROL Include]** 옆의 **[!UICONTROL Visitor]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL Definition]**&#x200B;에서 활동의 최적화 지표를 선택합니다.

   이 예제에서는 [!UICONTROL Revenue]을(를) 최적화 지표로 가정합니다.

1. &quot;[!UICONTROL is greater than]&quot; 연산자를 선택한 다음 &quot;0&quot;을(를) 지정하십시오.

   이러한 설정은 양의 지표 값을 갖는 모든 방문자를 필터링합니다.

1. **[!UICONTROL Save]** 아이콘을 클릭합니다.

   ![양의 지표 값](/help/integrations/assets/positive-metric-value.png)

1. A4T 패널에 &quot;양의 지표 값을 갖는 방문자&quot;라는 새로 만든 세그먼트를 추가합니다.
1. [!UICONTROL Unique Visitors] 지표를 &quot;양수 지표 값을 가진 방문자&quot;와 같은 열에 끌어서 놓습니다.

   이 구성은 지표 값이 양수인 모든 고유 방문자의 세그먼트를 만듭니다. 이 예에서는 매출이 0보다 큰 모든 고유 방문자입니다.

#### [!UICONTROL Conversion Rate] 지표 업데이트 {#update-conversion-metric}

1. 아직 제거하지 않은 경우 아래 설명된 대로 패널에서 기존 [!UICONTROL Conversion Rate] 열을 제거하십시오.
1. 왼쪽 레일에서 **[!UICONTROL Metrics]** 섹션 옆에 있는 &quot;+&quot; 기호를 클릭하여 지표를 추가합니다.
1. 지표의 이름을 &quot;전환율&quot;로 지정하고 &quot;([!UICONTROL Unique Visitors]&#x200B;(양수 지표 값 포함)&quot;을(를) &quot;고유 방문자 수&quot;로 나누어 아래와 같이 정의합니다.

   양수 지표 값을 가진 방문자 수, 구분 연산자, 분자에서 &quot;고유 방문자 수&quot; 지표 및 &quot;고유 방문자 수&quot;를 분모로 하여 새로 만든 세그먼트(아래에 정의된 단계)를 추가합니다.

   ![A4T 패널의 전환율](/help/integrations/assets/conversion-rate.png)

1. **[!UICONTROL Save]** 아이콘을 클릭합니다.

1. 새로 만든 &quot;전환율&quot; 지표를 기존 패널로 끌어서 놓습니다.
1. 톱니바퀴 아이콘을 클릭한 다음 **[!UICONTROL Percent]** 확인란의 선택을 취소하십시오. 이 값을 사용하면 혼동이 발생할 수 있기 때문입니다.

   보고서의 올바른 구성은 다음 그림과 유사한 결과를 산출해야 합니다.

   ![A4T 패널 보고서의 고유 방문 전환율](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target] 정의 전환율

보고서를 구성하려면 A4T 보고서에서 다음과 같이 변경합니다.

| 변경 필요 | Target에서 트리거된 보고서 | A4T 패널 보고서 |
| --- | --- | --- |
| [!DNL Analytics] 전환 지표가 있는 [!DNL Target] 보고 | <ul><li>[!UICONTROL Confidence] 지표를 제거합니다.</li><li>[!UICONTROL Lift (Low)] 및 [!UICONTROL Lift (High)]을(를) 제거합니다. 리프트 유지(메드).</li><li>혼동을 방지하기 위해 [!UICONTROL Conversion Rate] 열에서 백분율 프레젠테이션의 선택을 취소하십시오. 아래의 [A4T에 대한 전체 지침](#guidance)을 참조하세요.</li></ul> | <ul><li>[!UICONTROL Confidence] 지표를 제거합니다.</li><li>[!UICONTROL Lift (Low)] 및 [!UICONTROL Lift (High)]을(를) 제거합니다. [!UICONTROL Lift (Med)] 유지</li><li>혼동을 방지하기 위해 [!UICONTROL Conversion Rate] 열에서 백분율 프레젠테이션의 선택을 취소하십시오. 아래의 [A4T에 대한 전체 지침](#guidance)을 참조하세요.</li><li>날짜 및 시간 범위가 [!DNL Target] 보고서에 표시되는 값과 일치하는지 확인하십시오. 아래의 [A4T에 대한 전체 지침](#guidance)을 참조하세요.</li></ul> |

보고서의 올바른 구성은 다음 그림과 유사한 결과를 산출해야 합니다.

![활동 전환](/help/integrations/assets/optimized-table.png)

## A4T에 대한 전체 지침 {#guidance}

[!UICONTROL Analytics for Target]의 보고서 화면에서 링크를 클릭하여 미리 빌드된 [!UICONTROL Target] 패널로 이동할 수 있습니다(&quot;[!DNL Target] 트리거된 보고서&quot;라고 이 가이드의 뒷부분에서 참조). 또는 [!DNL Analytics]에서 A4T 패널을 만들 수 있습니다(자세한 내용은 이 섹션의 뒷부분).

다음 섹션에서는 이러한 방법 중 어느 것을 선택하느냐에 따라 필요한 구성을 지정합니다. 그러나 다음 단계는 A4T의 전반적인 지침 역할을 합니다.

* 패널 생성 방법에 관계없이 A4T 패널에서 신뢰도 지표를 제거합니다(둘 다 아래에 자세히 설명되어 있음). 대신 [!DNL Target] 보고에서 이러한 값을 참조합니다. 또한 [!DNL Target] 보고에서 활동 승자를 식별할 수 있습니다. 활동 우승자 식별에 대한 자세한 내용은 아래의 [활동 우승자 식별](#winner) 섹션에서 확인할 수 있습니다.
&#x200B;>>
* 혼동을 방지하려면 [!UICONTROL Percent] 지표의 &quot;[!UICONTROL Conversion Rate]&quot; 프레젠테이션을 선택 취소하십시오. 아래 [[!UICONTROL Conversion Rate] 열에서 백분율 숨기기](#hide-percentage)를 참조하세요.
&#x200B;>>
* A4T 패널을 작성하는 경우 날짜 및 시간 범위가 [!DNL Target] 보고서의 날짜 및 시간 범위와 일치하는지 확인하십시오. 아래의 [A4T 패널에서 날짜 및 시간 정렬](#aligning-date-and-time)을 참조하십시오.

### [!UICONTROL Conversion Rate] 열에서 백분율 숨기기 {#hide-percentage}

1. **열의 제목 옆에 있는**&#x200B;톱니바퀴[!UICONTROL Conversion Rate] 아이콘을 클릭합니다.

   ![전환율 열의 톱니바퀴 아이콘](/help/integrations/assets/coversion-rate-gear-icon.png)

   [!UICONTROL Column] 설정 대화 상자가 표시됩니다.

   ![열 설정 대화 상자](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. **[!UICONTROL Percent]** 확인란의 선택을 취소합니다.

   이제 A4T 패널에 [!UICONTROL Conversion Rate]&#x200B;(으)로 백분율이 포함되지 않으며 아래와 같이 [!DNL Target]과(와) 일치합니다.

   ![백분율 없음을 표시하는 전환율 열](/help/integrations/assets/no-percentages.png)

### A4T 패널에서 날짜 및 시간 정렬 {#aligning-date-and-time}

1. 각 패널 아래에서 패널이 참조하는 날짜 범위를 확인하여 날짜 범위가 [!DNL Target] 보고서의 날짜 범위와 일치하는지 확인하십시오.

   ![A4T 패널의 날짜 범위](/help/integrations/assets/date-range.png)

1. [!DNL Analytics]에서 시간 범위를 12:00am - 11:59pm(으)로 설정합니다.

### 활동 우승자 식별 {#winner}

신뢰도 값이 95%보다 크거나 같은 채택 전환율이 있는 경우 [!DNL Auto-Allocate]개의 활동 당첨자가 선택됩니다. 신뢰도 계산은 [!DNL Target]이(가) [!DNL Target] 활동에 대해 권장하는 보다 보수적인 방법을 반영하므로 이러한 값은 [!UICONTROL Auto-Allocate] 보고서에서 참조되어야 합니다. [에서 ](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank}자동 할당의 통계적 보장&#x200B;*[!UICONTROL Adobe Target Business Practitioner Guide]*&#x200B;을(를) 참조하십시오.

>[!NOTE]
>
>[!DNL Analysis Workspace]의 A4T 패널에서 &quot;아직 우승자 없음&quot; 및 &quot;우승자&quot; 배지를 사용할 수 없습니다. 또한 [!DNL Target] 활동에 대한 [!UICONTROL Auto-Allocate] 보고서에 표시되는 우승자 &quot;별&quot; 배지도 무시해야 합니다. [에서 ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank}A4T의 자동 할당 및 자동 타겟 활동에 대한 지원&#x200B;*에서*&#x200B;자동 할당&#x200B;*[!UICONTROL Adobe Target Business Practitioner Guide]*&#x200B;을 참조하십시오.

### [!UICONTROL Auto-Allocate]에서 [!DNL Analysis Workspace] 패널에 대한 A4T 만들기

1. [!UICONTROL Auto-Allocate] 활동 보고서에 대한 A4T 패널을 만들려면 아래와 같이 [!UICONTROL Analytics for Target]의 [!DNL Analysis Workspace] 패널로 시작합니다.

   ![Analytics for Target - 자동 할당 보고서](/help/integrations/assets/a4t-auto-allocate-report.png)

1. 다음을 선택합니다.

   * **[!UICONTROL Control Experience]**: 원하는 환경을 선택하십시오.
   * **[!UICONTROL Normalizing Metric]**: **[!UICONTROL Visitors]**&#x200B;을(를) 선택합니다(기본적으로 A4T 패널에 포함됨). [!UICONTROL Auto-Allocate]은(는) 항상 고유 방문자별로 전환율을 표준화합니다.
   * **성공 지표**: 활동을 만드는 동안 사용한 것과 동일한(최적화) 지표를 선택합니다. [!DNL Target]이(가) 정의한 전환 지표인 경우 **[!UICONTROL Activity Conversion]**&#x200B;을(를) 선택합니다. 그렇지 않으면 사용한 [!DNL Adobe Analytics] 지표를 선택하십시오.









