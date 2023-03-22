---
title: 에서 A4T 보고서를 설정하는 방법 [!DNL Analysis Workspace] 대상 [!DNL Auto-Target] 활동
description: 에서 A4T 보고서를 구성하는 방법 [!DNL Analysis Workspace] 실행 시 예상되는 결과를 얻으려면 [!UICONTROL 자동 Target] 활동?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium newtab=true" tooltip="See what's included in Target Premium."
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#beta newtab=true" tooltip="What are Target Beta release features?"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 538dfe6a26b4f62c52b24d54a189738677e63bf3
workflow-type: tm+mt
source-wordcount: '2641'
ht-degree: 1%

---

# 에서 A4T 보고서 설정 [!DNL Analysis Workspace] 대상 [!DNL Auto-Target] 활동

>[!IMPORTANT]
>
>대상 [!UICONTROL 자동 Target] 활동, 보고 위치 확인 [!DNL Analytics Workspace] A4T 패널을 수동으로 만듭니다.

다음 [!UICONTROL Target 분석] (A4T) 통합 [!DNL Auto-Target] 활동은 [!DNL Adobe Target] 앙상블 기계 학습(ML) 알고리즘을 사용하여 프로필, 행동 및 컨텍스트에 따라 각 방문자에 대해 가장 적합한 경험을 선택할 수 있습니다 [!DNL Adobe Analytics] 목표 지표.

다양한 분석 기능은에서 사용할 수 있지만 [!DNL Adobe Analytics] [!DNL Analysis Workspace], 기본값에 대한 몇 가지 수정 사항 **[!UICONTROL Target 분석]** 패널을 올바르게 해석하려면 [!DNL Auto-Target] 실험 활동 간의 차이로 인한 활동(수동 [!UICONTROL A/B 테스트] 및 [!UICONTROL 자동 할당]) 및 개인화 활동( )[!UICONTROL [!UICONTROL 자동 Target]]).

이 자습서에서는 분석을 위한 권장 수정 사항을 안내합니다 [!UICONTROL 자동 Target] 활동 [!DNL Analysis Workspace]- 다음 주요 개념을 기반으로 합니다.

* 다음 **[!UICONTROL 제어 및 타깃팅된]** 차원을 사용하여 [!UICONTROL 제어] 경험 대 [!UICONTROL 자동 Target] 앙상블 ML 알고리즘.
* 방문 횟수는 성능의 경험 수준 분류를 볼 때 정규화 지표로 사용해야 합니다. 게다가, [Adobe Analytics의 기본 계산 방법론에는 사용자가 활동 컨텐츠를 실제로 보지 않는 방문이 포함될 수 있습니다](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html#metrics){target=_blank}하지만 적절한 범위 지정 세그먼트를 사용하여 이 기본 동작을 수정할 수 있습니다(아래 세부 정보).
* 지정된 속성 모델에서 &quot;방문 전환 확인 기간&quot;이라고도 하는 방문 전환 확인 범위 속성은 [!DNL Adobe Target] 교육 단계 동안 ML 모델을 사용하고, 목표 지표를 분류할 때는 동일한(기본값이 아닌) 속성 모델을 사용해야 합니다.

## 용 A4T 만들기 [!UICONTROL 자동 Target] 패널 [!DNL Analysis Workspace]

에 대한 A4T를 만들려면 [!UICONTROL 자동 Target] 보고서, 다음으로 시작 **[!UICONTROL Target 분석]** 패널 [!DNL Analysis Workspace]아래에 표시된 대로 또는 자유 형식 테이블로 시작합니다. 그런 다음 다음을 선택합니다.

1. **[!UICONTROL 제어 경험]**: 원하는 경험을 선택할 수 있습니다. 그러나 이 선택 사항은 나중에 재정의할 수 있습니다. 에 대해 [!UICONTROL 자동 Target] 활동, 제어 경험은 a) 모든 경험에서 임의로 서비스하거나 b) 하나의 경험을 제공합니다(이 선택 사항은 의 활동 생성 시 만들어짐) [!DNL Adobe Target]). 선택(b)을 선택하더라도 [!UICONTROL 자동 Target] 활동은 특정 경험을 제어로 지정했습니다. 다음에 대한 A4T 분석을 위해 이 자습서에 설명된 접근 방식을 따라야 합니다 [!UICONTROL 자동 Target] 활동.
2. **[!UICONTROL 지표 정규화]**: 선택 [!UICONTROL 방문 횟수].
3. **[!UICONTROL 성공 지표 를 참조하십시오]**: 보고할 지표를 선택할 수 있지만 일반적으로 활동을 만들 때 최적화를 위해 선택한 것과 동일한 지표에 대한 보고서를 볼 수 있습니다 [!DNL Target].

   ![[!UICONTROL Target 분석] 패널 설정 [!UICONTROL 자동 Target] 활동.](assets/Figure1.png)

   *그림 1: [!UICONTROL Target 분석] 패널 설정 [!UICONTROL 자동 Target] 활동.*

