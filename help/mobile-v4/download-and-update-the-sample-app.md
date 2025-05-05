---
title: We.Travel 샘플 앱 다운로드 및 업데이트
description: We.Travel 샘플 앱은 Adobe Mobile Services SDK v4를 사용하여 미리 구현됩니다. 자체 Experience Cloud 조직 및 솔루션 계정을 가리키도록 업데이트하기만 하면 됩니다.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# We.Travel 샘플 앱 다운로드 및 업데이트

We.Travel 샘플 앱은 Adobe Mobile Services SDK v4를 사용하여 미리 구현됩니다. 자체 Experience Cloud 조직 및 솔루션 계정을 가리키도록 업데이트하기만 하면 됩니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* Android Studio에서 We.Travel 샘플 앱을 다운로드하여 엽니다.
* [!DNL Target]에 대한 Mobile Services SDK 설정 확인 및 업데이트

## We.Travel 앱 다운로드

* [sample-app-android-SDKv4-Base-Version.zip 다운로드](assets/sample-app-android-SDKv4-Base-Version.zip)
* zip 파일 압축 풀기
* Android Studio에서 앱을 기존 프로젝트로 엽니다(&quot;잘못된 VCS 루트 매핑&quot;에 대한 오류 무시).
* 에뮬레이터에서 앱을 실행하여 앱이 빌드되고 홈 화면이 표시되는지 확인합니다.
* 앱을 검색하고 예약 프로세스를 완료할 수 있는지 확인합니다(결제 옵션을 선택하고 &quot;진행&quot;을 눌러 청구 화면을 건너뜁니다!).

  ![앱 열기](assets/wetravel_homeScreen.png)![확인 화면](assets/wetravel_confirmationScreen.png)

## [!DNL Target]에 대한 Mobile Services SDK 설정 확인 및 업데이트

Adobe Mobile Services SDK가 We.Travel 앱 [에 따라 ](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en) 내에 미리 설치되었습니다. 이제 자신의 [!DNL Target] 계정을 가리키도록 설치를 업데이트합니다.

먼저 Mobile Services 사용자 인터페이스에서 새 앱을 만듭니다.

1. [Adobe Mobile Services 인터페이스](https://mobilemarketing.adobe.com/)에 로그인합니다.
1. [!UICONTROL Manage Apps] (으)로 이동한 다음 **[!UICONTROL Add]**&#x200B;을(를) 클릭하여 이 자습서에서 사용할 새 앱을 추가합니다(**[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**).
1. 비프로덕션 데이터가 포함된 Analytics 보고서 세트를 선택하고, 앱에 이름을 지정하고, **[!UICONTROL Standard]** 유형을 선택하고 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.
1. 앱이 추가되면 [!UICONTROL SDK Target Options] 섹션의 다음 화면에 [!DNL Target] 클라이언트 코드를 추가하십시오. `at.js` 다운로드 단추 옆의 **[!UICONTROL Setup]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit Settings]** 아래의 [!DNL Target] 인터페이스에서 클라이언트 코드를 찾을 수 있습니다.
1. [!UICONTROL Request Timeout] 설정은 시간 제한 명령을 실행하기 전에 앱이 [!DNL Target] 서버의 응답을 기다리는 시간을 결정합니다. 기본 설정을 그대로 둡니다.
1. [!UICONTROL Visitor ID Service]을(를) 사용하도록 설정하고 드롭다운에서 [!UICONTROL Organization]이(가) 선택되어 있는지 확인하십시오.
1. 창의 오른쪽 위에 있는 **[!UICONTROL Save]**([!UICONTROL Universal Links], [!UICONTROL App Links] 옵션 또는 [!UICONTROL Push Services] 섹션에 있는 옵션 아님)을 클릭하여 변경 내용을 저장합니다.
1. 페이지 하단에 있는 앱 SDK 다운로드 섹션으로 스크롤하여 구성 파일을 다운로드합니다.

   ![구성 파일 다운로드](assets/config_file.jpg)

1. Android Studio 프로젝트 자산 폴더(앱 > src > 기본 > 자산)에서 `ADBMobileConfig.json` 파일을 바꿉니다.

1. 이제 `ADBMobileConfig.json` 파일을 열고 [!DNL Target] 클라이언트 코드 및 Analytics 세부 정보와 같은 예상 변경 내용이 포함되어 있는지 확인합니다.
   ![구성 파일 다운로드](assets/client_code.jpg)

설정이 표시되지 않으면 [!UICONTROL Mobile Services] 인터페이스에서 올바른 **[!UICONTROL Save]** 단추를 클릭하고 파일을 올바른 위치에 복사했는지 확인하십시오.

축하합니다! [!DNL Target] 계정 세부 정보로 SDK를 업데이트했습니다! 다음 단원에서 [!DNL Target]개의 요청을 추가한 후 구성에 대한 추가 유효성 검사를 수행합니다.

**[다음 : &quot;Target 요청 추가&quot; >](add-requests.md)**
