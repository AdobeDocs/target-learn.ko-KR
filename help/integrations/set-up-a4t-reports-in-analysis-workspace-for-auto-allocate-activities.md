---
title: 에서 A4T 보고서를 설정하는 방법 [!DNL Analysis Workspace] 대상 [!UICONTROL 자동 할당] 활동
description: 구성 방법 [!UICONTROL Analytics for Target] 의 (A4T) 보고서 [!DNL Adobe] [!DNL Analysis Workspace] 실행 시 [!UICONTROL 자동 할당] 활동.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 78e5b5f7fa8f4c1a08c06c6d2b0e1a5242cd464c
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---

# 에서 A4T 보고서 설정 [!DNL Analysis Workspace] 대상 [!DNL Auto-Allocate] 활동

An [[!UICONTROL 자동 할당] 활동](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html){target=_blank} 위치: [!DNL Adobe Target] 은 둘 이상의 경험에서 승자를 식별하고, 테스트가 계속 실행되고 학습되는 동안 방문자 트래픽을 승자에게 자동으로 재할당합니다. 다음 [!UICONTROL Analytics for Target] 용 (A4T) 통합 [!UICONTROL 자동 할당] 에서 보고 데이터를 볼 수 있습니다. [!DNL Adobe Analytics]및에 정의된 사용자 지정 이벤트 또는 지표에 대해 최적화할 수 있습니다 [!DNL Analytics].

