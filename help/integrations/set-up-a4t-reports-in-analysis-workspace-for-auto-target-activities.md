---
title: ' [!DNL Analysis Workspace] for [!DNL Auto-Target] Activities에서 A4T 보고서를 설정하는 방법'
description: '[!UICONTROL Auto-Target] 활동을 실행할 때 예상된 결과를 얻으려면  [!DNL Analysis Workspace] 에서 A4T 보고서를 어떻게 구성합니까?'
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=ko#premium newtab=true" tooltip="Target Premium에 포함된 내용을 확인합니다."
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 78e5b5f7fa8f4c1a08c06c6d2b0e1a5242cd464c
workflow-type: tm+mt
source-wordcount: '2430'
ht-degree: 1%

---

# [!DNL Auto-Target] 활동에 대해 [!DNL Analysis Workspace]에서 A4T 보고서 설정

>[!IMPORTANT]
>
>[!UICONTROL Auto-Target] 활동의 경우 [!DNL Analytics Workspace]에서 보고를 확인하고 A4T 패널을 수동으로 만들어야 합니다.

[!DNL Auto-Target] 활동에 대한 [!UICONTROL Analytics for Target] (A4T) 통합에서는 [!DNL Adobe Analytics] 목표 지표를 사용하는 동안 [!DNL Adobe Target] ML(Ensemble Machine Learning) 알고리즘을 사용하여 각 방문자의 프로필, 동작 및 컨텍스트를 기반으로 최상의 경험을 선택합니다.

[!DNL Adobe Analytics] [!DNL Analysis Workspace]에서 다양한 분석 기능을 사용할 수 있지만 실험 활동(수동 [!UICONTROL A/B Test] 및 [!UICONTROL Auto-Allocate])과 개인화 활동([!UICONTROL [!UICONTROL Auto-Target]]) 간의 차이로 인해 [!DNL Auto-Target] 활동을 올바르게 해석하려면 기본 **[!UICONTROL Analytics for Target]** 패널을 몇 가지 수정해야 합니다.

이 자습서에서는 다음 주요 개념을 기반으로 하는 [!DNL Analysis Workspace]의 [!UICONTROL Auto-Target] 활동을 분석하기 위한 권장 수정 사항을 안내합니다.

* **[!UICONTROL Control vs Targeted]** 차원은 [!UICONTROL Control] 경험과 [!UICONTROL Auto-Target] 앙상블 ML 알고리즘에서 제공하는 경험을 구별하는 데 사용할 수 있습니다.
* 경험 수준 성능 분류를 볼 때 방문 횟수를 표준화 지표로 사용해야 합니다. 또한 [Adobe Analytics의 기본 계산 방법론에는 사용자가 실제로 활동 컨텐츠를 보지 못하는 방문](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=ko#metrics){target=_blank}이 포함될 수 있지만 적절한 범위의 세그먼트를 사용하여 이 기본 동작을 수정할 수 있습니다(아래 세부 정보).
* 지정된 속성 모델에서 &quot;방문 전환 확인 기간&quot;이라고도 하는 방문 전환 확인 범위 속성은 [!DNL Adobe Target] ML 모델이 교육 단계에서 사용하며, 목표 지표를 분류할 때 동일한(기본값이 아닌) 속성 모델을 사용해야 합니다.

## [!DNL Analysis Workspace]에서 [!UICONTROL Auto-Target] 패널에 대한 A4T 만들기

[!UICONTROL Auto-Target] 보고서에 대한 A4T를 만들려면 아래와 같이 [!DNL Analysis Workspace]의 **[!UICONTROL Analytics for Target]** 패널로 시작하거나 자유 형식 테이블로 시작합니다. 그런 다음 다음을 선택합니다.

1. **[!UICONTROL Control Experience]**: 모든 경험을 선택할 수 있지만 나중에 이 선택을 재정의합니다. [!UICONTROL Auto-Target] 활동의 경우 제어 경험은 실제로 제어 전략이며, a) 모든 경험에서 임의로 제공되거나 b) 단일 경험을 제공합니다(이 선택은 [!DNL Adobe Target]의 활동 생성 시 수행됩니다). 선택(b)을 선택하더라도 [!UICONTROL Auto-Target] 활동에서 특정 경험을 제어로 지정했습니다. [!UICONTROL Auto-Target] 활동에 대한 A4T 분석을 위해 이 자습서에 설명된 접근 방식을 따라야 합니다.
2. **[!UICONTROL Normalizing Metric]**: [!UICONTROL Visits] 선택.
3. **[!UICONTROL Success Metrics]**: 보고할 지표를 선택할 수 있지만 일반적으로 [!DNL Target]에서 활동을 만드는 동안 최적화를 위해 선택한 지표와 동일한 지표에 대한 보고서를 확인해야 합니다.

   [!UICONTROL Auto-Target] 활동에 대한 ![[!UICONTROL Analytics for Target] 패널 설정입니다.](assets/Figure1.png)

   *그림 1: [!UICONTROL Auto-Target] 활동에 대한 [!UICONTROL Analytics for Target] 패널 설정.*

