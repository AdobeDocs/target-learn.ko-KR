---
title: 사용자 지정 기준 관리 방법
description: 이 튜토리얼에서는 Adobe Target API를 사용하여 Adobe Target Recommendations 기준을 관리, 만들기, 목록 작성, 편집, 가져오기 및 삭제하는 데 필요한 단계를 개발자에게 안내합니다.
role: Developer
level: 중간
topic: 개인화, 관리, 통합, 개발
feature: API/SDK, Recommendations, 관리 및 구성
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 1%

---


# 사용자 지정 기준 관리

경우에 따라 [!DNL Recommendations]에서 제공하는 알고리즘이 홍보할 특정 항목을 표시할 수 없습니다. 이러한 경우 사용자 지정 기준은 지정된 키 항목 또는 범주에 대해 특정 권장 항목 세트를 제공할 수 있는 방법을 제공합니다. 키 항목 또는 카테고리와 권장 항목 간 매핑을 정의하고 해당 매핑을 사용자 지정 기준으로 가져옵니다. 이 프로세스는 [사용자 지정 기준 문서](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)에 설명되어 있습니다. 해당 문서에 언급된 대로 [!DNL Target] 사용자 인터페이스(UI)를 통해 사용자 정의 기준을 만들고, 편집하고, 삭제할 수 있습니다. 그러나 [!DNL Target]은(는) 사용자 지정 기준을 보다 세부적으로 관리할 수 있는 사용자 지정 기준 API 세트도 제공합니다.

>[!IMPORTANT]
>
>사용자 지정 기준에 대해 다음 사용 지침을 따르십시오.
>
> API를 사용하여 지정된 사용자 지정 기준에 대한 모든 작업(만들기, 편집, 삭제)을 수행하거나 UI를 사용하여 모든 작업(만들기, 편집, 삭제)을 수행합니다. UI와 API를 조합하여 사용자 지정 기준을 관리하면 정보가 충돌하거나 예기치 않은 결과가 발생할 수 있습니다. 예를 들어, UI에서 사용자 지정 기준을 만든 다음 API를 통해 편집하면 API를 통해 볼 수 있는 대로 백 엔드에서 업데이트되더라도 UI에 업데이트가 반영되지 않습니다.

## 사용자 지정 기준 만들기

[사용자 지정 기준 만들기 API](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)를 사용하여 사용자 지정 기준을 만들려면 구문은 다음과 같습니다.

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>이 연습에서 설명한 대로 사용자 지정 기준 만들기 API를 사용하여 만든 사용자 지정 기준은 UI에 나타나며, 여기서 UI는 지속됩니다. UI에서 편집하거나 삭제할 수 없습니다. API **를 통해**&#x200B;을 편집하거나 삭제할 수 있지만 어느 방식으로든 [!DNL Target] UI에 계속 표시됩니다. UI에서 편집 또는 삭제 옵션을 유지하려면 사용자 지정 기준 만들기 API를 사용하는 것과 대조적으로 [설명서](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)당 UI를 사용하여 사용자 지정 기준을 만드십시오.

위의 경고를 읽은 후에만 이 튜토리얼을 진행하여 나중에 UI에서 삭제할 수 없는 새 사용자 정의 기준을 만드는 것이 좋습니다.

1. **사용자 지정 기준 만들기**&#x200B;에 대해 `TENANT_ID` 및 `API_KEY`이 이전에 설정된 포스트만 환경 변수를 참조하는지 확인합니다. 비교를 위해 아래 이미지를 사용하십시오.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. 사용자 지정 기준 CSV 파일의 위치를 정의하는 **본문**&#x200B;을 **raw** JSON으로 추가합니다. [사용자 지정 기준 API 만들기](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) 문서에 제공된 예제를 템플릿으로 사용하여 `environmentId` 및 기타 필요한 값을 제공합니다. 이 예에서는 LAST_PURCHASED를 키로 사용합니다.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. 요청을 보내고 방금 만든 사용자 지정 기준의 세부 사항이 포함된 응답을 확인합니다.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. 사용자 지정 기준이 만들어졌는지 확인하려면 Adobe Target 내에서 **[!UICONTROL Recommendations] > [!UICONTROL 기준]**&#x200B;으로 이동하여 이름으로 기준을 검색하거나 다음 단계에서 **사용자 지정 기준 목록 API**&#x200B;를 사용하십시오.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

