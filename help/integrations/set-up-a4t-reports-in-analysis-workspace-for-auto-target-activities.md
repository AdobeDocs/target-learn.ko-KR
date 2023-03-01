---
title: 에서 A4T 보고서를 설정하는 방법 [!DNL Analysis Workspace] 대상 [!DNL Auto-Target] 활동
description: 에서 A4T 보고서를 구성하는 방법 [!DNL Analysis Workspace] 을(를) 실행할 때 예상한 결과를 얻으려면 [!UICONTROL 자동 Target] 활동?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium" tooltip="See what's included in Target Premium."
badgeBeta: label="Beta" type="Informative"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 12dc82a96a8df234d02dc56e9e5904571f2152ba
workflow-type: tm+mt
source-wordcount: '2636'
ht-degree: 1%

---

# 에서 A4T 보고서 설정 [!DNL Analysis Workspace] 대상 [!DNL Auto-Target] 활동

>[!NOTE]
>
>이 기능은 현재 베타 버전이며 모든 사용자가 사용할 수 있습니다. [Target Premium](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium){target=_blank} 예정된 릴리스의 고객.

>[!IMPORTANT]
>
>대상 [!UICONTROL 자동 Target] 활동에서 보고를 확인해야 합니다. [!DNL Analytics Workspace] 및 를 수동으로 만들어 A4T 패널을 만듭니다.

다음 [!UICONTROL Target 분석] 용 (A4T) 통합 [!DNL Auto-Target] 활동 사용 [!DNL Adobe Target]의 ML(Ensemble Machine Learning) 알고리즘 을 사용하여 프로필, 동작 및 컨텍스트를 기반으로 각 방문자에게 가장 적합한 경험을 선택합니다. [!DNL Adobe Analytics] 목표 지표.

다양한 분석 기능은에서 사용할 수 있습니다 [!DNL Adobe Analytics] [!DNL Analysis Workspace], 기본값에 대한 몇 가지 수정 사항 **[!UICONTROL Target 분석]** 올바르게 해석하려면 패널이 필요합니다. [!DNL Auto-Target] 실험 활동(수동 A/B 및 자동 할당)과 개인화 활동([!UICONTROL 자동 Target]).

이 자습서에서는 분석을 위한 권장 수정 사항을 안내합니다 [!UICONTROL 자동 Target] 의 활동 [!DNL Workspace]: 다음 주요 개념을 기반으로 합니다.

* 다음 **[!UICONTROL 제어 및 타깃팅]** 차원은 제어 경험과 에서 제공하는 경험을 구별하는 데 사용할 수 있습니다. [!UICONTROL 자동 Target] ensemble ML 알고리즘.
* 경험 수준 성능 분류를 볼 때 방문 횟수를 표준화 지표로 사용해야 합니다. 또한, [Adobe Analytics의 기본 계산 방법론에는 사용자가 활동 컨텐츠를 실제로 보지 않는 방문 횟수가 포함될 수 있습니다](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics)적절한 범위의 세그먼트를 사용하여 이 기본 동작을 수정할 수 있습니다(아래에 자세히 설명).
* 방문 전환 확인 범위 속성(지정된 속성 모델에서 &quot;방문 전환 확인 기간&quot;이라고도 함)은 다음 위치에서 사용됩니다. [!DNL Adobe Target]교육 단계 동안의 의 ML 모델 및 목표 지표를 분류할 때 동일한(기본값이 아닌) 속성 모델을 사용해야 합니다.

## 용 A4T 만들기 [!UICONTROL 자동 Target] 패널 위치 [!DNL Workspace]

용 A4T를 만들려면 [!UICONTROL 자동 Target] 보고서, 다음 중 하나로 시작 **[!UICONTROL Target 분석]** 패널 위치 [!DNL Workspace]아래에 표시된 대로 또는 자유 형식 테이블로 시작합니다. 그런 다음 다음을 선택합니다.

