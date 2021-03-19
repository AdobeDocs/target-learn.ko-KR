---
title: 레이아웃 개인화
description: '이 마지막 수업에서는 고객을 위한 Target에서 2개의 개인화 활동을 만듭니다. 앱에서 활동을 로드하고 표시하고 콘텐츠가 올바른 위치에 적시에 표시되는지 확인하는 방법을 알아봅니다.  '
role: Developer
level: 중간
topic: 모바일, 개인화
feature: 모바일 구현
doc-type: tutorial
kt: 3040
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 1%

---


# 레이아웃 개인화

이제 모든 것을 통합하여 개인화된 경험을 제작해야 합니다. _활동_&#x200B;은 위치, 대상 및 오퍼를 함께 연결하는 [!DNL Target] 메커니즘으로, 앱에서 요청이 수행된 경우 [!DNL Target]가 개인화된 컨텐츠와 응답합니다. [!DNL Target]에서 2개의 개인화 활동을 작성하고 개인화된 컨텐츠가 적시에 올바른 사용자에게 표시되는지 확인할 것입니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* Adobe Target에서 활동 만들기
* 샘플 앱의 활동 유효성 검사

## Adobe Target에서 활동 만들기

사용자 참여 및 컨텍스트 기반 오퍼 활동을 만드는 방법을 알아봅니다.

### 첫 번째 활동 - &quot;사용자 참여&quot;

다음은 Adobe에서 구축할 활동에 대한 요약입니다.

| 대상자 | 위치 | 오퍼 |
|---|---|---|
| 새 모바일 앱 사용자 | wetravel_engage_home, wetravel_engage_search | 홈:새 사용자 참여, 검색:새 사용자 참여 |
| 재방문 모바일 앱 사용자 | wetravel_engage_home, wetravel_engage_search | 홈:돌아온 사용자, default_content |

[!DNL Target] 인터페이스에서 다음을 수행합니다.

1. **[!UICONTROL 활동]** > **[!UICONTROL 활동 만들기]** > **[!UICONTROL 경험 타깃팅]**&#x200B;을 선택합니다.

   ![활동 만들기](assets/activity_create_1.jpg)

1. **[!UICONTROL 모바일 앱]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 양식 작성기]**&#x200B;를 선택합니다.
1. 작업 영역(이전 수업에서 사용한 작업 영역)을 선택합니다.
1. 속성(이전 수업에서 사용한 것과 동일한 속성)을 선택합니다.
1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   ![활동 만들기](assets/activity_create_2.jpg)

1. 활동 제목을 **[!UICONTROL 사용자 참여]**&#x200B;로 변경합니다.
1. **[!UICONTROL 줄임표]** > **[!UICONTROL 대상자 변경]**을 선택합니다.
   ![신규 모바일 앱 사용자가 대상 변경](assets/activity_create_3.jpg)
1. 대상을 **[!UICONTROL 새 모바일 앱 사용자]**&#x200B;로 설정합니다.
1. **[!UICONTROL 완료를 클릭합니다]**.
   ![신규 모바일 앱 사용자 대상](assets/activity_create_4.jpg)

1. 위치를 _wetrevel_engage_home_&#x200B;으로 변경합니다.
1. 기본 컨텐츠 옆에 있는 드롭다운 화살표를 선택하고 **[!UICONTROL HTML 오퍼 변경]**&#x200B;을 선택합니다.

   ![신규 모바일 앱 사용자 대상](assets/activity_create_5.jpg)

1. **[!UICONTROL 홈:새 사용자]** 오퍼에 참여합니다.
1. **[!UICONTROL 완료]**&#x200B;를 선택합니다.

   ![신규 모바일 앱 사용자 대상](assets/activity_create_6.jpg)

1. **[!UICONTROL 위치 추가]**를 선택합니다.
   ![신규 모바일 앱 사용자 대상](assets/activity_create_7.jpg)

1. _wetrevel_engage_search_ 위치를 선택합니다.
1. HTML 오퍼를 변경합니다.

   ![신규 모바일 앱 사용자 대상](assets/activity_create_8.jpg)