이 경우 오류가 있습니다. **목록 사용자 지정 기준 API**&#x200B;을 사용하여 사용자 지정 기준을 보다 자세히 검사하여 오류를 조사하겠습니다.

## 목록 사용자 지정 기준

각 사용자 지정 기준의 세부 사항과 함께 모든 사용자 지정 기준 목록을 검색하려면 [목록 사용자 지정 기준 API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)를 사용합니다. 구문은 다음과 같습니다.

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. `TENANT_ID` 및 `API_KEY`을(를) 전과 같이 확인하고 요청을 전송합니다. 응답에서 사용자 지정 기준 ID와 앞서 언급한 오류 메시지에 대한 세부 사항을 확인하십시오.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

이 경우 서버 정보가 잘못되어 오류가 발생했습니다. 즉, [!DNL Target]은(는) 사용자 지정 기준 정의가 포함된 CSV 파일에 액세스할 수 없습니다. 사용자 지정 기준을 편집하여 이 문제를 해결하겠습니다.

## 사용자 지정 기준 편집

사용자 지정 기준 정의의 세부 사항을 변경하려면 [사용자 지정 기준 편집 API](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom)을 사용합니다. 구문은 다음과 같습니다.

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 전과 같이 `TENANT_ID` 및 `API_KEY`을 확인합니다.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. 편집할 (단일) 사용자 지정 기준의 기준 ID를 지정합니다.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. 본문에서는 업데이트된 JSON에 올바른 서버 정보를 제공합니다. 이 단계에서 액세스할 수 있는 서버에 대한 FTP 액세스를 지정합니다.
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. 요청을 보내고 응답을 기록합니다.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

**사용자 지정 기준 가져오기 API**&#x200B;를 사용하여 업데이트된 사용자 지정 기준의 성공을 확인하겠습니다.

## 사용자 지정 기준 가져오기

특정 사용자 지정 기준에 대한 사용자 지정 기준 세부 사항을 보려면 [사용자 지정 기준 API 가져오기](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom)를 사용하십시오. 구문은 다음과 같습니다.

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 세부 정보를 가져올 사용자 지정 기준의 기준 ID를 지정합니다. 요청을 보내고 응답을 검토합니다.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. 성공 확인 (이 경우 더 이상 FTP 오류가 없는지 확인하십시오.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (선택 사항) UI에서 업데이트가 정확하게 반영되는지 확인합니다.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## 사용자 지정 기준 삭제

앞서 언급한 기준 ID를 사용하여 [사용자 지정 기준 삭제 API](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)를 사용하여 사용자 지정 기준을 삭제합니다. 구문은 다음과 같습니다.

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 삭제할 (단일) 사용자 지정 기준의 기준 ID를 지정합니다. **보내기**를 클릭합니다.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. 사용자 지정 기준 가져오기를 사용하여 기준이 삭제되었는지 확인합니다.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
이 경우 예상 404 오류는 삭제된 기준을 찾을 수 없음을 나타냅니다.

>[!NOTE]
>사용자 지정 기준 만들기 API를 사용하여 만들었기 때문에 [!DNL Target] UI가 삭제되어도 기준이 제거되지 않습니다.

축하합니다! 이제 [!DNL Recommendations] API를 사용하여 사용자 지정 기준을 만들고, 나열하고, 편집하고, 삭제하고, 자세한 내용을 볼 수 있습니다. 다음 섹션에서는 [!DNL Target] 배달 API를 사용하여 권장 사항을 검색합니다.

[다음 &quot;서버측 전달 API를 사용하여 Recommendations 가져오기&quot; >](fetch-recs-server-side-delivery-api.md)
