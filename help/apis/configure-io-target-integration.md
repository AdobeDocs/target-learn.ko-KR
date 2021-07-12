---
title: Adobe Target API에 대한 인증을 구성하는 방법
description: 이 자습서에서는 개발자가 Adobe Target API와 성공적으로 상호 작용하는 데 필요한 인증 토큰을 생성하는 데 필요한 단계를 안내합니다. 다음 단계에 따라 Adobe 개발자 콘솔을 사용하여 Target API를 사용하는 데 필요한 bearer 액세스 토큰을 생성하고 테스트하십시오.
role: Developer, Admin, Architect
level: Intermediate
topic: 개인화, 관리, 통합, 개발
feature: API/SDK, 관리 및 구성
doc-type: tutorial
kt: null
thumbnail: null
author: Judy Kim
exl-id: 8a1e93e4-67b2-4942-a8da-fc0f2cbb2df2
source-git-commit: ee9aac0144e35abf32c5d8eafe10a013bf30d8d3
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 2%

---

# Adobe Target API에 대한 인증 구성

[!DNL Recommendations] 관리 API를 포함하는 Adobe Target 관리 API는 인증된 사용자만 Adobe Target에 액세스하는 데 사용할 수 있도록 인증에 의해 보호됩니다. [Adobe 개발자 콘솔](https://console.adobe.io/)을 사용하여 [!DNL Target]를 포함한 모든 Adobe Experience Cloud 솔루션에 대한 이 인증을 관리합니다.

이 단원에서는 Adobe Target API와 성공적으로 상호 작용하는 데 필요한 인증 토큰을 생성하는 데 필요한 사전 절차를 안내합니다. 다음에 나오는 섹션에서 다음을 수행합니다.

1. Adobe 개발자 콘솔에서 프로젝트를 만듭니다(이전에 통합이라고 함).
2. 프로젝트 세부 사항을 Postman으로 내보냅니다.
3. 베어러 액세스 토큰을 생성합니다.
4. 베어러 액세스 토큰을 테스트합니다.

## 사전 요구 사항

| 리소스 | 세부 사항 |
| --- | --- |
| 포스트맨 | 이러한 단계를 성공적으로 완료하려면 운영 체제에 대한 [Postman app](https://www.postman.com/downloads/)을 가져오십시오. Postman Basic은 계정 생성과 함께 무료입니다. 일반적으로 Adobe Target API를 사용하기 위해 필요하지 않지만 Postman을 사용하면 API 워크플로우를 보다 쉽게 만들 수 있고 Adobe Target에서는 API를 실행하고 작동 방법을 학습하는 데 도움이 되는 여러 Postman 컬렉션을 제공합니다. 이 자습서의 나머지 부분에서는 Postman에 대한 작업 지식을 가정합니다. 도움이 필요하면 [Postman 설명서](https://learning.getpostman.com/)를 참조하십시오. |
| 참조 | 이 자습서의 나머지 부분에서 다음 리소스에 익숙하다고 가정합니다.<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Target Adobe I/O 설명서](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API 설명서](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## Adobe I/O 프로젝트 만들기

이 섹션에서는 Adobe 개발자 콘솔에 액세스하고 [!DNL Adobe Target]에 대한 프로젝트를 만듭니다. 자세한 내용은 프로젝트](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md)에서 [설명서를 참조하십시오.

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. [Adobe Admin Console](https://adminconsole.adobe.com/)에서 Adobe 사용자 계정에 [제품 관리자](https://helpx.adobe.com/enterprise/using/admin-roles.html) 및 [개발자](https://helpx.adobe.com/enterprise/using/manage-developers.html) 수준 액세스 권한이 모두 부여되었는지 확인합니다. [!DNL Target]

2. [Adobe 개발자 콘솔](https://console.adobe.io/)에서 이 통합을 만들 Experience Cloud 조직을 선택합니다. (단일 Experience Cloud 조직에만 액세스할 수 있을 수 있습니다.)

   ![configure-io-target-createproject2.png](assets/configure-io-target-createproject2.png)

3. **[!UICONTROL 새 프로젝트 만들기]**&#x200B;를 클릭합니다.

   ![configure-io-target-createproject3.png](assets/configure-io-target-createproject3.png)

4. Adobe 서비스 및 제품에 액세스하려면 **[!UICONTROL API]** 추가 를 클릭하십시오.

   ![API 추가](assets/configure-io-target-createproject4.png)

5. 통합할 Adobe 서비스로 **[!DNL Adobe Target]** 를 선택합니다. 표시되는 **[!UICONTROL 다음]** 단추를 클릭합니다.

   ![configure-io-target-createproject5](assets/configure-io-target-createproject5.png)

6. 공개 및 개인 키를 Target에 대해 만들고 있는 서비스 계정 통합에 연결할 옵션을 선택합니다. 이 자습서에서 **[!UICONTROL 옵션 1: 키 쌍]**&#x200B;을(를) 생성하고 **[!UICONTROL 키 쌍 생성]**을(를) 클릭합니다.
   ![configure-io-target-createproject6](assets/configure-io-target-createproject6.png)

7. 결과를 확인합니다! 지침에 따라 개인 키가 포함된 자동으로 다운로드한 구성 파일(`config`)을 기록해 두십시오. **[!UICONTROL 다음]**을 클릭합니다.
   ![configure-io-target-createproject7](assets/configure-io-target-createproject7.png)
8. 파일 시스템에서 이전 단계에서 생성된 압축 구성 파일인 `config` 위치를 확인합니다. 이 `config` 파일에는 개인 키가 포함되어 있으며, 이 개인 키는 나중에 사용해야 합니다. 파일 시스템 내의 정확한 위치는 여기에 표시된 위치와 다를 수 있습니다.
   ![configure-io-target-createproject8](assets/configure-io-target-createproject8.png)
9. Adobe 개발자 콘솔로 돌아가서 [!DNL Recommendations]를 사용하는 속성에 해당하는 [제품 프로필](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html)을 선택합니다. 속성을 사용하지 않는 경우 기본 작업 공간 옵션을 선택합니다. **[!UICONTROL 구성된 API]**를 클릭합니다.
   ![configure-io-target-createproject9](assets/configure-io-target-createproject9.png)

10. **[!UICONTROL 통합 만들기]**&#x200B;를 클릭합니다. API가 성공적으로 구성되었음을 나타내는 임시 메시지를 수신해야 합니다.

11. 마지막 단계로 프로젝트 이름을 원래 `Project 1`보다 의미 있는 이름으로 변경합니다. 이렇게 하려면 표시된 대로 탐색 경로를 사용하여 프로젝트로 이동하고 **[!UICONTROL 프로젝트 편집]** 을 클릭하여 **[!UICONTROL 프로젝트 편집] 모달에 액세스한 다음 프로젝트 이름을 변경합니다.

![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>이 자습서에서는 프로젝트 이름을 &quot;Target 통합&quot;으로 지정합니다. Adobe Target 이외의 용도로 프로젝트를 사용할 것으로 예상되는 경우, 적절하게 이름을 지정할 수 있습니다. 예를 들어, Adobe Experience Cloud의 다른 솔루션과 함께 사용할 수 있으므로, 이름을 &quot;Adobe API&quot; 또는 &quot;Experience Cloud API&quot;로 지정하도록 선택할 수 있습니다.

## 프로젝트 세부 사항 내보내기

이제 [!DNL Target] 액세스에 사용할 수 있는 Adobe 프로젝트가 있으므로, Adobe API 요청과 함께 해당 프로젝트의 세부 사항을 전송해야 합니다. 이러한 세부 사항은 여러 [!DNL Target] API를 포함하여 여러 Adobe API와 상호 작용하기 위해 필요합니다. 예를 들어 통합 세부 사항에는 [!DNL Target] 관리 API에 필요한 인증 및 정보가 포함됩니다. 따라서 Postman과 함께 API를 사용하려면 해당 세부 사항을 Postman으로 가져와야 합니다.

Postman에서 프로젝트의 세부 사항을 지정하는 방법에는 여러 가지가 있지만, 이 섹션에서는 사전 빌드된 일부 기능 및 컬렉션을 사용합니다. 먼저(이 섹션에서) 통합 세부 사항을 Postman 환경으로 내보냅니다. 다음 (다음 섹션에서) 필요한 Adobe 리소스에 대한 액세스 권한을 부여하는 베어러 액세스 토큰을 생성합니다.

>[!NOTE]
>
>[!DNL Target] 을 포함하여 모든 Experience Cloud 솔루션에 적용할 수 있는 비디오 지침은 [Experience Platform API와 함께 Postman 사용](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html) 을 참조하십시오. 다음 섹션은 [!DNL Target] API와 관련이 있습니다.
>
> 1. Postman으로 Adobe I/O 통합 세부 정보 내보내기
> 2. Postman을 사용하여 액세스 토큰 생성

>
> 
이러한 단계는 아래에도 제공됩니다.

1. 여전히 [Adobe 개발자 콘솔](https://console.adobe.io/)에서 새 프로젝트의 **[!UICONTROL 서비스 계정(JWT)]** 자격 증명을 보려면 탐색합니다. 표시된 대로 왼쪽 탐색 또는 **[!UICONTROL 자격 증명]** 섹션을 사용합니다.
   ![JWT1](assets/configure-io-target-jwt1.png)
자격 증명  **[!UICONTROL 세부 사항]**&#x200B;에서  **공개 키**,  **클라이언트 ID** 및 서비스 계정과 관련된 기타 정보를 볼 수 있습니다.
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. **[!UICONTROL Adobe Target]** API에 대한 정보로 이동하려면 을 클릭하십시오. 표시된 대로 왼쪽 탐색 또는 **[!UICONTROL 연결된 제품 및 서비스]** 섹션을 사용합니다.
   ![JWT2](assets/configure-io-target-jwt2.png)
3. Postman 환경에 대한 인증 정보를 캡처하는 JSON 파일을 만들려면 **[!UICONTROL Download for Postman]** > **[!UICONTROL 서비스 계정(JWT)]**을 클릭합니다.
   ![JWT3](assets/configure-io-target-jwt3.png)
파일 시스템에서 JSON 파일을 확인합니다.
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. Postman에서 톱니바퀴 아이콘을 클릭하여 환경을 관리한 다음, **가져오기**를 클릭하여 JSON 파일(환경)을 가져옵니다.
   ![JWT4](assets/configure-io-target-jwt4.png)
5. 파일을 선택하고 **열기**를 클릭합니다.
   ![JWT5](assets/configure-io-target-jwt5.png)
6. Postman **환경 관리** 모달에서 새로 가져온 환경의 이름을 클릭하여 검사합니다. (환경 이름은 여기에 표시된 환경 이름과 다를 수 있습니다. 원하는 대로 이름을 편집합니다. 반드시 Adobe 프로젝트 이름과 일치할 필요는 없습니다.)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. 참고 `CLIENT_SECRET` 및 `API_KEY`(다른 변수와 함께)의 값은 Adobe 개발자 콘솔에 정의된 대로 통합에서 미리 채워져 있습니다. (Postman `CLIENT_SECRET` 변수는 개발자 콘솔에 표시된 대로 `CLIENT SECRET` Adobe 자격 증명과 일치해야 하며 Postman의 `API_KEY`도 개발자 콘솔에서 `CLIENT ID`와 일치해야 합니다.) 그와 대조적으로, 참고 `PRIVATE_KEY`, `JWT_TOKEN` 및 `ACCESS_TOKEN`는 비어 있습니다. 먼저 `PRIVATE_KEY` 값을 제공하겠습니다.
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**놀라워요!**
   >
   >퀴즈! 개인 키가 어디에 있는지 기억하시나요?
   >맞습니다. Adobe 개발자 콘솔에서 이전에 다운로드한 `config` 파일에 있습니다.

8. 파일 시스템에서 `config` 파일을 열고 `private` 키 파일을 엽니다.
   ![JWT8](assets/configure-io-target-jwt8.png)
9. `private` 키 파일의 전체 내용을 선택하고 복사합니다.
   ![JWT9](assets/configure-io-target-jwt9.png)
10. Postman에서 개인 키 값을 **INITIAL VALUE** 및 **CURRENT VALUE** 필드에 붙여 넣습니다.
   ![JWT10](assets/configure-io-target-jwt10.png)
11. **[!UICONTROL 업데이트]**&#x200B;를 클릭하고 환경 모달을 닫습니다.


## 베어러 액세스 토큰 생성

이 섹션에서는 Adobe Target API와의 상호 작용을 인증하는 데 필요한 bearer 액세스 토큰을 생성합니다. 베어러 액세스 토큰을 생성하려면 통합 세부 사항(이전 섹션에 설정됨)을 [IMS(Identity Management Service)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md)에 보내야 합니다. 이 작업을 수행하는 방법에는 몇 가지가 있지만, 이 자습서에서는 IMS API에 대한 맞춤형 POST 요청을 빌드했습니다. 농담이지 이 자습서에서는 프로세스를 직접적이고 쉽게 만드는 사전 빌드된 IMS 호출이 포함된 Postman 컬렉션을 이용합니다. 컬렉션을 가져온 후에는 필요할 때마다 다시 사용하여 Adobe Target뿐만 아니라 다른 Adobe API에 대한 새 토큰을 생성할 수 있습니다.

1. [Identity Management 서비스 API 샘플 호출 Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)로 이동합니다.
   ![token1](assets/configure-io-target-generatetoken1.png)
2. **Adobe I/O 액세스 토큰 생성 Postman 컬렉션을 클릭합니다**.
   ![token2](assets/configure-io-target-generatetoken2.png)
3. **Raw**를 클릭한 다음 결과 JSON을 클립보드에 복사하여 이 컬렉션에 대한 원시 JSON을 가져옵니다. (또는 원시 JSON을 .json 파일로 저장할 수 있습니다.)
   ![token3](assets/configure-io-target-generatetoken3.png)
4. Postman에서 클립보드에서 원시 JSON을 붙여 넣어 컬렉션을 가져옵니다. (또는 저장한 .json 파일을 업로드할 수 있습니다.) **계속**을 클릭합니다.
   ![토큰 4](assets/configure-io-target-generatetoken4.png)
5. **[!UICONTROL IMS 선택: JWT 액세스 토큰 생성 Postman 컬렉션에서 사용자 토큰]** 요청을 통해 + 인증을 생성하고 환경을 선택한 다음 **Send** 를 클릭하여 토큰을 생성합니다.

   ![토큰5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >이 베어러 액세스 토큰은 24시간 동안 유효합니다. 새 토큰을 생성해야 할 때마다 요청을 다시 전송합니다.

6. 환경 관리 모달을 다시 열고 환경을 선택합니다.
   ![token6](assets/configure-io-target-jwt11.png)
7. 이제 `ACCESS_TOKEN` 및 `JWT_TOKEN` 값이 채워집니다.
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>Q: JWT(JSON 웹 토큰) 및 bearer 액세스 토큰을 생성하려면 Adobe I/O 액세스 토큰 생성 Postman 컬렉션을 사용해야 합니까?
>
>A: 아니! Adobe I/O 액세스 토큰 생성 Postman 컬렉션은 Postman에서 JWT 및 bearer 액세스 토큰을 보다 쉽게 생성할 수 있도록 편의성으로 사용할 수 있습니다. 또는 Adobe 개발자 콘솔 내의 기능을 사용하여 베어러 액세스 토큰을 수동으로 생성할 수 있습니다.

## 베어러 액세스 토큰 테스트

이 연습에서는 [!DNL Target] 계정에서 활동 목록을 검색하는 API 요청을 전송하여 새 베어러 액세스 토큰을 사용합니다. 성공적인 응답은 API를 사용하기 위해 Adobe 프로젝트 및 인증이 예상대로 작동하는지 나타냅니다.

1. [Adobe Target Admin API Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection)을 가져옵니다. Postman에서 컬렉션을 가져올 때까지 모든 메시지를 따릅니다.
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. 컬렉션을 확장하고 **[!UICONTROL 활동 나열]** 요청을 확인합니다.
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. `{{access_token}}` 과 같은 변수는 처음에 해결되지 않습니다. 이 문제를 다양한 방법으로 해결할 수 있습니다. 예를 들어, `{{access_token}}` 이라는 새 컬렉션 변수를 정의할 수 있습니다. 이 자습서에서는 대신 API 요청을 변경하여 이전에 사용한 Postman 환경을 활용합니다. 이렇게 하면 환경이 Adobe API에 공통되는 모든 변수를 하나의 일관된 통합으로 계속 사용할 수 있습니다.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. `{{access_token}}`을 `{{ACCESS_TOKEN}}`(으)로 바꿀 입력합니다.
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. `{{api_key}}`을 `{{API_KEY}}`(으)로 바꿀 입력합니다.
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. `{{tenant}}`을 `{{TENANT_ID}}`(으)로 바꿀 입력합니다. 참고 `{{TENANT_ID}}`은(는) 아직 인식되지 않습니다.
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. 환경 관리 모달을 열고 환경을 선택합니다.
   ![JWT11](assets/configure-io-target-jwt11.png)
1. 새 `{{TENANT_ID}}` 환경 변수를 추가하려면 을 입력합니다. 테넌트 ID 값을 복사하여 새 `TENANT_ID` 환경 변수의 **INITIAL VALUE** 및 **CURRENT VALUE** 필드에 붙여넣습니다.

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >테넌트 ID는 [!DNL Target] `clientcode`과 다릅니다. 테넌트 ID는 [!DNL Target]에 로그인한 경우 URL에 있습니다. 테넌트 ID를 얻으려면 [!DNL Adobe Experience Cloud]에 로그인하고 [!DNL Target] 를 열고 [!DNL Target] 카드를 클릭합니다. URL 하위 도메인에 언급된 대로 테넌트 ID 값을 사용합니다.
   >
   >예를 들어 Adobe Target에 로그인할 때 URL이
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >그러면 테넌트 ID가 &quot;mycompany&quot;입니다.

1. 올바른 환경을 선택했는지 확인한 후 요청을 보내십시오. 활동 목록이 포함된 응답을 받아야 합니다.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

축하합니다! Adobe 인증을 확인했으므로 이 인증을 사용하여 Adobe Target API(및 다른 Adobe API)와 상호 작용할 수 있습니다. 예를 들어 [Recommendations API](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html)를 사용하여 권장 사항을 만들거나 관리할 수 있습니다.
