---
title: API를 사용하여 Recommendations 카탈로그를 관리하는 방법
description: 이 자습서 부분에서는 개발자에게 Recommendations 카탈로그에서 Adobe Target API를 사용하여 엔티티를 생성, 업데이트, 저장, 가져오기 및 삭제하는 데 필요한 단계를 안내합니다.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 8060b69b-e8e5-4fe7-895f-742410d8ed45
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 2%

---

# 사용자 관리 [!DNL Recommendations] API를 사용한 카탈로그

이때 JWT 인증 플로우를 사용하여 Adobe I/O에서 Adobe Target 관리 API를 사용하기 위해 액세스 토큰을 생성하는 방법을 알아보았습니다.

를 사용할 수 있습니다 [Recommendations API](https://developers.adobetarget.com/api/recommendations/) 권장 사항 카탈로그에서 항목을 추가, 업데이트 또는 삭제하려면 나머지 Adobe Target 관리 API와 마찬가지로, [!DNL Recommendations] API에는 인증이 필요합니다.

>[!TIP]
>
>보내기 **[!UICONTROL IMS: 사용자 토큰을 통한 JWT 생성 + 인증]** 액세스 토큰이 24시간 후에 만료되므로 인증을 위해 새로 고쳐야 할 때마다 요청합니다. 자세한 내용은 [Adobe API 인증 구성](https://developer.adobe.com/target/before-administer/configure-authentication/)자세한 내용은 {target=_blank}.

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>계속하기 전에 [Recommendations Postman 컬렉션](https://developers.adobetarget.com/api/recommendations/#section/Postman).

## 엔티티 저장 API를 사용하여 항목 생성 및 업데이트

을(를) 채우려면 [!DNL Recommendations] CSV 제품 피드 또는 API가 아닌 API를 사용하는 제품 데이터베이스 [!DNL Target] 제품 페이지에서 실행되는 요청, [엔티티 저장 API](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities). 이 요청은 한 번의 클릭으로 항목을 추가하거나 업데이트합니다 [!DNL Target] 환경. 구문은 다음과 같습니다.

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

예를 들어, 엔티티 저장 을 사용하면 재고 또는 가격에 대한 임계값과 같은 특정 임계값이 충족될 때마다 항목을 갱신하여 해당 항목에 플래그를 지정하고 권장되지 않도록 할 수 있습니다.

1. 다음으로 이동 **[!DNL Target]> [!UICONTROL 설정] > [!UICONTROL 호스트] > [!UICONTROL 환경]** 얻다 [!DNL Target] 항목을 추가하거나 업데이트할 환경 ID입니다.

   ![SaveEntities1](assets/SaveEntities01.png)

2. 확인 `TENANT_ID` 및 `API_KEY` 이전에 설정한 Postman 환경 변수를 참조하십시오. 비교하려면 아래 이미지를 사용하십시오. 필요한 경우 API 요청의 헤더와 경로를 수정하여 아래 이미지에 있는 헤더와 일치시킵니다.

   ![SaveEntities3](assets/SaveEntities03.png)

3. JSON을 다음으로 입력 **원시** 의 코드 **본문**. 를 사용하여 환경 ID를 지정하는 것을 잊지 마십시오 `environment` 변수를 채우는 방법을 설명합니다. (아래 예에서 환경 ID는 6781입니다.)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   다음은 Toast Oven Oven 제품의 관련 엔티티 값과 함께 entity.id kit2001을 환경 6781에 추가하는 샘플 JSON입니다.

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

4. **보내기**&#x200B;를 클릭합니다. 다음 응답을 수신해야 합니다.

   ![SaveEntities5.png](assets/SaveEntities05.png)

JSON 개체의 크기를 조정하여 여러 제품을 보낼 수 있습니다. 예를 들어 이 JSON은 두 개의 엔티티를 지정합니다.

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

1. 이제 네 차례야! 를 사용하십시오 **엔티티 저장** API를 사용하여 카탈로그에 다음 항목을 추가합니다. 위의 샘플 JSON을 시작점으로 사용하십시오. (추가 엔티티를 포함하려면 JSON을 확장해야 합니다.)

   ![SaveEntities6.png](assets/SaveEntities06.png)

이런, 그 마지막 두 품목이 어울리지 않는 것 같군요. 다음 문서를 사용하여 검사하겠습니다. **엔티티 가져오기** API를 사용하고, 필요한 경우 **엔티티 삭제** API.

## 엔티티 가져오기 API를 사용하여 항목 세부 사항 가져오기

기존 항목의 세부 사항을 검색하려면 [엔티티 API 가져오기](https://developers.adobetarget.com/api/recommendations/#operation/getEntity). 구문은 다음과 같습니다.

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

엔티티 세부 정보는 한 번에 하나의 엔티티에 대해서만 검색할 수 있습니다. 엔티티 가져오기 를 사용하여 카탈로그에서 업데이트가 수행되었는지 확인하거나 카탈로그의 콘텐츠를 감사할 수 있습니다.

1. API 요청에서 변수를 사용하여 엔티티 ID를 지정합니다 `entityId`. 다음 예제는 entityId=kit2004를 사용하는 엔터티에 대한 세부 정보를 반환합니다.

   ![GetEntity1](assets/GetEntity1.png)

2. 확인 `TENANT_ID` 및 `API_KEY` 이전에 설정한 Postman 환경 변수를 참조하십시오. 비교하려면 아래 이미지를 사용하십시오. 필요한 경우 API 요청의 헤더와 경로를 수정하여 아래 이미지에 있는 헤더와 일치시킵니다.

   ![GetEntity2](assets/GetEntity2.png)

3. 요청을 보냅니다.

   ![GetEntity3](assets/GetEntity3.png)
위 예제와 같이 엔티티를 찾을 수 없다는 오류가 표시되면 요청을 올바른 로 제출했는지 확인합니다 [!DNL Target] 환경.

   >[!NOTE]
   명시적으로 지정된 환경이 없으면 엔티티 가져오기가 [기본 환경](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=en) 전용. 기본 환경 이외의 환경에서 가져오려면 환경 ID를 지정해야 합니다.

4. 필요한 경우 을(를) 추가합니다. `environmentId` 매개 변수를 설정하고 요청을 다시 전송합니다.

   ![GetEntity4](assets/GetEntity4.png)

5. 다른 보내기 **엔티티 가져오기** request, this time to inspect the entityId=kit2005.

   ![GetEntity5](assets/GetEntity5.png)

이러한 엔티티를 카탈로그에서 제거해야 한다고 결정한다고 가정합니다. 을(를) 사용해 보겠습니다. **엔티티 삭제** API.

## 엔티티 삭제 API를 사용하여 항목 삭제

카탈로그에서 항목을 제거하려면 [엔티티 API 삭제](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities). 구문은 다음과 같습니다.

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
이 API는 지정한 ID에서 참조하는 엔티티를 삭제합니다.
제공된 엔티티 ID가 없으면 주어진 환경의 모든 엔티티가 삭제됩니다. 환경 ID가 제공되지 않으면 모든 환경에서 엔티티가 삭제됩니다. 조심해서 사용하십시오!

1. 다음으로 이동 **[!DNL Target]> [!UICONTROL 설정] > [!UICONTROL 호스트] > [!UICONTROL 환경]** 얻다 [!DNL Target] 항목을 삭제할 환경 ID입니다.

   ![DeleteEntities1](assets/SaveEntities01.png)

2. API 요청에서 구문을 사용하여 삭제할 엔티티의 엔티티 ID를 지정합니다 `&ids=[comma-delimited-entity-ids]` (쿼리 매개 변수) 두 개 이상의 엔티티를 삭제할 때 ID를 쉼표로 구분하십시오.

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. 구문을 사용하여 환경 ID를 지정합니다 `&environment=[environmentId]`를 선택하지 않으면 모든 환경의 엔티티가 삭제됩니다.

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. 확인 `TENANT_ID` 및 `API_KEY` 이전에 설정한 Postman 환경 변수를 참조하십시오. 비교하려면 아래 이미지를 사용하십시오. 필요한 경우 API 요청의 헤더와 경로를 수정하여 아래 이미지에 있는 헤더와 일치시킵니다.

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. 요청을 보냅니다.

   ![DeleteEntities5](assets/DeleteEntities5.png)

6. 을 사용하여 결과 확인 **엔티티 가져오기**: 이제 삭제된 엔티티를 찾을 수 없음을 나타냅니다.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

축하합니다! 이제 를 사용할 수 있습니다 [!DNL Recommendations] 카탈로그에 있는 엔티티에 대한 세부 정보를 생성, 업데이트, 삭제 및 가져오는 API입니다. 다음 섹션에서는 사용자 지정 기준을 관리하는 방법을 알아봅니다.

[다음 &quot;사용자 지정 기준 관리&quot; >](https://developer.adobe.com/target/before-administer/recs-api/manage-custom-criteria/){target=_blank}
