---
title: 에서 A4T 보고서를 설정하는 방법 [!DNL Analysis Workspace] 대상 [!UICONTROL 자동 할당] 활동
description: 에서 A4T 보고서를 구성하는 방법 [!DNL Analysis Workspace] 실행 시 예상되는 결과를 얻으려면 [!UICONTROL 자동 할당] 활동.
role: User
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#beta newtab=true" tooltip="What are Target Beta release features?"
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 1dc33affb1e9782f1b9c1d01402124dd40dac436
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# 에서 A4T 보고서 설정 [!DNL Analysis Workspace] 대상 [!DNL Auto-Allocate] 활동

An [!DNL Auto-Allocate] 활동은 둘 이상의 경험에서 승자를 식별하고, 테스트가 계속 실행되고 학습되는 동안 더 많은 트래픽을 승자에게 자동으로 재할당합니다. 다음 [!UICONTROL Target 분석] (A4T) 통합 [!UICONTROL 자동 할당] 에서는 보고 데이터를 볼 수 있습니다. [!DNL Adobe Analytics], 및에 정의된 사용자 지정 이벤트 또는 지표에 대해서도 최적화할 수 있습니다. [!DNL Analytics].

다양한 분석 기능은에서 사용할 수 있지만 [!DNL Adobe Analytics] [!DNL Analysis Workspace], 기본값에 대한 몇 가지 수정 사항 **[!UICONTROL Target 분석]** 패널을 올바르게 해석하려면 [!DNL Auto-Allocate] 활동, 즉 [최적화 기준](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

이 자습서에서는 분석을 위한 권장 수정 사항을 안내합니다 [!DNL Auto-Allocate] 활동 [!DNL Analysis Workspace]. 주요 개념은 다음과 같습니다.

* [!UICONTROL 방문자 수] 는 항상 의 정규화 지표로 사용해야 합니다. [!DNL Auto-Allocate] 활동.
* 지표가 [!DNL Adobe Analytics] 지표에서 전환율에 대한 적절한 분자는 활동 설정 중에 선택한 최적화 기준의 유형에 따라 달라집니다.
   * &quot;고유 방문자 전환율 최대화&quot; 최적화 기준에는 분자가 지표의 양수 값을 가진 고유 방문자 수의 카운트인 전환율이 있습니다.
   * 방문자당 지표 값 최대화&quot;에는 분자가 의 일반 지표 값인 전환율이 있습니다 [!DNL Adobe Analytics]. 기본적으로 **[!UICONTROL Target 분석]** 패널 [!DNL Analysis Workspace].
* 최적화 지표가 [!DNL Target] 정의된 전환 지표, 기본값 **[!UICONTROL Target 분석]** 패널 [!DNL Analysis Workspace] 패널 구성을 처리합니다.
* 모든 경우에 [!UICONTROL 자동 할당] 이전에 만들어진 활동 [!DNL Target Standard/Premium] 23.3.1 릴리스(2023년 3월 28일) [!DNL Analytics Workspace] 및 [!DNL Target] 에 대해 동일한 값 표시 [!UICONTROL 신뢰도].

   모든 경우에 [!UICONTROL 자동 할당] 2023년 3월 28일 이후에 만들어진 신뢰 구간 값은에 표시됩니다. [!DNL Analysis Workspace] 반영하지 않음 [에 사용되는 보다 보수적인 통계 [!UICONTROL 자동 할당]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} 이러한 활동이 *둘 다* 다음 조건 중 하나를 선택합니다.

   * [!DNL Analytics] 를 보고 소스로 사용(A4T)
   * [!DNL Analytics] 최적화 지표

   If *둘 다* 이러한 조건 중 A4T 패널에서 신뢰 지표를 제거해야 합니다. 대신 다음 값을에서 참조합니다. [!DNL Target] 보고.

## 용 A4T 만들기 [!DNL Auto-Allocate] 패널 [!DNL Analysis Workspace]

에 대한 A4T를 만들려면 [!DNL Auto-Allocate] 보고서 시작 **[!UICONTROL Target 분석]** 패널 [!DNL Analysis Workspace]아래에 표시된 대로, 그런 다음 다음을 선택합니다.

1. **[!UICONTROL 제어 경험]**: 원하는 경험을 선택할 수 있습니다.
2. **[!UICONTROL 지표 정규화]**: 방문자를 선택합니다. [!DNL Auto-Allocate] 고유 방문자별로 항상 전환율을 정규화합니다.
3. **[!UICONTROL 성공 지표 를 참조하십시오]**: 활동을 만들 때 사용한 것과 동일한 지표를 선택합니다. 만약 [!DNL Target] 정의된 전환 지표, 선택 **활동 전환**. 그렇지 않으면 [!DNL Adobe Analytics] 사용한 지표.

![[!UICONTROL Target 분석] 패널 설정 [!DNL Auto-Allocate] 활동.](assets/AAFigure1.png)

*그림 1: [!UICONTROL Target 분석] 패널 설정 [!DNL Auto-Allocate] 활동.*

>[!NOTE]
>
> 또한 사전 빌드된 **[!UICONTROL Target 분석]** 패널의 보고서 화면에서 링크를 클릭하면 표시됩니다. [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL 전환] 지표 또는 [!DNL Analytics] &quot;방문자당 지표 값 최대화&quot; 최적화 기준이 있는 지표

기본 A4T 패널 핸들 [!DNL Auto-Allocate] 목표 지표가 [!DNL Target] 전환 또는 [!DNL Analytics] 최적화 기준이 있는 지표 &quot;방문자당 지표 값 최대화&quot;입니다.

이 패널의 한 예는 [!UICONTROL 매출] 지표. 여기서 &quot;방문자당 지표 값 최대화&quot;는 활동 생성 시 최적화 기준으로 선택되었습니다. 앞서 언급했듯이 [!DNL Auto-Allocate] 에서는 보다 보수적 신뢰 계산을 사용하는데, **[!UICONTROL Target 분석]** 패널. Adobe은 A4T 패널과 관련된 하위 및 상위 상승도 지표에서 신뢰 지표를 제거할 것을 권장합니다. 대신 다음 값을에서 참조하십시오. [!DNL Target] 보고.

![[!UICONTROL Target 분석 - 자동 할당 보고서] 패널](assets/AAFigure2.png)

*그림 2: 에 대한 권장 보고서 [!DNL Auto-Allocate] 을 사용하여 활동 [!DNL Analytics] 지표 &quot;방문자당 지표 값 최대화&quot; 기준. 이러한 유형의 지표와 [!DNL Target] 정의된 전환 지표, 기본값&#x200B;**[!UICONTROL Target 분석]**패널 [!DNL Analysis Workspace] 사용할 수 있습니다.*

## [!DNL Analytics] &quot;고유 방문자 전환율 최대화&quot; 최적화 기준을 사용한 지표

다음 경우에 [!DNL Adobe Analytics] 지표는 의 최적화 기준과 함께 사용됩니다 *고유 방문자 전환율 최대화*, 기본 **[!UICONTROL Target 분석]** 패널 [!DNL Analysis Workspace] 를 수정해야 합니다.

이제 성공 지표는 전환 지표가 긍정적이었던 고유 방문자 수입니다. 이 작업은 양의 지표 값이 있는 히트로 필터링하는 세그먼트를 만들어 수행할 수 있습니다. 이 세그먼트를 다음과 같이 만듭니다.

1. 을(를) 선택합니다 **[!UICONTROL 구성 요소]** > **[!UICONTROL 세그먼트 만들기]** 옵션 [!DNL Analysis Workspace] 도구 모음
1. 활동 생성 시 사용된 지표를 왼쪽 패널에서 로 드래그합니다 **[!UICONTROL 정의]** 상자에 표시되지 않습니다.
1. 지표의 값을 선택합니다 **보다 큼** 0의 숫자 값입니다.
1. 에서 **[!UICONTROL 포함]** 드롭다운에서 을 선택합니다. **[!UICONTROL 방문자 수]**.
1. 세그먼트에 적절한 이름을 지정합니다.

세그먼트 만들기의 예는 아래 그림에 표시되어 있습니다. 여기서 를 선택합니다 [!UICONTROL 긍정적인 수입이 있는 방문자].

![[!UICONTROL 긍정적인 수입이 있는 방문자] 세그먼트 [!DNL Analysis Workspace]](assets/AAFigure3.png)

*그림 3: 세그먼트 생성 대상 [!DNL Adobe Analytics] 최적화 기준이 &quot;과 동일한 지표[!UICONTROL 고유 방문자 전환율 최대화].&quot; 이 예에서 지표는 다음과 같습니다 [!UICONTROL 매출], 및 최적화 목표는 긍정적인 매출로 방문자 수를 최대화하는 것입니다.*

해당 세그먼트가 만들어지면, 기본값은 입니다  **[!UICONTROL Target 분석]** 패널 [!DNL Analysis Workspace] 수정할 수 있습니다.

1. 초 추가 **고유 방문자 수** 기존 지표와 함께 [!UICONTROL 방문자 수] 지표 열 을 참조하십시오.
2. 첫 번째 열 아래에 새로 만든 세그먼트를 드래그하여 그림 4와 유사한 패널을 만듭니다. 차이점 확인: 매출에 긍정적인 고유 방문자 수는 각 경험에 할당된 총 고유 방문자 수의 일부입니다.

   ![그림 4.png](assets/AAFigure4.png)

   *그림 4: 필터링 [!UICONTROL 고유 방문자 수] 새로 만든 세그먼트에 의해*

3. 전환율은 [빠르게 계산](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) 첫 번째 열과 두 번째 열을 모두 강조 표시하고 마우스 오른쪽 단추를 클릭하여 선택 **[!UICONTROL 선택 항목에서 지표 만들기]** > **[!UICONTROL 나누기]**.

   기본 전환율은 아래 이미지와 같이 제거하고 이 새 계산된 지표로 대체해야 합니다. 새로 만든 계산된 지표를 편집하여 **[!UICONTROL 형식]** > **[!UICONTROL Percent]** 표시된 대로 최대 2개의 소수 자리를 사용할 수 있습니다.

   ![그림 5.png](assets/AAFigure5.png)

   *그림 5: 마지막 [!UICONTROL 자동 할당] 쌍된 수입 전환 지표에 대한 전환율을 보여주는 패널*

## 요약

이 자습서의 단계는 를 올바르게 구성하는 방법에 대해 보여줍니다 [!DNL Analysis Workspace] 표시 [!UICONTROL 자동 할당] 보고 데이터.

요약하려면 다음을 수행하십시오.

* 지표가 [!DNL Target] 정의된 전환 지표 또는 [!DNL Adobe Analytics] 최적화 기준이 &quot;방문자당 지표 값 최대화&quot;인 지표는 정규화 지표로 방문자로 구성된 기본 작업 공간 패널을 사용해야 합니다.
* 지표가 [!DNL Adobe Analytics] 최적화 기준이 &quot;고유 방문자 전환율 최대화&quot;인 지표는 지표가 긍정인 방문자의 분수로 정의된 전환율을 사용해야 합니다. 이 작업은 세그먼트를 [!UICONTROL 고유 방문자] 지표.