1. **[!UICONTROL 제어 경험]**: 모든 경험을 선택할 수 있지만 나중에 이 선택을 재정의합니다. 에 대한 참고 사항 [!UICONTROL 자동 Target] 활동. 제어 경험은 실제로 제어 전략이며, a) 모든 경험 중에서 임의로 제공되거나 b) 단일 경험을 제공합니다(이 선택은 의 활동 생성 시 수행됩니다). [!DNL Adobe Target]). (b)를 선택했더라도 [!UICONTROL 자동 Target] 활동은 특정 경험을 제어로 지정했습니다. 이에 대한 A4T 분석을 위해서는 이 자습서에 설명된 접근 방식을 따라야 합니다 [!UICONTROL 자동 Target] 활동.
2. **[!UICONTROL 지표 표준화]**: 방문 횟수 를 선택합니다.
3. **[!UICONTROL 성공 지표]**: 보고할 지표를 선택할 수 있지만 일반적으로 의 활동 생성 중 최적화를 위해 선택한 동일한 지표에 대한 보고서를 확인해야 합니다 [!DNL Target].

![그림1.png](assets/Figure1.png)
*그림 1: [!UICONTROL Target 분석] 패널 설정 [!UICONTROL 자동 Target] 활동.*

>[!NOTE]
>
>을(를) 설정하려면 [!UICONTROL Target 분석] 패널 [!UICONTROL 자동 Target] 활동, 제어 경험 선택, 선택 [!UICONTROL 방문 횟수] 표준화 지표로, 그리고 다음 기간 동안 최적화를 위해 선택한 것과 동일한 목표 지표를 선택합니다 [!DNL Target] 활동 만들기.

## 사용 [!UICONTROL 제어 및 타깃팅] 비교할 차원 [!DNL Target] 컨트롤에 앙상블 ML 모델

기본 A4T 패널은 클래식(수동) A/B 테스트용 또는 [!UICONTROL 자동 할당] 목표가 개별 경험의 성과를 제어 경험과 비교하는 활동입니다. 위치 [!UICONTROL 자동 Target] 그러나 활동의 첫 번째 순서는 컨트롤 간의 비교여야 합니다. *전략* 및 타깃팅됨 *전략* (즉, 전체 성능 상승도 결정) [!UICONTROL 자동 Target] ensemble ML 모델(제어 전략에 대한).

이 비교를 수행하려면 **[!UICONTROL 제어 및 타깃팅(Target 분석)]** 차원. 드래그 앤 드롭하여 바꾸기 **[!UICONTROL Target 경험]** 기본 A4T 보고서의 차원입니다.

이 대체 함수는 A4T 패널에서 기본 상승도 및 신뢰도 계산을 무효화합니다. 혼동을 방지하기 위해 다음 보고서를 남겨두고 기본 패널에서 이러한 지표를 제거할 수 있습니다.

![Figure2.png](assets/Figure2.png)

*그림 2: 권장되는 기준 보고서 [!DNL Auto-Target] 활동. 이 보고서는 타깃팅된 트래픽(앙상블 ML 모델에서 제공됨)을 제어 트래픽과 비교하도록 구성되었습니다.*

