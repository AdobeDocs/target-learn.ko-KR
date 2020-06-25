---
title: 기능 플래그 지정
seo-title: 기능 플래그 지정
description: Adobe Target을 사용하여 색상, 복사, 버튼, 텍스트 및 이미지와 같은 UX 기능을 테스트하고 특정 사용자에게 이러한 기능을 제공할 수 있습니다.
seo-description: Adobe Target을 사용하여 색상, 복사, 버튼, 텍스트 및 이미지와 같은 UX 기능을 테스트하고 특정 사용자에게 이러한 기능을 제공할 수 있습니다.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---


# 기능 플래그 지정

모바일 앱 제품 사용자는 여러 앱 릴리스에 투자하지 않고도 앱에 새로운 기능을 선보일 수 있는 유연성이 필요합니다. 효과를 테스트하기 위해 사용자 기준의 백분율로 점진적으로 기능을 롤아웃할 수도 있습니다. Adobe Target을 사용하여 색상, 복사, 버튼, 텍스트 및 이미지와 같은 UX 기능을 테스트하고 특정 사용자에게 이러한 기능을 제공할 수 있습니다.

이 단원에서 &quot;기능 플래그&quot; 오퍼를 만들어 특정 앱 기능을 활성화할 수 있습니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 일괄 프리페치 요청에 새 위치 추가
* 기능 플래그로 사용할 오퍼를 사용하여 [!DNL Target] 활동 만들기
* 앱에서 기능 플래그 오퍼 로드 및 유효성 검사

## 홈 활동에 프리페치 요청에 새 위치 추가

이전 학습의 데모 앱에서 &quot;wetravel_feature_flag_recs&quot;라는 새 위치를 홈 활동의 프리페치 요청에 추가하고 새로운 Java 방법을 사용하여 화면에 로드합니다.

>[!NOTE] 프리페치 요청을 사용할 때의 이점 중 하나는 새 요청을 추가해도 네트워크 오버헤드가 추가로 추가되지 않거나 요청이 프리페치 요청 내에 패키지되어 추가 로드 작업이 발생하지 않는다는 것입니다

먼저 wetravel_feature_flag_recs 상수가 Constant.java 파일에 추가되었는지 확인합니다.

![기능 플래그 상수 추가](assets/feature_flag_constant.jpg)

코드는 다음과 같습니다.

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

이제 프리페치 요청에 위치를 추가하고 다음과 같은 새 함수를 로드합니다. `processFeatureFlags()`

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

### 기능 플래그 요청 유효성 확인

코드가 추가되면 홈 활동에서 에뮬레이터를 실행하고 Logcat에서 업데이트된 응답을 확인하십시오.

![기능 플래그 위치 확인](assets/feature_flag_code_logcat.jpg)

## 기능 플래그 JSON 오퍼 만들기

이제 깃발 또는 트리거로 작동하는 간단한 JSON 오퍼를 만들어 앱에서 기능 롤아웃을 받을 수 있는 대상자와 같은 특정 고객을 대상으로 합니다. 인터페이스에서 새 오퍼를 [!DNL Target] 만듭니다.

![기능 플래그 JSON 오퍼 만들기](assets/feature_flag_json_offer.jpg)

{&quot;enable&quot;:1} 값으로 &quot;Feature Flag v1&quot; 이름을 지정하자

![feature_flag_v1 JSON 오퍼](assets/feature_flag_json_name.jpg)

## 활동 만들기

이제 해당 오퍼와 함께 A/B 테스트 활동을 만듭니다. 활동을 만드는 방법에 대한 자세한 내용은 이전 단원을 참조하십시오. 활동에는 이 예제의 대상이 하나만 필요합니다. 라이브 시나리오에서 특정 기능 롤아웃에 대한 특정 사용자 지정 대상을 만든 다음 해당 대상을 사용하도록 활동을 설정할 수 있습니다. 이 예에서는 기능 업데이트를 보게 될 방문자에게 트래픽 50/50(50%, 표준 경험을 보게 될 방문자에게 50%)을 할당하기만 하면 됩니다. 다음은 활동에 대한 구성입니다.

1. 활동 이름 지정 &quot;기능 플래그&quot;
1. &quot;wetravel_feature_flag_recs&quot; 위치를 선택합니다.
1. 컨텐츠를 &quot;기능 플래그 v1&quot; JSON 오퍼로 변경

   ![기능 플래그 활동 구성](assets/feature_flag_activity.jpg)

1. 경험 **[!UICONTROL 추가를]** 클릭하여 경험 B를 추가합니다.
1. &quot;wetravel_feature_flag_recs&quot; 위치 유지
1. 컨텐츠의 **[!UICONTROL 기본 컨텐츠]** 유지
1. Click **[!UICONTROL Next]** to advance to the [!UICONTROL Targeting] screen

   ![기능 플래그 활동 구성](assets/feature_flag_activity_2.jpg)

1. 타깃팅  화면에서 [!UICONTROL 트래픽 할당] 방법이 기본 설정(수동)으로 설정되어 있고 각 경험에 기본 50% 할당이 있는지 확인합니다. 다음 **[!UICONTROL 을]** 선택하여 **[!UICONTROL 목표 및 설정으로]**&#x200B;진행합니다.

   ![기능 플래그 활동 구성](assets/feature_flag_activity_3.jpg)

1. 기본 **[!UICONTROL 목표를]** 전환으로 **[!UICONTROL 설정합니다]**.
1. 작업을 Mbox를 **[!UICONTROL 조회하도록 설정합니다]**. &quot;wetravel_context_dest&quot; 위치를 사용합니다(이 위치가 확인 화면에 있으므로 새 기능으로 인해 더 많은 전환이 발생하는지 여부를 확인할 수 있습니다).
1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭합니다.

   ![기능 플래그 활동 구성](assets/feature_flag_activity_4.jpg)

활동 활성화.

## 기능 플래그 활동 유효성 확인

이제 에뮬레이터를 사용하여 요청을 확인합니다. 타깃팅을 사용자의 50%로 설정했으므로 50%가 기능 플래그 응답에 `{enable:1}` 값이 포함됩니다.

![기능 플래그 유효성 검사](assets/feature_flag_validation.jpg)

값이 표시되지 않으면 경험에 대한 타깃팅이 되지 않았음을 의미합니다. `{enable:1}` 임시 테스트로서 오퍼를 강제로 표시하려면 다음을 수행할 수 있습니다.

1. 활동을 비활성화합니다.
1. 새로운 기능 경험에서 트래픽 할당을 100%로 변경합니다.
1. 저장 및 다시 활성화합니다.
1. 에뮬레이터의 데이터를 지운 다음 앱을 다시 시작합니다.
1. 이제 오퍼가 `{enable:1}` 값을 반환해야 합니다.

라이브 시나리오에서 이 응답을 사용하여 앱에 더 많은 사용자 정의 논리를 활성화하여 타겟 고객을 표시할 특정 기능 세트를 표시할 수 있습니다. `{enable:1}`

## 결론

잘했어! 이제 특정 사용자 사용자에게 기능을 롤아웃하는 데 필요한 기술이 제공됩니다.