>[!TIP]
>
>을(를) 설정하려면 [!UICONTROL Target 분석] 패널 대상 [!UICONTROL 자동 Target] 활동, 제어 경험 선택 [!UICONTROL 방문 횟수] 을(를) 정규화 지표로 선택하고 [!DNL Target] 활동을 만들 수 있습니다.

## 를 사용하십시오 [!UICONTROL 제어 및 타깃팅됨] 비교할 차원 [!DNL Target] Ensemble ML 모델을 통해 제어

기본 A4T 패널은 클래식(수동)용으로 설계되었습니다 [!UICONTROL A/B 테스트] 또는 [!UICONTROL 자동 할당] 목표가 개별 경험의 성과를 제어 경험과 비교하는 것입니다. in [!UICONTROL 자동 Target] 그러나 첫 번째 순서 비교는 컨트롤 사이에 있어야 합니다 *전략* 타겟팅한 *전략*. 즉, [!UICONTROL 자동 Target] 제어 전략에 대한 앙상블 ML 모델.

이 비교를 수행하려면 **[!UICONTROL 제어 및 타깃팅된(Target 분석)]** 차원. 을(를) 끌어서 놓아 바꿉니다 **[!UICONTROL Target 경험]** 차원 값을 지정한 경우 이해할 수 있도록 해줍니다.

이 대체는 기본값을 무효화합니다 [!UICONTROL 상승도 및 신뢰도] a4T 패널의 계산. 혼동을 방지하기 위해 다음 보고서를 남겨둔 채 기본 패널에서 이러한 지표를 제거할 수 있습니다.

![[!UICONTROL 전환별 경험] 패널 [!DNL Analysis Workspace]](assets/Figure2.png)

*그림 2: 에 대한 권장 기준 보고서 [!DNL Auto-Target] 활동. 이 보고서는 타깃팅된 트래픽(Ensemble ML 모델에서 제공)을 제어 트래픽과 비교하도록 구성되었습니다.*

>[!NOTE]
>
>현재, [!UICONTROL 상승도 및 신뢰도] 숫자를 사용할 수 없습니다. [!UICONTROL 제어 및 타깃팅된] 에 대한 A4T 보고서의 차원 [!UICONTROL 자동 Target]. 지원이 추가되기 전까지 [!UICONTROL 상승도 및 신뢰도] 를 다운로드하여 수동으로 계산할 수 있습니다. [신뢰도 계산기](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx).

## 지표의 경험 수준 분류 추가

Ensemble ML 모델이 수행되는 방식에 대한 자세한 통찰력을 얻으려면 의 경험 수준 분류를 검사할 수 있습니다 **[!UICONTROL 제어 및 타깃팅된]** 차원. in [!DNL Analysis Workspace]를 드래그하여 **[!UICONTROL Target 경험]** 차원을 보고서에 차원으로 분류한 다음 각 제어 및 타깃팅된 차원을 개별적으로 분류합니다.

![[!UICONTROL 전환별 경험] 패널 [!DNL Analysis Workspace]](assets/Figure3.png)

*그림 3: Target 경험별로 타깃팅된 차원 분류*

결과 보고서의 예는 다음과 같습니다.

![[!UICONTROL 전환별 경험] 패널 [!DNL Analysis Workspace]](assets/Figure4.png)

*그림 4: 표준 [!UICONTROL 자동 Target] 경험 수준 분류가 있는 보고서. 목표 지표는 다를 수 있으며, 제어 전략에는 단일 경험이 있을 수 있습니다.*