>[!NOTE]
>
>현재, 상승도 및 신뢰도 수치는 다음에 사용할 수 없습니다. [!UICONTROL 제어 및 타깃팅] 용 A4T 보고서 차원 [!UICONTROL 자동 Target]. 지원이 추가되기 전까지 를 다운로드하여 상승도 및 신뢰도를 수동으로 계산할 수 있습니다. [신뢰도 계산기](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## 지표의 경험 수준 분류 추가

앙상블 ML 모델이 어떻게 작동하는지 자세히 알아보려면 의 경험 수준 분류를 검사할 수 있습니다. **[!UICONTROL 제어 및 타깃팅]** 차원. 위치 [!DNL Workspace]를 클릭하고 **[!UICONTROL Target 경험]** 차원을 보고서에 가져온 다음 각 제어 및 타깃팅된 차원을 별도로 분류합니다.

![Figure3.png](assets/Figure3.png)
*그림 3: Target 경험별로 타겟팅된 차원 분류*

결과 보고서의 예가 여기에 나와 있습니다.

![그림4.png](assets/Figure4.png)
*그림 4: 표준 [!UICONTROL 자동 Target] 경험 수준 분류로 보고합니다. 목표 지표는 다를 수 있으며 제어 전략에는 단일 경험이 있을 수 있습니다.*

>[!TIP]
>
>위치 [!DNL Workspace]에서 비율을 숨기려면 톱니바퀴 아이콘을 클릭합니다. [!UICONTROL 전환율] 열: 경험 전환율에 초점을 유지할 수 있습니다. 전환율은 소수점 형식으로 지정되지만, 그에 따라 백분율로 해석됩니다.

## &quot;방문 횟수&quot;가 다음에 대한 올바른 표준화 지표인 이유 [!UICONTROL 자동 Target] 활동

분석 시 [!UICONTROL 자동 Target] 활동, 항상 선택 [!UICONTROL 방문 횟수] 를 기본 표준화 지표로 사용합니다. [!UICONTROL 자동 Target] 개인화는 방문당 한 번(공식적으로 한 번) 방문자에 대한 경험을 선택합니다. [!DNL Adobe Target] session) - 사용자에게 표시되는 경험이 모든 방문 시 변경될 수 있음을 의미합니다. 따라서 다음을 사용하는 경우 [!UICONTROL 고유 방문자 수] 표준화 지표로서 단일 사용자가 (서로 다른 방문에 대해) 여러 경험을 보게 될 수 있다는 사실은 전환율을 혼란스럽게 할 수 있습니다.

간단한 예는 이 점을 보여 줍니다. 두 명의 방문자가 두 개의 경험만 있는 캠페인을 입력하는 시나리오를 생각해 보십시오. 첫 번째 방문자가 두 번 방문합니다. 이 경험은 첫 번째 방문에서는 경험 A에 할당되지만, 두 번째 방문에서는 프로필 상태가 변경되어 경험 B에 할당됩니다. 두 번째 방문 후에 방문자는 주문을 하여 전환됩니다. 전환은 가장 최근에 표시된 경험(경험 B)에 기인합니다. 두 번째 방문자도 두 번 방문하고, 두 번 모두 경험 B가 표시되지만, 전환되지는 않습니다.

방문자 수준 및 방문 수준 보고서를 비교해 보겠습니다.

| 경험 | 고유 방문자 수 | 방문 횟수 | 변환 | Visitor norm. 콘브 비율 | 노름 방문. 콘브 비율 |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| 총계 | 2 | 4 | 1 | 50% | 25% |

*표 1: 결정이 방문에 고정(일반 A/B 테스트와 마찬가지로 방문자가 아님)되는 시나리오에 대한 방문자 표준화 보고서와 방문 표준화 보고서를 비교하는 예제. 이 시나리오에서는 방문자 표준화 지표가 혼란을 겪고 있습니다.*

표에서 보듯이 방문자 수준 숫자의 명백한 부조화가 있습니다. 총 두 명의 고유 방문자가 있음에도 불구하고 각 경험에 대한 개별 고유 방문자의 합이 아닙니다. 방문자 수준 전환율이 반드시 잘못된 것은 아니지만 개별 경험을 비교할 때 방문 수준 전환율이 훨씬 더 적절합니다. 형식적으로 분석 단위(&quot;방문 횟수&quot;)는 의사 결정 고착성의 단위와 동일하며, 이는 지표의 경험 수준 분류를 추가하고 비교할 수 있음을 의미합니다.

## 활동에 대한 실제 방문 필터링

다음 [!DNL Adobe Analytics] 방문에 대한 기본 계산 방법론 [!DNL Target] 활동에는 사용자가 와 상호 작용하지 않은 방문이 포함될 수 있습니다. [!DNL Target] 활동. 이것은 다음 이유로 인한 것입니다. [!DNL Target] 활동 할당은에서 유지됩니다. [!DNL Analytics] 방문자 컨텍스트. 결과적으로 방문에 대한 횟수입니다 [!DNL Target] 활동은 때때로 부풀려져 전환율 저하를 초래할 수 있습니다.

사용자가 실제로 상호 작용한 방문에 대해 보고하려는 경우 [!UICONTROL 자동 Target] 활동(활동 항목, 디스플레이/방문 이벤트 또는 전환을 통해)에서는 다음 작업을 수행할 수 있습니다.

