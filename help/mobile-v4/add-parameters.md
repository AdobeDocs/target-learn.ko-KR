---
title: 요청에 매개 변수 추가
description: 이 단원에서는 이전 단원에서 추가한 Target 요청에 Adobe 라이프사이클 지표와 사용자 지정 매개 변수를 추가합니다. 이러한 지표 및 매개 변수는 튜토리얼의 후반부에 개인화된 고객을 만드는 데 사용됩니다.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: 199fbde58696a0511623c5500cc6afbbcfdd67a3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# 요청에 매개 변수 추가

이 단원에서 Adobe 라이프사이클 지표와 사용자 지정 매개 변수를 이전 단원에서 추가한 [!DNL Target] 요청에 추가합니다. 이러한 지표 및 매개 변수는 튜토리얼의 후반부에 개인화된 고객을 만드는 데 사용됩니다.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* Adobe 모바일 라이프사이클 지표 추가
* 프리페치 요청에 매개 변수 추가
* 라이브 위치에 매개 변수 추가
* 두 요청에 대한 매개 변수 유효성 검사

## 라이프사이클 매개 변수 추가

이제 [Adobe 모바일 라이프사이클 지표를 활성화하겠습니다](https://docs.adobe.com/content/help/en/mobile-services/android/metrics.html). 이렇게 하면 사용자의 장치 및 앱과의 참여에 대한 풍부한 정보가 포함된 매개 변수가 위치 요청에 추가됩니다. 라이프사이클 요청이 제공하는 데이터를 사용하여 다음 단원에서 고객을 구성합니다.

라이프사이클 지표를 활성화하려면 HomeActivity 컨트롤러를 다시 열고 onResume() 함수 `Config.collectLifecycleData(this);` 에 추가합니다.

![라이프사이클 요청](assets/lifecycle_code.jpg)

### 프리페치 요청에 대한 라이프사이클 매개 변수 유효성 확인

에뮬레이터를 실행하고 Logcat을 사용하여 라이프사이클 매개 변수의 유효성을 확인합니다. &quot;프리페치&quot;를 필터링하여 프리페치 응답을 찾고 새 매개 변수를 찾습니다.
![라이프사이클 유효성 검사](assets/lifecycle_validation.jpg)

HomeActivity 컨트롤러 `Config.collectLifecycleData()` 에만 추가되었지만 감사 화면 상의 Target 요청과 함께 전송된 라이프사이클 지표도 볼 수 있습니다.

## at_property 매개 변수를 프리페치 요청에 추가

Adobe Target 속성은 인터페이스에서 정의되며 앱 및 웹 사이트를 개인화하기 위한 경계를 설정하는 데 사용됩니다. [!DNL Target] at_property 매개 변수는 오퍼와 활동이 액세스 및 유지되는 특정 속성을 식별합니다. 프리페치 및 라이브 위치 요청에 속성을 추가합니다.

>[!NOTE]
>
>라이센스에 따라 인터페이스에 속성 옵션이 표시되거나 표시되지 않을 수 있습니다. [!DNL Target] 이러한 옵션이 없거나 회사에서 [속성]을 사용하지 않는 경우 이 단원의 다음 섹션으로 건너뛸 수 있습니다.

설정 > 속성 아래의 [!DNL Target] 인터페이스에서 [!UICONTROL at_property 값을 검색할 수] 있습니다 .  속성 위에 마우스를 놓고 코드 조각 아이콘을 선택하고 값을 `at_property` 복사합니다.

![복사 위치(_Property)](assets/at_property_interface.jpg)

다음과 같이 프리페치 요청의 각 위치에 대한 매개 변수로 추가합니다.
![at_property 매개 변수](assets/params_at_property.jpg)여기에 함수 `targetPrefetchContent()` 에 대한 업데이트된 코드가 있습니다(at_property 값을 업데이트하려면 여기 __자리 표시자 텍스트!).

```java
public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();

        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");

        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();

                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
```

### 매개 변수 정보

향후 프로젝트의 경우 추가 매개 변수를 구현할 수 있습니다. 이 방법을 사용하면 세 가지 유형의 매개 변수를 사용할 수 있습니다. `createTargetPrefetchObject()` `locationParams`, `orderParams`and `productParams`. 이러한 매개 변수를 프리페치 요청에 추가하는 방법에 대한 [자세한 내용은 설명서를 참조하십시오](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html).

또한 프리페치 요청의 각 위치에 서로 다른 위치 매개 변수를 추가할 수 있습니다. 예를 들어 param2라는 다른 맵을 만들고, 새 매개 변수를 삽입한 다음, 한 위치에서 param2를 설정하고, 다른 위치로 param1을 설정할 수 있습니다. 다음은 한 예입니다.

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## 프리페치 요청의 at_property 매개 변수 유효성 검사

이제 에뮬레이터를 실행하고 Logcat을 사용하여 두 위치에 대한 프리페치 요청 및 응답에 at_property가 표시되는지 확인합니다.
![at_property 매개 변수의 유효성 확인](assets/parameters_at_property_validation.jpg)

## 라이브 위치 요청에 사용자 지정 매개 변수 추가

이전 단원에서 라이브 위치 요청(wetravel_context_dest)이 추가되었으므로 예약 프로세스의 최종 확인 화면에 관련 프로모션을 표시할 수 있습니다. 사용자의 대상에 따라 프로모션을 개인화하고, 이를 요청에 매개 변수로 추가하고자 합니다. 제어 원점과 at_property 값에 대한 매개 변수를 추가하겠습니다.

ThankYouActivity 컨트롤러의 targetLoadRequest() 함수에 다음 매개 변수를 추가합니다.
![라이브 위치 요청에 매개 변수 추가](assets/parameters_live_location.jpg)는 targetLoadRequest() 함수에 대한 업데이트된 코드입니다. 자리 표시자 텍스트를 업데이트해야 합니다.

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Map<String, Object> locationParams = new HashMap<>();
    locationParams.put("at_property","add your at_property value here");
    locationParams.put("locationSrc", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.departure,"")));
    locationParams.put("locationDest", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.destination,"")));

    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, locationParams, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
        try {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    AppDialogs.dialogLoaderHide();
                    filterRecommendationBasedOnOffer(recommandations, response);
                    recommandationbAdapter.notifyDataSetChanged();
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
        }
    });
    Target.clearPrefetchCache();
}
```

### 라이브 위치 요청에서 사용자 지정 매개 변수 유효성 검사

에뮬레이터를 실행하고 Logcat을 엽니다. 매개 변수 중 하나에 대해 필터링하여 요청에 필요한 매개 변수가 포함되어 있는지 확인합니다.
![라이브 위치 요청에서 사용자 지정 매개 변수 유효성 검사](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>주문 확인 요청 및 매개변수: 이 데모 프로젝트에서는 사용되지 않지만, 주문 세부 사항은 일반적으로 실제 구현에서 캡처되므로 주문 세부 사항을 지표/차원으로 사용할 [!DNL Target] 수 있습니다. 주문 확인 요청 및 매개 변수를 [구현하는 방법에 대한 지침은 설명서를 참조하십시오](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-target-methods.html).

>[!NOTE]
>
>Target용 Analytics(A4T): Adobe Analytics을 [!DNL Target] Target SDK에서 수집한 모든 지표/차원을 Adobe Analytics에서 볼 수 있습니다. 자세한 내용은 [A4T](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) 개요를 참조하십시오.

잘했어! 이제 매개 변수가 제공되므로 이러한 매개 변수를 사용하여 Adobe Target에서 대상과 오퍼를 만들 수 있습니다.

**[다음: &quot;대상 및 오퍼 만들기&quot; >](create-audiences-and-offers.md)**