>[!TIP]
>
>[!UICONTROL Auto-Target] 활동에 대해 [!UICONTROL Analytics for Target] 패널을 설정하려면 모든 제어 경험을 선택하고 [!UICONTROL Visits]을(를) 표준화 지표로 선택한 다음 [!DNL Target] 활동 생성 중 최적화를 위해 선택한 것과 동일한 목표 지표를 선택하십시오.

## [!UICONTROL Control vs.Targeted] 차원을 사용하여 [!DNL Target] 앙상블 ML 모델을 컨트롤과 비교합니다.

기본 A4T 패널은 클래식(수동) [!UICONTROL A/B Test] 또는 [!UICONTROL Auto-Allocate] 활동을 위해 디자인되었습니다. 이 경우 개별 경험의 성능을 제어 경험과 비교하는 것이 목표입니다. 그러나 [!UICONTROL Auto-Target] 활동에서는 컨트롤 *전략*&#x200B;과(와) 타깃팅된 *전략* 간의 첫 번째 순서 비교가 필요합니다. 즉, 제어 전략에 대한 [!UICONTROL Auto-Target] 앙상블 ML 모델의 전체 성능 상승도를 결정합니다.

이 비교를 수행하려면 **[!UICONTROL Control vs Targeted (Analytics for Target)]** 차원을 사용하십시오. 끌어서 놓아 기본 A4T 보고서의 **[!UICONTROL Target Experiences]** 차원을 바꾸십시오.

이 대체 함수는 A4T 패널에서 기본 [!UICONTROL Lift and Confidence] 계산을 무효화합니다. 혼동을 방지하기 위해 다음 보고서를 남겨두고 기본 패널에서 이러한 지표를 제거할 수 있습니다.