1. **[!UICONTROL 검색:새 사용자]** 오퍼에 참여합니다.
1. **[!UICONTROL 완료를 클릭합니다]**.

   ![신규 모바일 앱 사용자 대상](assets/activity_create_9.jpg)

고객을 위치 및 오퍼에 연결함으로써 새로운 모바일 앱 사용자를 위한 개인화된 경험을 제작할 수 있습니다. 이제 경험이 다음과 같아야 합니다.

![최종 경험](assets/activity_engage_users_a_final.jpg)

이제 돌아온 모바일 앱 사용자를 위한 경험을 만듭니다.

1. 왼쪽에서 **[!UICONTROL 경험 타깃팅 추가]**&#x200B;를 선택합니다.
1. 대상 **[!UICONTROL 재계약 모바일 앱 사용자]**&#x200B;를 선택합니다.
1. **[!UICONTROL 완료]**를 선택합니다.
   ![재방문 모바일 앱 사용자 대상](assets/activity_create_11.jpg)

이제 이전에 새 경험을 구성하는 데 사용한 동일한 프로세스를 사용하십시오. 돌아온 모바일 앱 사용자 경험에 대한 구성은 다음과 같아야 합니다.

![최종 모바일 앱 사용자 반환](assets/activity_engage_users_b_final.jpg)

설정의 다음 화면으로 계속하겠습니다.

1. **[!UICONTROL 다음]**&#x200B;을 클릭하여 **[!UICONTROL 타게팅]** 화면으로 이동합니다.
1. 타깃팅을 위한 기본 설정을 사용합니다. 겹치는 대상(예:_New York 사용자_ 및 _첫 번째 사용자_)는 이 화면에서 우선 순위 순서를 정렬할 수 있습니다.
1. **[!UICONTROL 다음]**&#x200B;을 클릭하여 **[!UICONTROL 목표 및 설정]**&#x200B;으로 이동합니다.

   ![사용자 활동 참여 - 타깃팅 기본값](assets/activity_engage_users_targeting.jpg)

이제 활동 설정을 완료하겠습니다.

1. **[!UICONTROL 기본 목표]**&#x200B;를 **[!UICONTROL 전환]**&#x200B;으로 설정합니다.
1. 작업을 **[!UICONTROL mbox]** > _wetravel_context_dest_&#x200B;로 설정합니다(이 위치는 확인 화면에 있으므로 이 위치를 사용하여 전환을 측정할 수 있습니다).

   ![사용자 활동 참여 - 목표](assets/activity_create_12.jpg)

1. 화면의 다른 모든 설정은 기본값으로 유지합니다.
1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭하여 활동을 저장합니다.
1. 다음 화면에서 **[!UICONTROL 활동]**&#x200B;을 활성화합니다.

![경험 B 대상](assets/activity_create_13.jpg)

우리의 첫 번째 활동은 이제 라이브이며 테스트할 준비가 되었습니다!

### 두 번째 활동 - &quot;상황에 맞는 제안&quot;

다음은 Adobe에서 빌드할 두 번째 활동에 대한 요약입니다.

| 대상자 | 위치 | 오퍼 |
| --- | --- | --- |
| 대상:샌디에이고 | wetravel_context_dest | 샌디에이고 프로모션 |
| 대상:로스앤젤레스 | wetravel_context_dest | 로스앤젤레스 홍보 |

다음 활동 - &quot;상황에 맞는 오퍼&quot;에 대해 위와 동일한 프로세스를 반복합니다. 두 경험에 대한 최종 구성은 아래와 같습니다.

#### 샌디에이고

![컨텍스트 기반의 제안 - 경험 A](assets/activity_contextual_a_final.jpg)

#### 로스앤젤레스

![컨텍스트 기반의 제안 - 경험 B](assets/activity_contextual_b_final.jpg)

목표 및 설정 단계에서 기본 목표를 예약 확인 화면의 위치로 변경합니다.

1. **[!UICONTROL 보고 설정]**&#x200B;에서 **[!UICONTROL 기본 목표]**&#x200B;를 **[!UICONTROL 전환]**&#x200B;으로 설정합니다.
1. 작업을 **[!UICONTROL mbox]** > _wetravel_context_dest_&#x200B;로 설정합니다(이 활동에서는 경험을 전달하는 동일한 위치이기도 하므로 이 지표가 기본적으로 의미가 없습니다.)
1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭합니다.

