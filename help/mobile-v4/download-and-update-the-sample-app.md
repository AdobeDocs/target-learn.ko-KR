---
title: We.Travel 샘플 앱 다운로드 및 업데이트
seo-title: 샘플 앱 다운로드 및 모바일 서비스 SDK 확인
description: 'We.Travel 샘플 앱은 Adobe Mobile Services SDK v4와 함께 미리 구현되어 있습니다. 해당 Experience Cloud 조직 및 솔루션 계정을 가리키도록 업데이트만 하면 됩니다.   '
seo-description: We.Travel 샘플 앱은 Adobe Mobile Services SDK v4와 함께 미리 구현되어 있습니다. 해당 Experience Cloud 조직 및 솔루션 계정을 가리키도록 업데이트만 하면 됩니다.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# We.Travel 샘플 앱 다운로드 및 업데이트

We.Travel 샘플 앱은 Adobe Mobile Services SDK v4와 함께 미리 구현되어 있습니다. 자신의 Experience Cloud 조직 및 솔루션 계정을 가리키도록 업데이트만 하면 됩니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* Android Studio에서 We.Travel 샘플 앱 다운로드 및 열기
* Mobile Services SDK 설정 확인 및 업데이트 [!DNL Target]

## We.Travel 앱 다운로드

* sample-app-android-SDKv4- [Base-Version.zip 다운로드](assets/sample-app-android-SDKv4-Base-Version.zip)
* zip 파일 압축 해제
* Android Studio에서 앱을 기존 프로젝트로 엽니다(&quot;잘못된 VCS 루트 매핑&quot;에 대한 오류 무시).
* 에뮬레이터에서 앱을 실행하여 앱이 빌드되고 홈 화면이 표시되는지 확인합니다
* 앱을 찾아보고 예약 프로세스를 완료할 수 있는지 확인합니다(결제 옵션을 선택한 다음 &quot;계속&quot;을 눌러 결제 화면을 건너뜁니다.)

   ![appConfirmation](assets/wetravel_homeScreen.png)![화면 열기](assets/wetravel_confirmationScreen.png)

## Mobile Services SDK 설정 확인 및 업데이트 [!DNL Target]

Adobe Mobile Services SDK는 설명서에 [따라 We.Travel 앱 내에 사전 설치되어 있습니다](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html). 이제 설치를 업데이트하여 자신의 [!DNL Target] 계정을 지정하게 됩니다.

먼저 Mobile Services 사용자 인터페이스에서 새 앱을 만듭니다.

1. Log in to the [Adobe Mobile Services interface](https://mobilemarketing.adobe.com).
1. 앱 [!UICONTROL 관리로]이동한 다음 **** 추가를&#x200B;**** 클릭하여 이 튜토리얼과 함께 사용할 새 앱을 추가합니다(앱 **[!UICONTROL 관리]**> 앱추가).
1. 비프로덕션 데이터가 포함된 Analytics 보고서 세트를 선택하고, 앱에 이름을 지정하고, **[!UICONTROL 표준]** 유형을 선택하고 **[!UICONTROL 저장을 클릭합니다]**.
1. SDK Target 옵션 [!DNL Target] 섹션의 다음 화면에 클라이언트 코드 [!UICONTROL 를 추가하고 나면] 클라이언트 코드를 SDK 옵션 [!DNL Target] 섹션 **[!UICONTROL 에 추가합니다. (클라이언트 코드를 인터페이스]** 에서 [설정] > [구현 ** > [구현] > []** ****`at.js` 구현] > [편집 설정]에서 찾을 수 있으며, 앱이 [다운로드] 단추 옆에 있습니다.)
1. 요청 [!UICONTROL 시간 초과] 설정은 앱이 시간 초과 명령을 실행하기 전에 [!DNL Target] 서버의 응답을 기다리는 시간을 결정합니다. 기본 설정은 그대로 두십시오.
1. 방문자 [!UICONTROL ID 서비스] 를 활성화하고 드롭다운에서 [!UICONTROL 조직] 을 선택해야 합니다.
1. 창 오른쪽 위에 있는 [ **[!UICONTROL 범용 링크]** ], [ [!UICONTROL 앱 링크]옵션] [!UICONTROL 또는 [푸시 서비스] ] 섹션을 클릭하여 변경 사항을  저장합니다.
1. 페이지 하단의 App SDK 다운로드 섹션으로 스크롤하고 구성 파일을 다운로드합니다.

   ![구성 파일 다운로드](assets/config_file.jpg)

1. Android Studio 프로젝트 에셋 폴더(앱 > src > 기본 > 에셋)의 `ADBMobileConfig.json` 파일을 교체합니다.

1. 이제 `ADBMobileConfig.json` 파일을 열고 클라이언트 코드 및 Analytics 세부 사항과 같은 예상 변경 사항이 [!DNL Target] 포함되어 있는지 확인합니다.
   ![구성 파일 다운로드](assets/client_code.jpg)

설정이 표시되지 않으면 **[!UICONTROL Mobile Services]** 인터페이스에서 올바른 [!UICONTROL 저장] 단추를 클릭한 후 파일을 올바른 위치에 복사했는지 확인하십시오.

축하합니다! 계정 세부 정보로 SDK를 업데이트했습니다! [!DNL Target] 다음 단원에서 요청을 추가한 후 구성에 대한 추가 유효성 검사를 [!DNL Target] 수행합니다.

**[다음: &quot;Target 요청 추가&quot; >](add-requests.md)**