>[!TIP]
>
>in [!DNL Analysis Workspace]에서 백분율 표시 아이콘을 클릭하면 [!UICONTROL 전환율] 열을 사용하여 경험 전환율에 집중할 수 있습니다. 그런 다음 전환율은 십진수 형식으로 지정되지만 백분율로 해석합니다.

## 이유 &quot;[!UICONTROL 방문 횟수]&quot;&quot;은(는) [!UICONTROL 자동 Target] 활동

분석 시 [!UICONTROL 자동 Target] 활동, 항상 선택 [!UICONTROL 방문 횟수] 를 기본 정규화 지표로 사용하십시오. [!UICONTROL 자동 Target] 개인화는 방문당 한 번(공식적으로, 한 번) 방문자에 대한 경험을 선택합니다 [!DNL Target] 세션)으로 포함될 수 있으므로 각 방문마다 방문자에게 표시되는 경험이 변경될 수 있습니다. 따라서 [!UICONTROL 고유 방문자 수] 표준화 지표이므로 단일 사용자가 여러 방문 동안 여러 경험을 보게 될 수 있다는 사실은 전환율을 혼동하게 합니다.

간단한 예는 이 점을 보여줍니다. 두 방문자가 두 개의 경험만 있는 캠페인에 들어가는 시나리오를 고려하십시오. 첫 번째 방문자가 두 번 방문합니다. 이 분류는 첫 번째 방문에서는 경험 A에 할당되지만, 두 번째 방문에서는 경험 B가 할당됩니다(해당 두 번째 방문에서 프로필 상태가 변경되어). 두 번째 방문 후 방문자는 순서를 지정하여 전환됩니다. 전환은 가장 최근에 표시된 경험(경험 B)으로 인한 것입니다. 두 번째 방문자도 두 번 방문하며 두 번 모두 경험 B를 표시하지만 전환되지는 않습니다.

방문자 수준 및 방문 수준 보고서를 비교할 수 있습니다.

| 경험 | 고유 방문자 수 | 방문 횟수 | 변환 | 방문자가 표준화된 전환율 | 방문 정규화된 전환율 |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| 총계 | 2 | 4 | 1 | 50% | 25% |

*표 1: 결정이 방문과 고정(방문자가 아님)되는 시나리오에 대한 방문자 정규화 및 방문 정규화 보고서를 비교하는 예제. 방문자가 표준화된 지표는 이 시나리오에서 혼동을 줍니다.*

표에 표시된 대로 방문자 수준 숫자의 명확한 차이가 있습니다. 총 고유 방문자 수가 두 명이라는 사실에도 불구하고 각 경험에 대한 개별 고유 방문자 수의 합이 아닙니다. 방문자 수준 전환율이 반드시 틀릴 필요는 없지만, 한 사람이 개별 경험을 비교할 때 방문 수준 전환율은 거의 틀림없이 더 적절합니다. 일반적으로 분석 단위(&quot;방문 횟수&quot;)는 의사 결정 고착성 단위와 동일하며, 이것은 지표 경험 수준 분류를 추가하고 비교할 수 있음을 의미합니다.

## 활동에 대한 실제 방문 횟수를 필터링합니다

다음 [!DNL Adobe Analytics] 방문 횟수에 대한 기본 계산 방법론 [!DNL Target] 활동에는 사용자가 [!DNL Target] 활동. 이 길은 도로 때문이다 [!DNL Target] 활동 지정은 [!DNL Analytics] 방문자 컨텍스트. 결과적으로 [!DNL Target] 활동이 부풀려질 수 있으므로 전환율이 낮아질 수 있습니다.

사용자가 실제로 와 상호 작용한 방문을 보고하려는 경우 [!UICONTROL 자동 Target] 활동(활동, 표시 또는 방문 이벤트, 또는 전환을 통해)을 만들 수 있는 작업은 다음과 같습니다.

1. 의 히트를 포함하는 특정 세그먼트를 만듭니다 [!DNL Target] 해당 활동의 활동
1. 필터 [!UICONTROL 방문 횟수] 이 세그먼트를 사용한 지표.

**세그먼트를 만들려면:**

