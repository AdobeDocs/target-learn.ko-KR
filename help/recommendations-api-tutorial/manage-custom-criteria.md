---
title: 사용자 지정 기준을 관리하는 방법
description: 이 자습서 부분에서는 Adobe Target API를 사용하여 Adobe Target Recommendations 기준을 관리, 만들기, 목록, 편집, 가져오기 및 삭제하는 데 필요한 단계를 개발자에게 안내합니다.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: ee63bd3e-200a-4c08-b364-9f17a479033b
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 1%

---

# 사용자 지정 기준 관리

경우에 따라 [!DNL Recommendations] 판촉할 특정 항목을 표시할 수 없습니다. 이러한 경우 사용자 지정 기준은 주어진 주요 항목 또는 카테고리에 대해 특정 권장 항목 세트를 제공하는 방법을 제공합니다. 키 항목 또는 카테고리와 권장 항목 간의 매핑을 정의하고 해당 매핑을 사용자 지정 기준으로 가져옵니다. 이 프로세스는 [사용자 지정 기준 설명서](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en). 해당 설명서에 설명된 대로 다음을 통해 사용자 지정 기준을 작성, 편집 및 삭제할 수 있습니다. [!DNL Target] 사용자 인터페이스(UI)입니다. 하지만, [!DNL Target] 또한 은 사용자 지정 기준을 보다 자세히 관리할 수 있도록 해주는 사용자 지정 기준 API 세트를 제공합니다.

>[!IMPORTANT]
>
>사용자 지정 기준에 대해 이 사용 지침을 따르십시오.
>
> API를 사용하여 주어진 사용자 지정 기준에 대해 모든 작업(만들기, 편집, 삭제)을 수행하거나 UI를 사용하여 모든 작업(만들기, 편집, 삭제)을 수행합니다. UI와 API의 조합을 통해 사용자 지정 기준을 관리하면 정보가 충돌하거나 예기치 않은 결과가 발생할 수 있습니다. 예를 들어, UI에서 사용자 지정 기준을 만든 다음 API를 통해 편집하면 API를 통해 표시되는 대로 백엔드에서 업데이트되더라도 UI에 업데이트가 반영되지 않습니다.

## 사용자 지정 기준 만들기

을 사용하여 사용자 지정 기준을 만들려면 [사용자 지정 기준 API 만들기](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom), 구문은 다음과 같습니다.

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>사용자 지정 기준 만들기 API를 사용하여 만든 사용자 지정 기준은 이 연습에서 설명한 대로 UI에 나타나고 여기에서 유지됩니다. UI에서 편집하거나 삭제할 수 없습니다. 편집하거나 삭제할 수 있습니다 **API 사용**&#x200B;하지만 어느 쪽이든 간에 계속 [!DNL Target] UI. UI에서 편집하거나 삭제하는 옵션을 유지 관리하려면 [설명서](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en)를 설정하는 것이 좋습니다.

위의 경고를 읽은 후에만 이 자습서를 진행하여 나중에 UI에서 삭제할 수 없는 새 사용자 지정 기준을 만들 수 있습니다.

1. 확인 `TENANT_ID` 및 `API_KEY` 대상 **사용자 지정 기준 만들기** 이전에 설정한 Postman 환경 변수를 참조하십시오. 비교하려면 아래 이미지를 사용하십시오.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. 추가 **본문** 로서의 **원시** 사용자 지정 기준 CSV 파일의 위치를 정의하는 JSON입니다. 에 제공된 예제를 사용합니다. [사용자 지정 기준 API 만들기](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) 설명서를 템플릿으로 사용하여 `environmentId` 및 기타 값을 필요에 따라 구성합니다. 이 예에서는 LAST_PURCHASED를 키로 사용합니다.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. 요청을 보내고 방금 만든 사용자 지정 기준의 세부 사항이 포함된 응답을 관찰합니다.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. 사용자 지정 기준이 만들어졌는지 확인하려면 Adobe Target 내에서 다음 위치로 이동합니다 **[!UICONTROL Recommendations] > [!UICONTROL 기준]** 이름을 기준으로 기준을 검색하거나 **목록 사용자 지정 기준 API** 을 클릭합니다.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

이 경우 오류가 있습니다. 사용자 지정 기준을 좀 더 자세히 검토하여 오류를 조사하겠습니다. **목록 사용자 지정 기준 API**.

## 사용자 지정 기준 나열

각 사용자 지정 기준의 세부 사항과 함께 목록을 검색하려면 [목록 사용자 지정 기준 API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom). 구문은 다음과 같습니다.

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. 확인 `TENANT_ID` 및 `API_KEY` 전과 마찬가지로 및 요청을 전송합니다. 응답에서 사용자 지정 기준 ID와 이전에 언급된 오류 메시지에 대한 세부 사항을 확인합니다.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

이 경우 서버 정보가 잘못되어 오류가 발생했습니다. 즉, [!DNL Target] 이 사용자 지정 기준 정의를 포함하는 CSV 파일에 액세스할 수 없습니다. 사용자 지정 기준을 편집하여 이 문제를 해결하겠습니다.

## 사용자 지정 기준 편집

사용자 지정 기준 정의의 세부 사항을 변경하려면 [사용자 지정 기준 API 편집](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom). 구문은 다음과 같습니다.

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 확인 `TENANT_ID` 및 `API_KEY`이전 과 마찬가지로 ).
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. 편집할 (단일) 사용자 지정 기준의 기준 ID를 지정합니다.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. Body에서 업데이트된 JSON에 올바른 서버 정보를 제공합니다. (이 단계에서는 액세스할 수 있는 서버에 대한 FTP 액세스 권한을 지정합니다.)
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. 요청을 보내고 응답을 확인합니다.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

다음을 사용하여 업데이트된 사용자 지정 기준의 성공을 확인하겠습니다. **사용자 지정 기준 API 가져오기**.

## 사용자 지정 기준 가져오기

특정 사용자 지정 기준에 대한 사용자 지정 기준 세부 사항을 보려면 [사용자 지정 기준 API 가져오기](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom). 구문은 다음과 같습니다.

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 세부 사항을 가져올 사용자 지정 기준의 기준 ID를 지정합니다. 요청을 보내고 응답을 검토합니다.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. 성공 확인. (이 경우 더 이상 FTP 오류가 없는지 확인합니다.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (선택 사항) UI에서 업데이트가 정확하게 반영되는지 확인합니다.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## 사용자 지정 기준 삭제

앞에서 언급한 기준 ID를 사용하여 사용자 지정 기준을 삭제하고 [사용자 지정 기준 API 삭제](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom). 구문은 다음과 같습니다.

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 삭제할 (단일) 사용자 지정 기준의 기준 ID를 지정합니다. **보내기**를 클릭합니다.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. 사용자 지정 기준 가져오기를 사용하여 기준이 삭제되었는지 확인합니다.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
이 경우 예상 404 오류는 삭제된 기준을 찾을 수 없음을 나타냅니다.

>[!NOTE]
>참고로, 기준은 [!DNL Target] UI는 사용자 지정 기준 만들기 API를 사용하여 만들어졌기 때문에 삭제되었지만,

축하합니다! 이제 다음을 사용하여 사용자 지정 기준에 대한 세부 사항을 만들고, 나열하고, 편집하고, 삭제하고, 가져올 수 있습니다 [!DNL Recommendations] API. 다음 섹션에서는 [!DNL Target] 권장 사항을 검색할 배달 API.

[다음 &quot;서버 측 배달 API를 사용하여 Recommendations 가져오기&quot; >](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=_blank}