1. 의 히트를 포함하는 특정 세그먼트를 만듭니다. [!DNL Target] 해당 활동 및
1. 필터 [!UICONTROL 방문 횟수] 이 세그먼트를 사용하는 지표.

**세그먼트를 만들려면 다음 작업을 수행하십시오.**

1. 다음 항목 선택 **[!UICONTROL 구성 요소 > 세그먼트 만들기]** 의 옵션 [!DNL Workspace] 도구 모음
2. 입력 **[!UICONTROL 제목]** 세그먼트. 아래 표시된 예에서 세그먼트 이름은 입니다 [!DNL "Hit with specific Auto-Target activity"].
3. 드래그 **[!UICONTROL Target 활동]** 세그먼트에 대한 차원 **[!UICONTROL 정의]** 섹션.
4. 사용 **[!UICONTROL 다음과 같음]** 연산자.
5. 특정 항목 검색 [!DNL Target] 활동.
6. 톱니바퀴 아이콘을 선택한 다음, **[!UICONTROL 속성 모델 > 인스턴스]** 아래 그림과 같이.
7. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

![그림5.png](assets/Figure5.png)
*그림 5: 여기에 표시된 세그먼트와 같은 세그먼트를 사용하여 [!UICONTROL 방문 횟수] 다음에 대한 A4T의 지표 [!UICONTROL 자동 Target] 보고서*

세그먼트가 만들어지면 이를 사용하여 다음을 필터링합니다. [!UICONTROL 방문 횟수] 지표, 따라서 [!UICONTROL 방문 횟수] 지표에는 사용자가 와 상호 작용한 방문만 포함됩니다. [!DNL Target] 활동.

**필터링하려면 [!UICONTROL 방문 횟수] 이 세그먼트 사용:**

1. 구성 요소 도구 모음에서 새로 만든 세그먼트를 드래그하여 아래쪽의 **[!UICONTROL 방문 횟수]** 파란색까지 지표 레이블 **[!UICONTROL 필터링 기준]** 프롬프트가 나타납니다.
2. 세그먼트를 해제합니다. 해당 지표에 필터가 적용됩니다.

최종 패널은 다음과 같이 표시됩니다.

![그림 6.png](assets/Figure6.png)
*그림 6: &quot;특정 자동 Target 활동이 있는 히트&quot; 세그먼트가 다음에 적용된 보고 패널 [!UICONTROL 방문 횟수] 지표. 이렇게 하면 사용자가 실제로 와 상호 작용한 방문만 보장됩니다. [!DNL Target] 해당 활동은 보고서에 포함됩니다.*

## 목표 지표 및 속성이 최적화 기준과 일치하는지 확인합니다

A4T 통합을 통해 [!UICONTROL 자동 Target] ML 모델 *교육* 와 동일한 전환 이벤트 데이터 사용 [!DNL Adobe Analytics] 사용 대상 *성능 보고서 생성*. 그러나 ML 모델을 교육할 때 이 데이터를 해석할 때 사용해야 하는 특정 가정이 있으며, 이는 의 보고 단계에서 수행되는 기본 가정과 다릅니다 [!DNL Adobe Analytics].

특히 [!DNL Adobe Target] ML 모델은 방문 범위 속성 모델을 사용합니다. 즉, 전환이 ML 모델에서 내린 결정에 &quot;기여하도록&quot; 전환하려면 활동에 대한 콘텐츠 표시와 동일한 방문에서 전환이 발생해야 한다고 가정합니다. 다음에 필요합니다. [!DNL Target] 적시에 해당 모델을 교육할 수 있도록 [!DNL Target] 전환(의 보고서에 대한 기본 속성 창)을 위해 최대 30일까지 대기할 수 없습니다. [!DNL Adobe Analytics]), 모델을 위한 교육 데이터에 포함하기 전에.

따라서 가 사용하는 속성 간의 차이는 [!DNL Target] 모델(교육 중)과 데이터 쿼리에 사용된 기본 속성(보고서 생성 중)의 비교 결과 불일치가 발생할 수 있습니다. ML 모델이 실제로 속성에 문제가 있을 때 제대로 작동하지 않는 것처럼 보일 수도 있습니다.