1. 을(를) 선택합니다 **[!UICONTROL 구성 요소 > 세그먼트 만들기]** 옵션 [!DNL Analysis Workspace] 도구 모음
2. 을(를) 지정합니다 **[!UICONTROL 제목]** 참조하십시오. 아래 표시된 예에서 이 세그먼트의 이름은 다음과 같습니다 [!DNL "Hit with specific Auto-Target activity"].
3. 을(를) 드래그합니다. **[!UICONTROL Target 활동]** 세그먼트를 위한 차원 **[!UICONTROL 정의]** 섹션을 참조하십시오.
4. 를 사용하십시오 **[!UICONTROL 다음과 같음]** 연산자를 사용할 수 있습니다.
5. 특정 항목 검색 [!DNL Target] 활동.
6. 톱니바퀴 아이콘을 클릭하고 다음을 선택합니다 **[!UICONTROL 속성 모델 > 인스턴스]** 아래 그림과 같이,
7. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

![의 세그먼트 [!DNL Analysis Workspace]](assets/Figure5.png)

*그림 5: 여기에 표시된 세그먼트와 같은 세그먼트를 사용하여 세그먼트를 [!UICONTROL 방문 횟수] 을 위한 A4T의 지표 [!UICONTROL 자동 Target] 보고서*

세그먼트가 만들어지면 세그먼트를 사용하여 [!UICONTROL 방문 횟수] 지표, [!UICONTROL 방문 횟수] 지표에는 사용자가 [!DNL Target] 활동.

**필터링하려면 [!UICONTROL 방문 횟수] 이 세그먼트 사용**

1. 구성 요소 도구 모음에서 새로 만든 세그먼트를 드래그하고 다음 의 기준 위로 마우스를 가져갑니다 **[!UICONTROL 방문 횟수]** 파란색까지 지표 레이블 **[!UICONTROL 필터 기준]** 프롬프트가 나타납니다.
2. 세그먼트를 해제합니다. 필터가 해당 지표에 적용됩니다.

최종 패널은 다음과 같이 나타납니다.

![[!UICONTROL 전환별 경험] 패널 [!DNL Analysis Workspace]](assets/Figure6.png)

*그림 6: 보고서에 &quot;특정 자동 Target 활동으로 히트&quot; 세그먼트가 적용된 보고 패널 [!UICONTROL 방문 횟수] 지표. 이 세그먼트는 사용자가 실제로 와 상호 작용한 방문만 보장합니다 [!DNL Target] 해당 활동은 보고서에 포함됩니다.*

## 목표 지표 및 속성이 최적화 기준과 일치하는지 확인합니다

A4T 통합에서는 [!UICONTROL 자동 Target] 대상 ML 모델 *훈련된* 와 동일한 전환 이벤트 데이터 사용 [!DNL Adobe Analytics] 사용 방법 *성과 보고서 생성*. 그러나 ML 모델을 교육할 때 이 데이터를 해석하는 데 사용해야 하는 특정 가정을 들 수 있습니다. 이러한 가정들은 의 보고 단계 동안 수행된 기본 가정과 다릅니다 [!DNL Adobe Analytics].

특히, [!DNL Adobe Target] ML 모델은 방문 범위 속성 모델을 사용합니다. 즉, ML 모델은 ML 모델에서 수행한 결정에 변환이 &quot;특성&quot;이 되도록 활동에 대한 콘텐츠 표시와 동일한 방문에서 전환이 발생해야 한다고 가정합니다. 다음 경우에 필요합니다 [!DNL Target] 그 모델들의 적시에 훈련을 보증하다. [!DNL Target] 전환 시 최대 30일(에 있는 보고서에 대한 기본 속성 창)을 기다릴 수 없습니다 [!DNL Adobe Analytics])를 클릭하여 제품에서 사용할 수 있습니다.

따라서 [!DNL Target] 모델(교육 중)과 데이터를 쿼리하는 데 사용되는 기본 속성(보고서 생성 중)이 일치하지 않을 수 있습니다. 실제로 문제가 속성에 있는 경우 ML 모델이 성과가 낮은 것으로 보일 수도 있습니다.

>[!TIP]
>
>ML 모델이 보고서에서 보고 있는 지표와 다르게 특성이 있는 지표에 대해 최적화되는 경우 모델이 예상대로 수행되지 않을 수 있습니다. 이를 방지하려면 보고서의 목표 지표가 [!DNL Target] ML 모델.

