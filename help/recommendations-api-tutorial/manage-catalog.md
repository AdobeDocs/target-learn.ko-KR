---
title: API를 사용하여 Recommendations 카탈로그 관리 방법
description: 자습서의 이 부분은 개발자가 Adobe Target API를 사용하여 Recommendations 카탈로그에서 개체를 만들고, 업데이트하고, 저장하고, 가져오고, 삭제하는 데 필요한 단계를 안내합니다.
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
source-wordcount: '924'
ht-degree: 1%

---


# API를 사용하여 [!DNL Recommendations] 카탈로그 관리

이때 JWT 인증 흐름을 사용하여 액세스 토큰을 생성하여 Adobe I/O과 함께 Adobe Target 관리 API를 사용하는 방법을 알아보았습니다.

[Recommendations API](https://developers.adobetarget.com/api/recommendations/)를 사용하여 권장 사항 카탈로그의 항목을 추가, 업데이트 또는 삭제할 수 있습니다. 나머지 Adobe Target 관리 API와 마찬가지로 [!DNL Recommendations] API는 인증이 필요합니다.

>[!TIP]
>
>**[!UICONTROL IMS::JWT 액세스 토큰이 24시간 후 만료되므로 인증을 위해 액세스 토큰을 새로 고쳐야 할 때마다 사용자 토큰]** 요청을 통해 + 인증을 생성합니다. 지침은 [Adobe API 인증 구성](../apis/configure-io-target-integration.md)을 참조하십시오.

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>계속하기 전에 [Recommendations Postman 컬렉션](https://developers.adobetarget.com/api/recommendations/#section/Postman)을 가져옵니다.

## 엔티티 저장 API를 사용하여 항목 만들기 및 업데이트

제품 페이지에서 실행하는 CSV 제품 피드 또는 [!DNL Target] 요청이 아닌 API를 사용하여 [!DNL Recommendations] 제품 데이터베이스를 채우려면 [개체 저장 API](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities)을 사용합니다. 이 요청은 단일 [!DNL Target] 환경에서 항목을 추가하거나 업데이트합니다. 구문은 다음과 같습니다.

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

예를 들어, 개체 저장은 해당 항목에 플래그를 지정하고 권장되지 않도록 하기 위해 재고 또는 가격 임계값과 같은 특정 임계값이 충족될 때마다 항목을 업데이트하는 데 사용할 수 있습니다.

1. **[!DNL Target]> [!UICONTROL 설정] > [!UICONTROL 호스트] > [!UICONTROL 환경]**&#x200B;으로 이동하여 항목을 추가하거나 업데이트할 [!DNL Target] 환경 ID를 가져옵니다.

   ![SaveEntities1](assets/SaveEntities01.png)

2. `TENANT_ID` 및 `API_KEY`이 이전에 설정된 Postman 환경 변수를 참조하는지 확인합니다. 비교를 위해 아래 이미지를 사용하십시오. 필요한 경우 아래 이미지에 있는 것과 일치하도록 API 요청의 헤더와 경로를 수정합니다.

   ![SaveEntities3](assets/SaveEntities03.png)

3. **본문**&#x200B;에 **raw** 코드로 JSON을 입력합니다. `environment` 변수를 사용하여 환경 ID를 지정하는 것을 잊지 마십시오. (아래 예에서 환경 ID는 6781입니다.)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   다음은 토스터기 오븐 제품의 관련 엔티티 값과 함께 entity.id kit2001을 환경 6781에 추가하는 샘플 JSON입니다.

   ```
      {
      "entities": [{
              "name": "Toaster Oven",
              "id": "kit2001",
              "environment": 6781,
              "categories": [
                  "housewares:appliances"
              ],
              "attributes": {
                  "inventory": 77,
                  "margin": 23,
                  "message": "crashing helicopter",
                  "pageUrl": "www.foobar.foo.com/helicopter.html",
                  "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
              }
          }]
      }
   ```

4. **보내기**&#x200B;를 클릭합니다. 다음 응답을 받아야 합니다.

   ![SaveEntities5.png](assets/SaveEntities05.png)

JSON 개체를 크기 조정하여 여러 제품을 전송할 수 있습니다. 예를 들어 이 JSON은 2개의 엔티티를 지정합니다.

```
    {
        "entities": [{
                "name": "Toaster Oven",
                "id": "kit2001",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 89,
                    "margin": 11,
                    "message": "Toaster Oven",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 102.5
                }
            },
            {
                "name": "Blender",
                "id": "kit2002",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 36,
                    "margin": 5,
                    "message": "Blender",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 54.5
                }
            }
        ]
    }
```

1. 이제 네 차례야! **개체 저장** API를 사용하여 다음 항목을 카탈로그에 추가합니다. 위의 샘플 JSON을 시작점으로 사용하십시오. (추가 개체를 포함하도록 JSON을 확장해야 합니다.)

   ![SaveEntities6.png](assets/SaveEntities06.png)

이런, 그 마지막 두 항목은 어울리지 않는 것 같아. **Get Entity** API를 사용하여 이들을 검사하고, 필요한 경우 **개체 삭제** API를 사용하여 삭제합니다.

## Get Entity API를 사용하여 항목 세부 사항 가져오기

기존 항목의 세부 사항을 검색하려면 [엔티티 API 가져오기](https://developers.adobetarget.com/api/recommendations/#operation/getEntity)를 사용합니다. 구문은 다음과 같습니다.

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

엔티티 세부 사항은 한 번에 하나의 엔티티에 대해서만 검색할 수 있습니다. Get Entity를 사용하여 카탈로그에서 업데이트가 수행되었는지 확인하거나, 그렇지 않으면 카탈로그의 컨텐츠를 감사할 수 있습니다.

1. API 요청에서 `entityId` 변수를 사용하여 개체 ID를 지정합니다. 다음 예제에서는 entityId=kit2004의 엔티티에 대한 세부 정보를 반환합니다.

   ![GetEntity1](assets/GetEntity1.png)

2. `TENANT_ID` 및 `API_KEY`이 이전에 설정된 Postman 환경 변수를 참조하는지 확인합니다. 비교를 위해 아래 이미지를 사용하십시오. 필요한 경우 아래 이미지에 있는 것과 일치하도록 API 요청의 헤더와 경로를 수정합니다.

   ![GetEntity2](assets/GetEntity2.png)

3. 요청을 전송합니다.

   ![GetEntity3](assets/GetEntity3.png)
위 예에서 보듯이 엔티티를 찾을 수 없다는 오류가 표시되면 올바른 환경에 요청을 제출하고 있는지  [!DNL Target] 확인합니다.

   >[!NOTE]
   명시적으로 지정된 환경이 없으면 Get Entity는 [기본 환경](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html#section_4F8539B07C0C45E886E8525C344D5FB0)에서만 엔티티를 가져오려고 시도합니다. 기본 환경 이외의 환경에서 가져오려는 경우 환경 ID를 지정해야 합니다.

4. 필요한 경우 `environmentId` 매개 변수를 추가하고 요청을 다시 전송합니다.

   ![GetEntity4](assets/GetEntity4.png)

5. 다른 **Get Entity** 요청을 이번에는 entityId=kit2005의 엔티티를 검사하십시오.

   ![GetEntity5](assets/GetEntity5.png)

이러한 엔티티를 카탈로그에서 제거해야 한다고 결정한다고 가정합니다. **개체 삭제** API를 사용하겠습니다.

## 개체 삭제 API를 사용하여 항목 삭제

카탈로그에서 항목을 제거하려면 [엔티티 API 삭제](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities)를 사용합니다. 구문은 다음과 같습니다.

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
이 API는 지정한 ID에서 참조하는 개체를 삭제합니다.
제공된 개체 ID가 없으면 주어진 환경의 모든 엔티티가 삭제됩니다. 환경 ID를 제공하지 않으면 모든 환경에서 엔티티가 삭제됩니다. 이것을 조심해서 사용하세요!

1. **[!DNL Target]> [!UICONTROL 설정] > [!UICONTROL 호스트] > [!UICONTROL 환경]**&#x200B;으로 이동하여 항목을 삭제할 환경 ID를 가져옵니다.[!DNL Target]

   ![DeleteEntities1](assets/SaveEntities01.png)

2. API 요청에서 `&ids=[comma-delimited-entity-ids]` 구문(쿼리 매개 변수)을 사용하여 삭제할 엔티티의 엔티티 ID를 지정합니다. 둘 이상의 엔티티를 삭제할 때에는 쉼표를 사용하여 ID를 구분합니다.

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. `&environment=[environmentId]` 구문을 사용하여 환경 ID를 지정하십시오. 그렇지 않으면 모든 환경의 엔티티가 삭제됩니다.

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. `TENANT_ID` 및 `API_KEY`이 이전에 설정된 Postman 환경 변수를 참조하는지 확인합니다. 비교를 위해 아래 이미지를 사용하십시오. 필요한 경우 아래 이미지에 있는 것과 일치하도록 API 요청의 헤더와 경로를 수정합니다.

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. 요청을 전송합니다.

   ![DeleteEntities5](assets/DeleteEntities5.png)

6. 삭제된 개체를 찾을 수 없음을 나타내는 **Get Entity**&#x200B;를 사용하여 결과를 확인합니다.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

축하합니다! 이제 [!DNL Recommendations] API를 사용하여 카탈로그의 개체에 대한 세부 정보를 만들고, 업데이트하고, 삭제하고, 얻을 수 있습니다. 다음 섹션에서는 사용자 지정 기준을 관리하는 방법을 알아봅니다.

[다음 &quot;사용자 지정 기준 관리&quot; >](manage-custom-criteria.md)