>[!TIP]
>
>ML 모델이 보고서에서 보고 있는 지표와 다르게 기여하는 지표에 대해 최적화하는 경우 모델이 예상대로 수행되지 않을 수 있습니다. 이를 방지하려면 보고서의 목표 지표가 Target의 ML 모델에서 사용하는 것과 동일한 지표 정의 및 속성을 사용하는지 확인하십시오.

정확한 지표 정의 및 속성 설정은 [최적화 기준](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported) 활동을 만드는 동안 을(를) 지정했습니다.

### Target 정의 전환 또는 를 사용하는 Analytics 지표 *방문당 지표 값 최대화*

지표가 Target 전환이거나 를 사용하는 Analytics 지표인 경우 **방문당 지표 값 최대화**, 목표 지표 정의를 사용하면 동일한 방문에서 여러 전환 이벤트가 발생할 수 있습니다.
Adobe Target의 ML 모델에서 사용하는 것과 동일한 속성 방법론이 있는 목표 지표를 보려면 다음 단계를 수행합니다.

![gearicon.png](assets/gearicon.png)

1. 결과 메뉴에서 다음으로 스크롤 **[!UICONTROL 데이터 설정]**.
1. 선택 **[!UICONTROL 기본이 아닌 속성 모델 사용]** (아직 선택하지 않은 경우):