정확한 지표 정의 및 속성 설정은 [최적화 기준](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank} 활동을 만드는 동안 지정했습니다.

### Target 정의된 전환 또는 [!DNL Analytics] 지표 *방문당 지표 값 최대화*

지표가 [!DNL Target] 전환 또는 [!DNL Analytics] 지표 **방문당 지표 값 최대화**, 목표 지표 정의를 사용하면 동일한 방문에서 여러 전환 이벤트가 발생할 수 있습니다.

에서 사용하는 것과 동일한 속성 방식이 있는 목표 지표를 보려면 [!DNL Target] ML 모델은 다음 단계를 수행합니다.

1. 목표 지표의 톱니바퀴 아이콘 위로 마우스를 가져갑니다.

   ![gearicon.png](assets/gearicon.png)

1. 결과 메뉴에서 로 스크롤합니다. **[!UICONTROL 데이터 설정]**.
1. 선택 **[!UICONTROL 비기본 속성 모델 사용]** (아직 선택하지 않은 경우)

   ![non-defaultattribtionmodel.png](assets/non-defaultattributionmodel.png)

1. **[!UICONTROL 편집]**&#x200B;을 클릭합니다.
1. 선택 **[!UICONTROL 모델]**: **[!UICONTROL 기여도]**, 및 **[!UICONTROL 전환 확인 기간]**: **[!UICONTROL 방문]**.

   ![기여도 byVisit.png](assets/ParticipationbyVisit.png)

1. **[!UICONTROL 적용]**&#x200B;을 클릭합니다.

이러한 단계는 목표 지표 이벤트가 발생한 경우 보고서가 경험 표시에 목표 지표를 기여하도록 합니다 *언제든지* (&quot;기여도&quot;)를 전달하는 것이 좋습니다.

### [!DNL Analytics] 지표 *고유 방문 전환율*

**긍정적인 지표 세그먼트로 방문 정의**

선택한 시나리오에서 *고유 방문 전환율을 최대화* 최적화 기준으로서, 전환율에 대한 올바른 정의는 지표 값이 긍정인 방문의 분수입니다. 이 작업은 세그먼트를 만들어 양수 값을 갖는 방문으로 필터링한 다음 방문 지표를 필터링함으로써 수행할 수 있습니다.

1. 전과 마찬가지로 을(를) 선택합니다 **[!UICONTROL 구성 요소 > 세그먼트 만들기]** 옵션 [!DNL Analysis Workspace] 도구 모음
2. 을(를) 지정합니다 **[!UICONTROL 제목]** 참조하십시오.

   아래 표시된 예에서 이 세그먼트의 이름은 다음과 같습니다 [!DNL "Visits with an order"].

3. 최적화 목표에 사용한 기본 지표를 세그먼트로 드래그합니다.

   아래 표시된 예에서는 **주문** 지표로, 전환율이 주문이 기록됩니다.

4. 세그먼트 정의 컨테이너의 왼쪽 위에서 을 선택합니다 **[!UICONTROL 포함]** **방문**.
5. 를 사용하십시오 **[!UICONTROL 보다 큼]** 연산자를 사용하여 값을 0으로 설정합니다.

   값을 0으로 설정하면 이 세그먼트에는 주문 지표가 긍정인 방문이 포함됩니다.

6. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

![그림 7.png](assets/Figure7.png)

*그림 7: 긍정적인 순서로 방문을 필터링하는 세그먼트 정의. 활동의 최적화 지표에 따라, 주문을 적절한 지표로 대체해야 합니다*

**활동 필터링된 지표의 방문에 적용합니다**

이제 이 세그먼트를 사용하여 양의 주문 수와 에 대한 히트가 있는 방문으로 필터링할 수 있습니다 [!DNL Auto-Target] 활동. 지표를 필터링하는 절차는 이전과 유사하며, 새 세그먼트를 이미 필터링된 방문 지표에 적용한 후에는 보고서 패널이 그림 8 처럼 표시되어야 합니다

![그림 8.png](assets/Figure8.png)

*그림 8: 올바른 고유 방문 전환 지표가 있는 보고서 패널: 활동의 히트가 기록되고 전환 지표(이 예제의 주문)가 0이 아닌 방문의 수입니다.*

