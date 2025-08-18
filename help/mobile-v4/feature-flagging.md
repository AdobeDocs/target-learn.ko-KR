---
title: 기능 플래그 지정
description: Adobe Target을 사용하여 색상, 복사, 단추, 텍스트 및 이미지와 같은 UX 기능을 실험하고 특정 대상에게 제공할 수 있습니다.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 034d13f2-63b1-44b0-b3dc-867efe37672f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# 기능 플래그 지정

모바일 앱 제품 소유자는 여러 앱 릴리스에 투자할 필요 없이 앱에 새로운 기능을 구축할 수 있는 유연성이 필요합니다. 효과를 테스트하기 위해 기능을 사용자 기준의 백분율로 점진적으로 롤아웃하려는 경우도 있습니다. Adobe Target을 사용하여 색상, 복사, 단추, 텍스트 및 이미지와 같은 UX 기능을 실험하고 특정 대상에게 제공할 수 있습니다.

이 단원에서는 특정 앱 기능을 활성화하는 트리거로 사용할 수 있는 &quot;기능 플래그&quot; 오퍼를 만듭니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 배치 미리 가져오기 요청에 새 위치 추가
* 기능 플래그로 사용할 오퍼를 사용하여 [!DNL Target] 활동 만들기
* 앱에서 기능 플래그 오퍼 로드 및 유효성 검사

## 홈 활동에 미리 가져오기 요청에 새 위치 추가

이전 단원의 데모 앱에서는 &quot;wetravel_feature_flag_recs&quot;라는 새 위치를 홈 활동의 미리 가져오기 요청에 추가하고 새로운 Java 메서드를 사용하여 화면에 로드합니다.

>[!NOTE]
>
>미리 가져오기 요청을 사용할 때 얻을 수 있는 이점 중 하나는 새 요청을 추가하면 네트워크 오버헤드가 추가되지 않거나 요청이 미리 가져오기 요청에 패키지화되어 추가 로드 작업이 발생한다는 것입니다

먼저 Constant.java 파일에 wetravel_feature_flag_recs 상수가 추가되었는지 확인합니다.

![기능 플래그 상수 추가](assets/feature_flag_constant.jpg)

코드는 다음과 같습니다.

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

이제 프리페치 요청에 위치를 추가하고 `processFeatureFlags()`(이)라는 새 함수를 로드합니다.

![기능 플래그 코드](assets/feature_flag_code.jpg)

다음은 전체 업데이트 코드입니다.

```java
public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();

    Map<String, Object> params1;
    params1 = new HashMap<String, Object>();
    params1.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");

    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_feature_flag_recs, params1));

    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    engageMessage();
                    processFeatureFlags();
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}

public void processFeatureFlags() {
    Target.loadRequest(Constant.wetravel_feature_flag_recs, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Feature Flags : " + s);
                            if(s != null && !s.isEmpty()) {
                                //enable or disable features
                            }
                        }
                    });
                }
            });
}
```

### 기능 플래그 요청의 유효성 검사

코드가 추가되면 홈 활동에서 에뮬레이터를 실행하고 Logcat에서 업데이트된 응답을 확인합니다.

![기능 플래그 위치 확인](assets/feature_flag_code_logcat.jpg)

## 기능 플래그 JSON 오퍼 만들기

이제 특정 대상(앱에서 기능 롤아웃을 수신할 대상)에 대한 플래그 또는 트리거로 작동하는 간단한 JSON 오퍼를 만듭니다. [!DNL Target] 인터페이스에서 새 오퍼를 만듭니다.

![기능 플래그 JSON 오퍼 만들기](assets/feature_flag_json_offer.jpg)

이름을 {&quot;enable&quot;:1} 값으로 &quot;기능 플래그 v1&quot;로 지정하겠습니다.

![feature_flag_v1 JSON 오퍼](assets/feature_flag_json_name.jpg)

## 활동 만들기