다양한 분석 기능은에서 사용할 수 있습니다 [!DNL Adobe Analytics] [!DNL Analysis Workspace], 기본값에 대한 몇 가지 수정 사항 [!UICONTROL Analytics for Target] 패널을 올바르게 해석해야 할 수 있음 [!UICONTROL 자동 할당] 활동. 의 뉘앙스로 인해 이러한 수정이 필요합니다. [최적화 지표 기준](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

각 유형의 최적화 지표는 다음과 같이 A4T에서 다른 보고서 구성을 필요로 합니다.

* 사용 [!DNL Analytics] 지표

   * [!UICONTROL 방문자당 지표 값 최대화]
   * [!UICONTROL 고유 방문자 전환율 최대화]

* 사용 [!DNL Target]-정의된 전환 지표

이 튜토리얼에서는 전반적인 A4T 지침 및 기준별 보고서 구성 단계를 다룹니다.

## 가 있는 Analytics 지표[!UICONTROL 방문자당 지표 값 최대화]&quot; 최적화 기준

**정의**: (전체 지표 값) / (방문자 수)

보고서를 구성하려면 A4T 보고서에서 다음과 같이 변경합니다.

| 변경 필요 | [!DNL Target]트리거된 보고서 | A4T 패널 보고서 |
| --- | --- | --- |
| 다음에 대한 지표 값 최대화 [!DNL Analytics] 지표 | <ul><li>제거 [!UICONTROL 신뢰도] 지표.</li><li>제거 [!UICONTROL 상승도(낮음)] 및 [!UICONTROL 상승도(높음)].</li><li>에서 백분율 표시 선택 취소 [!UICONTROL 전환율] 혼동을 방지하는 열입니다. 다음을 참조하십시오 [A4T에 대한 전체 지침](#guidance) 아래요.</li><li>이름 바꾸기 [!UICONTROL 전환] 지표를 &quot;지표 / 방문자&quot;로 평가합니다.</li></ul> | <ul><li>제거 [!UICONTROL 신뢰도] 지표.</li><li>제거 [!UICONTROL 상승도(낮음)] 및 [!UICONTROL 상승도(높음)].</li><li>에서 백분율 표시 선택 취소 [!UICONTROL 전환율] 혼동을 방지하는 열입니다. 다음을 참조하십시오 [A4T에 대한 전체 지침](#guidance) 아래요.</li><li>이름 바꾸기 [!UICONTROL 전환] 지표를 &quot;지표 / 방문자&quot;로 평가합니다.</li><li>날짜 및 시간 범위가 [!DNL Target] 보고서. 다음을 참조하십시오 [A4T에 대한 전체 지침](#guidance) 아래요.</li></ul> |

![매출에 대한 지표 값 최대화](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] 지표가 &quot;[!UICONTROL 고유 방문자 전환율]&quot; 최적화 기준

**정의**: ( 양수 값을 갖는 고유 방문자 수) / (총 고유 방문자 수)

예: 최적화 지표가 다음과 같다고 가정합니다. [!UICONTROL 매출]. 활동에는 5명의 고유 방문자가 있으며, 이 고유 방문자 중 3명이 구매합니다. 이 예에서 이 값은 (3명의 방문자 [!UICONTROL 매출] 는 양수입니다) / (총 5명의 고유 방문자 수) = 0.6 = 60%.

>[!NOTE]
>
>여기에서 참조한 전환율은 클릭, 노출 등과 같은 주문 이외의 작업을 의미할 수 있습니다. 이러한 경우 기준은 여전히 각각 페이지를 클릭하거나 본 방문자의 수를 최대화하는 것입니다.

보고서를 구성하려면 A4T 보고서에서 다음과 같이 변경합니다.

| 변경 필요 | Target에서 트리거된 보고서 | A4T 패널 보고서 |
| --- | --- | --- |
| 에 대한 전환 최대화 [!DNL Analytics] 지표 | <ul><li>[!UICONTROL 신뢰도] 지표를 제거해야 합니다.</li><li>모두 제거 [!UICONTROL 상승도] 지표.</li><li>에서 백분율 표시 선택 취소 [!UICONTROL 전환율] 혼동을 방지하는 열입니다. 다음을 참조하십시오 [A4T에 대한 전체 지침](#guidance) 아래요.</li></ul> | <ul><li>제거 [!UICONTROL 신뢰도] 지표.</li><li>모두 제거 [!UICONTROL 상승도] 지표.</li><li>분석된 활동을 본 방문자를 양의 지표 값으로 필터링하는 세그먼트를 만듭니다. 다음을 참조하십시오 [세그먼트 만들기](#segment) 아래요.</li><li>자동으로 채워진 필드 바꾸기 [!UICONTROL 전환율] 그래서 이것이 사이의 분할입니다. [!UICONTROL 고유 방문자 수] ( 양의 지표 값 및 고유 방문자 수 포함). 다음을 참조하십시오 [전환율 지표 업데이트](#update-conversion-metric) 아래요.</li><li>에서 백분율 표시 선택 취소 [!UICONTROL 전환율] 혼동을 방지하는 열입니다. 다음을 참조하십시오 [A4T에 대한 전체 지침](#guidance) 아래요.</li><li>날짜 및 시간 범위가 [!DNL Target] 보고서. 다음을 참조하십시오 [A4T에 대한 전체 지침](#guidance) 아래요.</li></ul> |

### 기본 A4T 패널 보고서 - 추가 지침

다음 섹션에는 기본 A4T 패널 보고서를 설정할 때의 추가 지침에 대한 자세한 정보가 포함되어 있습니다.

#### 세그먼트 만들기 {#segment}

1. 다음을 클릭합니다. **&quot;+&quot; 기호** 다음에 **[!UICONTROL 세그먼트]** 왼쪽 레일에서.

   ![왼쪽 레일의 세그먼트 옆에 더하기 기호가 있습니다.](/help/integrations/assets/plus-sign.png)

1. 세그먼트 제목을 &quot;양의 지표 값을 가진 방문자&quot;로 지정합니다.
1. 아래 **[!UICONTROL 정의]**, 옆에 있음 **[!UICONTROL 포함]**, 선택 **[!UICONTROL 방문자]**.
1. 아래 **[!UICONTROL 정의]**&#x200B;활동에서 최적화 지표를 선택합니다.

   이 예에서는 다음과 같이 가정합니다 [!UICONTROL 매출] 를 최적화 지표로 사용합니다.

1. 을(를) 선택합니다.[!UICONTROL 다음보다 큼]&quot; 연산자를 지정한 다음 &quot;0&quot;을 지정합니다.

   이러한 설정은 양의 지표 값을 갖는 모든 방문자를 필터링합니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

   ![양수 지표 값](/help/integrations/assets/positive-metric-value.png)

1. A4T 패널에 &quot;양의 지표 값을 갖는 방문자&quot;라는 새로 만든 세그먼트를 추가합니다.
1. 을(를) 끌어다 놓습니다. [!UICONTROL 고유 방문자 수] 지표가 &quot;양수 지표 값을 가진 방문자&quot;와 동일한 열에 있음.

   이 구성은 지표 값이 양수인 모든 고유 방문자의 세그먼트를 만듭니다. 이 예에서는 매출이 0보다 큰 모든 고유 방문자입니다.

#### 업데이트 [!UICONTROL 전환율] 지표 {#update-conversion-metric}

1. 아직 제거하지 않은 경우 기존 을 제거합니다 [!UICONTROL 전환율] 아래 설명된 대로 패널의 열입니다.
1. 다음 옆에 있는 &quot;+&quot; 기호를 클릭하여 지표를 추가합니다. **[!UICONTROL 지표]** 섹션(왼쪽 레일)을 참조하십시오.
1. 지표의 이름을 &quot;전환율&quot;로 지정하고 &quot;([!UICONTROL 고유 방문자 수] ( 양(+)의 지표 값을 사용)하여 아래에 표시된 대로 &quot;고유 방문자 수&quot;로 나눈 값입니다.

   양수 지표 값을 가진 방문자 수, 구분 연산자, 분자에서 &quot;고유 방문자 수&quot; 지표 및 &quot;고유 방문자 수&quot;를 분모로 하여 새로 만든 세그먼트(아래에 정의된 단계)를 추가합니다.

   ![A4T 패널의 전환율입니다.](/help/integrations/assets/conversion-rate.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

1. 새로 만든 &quot;전환율&quot; 지표를 기존 패널로 끌어서 놓습니다.
1. 톱니바퀴 아이콘을 클릭한 다음, **[!UICONTROL 백분율]** 이 값은 혼동을 일으킬 수 있기 때문입니다.

   보고서의 올바른 구성은 다음 그림과 유사한 결과를 산출해야 합니다.

   ![A4T 패널 보고서의 고유 방문 전환율](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]-정의된 전환율

보고서를 구성하려면 A4T 보고서에서 다음과 같이 변경합니다.

| 변경 필요 | Target에서 트리거된 보고서 | A4T 패널 보고서 |
| --- | --- | --- |
| [!DNL Analytics] 보고 방법 [!DNL Target] 전환 지표 | <ul><li>제거 [!UICONTROL 신뢰도] 지표.</li><li>제거 [!UICONTROL 상승도(낮음)] 및 [!UICONTROL 상승도(높음)].</li><li>에서 백분율 표시 선택 취소 [!UICONTROL 전환율] 혼동을 방지하는 열입니다. 다음을 참조하십시오 [A4T에 대한 전체 지침](#guidance) 아래요.</li></ul> | <ul><li>제거 [!UICONTROL 신뢰도] 지표.</li><li>제거 [!UICONTROL 상승도(낮음)] 및 [!UICONTROL 상승도(높음)].</li><li>에서 백분율 표시 선택 취소 [!UICONTROL 전환율] 혼동을 방지하는 열입니다. 다음을 참조하십시오 [A4T에 대한 전체 지침](#guidance) 아래요.</li><li>날짜 및 시간 범위가 [!DNL Target] 보고서. 다음을 참조하십시오 [A4T에 대한 전체 지침](#guidance) 아래요.</li></ul> |

보고서의 올바른 구성은 다음 그림과 유사한 결과를 산출해야 합니다.

![활동 전환](/help/integrations/assets/optimized-table.png)

## A4T에 대한 전체 지침 {#guidance}

사전 설치된 로 이동할 수 있습니다. [!UICONTROL Analytics for Target] 의 보고서 화면에서 링크를 클릭하여 패널 만들기 [!UICONTROL Target] (이 설명서는 뒷부분에서 &quot;[!DNL Target]-triggered report&quot;). 또는 에서 A4T 패널을 빌드할 수 있습니다 [!DNL Analytics] (자세한 내용은 이 섹션의 뒷부분에서 설명합니다.)

다음 섹션에서는 이러한 방법 중 어느 것을 선택하느냐에 따라 필요한 구성을 지정합니다. 그러나 다음 단계는 A4T의 전반적인 지침 역할을 합니다.

* 패널 생성 방법에 관계없이 A4T 패널에서 신뢰도 지표를 제거합니다(둘 다 아래에 자세히 설명되어 있음). 대신,에서 이 값을 참조합니다. [!DNL Target] 보고. 또한 활동 우승자를 다음에서 식별할 수 있습니다. [!DNL Target] 보고. 활동 우승자 식별에 대한 자세한 내용은 [활동 우승자 식별](#winner) 아래 섹션.
>>
* 혼동을 피하려면 &quot;[!UICONTROL 백분율]&quot; 프레젠테이션 [!UICONTROL 전환율] 지표. 다음을 참조하십시오 [다음에서 백분율 숨기기 [!UICONTROL 전환율] 열](#hide-percentage) 아래요.
>>
* A4T 패널을 작성하는 경우 날짜 및 시간 범위가 의 날짜 및 시간 범위와 일치하는지 확인합니다. [!DNL Target] 보고서. 다음을 참조하십시오 [A4T 패널에서 날짜 및 시간 정렬](#aligning-date-and-time) 아래요.

### 다음에서 백분율 숨기기 [!UICONTROL 전환율] 열 {#hide-percentage}

1. 다음을 클릭합니다. **톱니바퀴** 아이콘: 제목 옆 [!UICONTROL 전환율] 열.

   ![전환율 열의 톱니바퀴 아이콘](/help/integrations/assets/coversion-rate-gear-icon.png)

   다음 [!UICONTROL 열] 설정 대화 상자가 표시됩니다.

   ![열 설정 대화 상자](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. 선택 취소 **[!UICONTROL 백분율]** 확인란.

   이제 A4T 패널에 백분율이 로 포함되지 않습니다. [!UICONTROL 전환율] 및 일치 [!DNL Target], 아래와 같이 표시됩니다.

   ![백분율을 표시하지 않는 전환율 열](/help/integrations/assets/no-percentages.png)

### A4T 패널에서 날짜 및 시간 정렬 {#aligning-date-and-time}

1. 각 패널 아래에서 패널이 참조하는 날짜 범위를 확인하여 날짜 범위가 의 날짜 범위와 일치하는지 확인하십시오. [!DNL Target] 보고서.

   ![A4T 패널의 날짜 범위](/help/integrations/assets/date-range.png)

1. 위치 [!DNL Analytics], 시간 범위를 오전 12:00부터 오후 11:59까지로 설정합니다.

### 활동 우승자 식별 {#winner}

[!DNL Auto-Allocate] 활동 우승자는 신뢰도 값이 95% 이상인 우승 전환율이 있는 경우 선택됩니다. 이러한 값은 [!DNL Target] 신뢰도 계산이 더 보수적인 방법을 반영하므로 보고서 [!DNL Target] 다음을 권장합니다. [!UICONTROL 자동 할당] 활동. 다음을 참조하십시오 [자동 할당의 통계적 보장](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} 다음에서 *[!UICONTROL Adobe Target 비즈니스 실무자 안내서]*.

>[!NOTE]
>
아직 우승자 없음 및 우승자 배지는 의 A4T 패널에서 사용할 수 없습니다 [!DNL Analysis Workspace]. 또한 우승자 &quot;별&quot; 배지가에 표시됨 [!DNL Target] 보고서 대상 [!UICONTROL 자동 할당] 활동은 무시해야 합니다. 다음을 참조하십시오 [자동 할당](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} 위치: *자동 할당 및 자동 타겟 활동에 대한 A4T 지원* 다음에서 *[!UICONTROL Adobe Target 비즈니스 실무자 안내서]*.

### 용 A4T 만들기 [!UICONTROL 자동 할당] 패널 위치 [!DNL Analysis Workspace]

1. 용 A4T 패널을 만들려면 [!UICONTROL 자동 할당] 활동 보고서, 다음으로 시작 [!UICONTROL Analytics for Target] 패널 위치 [!DNL Analysis Workspace]아래에 표시된 대로 를 클릭합니다.

   ![Analytics for Target - 자동 할당 보고서](/help/integrations/assets/a4t-auto-allocate-report.png)

1. 다음을 선택합니다.

   * **[!UICONTROL 제어 경험]**: 경험을 선택합니다.
   * **[!UICONTROL 지표 표준화]**: 선택 **[!UICONTROL 방문자 수]** (기본적으로 A4T 패널에 포함됨). [!UICONTROL 자동 할당] 항상 고유 방문자에 의한 전환율을 표준화합니다.
   * **성공 지표**: 활동 생성 중에 사용한 것과 동일한 (최적화) 지표를 선택합니다. 이 항목이 [!DNL Target]-정의된 전환 지표, 선택 **[!UICONTROL 활동 전환]**. 그렇지 않으면 [!DNL Adobe Analytics] 사용한 지표입니다.