![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. **[!UICONTROL 편집]**&#x200B;을 클릭합니다.
1. 선택 **[!UICONTROL 모델]**: **[!UICONTROL 기여도]**, 및 **[!UICONTROL 전환 확인 기간]**: **[!UICONTROL 방문]**.

![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. **[!UICONTROL 적용]**&#x200B;을 클릭합니다.

이 단계에서는 목표 지표 이벤트가 발생한 경우 목표 지표가 경험 표시에 기여하도록 합니다 *언제든지* (&quot;참여&quot;) 경험을 표시한 동일한 방문에 속합니다.

### 를 사용하는 Analytics 지표 *고유 방문 전환율*

**양성 지표 세그먼트로 방문 정의**

을(를) 선택한 시나리오에서 *고유 방문 전환율 최대화* 최적화 기준으로서, 전환율에 대한 올바른 정의는 지표 값이 양수인 방문 횟수의 비율입니다. 이 작업은 지표가 양수 값을 갖는 방문으로 필터링하는 세그먼트를 만든 다음 방문 지표를 필터링하여 수행할 수 있습니다.


1. 이전과 같이 **[!UICONTROL 구성 요소 > 세그먼트 만들기]** 옵션을 선택합니다.
2. 입력 **[!UICONTROL 제목]** 세그먼트. 아래 표시된 예에서 세그먼트 이름은 입니다 [!DNL "Visits with an order"].
3. 최적화 목표에서 사용한 기본 지표를 세그먼트로 드래그합니다. 아래 표시된 예에서는 **주문 수** 지표를 사용하여 전환이 주문이 기록된 방문 비율을 측정하도록 합니다.
4. 세그먼트 정의 컨테이너의 왼쪽 상단에서 을 선택합니다. **[!UICONTROL 포함]** **방문**.
5. 사용 **[!UICONTROL 다음보다 큼]** 연산자 를 실행하고 값을 0으로 설정합니다(즉, 이 세그먼트에는 주문 지표가 양수인 방문이 포함됨).
6. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

![그림7.png](assets/Figure7.png)
*그림 7: 양수 순서가 있는 방문에 대한 세그먼트 정의 필터링 활동의 최적화 지표에 따라 주문을 적절한 지표로 대체해야 합니다*

**활동 필터링 지표에서 방문 횟수에 적용**

이제 이 세그먼트를 사용하여 양의 주문 수가 있는 방문 및 다음에 대한 히트가 있는 방문으로 필터링할 수 있습니다. [!DNL Auto-Target]활동. 지표 필터링 절차는 이전과 유사하며, 이미 필터링된 방문 지표에 새 세그먼트를 적용한 후에는 보고서 패널이 그림 8과 같이 표시되어야 합니다

![그림8.png](assets/Figure8.png)
*그림 8: 올바른 고유 방문 전환 지표(즉, 활동의 히트가 기록된 방문 수와 전환 지표(이 예제의 주문)가 0이 아닌 방문 수)가 있는 보고서 패널.*


## 마지막 단계: 위의 마법을 캡처하는 전환율 만들기

에 대한 수정 사항 포함 [!UICONTROL 방문] 및 이전 섹션의 목표 지표는 의 기본 A4T에 대해 최종 수정해야 합니다. [!UICONTROL 자동 Target] 보고 패널은 적절하게 필터링된 목표에 대한 올바른 속성이 있는 목표 지표의 올바른 비율인 전환율을 만드는 것입니다 [!UICONTROL 방문 횟수] 지표.

다음 단계를 사용하여 계산된 지표를 만들어 이 작업을 수행합니다.

1. 다음 항목 선택 **[!UICONTROL 구성 요소 > 지표 만들기]** 의 옵션 [!DNL Workspace] 도구 모음
1. 입력 **[!UICONTROL 제목]** 을 참조하십시오. 예를 들어 &quot;활동 XXX에 대한 방문 수정 전환율&quot;이 있습니다.
1. 선택 **[!UICONTROL 형식]** = 백분율 및 **[!UICONTROL 소수점 이하 자리 수]** = 2.
1. 활동에 대한 관련 목표 지표를 드래그합니다(예: [!UICONTROL 활동 전환])를 정의에 추가하고, 이 목표 지표의 톱니바퀴 아이콘을 사용하여 앞에서 설명한 대로 기여도 분석 모델을 (참여|방문)으로 조정합니다.
1. 선택 **[!UICONTROL 추가 > 컨테이너]** 의 오른쪽 상단에서 **[!UICONTROL 정의]** 섹션.
1. 두 컨테이너 간÷ 나눗셈(나눗셈) 연산자를 선택합니다.
1. 이전에 만든 세그먼트(&quot;Hit with specific&quot;)를 드래그합니다. [!UICONTROL 자동 Target] 이 자습서의 &quot;activity&quot; - 다음을 위한 [!DNL Auto-Target] 활동.
1. 드래그 **[!UICONTROL 방문 횟수]** 세그먼트 컨테이너에 대한 지표입니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

>[!TIP]
>
> 를 사용하여 이 지표를 만들 수도 있습니다. [빠른 계산된 지표 기능](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en).

전체 계산된 지표 정의가 여기에 표시됩니다.

![Figure9.png](assets/Figure9.png)
*그림 9: 방문 및 속성이 수정된 모델 전환율 지표 정의. (이 지표는 목표 지표 및 활동에 따라 다릅니다. 즉, 이 지표 정의는 활동 간에 다시 사용할 수 없습니다.)*

>[!IMPORTANT]
>
>A4T 패널의 전환율 지표는 테이블의 전환 이벤트나 표준화 지표에 연결되어 있지 않습니다. 이 자습서에서 제안한 내용을 수정해도 전환율이 변경 사항에 자동으로 조정되지 않습니다. 따라서 전환 이벤트 속성 및 표준화 지표 중 하나(또는 둘 다)를 수정하는 경우 위와 같이 전환율도 수정하는 마지막 단계로 기억해야 합니다.

## 요약: 최종 샘플 [!DNL Workspace] 패널 [!UICONTROL 자동 Target] 보고서

위의 모든 단계를 단일 패널에 결합하면 아래 그림에 권장 보고서에 대한 전체 보기가 표시됩니다. [!UICONTROL 자동 Target] A4T 활동. 이 보고서는 [!DNL Target] 목표 지표를 최적화하기 위한 ML 모델이며, 이 자습서에 설명된 모든 뉘앙스와 권장 사항이 통합되어 있습니다. 이 보고서는 기존 계산 방법론과 가장 유사합니다 [!DNL Target]- 보고 중심 [!UICONTROL 자동 Target] 활동.

![그림 10.png](assets/Figure10.png)
*그림 10: 최종 A4T [!UICONTROL 자동 Target] 보고서 위치: [!DNL Adobe Analytics] [!DNL Workspace]: 이 문서의 이전 섹션에 설명된 지표 정의에 대한 모든 조정을 결합합니다.*