![컨텍스트 기반의 제안 - 경험](assets/activity_create_14.jpg)

다음 화면에서 활동을 활성화합니다.

이제 두 번째 활동이 라이브이며 테스트할 준비가 되었습니다!

## 홈 오퍼 유효성 확인

에뮬레이터를 실행하고 홈 화면 하단에 표시할 첫 번째 오퍼를 확인합니다. 앱 실행 횟수가 5회 이상인 재방문 사용자는 _다시 시작_ 오퍼가 표시됩니다. 새 사용자(앱 시작 횟수가 5회 미만인 경우)는 _새 사용자_ 메시지가 표시됩니다.

![홈 오퍼 유효성 확인](assets/layout_home_validate.jpg)

새 사용자 오퍼가 표시되지 않으면 에뮬레이터에 대한 데이터를 지우십시오. 그러면 다음에 앱을 실행할 때 앱 시작이 1로 재설정됩니다. 이 작업은 **[!UICONTROL 도구]** > **[!UICONTROL AVD 관리자]**&#x200B;에서 수행됩니다. Logcat이 제대로 작동하지 않는 경우 Android Studio를 다시 시작해야 할 수도 있습니다.

![에뮬레이터 지우기](assets/layout_home_validate_avd_wipe.jpg)

_wetravel_engage_home_&#x200B;을 필터링하여 Logcat에서 응답의 유효성을 검사할 수도 있습니다.

![홈 오퍼 유효성 확인 - Logcat](assets/layout_home_validate_logcat.jpg)

## 검색 오퍼 유효성 확인

**[!UICONTROL 대상]**&#x200B;으로 **[!UICONTROL 산호세]** 및 **[!UICONTROL 샌디에이고]**&#x200B;를 선택하고 **[!UICONTROL 대상]**&#x200B;버스 찾기&#x200B;]**를 클릭하여 사용 가능한 버스를 검색합니다.**[!UICONTROL 

결과 화면에서 _필터 사용_ 메시지가 표시됩니다. 앱 실행 횟수가 5회 이상인 돌아온 사용자는 이 위치에 대한 기본 컨텐츠가 설정되어 있기 때문에(비어 있음) 메시지가 표시되지 않습니다.

![검색 오퍼 유효성 확인](assets/layout_search_validate.jpg)

## 감사 화면에서 컨텍스트 오퍼 유효성 확인

이제 예약 프로세스를 계속합니다.

* 결과 화면에서 버스를 선택합니다.
* 체크아웃 화면에서 시트를 선택합니다.
* 결제 화면에서 **[!UICONTROL 신용 카드]**&#x200B;를 선택합니다(결제 정보는 비워 두십시오. 실제 예약은 이루어지지 않습니다).

샌디에고가 대상으로 선택되었으므로 확인 화면에 _DJ SAM_ 오퍼 배너가 표시됩니다.

![컨텍스트 오퍼 유효성 확인 - 샌디에이고](assets/layout_context_san_diego.jpg)

이제 **[!UICONTROL 완료]**&#x200B;를 선택하고 Los Angeles를 대상으로 다른 예약을 시도하십시오. 확인 화면에 _Universal Studios_ 배너가 표시되어야 합니다.

![컨텍스트 오퍼 유효성 확인 - 로스앤젤레스](assets/layout_context_los_angeles.jpg)

## 결론

축하합니다! Android용 Adobe Target SDK 4.x의 주요 부분을 설명합니다. 이제 Android 앱에서 개인화를 구현할 수 있는 역량을 갖추게 되었습니다. 이 설명서 및 데모 앱을 참조하여 향후 프로젝트를 참조할 수 있습니다.

다음:기능 플래그 지정은 Android의 Adobe Target에서 구현할 수 있는 또 다른 기능입니다. 기능 플래그를 살펴보려면 다음 단원을 참조하십시오.

**[다음:기능 플래그 지정 >](feature-flagging.md)**
