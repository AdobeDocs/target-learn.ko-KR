---
title: Android용 Adobe Mobile Services SDK v4가 포함된 Adobe Target
description: Android용 Adobe Mobile Services SDK v4가 포함된 Adobe Target은 이미 Adobe Mobile Services SDK v4를 사용하고 있고 Adobe Target에서 앱 환경을 개인화하려는 Android 개발자에게 완벽한 시작점입니다.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile, Overview
doc-type: tutorial
kt: 3040
exl-id: 20f8ed4f-a86d-4c5e-9296-71a93724caa3
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# Android용 Adobe Mobile Services SDK v4가 포함된 Adobe Target - 개요

_Android용 Adobe Mobile Services SDK v4가 포함된 Adobe Target_&#x200B;은(는) 이미 Adobe Mobile Services SDK v4를 사용하고 있고 Adobe Target에서 앱 환경을 개인화하려는 Android 개발자에게 완벽한 시작점입니다.

데모 Android 앱이 제공되므로 학습 내용을 완료하십시오. 이 자습서를 완료하고 나면 Android 앱에서 [!DNL Target] 구현을 시작할 수 있습니다.

이 자습서를 완료하면 다음 작업을 수행할 수 있습니다.

* [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en) 설정의 유효성 검사
* 다음 유형의 [!DNL Target] 요청을 구현합니다.
   * [!DNL Target]개 콘텐츠 미리 가져오기
   * 단일 요청에 여러 [!DNL Target]개 위치(mbox)를 일괄 처리
   * 요청 차단(앱 표시 전 실행)
   * 비차단 요청(백그라운드에서 실행)
   * 실시간(비캐싱)
   * 캐시 무효화 다시 가져오기
* 향상된 개인화를 위해 요청에 매개 변수 추가
* 대상자 및 오퍼 만들기
* 레이아웃 개인화
* 기능 플래깅으로 새로운 기능 롤아웃

## 전제 조건

이 단원에서 다음을 수행하는 것으로 가정합니다.

* Adobe Target 인터페이스에 대한 Adobe ID 및 승인자 수준 액세스 권한이 있습니다(아래 확인 단계 참조)
* 자신의 계정에 요청할 수 있도록 Adobe Target 클라이언트 코드를 알고 있습니다. 클라이언트 코드는 의 Adobe Target 인터페이스에 표시됩니다.   설정 > 구현 > at.js 설정 편집 화면
* [Mobile Services 사용자 인터페이스](https://mobilemarketing.adobe.com/)에 대한 액세스 권한이 있고 이에 익숙합니다.
* Android 모바일 앱 개발을 위한 IDE가 있습니다. 이 튜토리얼은 다양한 단계 및 스크린샷에서 [Android Studio](https://developer.android.com/studio/install)를 제공합니다.

Experience Cloud 솔루션에 대한 필수 액세스 권한이 없는 경우 Experience Cloud 관리자에게 문의하십시오.

또한 사용자가 Java의 Android 개발에 익숙하다고 가정합니다. Java 전문가가 아니어도 단원을 완료할 수 있지만, 코드를 읽고 이해할 수 있으면 단원을 최대한 활용할 수 있습니다.

### Adobe Target 액세스 확인

이 단원에서는 Adobe Target에 액세스해야 합니다. 다음 단계로 이동하기 전에 다음을 수행하여 Adobe Target에 액세스할 수 있는지 확인하십시오.

1. [Adobe Experience Cloud](https://experience.adobe.com/)에 로그인
1. Experience Cloud 홈 화면에서 [!DNL Target]:
   ![Experience Cloud 홈 화면](assets/aec_homeScreen_clickTarget.png)
1. 아래 그림과 같이 Adobe Target의 활동 목록에 도달하면 사용자에게 승인자 수준 액세스 권한이 있는지 확인해야 합니다. [!DNL Target]에 액세스할 수 없거나 승인자 수준 액세스 권한을 확인할 수 없는 경우 회사의 Experience Cloud 관리자 중 한 명에게 연락하여 이 액세스 권한을 요청하고 이 자습서가 승인되면 다시 시작하십시오.

   ![Adobe UI](assets/targetUI_approver.png)

## 단원 정보

이 단원들에서는 Adobe Target 계정을 사용하여 &quot;We.Travel&quot;이라는 데모 여행 앱에 Adobe Target을 구현하게 됩니다. 자습서가 종료되면 앱 사용에 따라 개인화된 메시지를 사용자에게 전달할 수 있습니다. 최종 개인화 경험은 다음과 같이 표시됩니다.

![We.Travel 앱 최종](assets/overview_final_result.jpg)

We.Travel 앱 내에서 구현 과정을 거치고 나면 자신의 모바일 앱에서 [!DNL Target]을(를) 사용할 수 있습니다.

시작해 보겠습니다!

**[다음 : &quot;샘플 앱 다운로드 및 업데이트&quot; >](download-and-update-the-sample-app.md)**