## 최종 단계: 위의 마법을 캡처하는 전환율을 만듭니다

수정 사항 사용 [!UICONTROL 방문] 이전 섹션의 목표 지표와 기본 A4T에 대해 최종 수정해야 하는 [!DNL Auto-Target] 보고 패널은 수정된 목표 지표의 비율인 전환율을 적절하게 필터링된 &quot;방문 횟수&quot; 지표로 만드는 것입니다.

이렇게 하려면 [!UICONTROL 계산된 지표] 다음 단계를 사용합니다.

1. 을(를) 선택합니다 **[!UICONTROL 구성 요소 > 지표 만들기]** 옵션 [!DNL Analysis Workspace] 도구 모음
1. 을(를) 지정합니다 **[!UICONTROL 제목]** 참조하십시오. 예를 들어, &quot;Activity XXX에 대한 방문 수정 전환율&quot;이 있습니다.
1. 선택 **[!UICONTROL 형식]** = 백분율 및 **[!UICONTROL 소수점 이하 자리 수]** = 2.
1. 활동에 대한 관련 목표 지표를 드래그합니다(예: [!UICONTROL 활동 전환])를 정의에 사용하고 이 목표 지표의 톱니바퀴 아이콘을 사용하여 앞에서 설명한 대로 속성 모델을 (기여도|방문)으로 조정합니다.
1. 선택 **[!UICONTROL 추가 > 컨테이너]** 오른쪽 상단에서 **[!UICONTROL 정의]** 섹션을 참조하십시오.
1. 두 컨테이너 사이에 나누기(÷) 연산자를 선택합니다.
1. 앞에서 만든 세그먼트(&quot;특정 항목으로 히트&quot;)를 드래그합니다. [!UICONTROL 자동 Target] 활동&quot;을 이 특정 자습서에서 확인하십시오 [!DNL Auto-Target] 활동.
1. 을(를) 드래그합니다. **[!UICONTROL 방문 횟수]** 지표를 세그먼트 컨테이너로 가져옵니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

>[!TIP]
>
> 또한 [빠른 계산된 지표 기능](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html).

전체 계산된 지표 정의가 여기에 표시됩니다.

![그림 9.png](assets/Figure9.png)

*그림 7: 방문 수정 및 속성 수정 모델 전환율 지표 정의. (이 지표는 목표 지표 및 활동에 따라 다릅니다. 즉, 이 지표 정의는 활동 간에 다시 사용할 수 없습니다.)*

>[!IMPORTANT]
>
>다음 [!UICONTROL 전환] A4T 패널의 비율 지표는 테이블의 전환 이벤트 또는 정규화 지표에 연결되어 있지 않습니다. 이 자습서에서 수정 사항을 제안하면 [!UICONTROL 전환] 비율은 변경 사항에 자동으로 조정되지 않습니다. 따라서 전환 이벤트 기여도 분석이나 정규화 지표(또는 둘 다)를 수정하는 경우 를 수정하는 마지막 단계로 기억해야 합니다 [!UICONTROL 전환] 비율( 위에 표시된 대로).

## 요약: 최종 샘플 [!DNL Analysis Workspace] 패널 대상 [!UICONTROL 자동 Target] 보고서

위의 모든 단계를 단일 패널에 결합하는 경우 아래 그림은 권장 보고서의 전체 보기를 보여줍니다 [!UICONTROL 자동 Target] A4T 활동. 이 보고서는 [!DNL Target] 목표 지표를 최적화하는 ML 모델. 이 보고서는 이 자습서에서 설명하는 모든 뉘앙스와 권장 사항을 통합합니다. 이 보고서는 기존의 방법론에 사용되는 계산 방법론과 가장 가깝습니다 [!DNL Target]보고 기반 [!UICONTROL 자동 Target] 활동.

이미지를 확장하려면 을(를) 클릭합니다.

![의 최종 A4T 보고서 [!DNL Analysis Workspace]](assets/Figure10.png "Analysis Workspace의 A4T 보고서"){width="600" zoomable="yes"}

*그림 10: 최종 A4T [!UICONTROL 자동 Target] 보고서 위치 [!DNL Adobe Analytics] [!DNL Workspace]- 이 자습서의 이전 섹션에 설명된 지표 정의에 대한 모든 조정을 결합합니다.*
