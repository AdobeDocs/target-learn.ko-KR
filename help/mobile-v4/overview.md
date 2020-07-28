---
title: Android용 Adobe Mobile Services SDK v4를 사용한 Adobe Target
description: Android용 Adobe Mobile Services SDK v4를 사용한 Adobe Target은 이미 Adobe Mobile Services SDK v4를 사용하고 있고 Adobe Target으로 앱 경험을 개인화하고자 하는 Android 개발자에게 완벽한 시작점입니다.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 2%

---


# 개요

_Adobe Mobile Services SDK v4 for Android_ 를 사용하는 Adobe Target은 이미 Adobe Mobile Services SDK v4를 사용하고 있고 Adobe Target으로 앱 경험을 개인화하고자 하는 Android 개발자에게 완벽한 시작점입니다.

데모 Android 앱이 제공됩니다. 이 튜토리얼을 완료하고 나면 Android 앱에서 구현 [!DNL Target] 을 시작할 준비가 되었습니다.

이 자습서를 완료하면 다음 작업을 수행할 수 있습니다.

* Adobe [Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html) 설정 유효성 확인
* 다음 유형의 [!DNL Target] 요청을 구현합니다.
   * 컨텐츠 프리페치 [!DNL Target]
   * 단일 요청에 여러 [!DNL Target] 위치(mbox)를 일괄 처리
   * 요청 차단(앱 표시 전에 실행)
   * 비차단 요청(백그라운드에서 실행)
   * 실시간(비캐싱)
   * 캐시 수정
* 향상된 개인화를 위한 요청에 매개 변수 추가
* 대상 및 오퍼 만들기
* 레이아웃 개인화
* 기능 플래그 지정으로 새로운 기능 롤아웃

## 전제 조건

이 수업에서, 귀하는

* Adobe Target 인터페이스에 대한 Adobe ID와 승인자 수준의 액세스 권한이 있어야 합니다(아래 확인 단계 참조).
* 자신의 계정에 대한 요청을 할 수 있도록 Adobe Target 클라이언트 코드를 알고 있어야 합니다. 클라이언트 코드는 설정 > 구현 > Edit at.js 설정 화면의 Adobe Target 인터페이스에 표시됩니다
* Mobile [Services 사용자 인터페이스에 대한 액세스 권한 및 이해](https://mobilemarketing.adobe.com)
* Android 모바일 앱 개발을 위한 IDE를 보유합니다. 이 자습서에서는 [다양한 단계 및 스크린샷에 Android Studio](https://developer.android.com/studio/install) 기능을 제공합니다

Experience Cloud 솔루션에 대한 필수 액세스 권한이 없는 경우 Experience Cloud 관리자에게 문의하십시오.

또한 Java의 Android 개발에 익숙하다고 가정합니다. 이 과정을 이수하기 위해 Java 전문가가 될 필요는 없지만 코드를 쉽게 읽고 이해할 수 있다면 더 많은 이점을 얻을 수 있습니다.

### Adobe Target 액세스 확인

이 단원을 사용하려면 Adobe Target에 액세스해야 합니다. 다음 단계를 진행하기 전에 다음을 수행하여 Adobe Target에 액세스할 수 있는지 확인합니다.

1. Adobe Experience Cloud에 [로그인](https://experience.adobe.com/)
1. From the Experience Cloud home screen, click [!DNL Target]:
   ![Experience Cloud 홈 화면](assets/aec_homeScreen_clickTarget.png)
1. 아래에 나와 있는 것처럼 Adobe Target의 활동 목록으로 이동하여 사용자에게 승인자 수준 액세스 권한이 있음을 확인해야 합니다. 승인자 수준 액세스 권한 [!DNL Target] 에 액세스할 수 없거나 이를 확인할 수 없는 경우 회사의 Experience Cloud 관리자에게 문의하고 이 액세스 권한을 요청하고 이 튜토리얼이 부여된 경우 다시 시작하십시오.

   ![Adobe UI](assets/targetUI_approver.png)

## 학습 정보

이 수업에서는 Adobe Target 계정을 사용하여 &quot;We.Travel&quot;이라는 데모 여행 앱에 Adobe Target을 구현할 것입니다. 튜토리얼이 종료될 때까지 사용자는 앱 사용에 따라 개인화된 메시지를 전달하게 됩니다. 최종 개인화 경험은 다음과 같습니다.

![We.Travel app final](assets/overview_final_result.jpg)

We.Travel 앱 내에서 구현 과정을 거친 후 모바일 앱 [!DNL Target] 에서 사용을 시작할 수 있습니다.

그럼 시작해 보겠습니다!

**[다음: &quot;샘플 앱 다운로드 및 업데이트&quot; >](download-and-update-the-sample-app.md)**