이제 해당 오퍼를 사용하여 A/B 테스트 활동을 만들겠습니다. 활동 만들기에 대한 자세한 단계는 이전 단원을 참조하십시오. 활동에는 이 예제에 대해 한 명의 대상자만 필요합니다. 라이브 시나리오에서는 특정 기능 롤아웃에 대한 특정 사용자 지정 대상을 작성한 다음, 해당 대상을 사용하도록 활동을 설정할 수 있습니다. 이 예제에서는 트래픽을 50/50(기능 업데이트를 보게 되는 방문자에게는 50%, 표준 경험을 보게 되는 방문자에게는 50%)만 할당하겠습니다. 다음은 활동에 대한 구성입니다.

1. 활동의 이름을 &quot;기능 플래그&quot;로 지정합니다.
1. &quot;wetravel_feature_flag_recs&quot; 위치 선택
1. 콘텐츠를 &quot;기능 플래그 v1&quot; JSON 오퍼로 변경

   ![기능 플래그 활동 구성](assets/feature_flag_activity.jpg)

1. 경험 B를 추가하려면 **[!UICONTROL Add Experience]**&#x200B;을(를) 클릭하십시오.
1. &quot;wetravel_feature_flag_recs&quot; 위치를 그대로 둡니다.
1. 콘텐츠에 대해 **[!UICONTROL Default Content]** 남기기
1. **[!UICONTROL Next]** 화면으로 이동하려면 [!UICONTROL Targeting]을(를) 클릭하십시오.

   ![기능 플래그 활동 구성](assets/feature_flag_activity_2.jpg)

1. [!UICONTROL Targeting] 화면에서 [!UICONTROL Traffic Allocation] 메서드가 기본 설정(수동)으로 설정되어 있고 각 경험에 기본 50% 할당이 있는지 확인합니다. **[!UICONTROL Next]**(으)로 이동하려면 **[!UICONTROL Goals & Settings]**&#x200B;을(를) 선택하십시오.

   ![기능 플래그 활동 구성](assets/feature_flag_activity_3.jpg)

1. **[!UICONTROL Primary Goal]**&#x200B;을(를) **[!UICONTROL Conversion]**(으)로 설정합니다.
1. 작업을 **[!UICONTROL Viewed an Mbox]**(으)로 설정합니다. &quot;wetravel_context_dest&quot; 위치를 사용합니다(이 위치는 확인 화면에 있으므로 새 기능이 더 많은 전환으로 이어지는지 확인하는 데 사용할 수 있습니다).
1. **[!UICONTROL Save & Close]** 아이콘을 클릭합니다.

   ![기능 플래그 활동 구성](assets/feature_flag_activity_4.jpg)

활동을 활성화합니다.

## 기능 플래그 활동 유효성 검사

이제 에뮬레이터를 사용하여 요청을 확인합니다. 타깃팅을 사용자의 50%로 설정했으므로 50%의 경우 기능 플래그 응답에 `{enable:1}` 값이 포함됩니다.

![기능 플래그 유효성 검사](assets/feature_flag_validation.jpg)

`{enable:1}` 값이 표시되지 않으면 해당 경험에 대한 타깃팅이 되지 않은 것입니다. 임시 테스트로서 오퍼를 강제로 표시하기 위해 다음을 수행할 수 있습니다.

1. 활동을 비활성화합니다.
1. 새 기능 경험에서 트래픽 할당을 100%로 변경합니다.
1. 저장하고 다시 활성화합니다.
1. 에뮬레이터에서 데이터를 지운 다음 앱을 다시 시작합니다.
1. 이제 오퍼가 `{enable:1}` 값을 반환합니다.

라이브 시나리오에서는 `{enable:1}` 응답을 사용하여 앱에서 더 많은 사용자 지정 논리를 활성화하여 대상 대상자를 표시할 특정 기능 집합을 표시할 수 있습니다.

## 결론

수고하셨습니다! 이제 특정 사용자 대상에게 기능을 롤아웃하는 데 필요한 기술을 갖추게 되었습니다.
