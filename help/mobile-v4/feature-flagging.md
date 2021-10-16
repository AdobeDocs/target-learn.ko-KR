---
title: 기능 플래그 지정
description: Adobe Target을 사용하여 색상, 복사, 단추, 텍스트 및 이미지와 같은 UX 기능을 실험하고 이러한 기능을 특정 대상에게 제공할 수 있습니다.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 034d13f2-63b1-44b0-b3dc-867efe37672f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 1%

---

# 기능 플래그 지정

모바일 앱 제품 소유자는 여러 앱 릴리스에 투자하지 않고도 앱에 새로운 기능을 배포할 수 있는 유연성을 필요로 합니다. 또한 효과를 테스트하기 위해 사용자 기반의 백분율로 기능을 점진적으로 롤아웃할 수도 있습니다. Adobe Target을 사용하여 색상, 복사, 단추, 텍스트 및 이미지와 같은 UX 기능을 실험하고 이러한 기능을 특정 대상에게 제공할 수 있습니다.

이 단원에서는 특정 앱 기능을 활성화하기 위한 트리거로 사용할 수 있는 &quot;기능 플래그&quot; 오퍼를 만듭니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 배치 미리 가져오기 요청에 새 위치 추가
* 기능 플래그로 사용될 오퍼를 사용하여 [!DNL Target] 활동을 만듭니다
* 앱에서 기능 플래그 오퍼를 로드하고 확인합니다

## Add a New Location to the Prefetch Request to the Home Activity

이전 단원의 데모 앱에서는 홈 활동의 프리페치 요청에 &quot;wetravel_feature_flag_recs&quot;라는 새 위치를 추가하고 새로운 Java 방법을 사용하여 화면에 로드합니다.

>[!NOTE]
>
>미리 가져오기 요청을 사용할 때의 이점 중 하나는 새 요청을 추가해도 추가적인 네트워크 오버헤드가 추가되지 않거나, 요청이 미리 가져오기 요청 내에 패키지화되어 추가 로드 작업이 수행된다는 것입니다

먼저 wetravel_feature_flag_recs 상수가 Constant.java 파일에 추가되었는지 확인합니다.

![Add feature flag constant](assets/feature_flag_constant.jpg)

다음은 코드입니다.

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

Now add the location to the prefetch request and load a new function called `processFeatureFlags()`:

![Feature Flag Code](assets/feature_flag_code.jpg)

다음은 전체 업데이트된 코드입니다.

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

코드가 추가되면 홈 활동에서 에뮬레이터를 실행하고 업데이트된 응답을 위해 Logcat을 시청합니다.

![기능 플래그 위치 유효성 검사](assets/feature_flag_code_logcat.jpg)

## 기능 플래그 JSON 오퍼 만들기

이제 앱에서 기능 롤아웃을 받을 대상, 특정 대상에 대한 플래그 또는 트리거로 역할을 하는 간단한 JSON 오퍼를 만듭니다. [!DNL Target] 인터페이스에서 새 오퍼를 만듭니다.

![기능 플래그 JSON 오퍼 만들기](assets/feature_flag_json_offer.jpg)

{&quot;enable&quot;:1} 값으로 &quot;Feature Flag v1&quot; 이름을 지정하겠습니다.

![feature_flag_v1 JSON 오퍼](assets/feature_flag_json_name.jpg)

## 활동 만들기

이제 해당 오퍼로 A/B 테스트 활동을 만들겠습니다. 활동을 만드는 자세한 단계는 이전 단원을 참조하십시오. 이 예제에서는 활동에 대상이 하나만 필요합니다. 라이브 시나리오에서는 특정 기능 롤아웃에 대해 특정 사용자 지정 대상을 작성 한 다음 해당 대상을 사용하도록 활동을 설정할 수 있습니다. 이 예에서는 기능 업데이트를 볼 수 있는 방문자에게 트래픽 50/50(50%, 표준 경험을 볼 수 있는 방문자에게는 50%)만 할당합니다. 다음은 활동에 대한 구성입니다.

1. 활동 이름을 &quot;기능 플래그&quot;로 지정합니다.
1. Select the &quot;wetravel_feature_flag_recs&quot; location
1. Change the content to the &quot;Feature Flag v1&quot; JSON offer

   ![Feature Flag Activity Config](assets/feature_flag_activity.jpg)

1. **[!UICONTROL 경험 추가]**&#x200B;를 클릭하여 경험 B를 추가합니다.
1. &quot;wetravel_feature_flag_recs&quot; 위치를 그대로 둡니다.
1. 컨텐츠의 경우 **[!UICONTROL 기본 컨텐츠]**&#x200B;를 그대로 둡니다.
1. **[!UICONTROL 다음]**&#x200B;을 클릭하여 [!UICONTROL 타깃팅] 화면으로 이동합니다.

   ![기능 플래그 활동 구성](assets/feature_flag_activity_2.jpg)

1. On the [!UICONTROL Targeting] screen, verify that the [!UICONTROL Traffic Allocation] method is set to the default setting (Manual) and that each experience has the default 50% allocation. **[!UICONTROL 다음]**&#x200B;목표 및 설정&#x200B;]**으로 이동하려면**[!UICONTROL &#x200B;을 선택합니다.

   ![기능 플래그 활동 구성](assets/feature_flag_activity_3.jpg)

1. **[!UICONTROL 기본 목표]**&#x200B;를 **[!UICONTROL 전환]**&#x200B;으로 설정합니다.
1. 작업을 **[!UICONTROL Viewed an Mbox]**&#x200B;로 설정합니다. We&#39;ll use the &quot;wetravel_context_dest&quot; location (since this location is on the Confirmation screen, we can use it to see if the new feature leads to more conversions).
1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭합니다.

   ![Feature Flag Activity Config](assets/feature_flag_activity_4.jpg)

활동 활성화.

## Validate the Feature Flag Activity

Now use the emulator to watch for the request. 타깃팅을 사용자의 50%로 설정했으므로 50%가 포함되므로 기능 플래그 응답에 `{enable:1}` 값이 포함됩니다.

![기능 플래그 유효성 검사](assets/feature_flag_validation.jpg)

`{enable:1}` 값이 표시되지 않으면 경험을 타깃팅하지 않은 것입니다. As a temporary test, to force the offer to show, you could:

1. 활동을 비활성화합니다.
1. 새 기능 경험에서 트래픽 할당을 100%로 변경합니다.
1. 저장하고 다시 활성화합니다.
1. 에뮬레이터에서 데이터를 지운 다음 앱을 다시 시작합니다.
1. The offer should now return the `{enable:1}` value.

라이브 시나리오에서 `{enable:1}` 응답을 사용하여 앱에서 더 많은 사용자 지정 논리를 활성화하여 타겟 대상을 표시할 특정 기능 세트를 표시할 수 있습니다.

## 결론

잘 했어요! 이제 특정 사용자 대상에게 기능을 롤아웃하는 데 필요한 기술을 보유하고 있습니다.