[!DNL Analysis Workspace]![&#128279;](assets/Figure2.png)의 [!UICONTROL Experiences by Activity Conversions] 패널

*그림 2: [!DNL Auto-Target] 활동에 대한 권장 기준 보고서. 이 보고서는 타깃팅된 트래픽(앙상블 ML 모델에서 제공됨)을 제어 트래픽과 비교하도록 구성되었습니다.*

>[!NOTE]
>
>현재 [!UICONTROL Auto-Target]에 대한 A4T 보고서의 [!UICONTROL Control vs Targeted] 차원에 대해 [!UICONTROL Lift and Confidence]개의 숫자를 사용할 수 없습니다. 지원이 추가되기 전까지 [신뢰도 계산기](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=ko)를 다운로드하여 [!UICONTROL Lift and Confidence]을(를) 수동으로 계산할 수 있습니다.

## 지표의 경험 수준 분류 추가

앙상블 ML 모델이 어떻게 작동하는지 자세히 알아보려면 **[!UICONTROL Control vs Targeted]** 차원의 경험 수준 분류를 검사할 수 있습니다. [!DNL Analysis Workspace]에서 **[!UICONTROL Target Experiences]** 차원을 보고서로 끌어온 다음 각 컨트롤 및 대상 차원을 별도로 분류합니다.

[!DNL Analysis Workspace]![&#128279;](assets/Figure3.png)의 [!UICONTROL Experiences by Activity Conversions] 패널

*그림 3: 대상 환경을 기준으로 대상 차원 분류*

결과 보고서의 예가 여기에 나와 있습니다.

[!DNL Analysis Workspace]![&#128279;](assets/Figure4.png)의 [!UICONTROL Experiences by Activity Conversions] 패널

*그림 4: 경험 수준 분류가 있는 표준 [!UICONTROL Auto-Target] 보고서. 목표 지표는 다를 수 있으며 제어 전략에는 단일 경험이 있을 수 있습니다.*

>[!TIP]
>
>[!DNL Analysis Workspace]에서 톱니바퀴 아이콘을 클릭하여 [!UICONTROL Conversion Rate] 열에서 백분율을 숨겨 경험 전환율에 초점을 맞추십시오. 그러면 전환율은 소수로 포맷되지만 그에 따라 백분율로 해석됩니다.

## [!UICONTROL Auto-Target] 활동에 대해 &quot;[!UICONTROL Visits]&quot;이(가) 올바른 표준화 지표인 이유

[!UICONTROL Auto-Target] 활동을 분석할 때는 항상 [!UICONTROL Visits]을(를) 기본 표준화 지표로 선택하십시오. [!UICONTROL Auto-Target] 개인화는 방문당 한 번(공식적으로, [!DNL Target] 세션당 한 번) 방문자에 대한 경험을 선택합니다. 즉, 방문자에게 표시되는 경험이 모든 방문마다 변경될 수 있습니다. 따라서 표준화 지표로 [!UICONTROL Unique Visitors]을(를) 사용하는 경우 한 명의 사용자에게 (서로 다른 방문에 걸쳐) 여러 경험이 표시될 수 있다는 사실은 전환율을 혼동하게 합니다.

간단한 예는 이 점을 보여 줍니다. 두 명의 방문자가 두 개의 경험만 있는 캠페인을 입력하는 시나리오를 생각해 보십시오. 첫 번째 방문자가 두 번 방문합니다. 이 경험은 첫 번째 방문에서는 경험 A에 할당되지만, 두 번째 방문에서는 프로필 상태가 변경되어 경험 B에 할당됩니다. 두 번째 방문 후에 방문자는 주문을 하여 전환됩니다. 전환은 가장 최근에 표시된 경험(경험 B)에 기인합니다. 두 번째 방문자도 두 번 방문하고, 두 번 모두 경험 B가 표시되지만, 전환되지는 않습니다.

방문자 수준 및 방문 수준 보고서를 비교해 보겠습니다.

| 경험 | 고유 방문자 수 | 방문 횟수 | 변환 | 방문자 표준화 전환율 | 방문 표준화된 전환율 |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| 총계 | 2 | 4 | 1 | 50% | 25% |

*표 1: 결정이 방문에 고정(일반 A/B 테스트와 마찬가지로 방문자가 아님)되는 시나리오에 대한 방문자 정규화 보고서와 방문 정규화 보고서를 비교하는 예제. 이 시나리오에서 방문자 표준화 지표가 혼동되고 있습니다.*

표에서 보듯이 방문자 수준 숫자의 명백한 부조화가 있습니다. 총 두 명의 고유 방문자가 있음에도 불구하고 각 경험에 대한 개별 고유 방문자의 합이 아닙니다. 방문자 수준 전환율이 반드시 잘못된 것은 아니지만 개별 경험을 비교할 때 방문 수준 전환율이 훨씬 더 적절합니다. 형식적으로 분석 단위(&quot;방문 횟수&quot;)는 의사 결정 고착성의 단위와 동일하며, 이는 지표의 경험 수준 분류를 추가하고 비교할 수 있음을 의미합니다.

## 활동에 대한 실제 방문 필터링

[!DNL Target] 활동에 대한 방문에 대한 [!DNL Adobe Analytics] 기본 계산 방법론에는 사용자가 [!DNL Target] 활동과 상호 작용하지 않은 방문이 포함될 수 있습니다. 이는 [!DNL Target] 활동 할당이 [!DNL Analytics] 방문자 컨텍스트에서 지속되는 방식 때문입니다. 그 결과 [!DNL Target] 활동에 대한 방문 횟수가 부풀려져 전환율이 저하될 수 있습니다.

사용자가 [!UICONTROL Auto-Target] 활동과 실제로 상호 작용한 방문에 대해 보고하려는 경우(활동 시작, 디스플레이 또는 방문 이벤트 또는 전환을 통해) 다음을 수행할 수 있습니다.

1. 해당 [!DNL Target] 활동의 히트를 포함하는 특정 세그먼트를 만든 다음
1. 이 세그먼트를 사용하여 [!UICONTROL Visits] 지표를 필터링합니다.

**세그먼트를 만들려면:**

1. [!DNL Analysis Workspace] 도구 모음에서 **[!UICONTROL Components > Create Segment]** 옵션을 선택합니다.
2. 세그먼트에 대한 **[!UICONTROL Title]**&#x200B;을(를) 지정하십시오. 아래 예제에서 세그먼트 이름은 [!DNL "Hit with specific Auto-Target activity"]입니다.
3. **[!UICONTROL Target Activities]** 차원을 세그먼트 **[!UICONTROL Definition]** 섹션으로 끌어옵니다.
4. **[!UICONTROL equals]** 연산자를 사용합니다.
5. 특정 [!DNL Target] 활동을 검색합니다.
6. 톱니바퀴 아이콘을 클릭한 다음 아래 그림과 같이 **[!UICONTROL Attribution model > Instance]**&#x200B;을(를) 선택합니다.
7. **[!UICONTROL Save]** 아이콘을 클릭합니다.

[!DNL Analysis Workspace]![&#128279;](assets/Figure5.png)의 세그먼트

*그림 5: 여기에 표시된 것과 같은 세그먼트를 사용하여 [!UICONTROL Auto-Target] 보고서에 대한 A4T에서 [!UICONTROL Visits] 지표를 필터링하십시오*

세그먼트가 만들어지면 이 세그먼트를 사용하여 [!UICONTROL Visits] 지표를 필터링합니다. [!UICONTROL Visits] 지표에는 사용자가 [!DNL Target] 활동과 상호 작용한 방문만 포함됩니다.

**이 세그먼트를 사용하여 [!UICONTROL Visits]을(를) 필터링하려면:**

1. 새로 만든 세그먼트를 구성 요소 도구 모음에서 드래그하고 파란색 **[!UICONTROL Filter by]** 프롬프트가 나타날 때까지 **[!UICONTROL Visits]** 지표 레이블의 아래쪽을 가리킵니다.
2. 세그먼트를 해제합니다. 필터가 해당 지표에 적용됩니다.

최종 패널은 다음과 같이 표시됩니다.

[!DNL Analysis Workspace]![&#128279;](assets/Figure6.png)의 [!UICONTROL Experiences by Activity Conversions] 패널

*그림 6: [!UICONTROL Visits] 지표에 &quot;특정 자동 타겟 활동이 있는 히트&quot; 세그먼트가 적용된 보고 패널. 이 세그먼트는 사용자가 해당 [!DNL Target] 활동과 실제로 상호 작용한 방문만 보고서에 포함되도록 합니다.*

## 목표 지표 및 속성이 최적화 기준과 일치하는지 확인합니다

A4T 통합을 통해 [!DNL Adobe Analytics]이(가) *성능 보고서 생성*&#x200B;에 사용하는 것과 동일한 전환 이벤트 데이터를 사용하여 [!UICONTROL Auto-Target] ML 모델을 *학습*&#x200B;할 수 있습니다. 그러나 ML 모델을 교육할 때 이 데이터를 해석하는 데 사용해야 하는 특정 가정이 있으며, 이는 [!DNL Adobe Analytics]의 보고 단계 동안 수행되는 기본 가정과 다릅니다.

특히 [!DNL Adobe Target] ML 모델은 방문 범위 속성 모델을 사용합니다. 즉, ML 모델은 전환이 ML 모델의 결정에 &quot;귀속&quot;되도록 하기 위해 활동에 대한 콘텐츠 표시와 동일한 방문에서 전환이 발생해야 한다고 가정합니다. [!DNL Target]이(가) 모델의 적시 교육을 보장하기 위해 필요합니다. [!DNL Target]은(는) 해당 모델의 교육 데이터에 변환([!DNL Adobe Analytics]의 보고서에 대한 기본 속성 창)을 포함하기 전에 최대 30일까지 기다릴 수 없습니다.

따라서 [!DNL Target] 모델에서 사용하는 속성과 데이터 쿼리에 사용되는 기본 속성(보고서 생성 중) 간의 차이로 인해 불일치가 발생할 수 있습니다. ML 모델이 실제로 속성에 문제가 있을 때 제대로 작동하지 않는 것처럼 보일 수도 있습니다.

>[!TIP]
>
>ML 모델이 보고서에서 보고 있는 지표와 다르게 기여하는 지표에 대해 최적화하는 경우 모델이 예상대로 수행되지 않을 수 있습니다. 이를 방지하려면 보고서의 목표 지표가 [!DNL Target] ML 모델에서 사용하는 것과 동일한 지표 정의 및 속성을 사용하는지 확인하십시오.

정확한 지표 정의 및 속성 설정은 활동을 만드는 동안 지정한 [최적화 기준](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=ko#supported){target=_blank}에 따라 다릅니다.

### 타겟 정의 전환 또는 *방문당 지표 값 최대화*&#x200B;를 사용하는 [!DNL Analytics] 지표

지표가 [!DNL Target] 전환이거나 **방문당 지표 값 최대화**&#x200B;를 사용하는 [!DNL Analytics] 지표인 경우 목표 지표 정의를 사용하면 동일한 방문에서 여러 전환 이벤트가 발생할 수 있습니다.

[!DNL Target] ML 모델에서 사용하는 기여도 분석 방법이 동일한 목표 지표를 보려면 다음 단계를 수행합니다.

1. 다음 목표 지표의 톱니바퀴 아이콘 위로 마우스를 가져갑니다.

   ![gearicon.png](assets/gearicon.png)

1. 결과 메뉴에서 **[!UICONTROL Data settings]**&#x200B;로 스크롤합니다.
1. **[!UICONTROL Use non-default  attribution model]**&#x200B;을(를) 선택합니다(아직 선택하지 않은 경우).

   ![비defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. **[!UICONTROL Edit]** 아이콘을 클릭합니다.
1. **[!UICONTROL Model]**: **[!UICONTROL Participation]**, **[!UICONTROL Lookback window]**: **[!UICONTROL Visit]**&#x200B;을(를) 선택하십시오.

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. **[!UICONTROL Apply]** 아이콘을 클릭합니다.

이 단계에서는 경험이 표시된 동일한 방문에서 목표 지표 이벤트가 *항상*(&quot;참여&quot;)일 경우 목표 지표를 경험 표시에 표시하도록 보고서가 지정합니다.

### *고유 방문 전환율*&#x200B;이 있는 [!DNL Analytics] 지표

**긍정적인 지표 세그먼트로 방문 정의**

최적화 기준으로 *고유 방문 전환율 최대화*&#x200B;를 선택한 시나리오에서 올바른 전환율 정의는 지표 값이 양수인 방문 비율입니다. 이 작업은 지표가 양수 값을 갖는 방문으로 필터링하는 세그먼트를 만든 다음 방문 지표를 필터링하여 수행할 수 있습니다.

1. 이전과 같이 [!DNL Analysis Workspace] 도구 모음에서 **[!UICONTROL Components > Create Segment]** 옵션을 선택하십시오.
2. 세그먼트에 대한 **[!UICONTROL Title]**&#x200B;을(를) 지정하십시오.

   아래 예제에서 세그먼트 이름은 [!DNL "Visits with an order"]입니다.

3. 최적화 목표에서 사용한 기본 지표를 세그먼트로 드래그합니다.

   아래 표시된 예에서는 **주문** 지표를 사용하므로 전환율은 주문이 기록된 방문의 비율을 측정합니다.

4. 세그먼트 정의 컨테이너의 왼쪽 상단에서 **[!UICONTROL Include]** **방문**&#x200B;을(를) 선택합니다.
5. **[!UICONTROL is greater than]** 연산자를 사용하고 값을 0으로 설정하십시오.

   값을 0으로 설정하면 이 세그먼트에는 주문 지표가 양수인 방문이 포함됩니다.

6. **[!UICONTROL Save]** 아이콘을 클릭합니다.

![그림7.png](assets/Figure7.png)

*그림 7: 양수 순서가 있는 방문에 대한 세그먼트 정의 필터링입니다. 활동의 최적화 지표에 따라 주문을 적절한 지표로 바꾸어야 합니다.*

**활동 필터링된 지표의 방문 횟수에 적용**

이제 이 세그먼트를 사용하여 [!DNL Auto-Target] 활동에 대한 히트가 있는 양의 주문 수가 있는 방문으로 필터링할 수 있습니다. 지표 필터링 절차는 이전과 유사하며, 이미 필터링된 방문 지표에 새 세그먼트를 적용한 후에는 보고서 패널이 그림 8과 같이 표시되어야 합니다

![그림8.png](assets/Figure8.png)

*그림 8: 올바른 고유 방문 전환 지표가 있는 보고서 패널: 활동에서 히트가 기록된 방문 수와 전환 지표(이 예제의 주문)가 0이 아닌 방문 수입니다.*

## 마지막 단계: 위의 마법을 캡처하는 전환율 만들기

이전 섹션에서 [!UICONTROL Visit] 및 목표 지표를 수정하면 [!DNL Auto-Target] 보고 패널의 기본 A4T에 대해 마지막으로 수정해야 하는 내용은 올바르게 필터링된 &quot;방문 수&quot; 지표에 대한 수정된 목표 지표의 올바른 비율인 전환율을 만드는 것입니다.

다음 단계를 사용하여 [!UICONTROL Calculated Metric]을(를) 만들어 이 작업을 수행합니다.

1. [!DNL Analysis Workspace] 도구 모음에서 **[!UICONTROL Components > Create Metric]** 옵션을 선택합니다.
1. 지표에 대해 **[!UICONTROL Title]**&#x200B;을(를) 지정하십시오. 예를 들어 &quot;활동 XXX에 대한 방문 수정 전환율&quot;이 있습니다.
1. **[!UICONTROL Format]** = 백분율 및 **[!UICONTROL Decimal Places]** = 2를 선택합니다.
1. 활동에 대한 관련 목표 지표(예: [!UICONTROL Activity Conversions])를 정의로 드래그하고 이 목표 지표의 톱니바퀴 아이콘을 사용하여 앞에서 설명한 대로 기여도 분석 모델을 (방문)으로 조정합니다.
1. **[!UICONTROL Definition]** 섹션의 오른쪽 상단에서 **[!UICONTROL Add > Container]**&#x200B;을(를) 선택합니다.
1. 두 컨테이너 간÷ 나눗셈(나눗셈) 연산자를 선택합니다.
1. 이 특정 [!DNL Auto-Target] 활동에 대해 이 자습서에서 &quot;특정 [!UICONTROL Auto-Target] 활동으로 히트&quot;라는 이전에 만든 세그먼트를 드래그합니다.
1. **[!UICONTROL Visits]** 지표를 세그먼트 컨테이너로 드래그합니다.
1. **[!UICONTROL Save]** 아이콘을 클릭합니다.

>[!TIP]
>
> [빠른 계산된 지표 기능](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=ko)을 사용하여 이 지표를 만들 수도 있습니다.

전체 계산된 지표 정의가 여기에 표시됩니다.

![그림9.png](assets/Figure9.png)

*그림 7: 방문 수정 및 속성 수정 모델 전환율 지표 정의. (이 지표는 목표 지표 및 활동에 따라 다릅니다. 즉, 이 지표 정의는 활동 간에 다시 사용할 수 없습니다.)*

>[!IMPORTANT]
>
>A4T 패널의 [!UICONTROL Conversion] 속도 지표가 테이블의 전환 이벤트 또는 표준화 지표에 연결되어 있지 않습니다. 이 자습서에서 제안한 내용을 수정하면 [!UICONTROL Conversion] 비율이 변경 내용에 자동으로 적용되지 않습니다. 따라서 전환 이벤트 속성 또는 표준화 지표(또는 둘 다)를 수정하는 경우 위에 표시된 대로 [!UICONTROL Conversion] 비율도 수정하는 마지막 단계로 기억해야 합니다.

## 요약: [!UICONTROL Auto-Target] 보고서에 대한 최종 샘플 [!DNL Analysis Workspace] 패널

위의 모든 단계를 단일 패널로 결합하면 아래 그림에서 [!UICONTROL Auto-Target]개의 A4T 활동에 대한 권장 보고서를 전체적으로 볼 수 있습니다. 이 보고서는 [!DNL Target] ML 모델에서 목표 지표를 최적화하는 데 사용한 보고서와 동일합니다. 이 보고서에는 이 자습서에서 설명한 모든 뉘앙스와 권장 사항이 통합되어 있습니다. 이 보고서는 기존의 [!DNL Target] 보고 기반 [!UICONTROL Auto-Target] 활동에서 사용되는 계산 방법론과도 가장 가깝습니다.

이미지를 확장하려면 클릭하십시오.

![Analysis Workspace의 [!DNL Analysis Workspace]](assets/Figure10.png "A4T 보고서에서 최종 A4T 보고서"){width="600" zoomable="yes"}

*그림 10: 이 자습서의 이전 섹션에 설명된 지표 정의에 대한 모든 조정을 결합하는 [!DNL Adobe Analytics] [!DNL Workspace]의 최종 A4T [!UICONTROL Auto-Target] 보고서입니다.*
