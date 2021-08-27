---
title: We.Travel 샘플 앱 다운로드 및 업데이트
description: 'We.Travel 샘플 앱은 Adobe Mobile Services SDK v4를 사용하여 미리 구현되었습니다. 자체 Experience Cloud 조직 및 솔루션 계정을 가리키도록 업데이트해야 합니다.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: ee58c7c85708722cf040cd9b039a2855dd390a16
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# We.Travel 샘플 앱 다운로드 및 업데이트

We.Travel 샘플 앱은 Adobe Mobile Services SDK v4를 사용하여 미리 구현되었습니다. 자신의 Experience Cloud 조직 및 솔루션 계정을 가리키도록 업데이트해야 합니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* Android Studio에서 We.Travel 샘플 앱을 다운로드하여 엽니다.
* [!DNL Target]에 대한 Mobile Services SDK 설정 확인 및 업데이트

## We.Travel 앱 다운로드

* [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip) 다운로드
* zip 파일의 압축을 해제합니다.
* Android Studio에서 앱을 기존 프로젝트로 엽니다(&quot;잘못된 VCS 루트 매핑&quot;에 대한 오류 무시).
* 에뮬레이터에서 앱을 실행하여 앱이 빌드되고 홈 화면이 표시되는지 확인합니다.
* 앱을 찾아보고 예약 프로세스를 완료할 수 있는지 확인합니다(결제 옵션을 선택하고 &quot;계속&quot;을 눌러 청구 화면을 건너뜁니다.).

   ![appConfirmation ](assets/wetravel_homeScreen.png)![화면을 엽니다.](assets/wetravel_confirmationScreen.png)

## [!DNL Target]에 대한 Mobile Services SDK 설정 확인 및 업데이트

Adobe 모바일 서비스 SDK는 설명서](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en)에 따라 We.Travel 앱 [에 사전 설치되어 있습니다. 이제 설치를 업데이트하여 자신의 [!DNL Target] 계정을 가리킵니다.

먼저 Mobile Services 사용자 인터페이스에서 새 앱을 만듭니다.

1. [Mobile Services Adobe 인터페이스](https://mobilemarketing.adobe.com/)에 로그인합니다.
1. [!UICONTROL 앱 관리]로 이동한 다음 **[!UICONTROL 추가]**&#x200B;를 클릭하여 이 자습서에서 사용할 새 앱을 추가합니다(**[!UICONTROL 앱 관리]** > **[!UICONTROL 추가]**).
1. 비프로덕션 데이터가 있는 Analytics 보고서 세트를 선택하고, 앱에 이름을 지정하고, **[!UICONTROL Standard]** 유형을 선택한 다음 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
1. 앱이 추가되면 [!UICONTROL SDK Target 옵션] 섹션의 다음 화면에 [!DNL Target] 클라이언트 코드를 추가합니다(**[!UICONTROL 설정]** > **[!UICONTROL 구현]** > **[!UICONTROL 설정 편집]**, `at.js` 단추 옆에 있는 [!DNL Target] 인터페이스에서 클라이언트 코드를 찾을 수 있습니다.).
1. [!UICONTROL 요청 시간 초과] 설정은 시간 제한 지침을 실행하기 전에 앱이 [!DNL Target] 서버의 응답을 기다리는 시간을 결정합니다. 기본 설정을 그대로 둡니다.
1. [!UICONTROL 방문자 ID 서비스]를 활성화하고 드롭다운에서 [!UICONTROL 조직]이 선택되었는지 확인합니다.
1. 창 오른쪽 상단에 있는 **[!UICONTROL 저장]** 을 클릭하여 변경 사항을 저장합니다([!UICONTROL 범용 링크], [!UICONTROL 앱 링크] 옵션 또는 [!UICONTROL 푸시 서비스] 섹션에 있는 항목이 아님).
1. 페이지 하단에 있는 앱 SDK 다운로드 섹션으로 스크롤하고 구성 파일을 다운로드합니다.

   ![구성 파일 다운로드](assets/config_file.jpg)

1. Android Studio 프로젝트 자산 폴더의 `ADBMobileConfig.json` 파일을 바꿉니다(앱 > src > main > assets).

1. 이제 `ADBMobileConfig.json` 파일을 열고 [!DNL Target] 클라이언트 코드 및 Analytics 세부 사항과 같은 예상 변경 사항이 포함되어 있는지 확인합니다.
   ![구성 파일 다운로드](assets/client_code.jpg)

설정이 표시되지 않으면 [!UICONTROL Mobile Services] 인터페이스에서 오른쪽 **[!UICONTROL 저장]** 단추를 클릭하고 파일을 올바른 위치에 복사했는지 확인하십시오.

축하합니다! SDK를 [!DNL Target] 계정 세부 정보로 업데이트했습니다. 다음 단원에서 [!DNL Target] 요청을 추가한 후에 구성에 대한 추가 유효성 검사를 수행합니다.

**[다음 : &quot;Target 요청 추가&quot; >](add-requests.md)**
