---
title: Adobe Target 요청 추가
description: 'Adobe Mobile Services SDK(v4)에서는 서로 다른 사용자를 위한 다양한 경험으로 앱을 개인화할 수 있는 Adobe Target 방법 및 기능을 제공합니다.   '
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---


# Adobe Target 요청 추가

Adobe Mobile Services SDK(v4)에서는 서로 다른 사용자 경험을 통해 앱을 개인화할 수 있는 Adobe Target 방법 및 기능을 제공합니다. 일반적으로 개인화된 콘텐츠를 검색하고 해당 컨텐츠의 영향력을 측정하기 위해 앱에서 Adobe Target으로 하나 이상의 요청이 수행됩니다.

이 단원에서는 요청을 구현하여 개인화를 위한 We.Travel 앱을 [!DNL Target] 준비합니다.

## 전제 조건

샘플 앱을 [다운로드하고 업데이트해야 합니다](download-and-update-the-sample-app.md).

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 일괄 프리페치 요청을 사용하여 여러 [!DNL Target] 오퍼(즉, 개인화된 컨텐츠)를 캐시합니다.
* 프리페치된 [!DNL Target] 위치 로드
* 실시간(프리페치 안 함) [!DNL Target] 위치 로드
* 캐시에서 프리페치된 위치 지우기
* 프리페치 요청 및 실시간 요청 유효성 확인

## 용어

다음은 이 자습서의 나머지 부분에서 사용할 주요 Target 용어입니다.

* **요청:**  Adobe Target 서버에 대한 네트워크 요청
* **오퍼:**  사용자 인터페이스(또는 API를 사용하여)에 정의된 코드 조각 또는 기타 텍스트 기반 컨텐츠의 [!DNL Target] 답으로 배달됩니다. 기본 모바일 앱 [!DNL Target] 에서 사용되는 경우 일반적으로 JSON입니다.
* **위치:**  오퍼를 특정 요청과 연관시키는 [!DNL Target] 인터페이스에서 사용되는 요청에 지정된 사용자 정의 이름
* **일괄 요청:**  여러 위치를 포함하는 단일 요청
* **프리페치 요청:**  앱에서 나중에 사용할 수 있도록 오퍼를 검색하고 이를 메모리에 캐시하는 단일 요청
* **일괄 프리페치 요청:**  프리페치가 여러 위치에 대해 오퍼를 제공하는 단일 요청
* **대상:**  인터페이스에 정의되거나 다른 Adobe 응용 프로그램에서 공유되는 [!DNL Target] [!DNL Target] 방문자 그룹(예: &quot;iPhone X visitors&quot;, &quot;Visitors in the California&quot;, &quot;First App Open&quot;)
* **활동:**  위치, 오퍼 및 대상을 연결하는 [!DNL Target] [!DNL Target] 사용자 인터페이스(또는 API를 사용하여 정의)에 정의된 구성 요소로 개인화된 경험 제작

## 일괄 프리페치 요청 추가

We.Travel에서 처음으로 실시하고자 하는 요청은 홈 화면에 두 [!DNL Target] 위치가 있는 배치 프리페치 요청입니다. 이후 단원에서 이러한 위치에 대한 오퍼를 구성하여 예약 프로세스를 안내하는 데 도움이 되는 메시지를 표시합니다.

프리페치 요청은 Adobe Target 서버 응답(오퍼)을 캐시하여 가능한 한 최소한의 [!DNL Target] 컨텐츠를 가져옵니다. 일괄 프리페치 요청은 각각 다른 위치에 연결된 여러 오퍼를 검색하고 캐시합니다. 나중에 사용자 세션에서 사용하기 위해 프리페치된 모든 위치가 장치에 캐시됩니다. 홈 화면에서 여러 위치를 프리페치함으로써 방문자가 앱을 탐색할 때 나중에 사용할 오퍼를 검색할 수 있습니다. 프리페치 방법에 대한 자세한 내용은 [프리페치 설명서를](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html) 참조하십시오.

### 배치 프리페치 요청 추가

HomeActivity 컨트롤러(홈 화면의 소스 코드)를 업데이트해 보겠습니다. 이 코드는 앱 > 메인 > java > com.wetrale > 컨트롤러 아래에 있습니다. 빨간색으로 표시된 두 개의 코드 블록을 추가합니다.

HomeActivity 컨트롤러(홈 화면의 소스 코드)부터 시작하겠습니다. 이 컨트롤러는 앱 > 메인 > java > com.wetrevel > 컨트롤러 아래에 있습니다.

빨간색으로 표시된 두 개의 코드 블록을 추가합니다.

![HomeActivity 프리페치 코드](assets/homeactivity.jpg)

HomeActivity 코드 끝까지 스크롤 다운한 다음 함수 뒤에 아래 제공된 코드를 추가하고 현재 `setHeader()` 함수를 *바꿉니다* `onResume()` .

```java
@Override
protected void onResume() {
    super.onResume();
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

IDE에서 파일에 가져온 클래스가 없다는 [!DNL Target] 경고가 나타날 수 있습니다. 아래 빨간색으로 표시된 대로 HomeActivity [!DNL Target] 컨트롤러 상단에 있는 클래스를 가져와야 합니다.

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Target 클래스 가져오기](assets/import.jpg)

&quot;symbol variable wetrevel_engage_home&quot;을 찾을 수 없으며 &quot;cannot find symbol variable wetrevel_engage_search&quot;에 대한 오류가 표시될 수 있습니다. 파일에 `Constant.java` 추가합니다(앱 > src > main > java > com > wetravel > Utils).

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Constant.java 파일에 위치 이름 추가](assets/constants.jpg)

### 일괄 프리페치 요청 코드 설명

| 코드 | 설명 |
|--- |--- |
| `targetPrefetchContent()` | 메서드를 사용하여 두 위치를 검색하고 캐시하는 사용자 정의 함수(SDK의 일부가 아님) [!DNL Target] [!DNL Target] 입니다. |
| `prefetchContent()` | 프리페치 요청을 보내는 [!DNL Target] SDK 메서드 |
| `Constant.wetravel_engage_home` | 홈 화면에 오퍼 컨텐츠를 표시하는 프리페치된 [!DNL Target] 위치 이름 |
| `Constant.wetravel_engage_search` | 검색 결과 화면에 오퍼 컨텐츠를 표시하는 프리페치된 [!DNL Target] 위치 이름입니다. 이 요청은 프리페치에서 두 번째 위치이므로 이 프리페치 요청을 &quot;프리페치 배치 요청&quot;이라고 합니다. |
| setUp() | 오퍼가 프리페치된 후 앱의 홈 화면을 렌더링하는 사용자 정의 [!DNL Target] 함수 |

### 비동기 및 동기 정보

방금 구현한 코드를 통해 프리페치 요청은 홈 화면이 렌더링되기 바로 전에 동기식 차단 호출로 이루어집니다. 새 코드를 HomeActivity 컨트롤러에 붙여넣을 때, 함수 실행을 Target 요청 이후로 `setUp()` `onResume()` 이동했습니다. 이는 첫 번째 화면이 렌더링되기 전에 Target 서버의 개인화된 컨텐츠가 반환되거나 시간 초과되는 것을 보장하므로 앱이 처음 열릴 때 컨텐츠를 개인화하고자 하는 시나리오에서 유용할 수 있습니다. 요청이 비동기적으로(백그라운드에서) 로드되도록 하려면 대신 함수 `setUp()` 내에서 `onCreate()` 호출하기만 하면 됩니다.

### 배치 프리페치 요청 유효성 확인

앱을 다시 빌드하고 Android 에뮬레이터를 엽니다. (다음 스크린샷은 Android Q 버전 9+, API 레벨 29의 Pixel 2를 사용합니다.) 프리페치 응답에 &quot;프리페치 응답 수신&quot;이 표시되어야 합니다.

홈 화면이 렌더링되면 프리페치 요청을 불러와야 합니다. Logcat에서 요청 및 응답 [!DNL "Target"] 을 보기 위해 필터링합니다.

![홈 화면에서 요청 유효성 확인](assets/prefetch_validation.jpg)

성공적인 응답이 없으면 파일의 설정과 HomeActivity 파일의 코드 구문을 `ADBMobileConfig.json` 확인합니다.

이제 두 위치가 장치에 캐시됩니다. 위치 이름은 [!DNL Target] 인터페이스에 잠시 지연되어 활동에서 사용할 때 다양한 드롭다운 메뉴에서 선택할 수 있습니다.

### 캐시된 각 위치에 대한 로드 요청 추가

이제 위치가 프리페치되고 해당 응답이 장치에 캐시되므로, 캐시를 통해 오퍼 컨텐츠를 검색하는 방법을 추가하여 응용 프로그램을 업데이트할 수 있습니다. `Target.loadRequest()` 프리페치 요청과 함께 실행되는 새 사용자 지정 방법 `engageMessage()` 을 추가합니다. `engageMessage()` 전화드리겠습니다 `Target.loadRequest()`. `engageMessage()` 실행 전에 `setUp()` 를 실행하여 로드 요청이 호출되도록 합니다.

먼저 HomeActivity에서 wetravel_engage_home 위치에 대한 `engageMessage()` 호출 및 메서드를 추가합니다.

![첫 번째 로드 요청 추가](assets/wetravel_engage_home_loadRequest.jpg)

다음은 업데이트된 코드입니다.

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
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
    }
```

이제 SearchBusActivity에서 wetravel_engage_search 위치에 대한 `engageMessage()` 호출 및 메서드를 추가합니다. 통화가 설정되기 전에 `engageMessage()` 호출은 `onResume()` 호출 전 `setUpSearch()` 에 설정되므로 화면이 설정되기 전에 실행됩니다.

![두 번째 로드 요청 추가](assets/wetravel_engage_search_loadRequest.jpg)

다음은 업데이트된 코드입니다.

```java
    @Override
    public void onResume() {
        super.onResume();
        engageMessage();
        setUpSearch();
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
                new Target.TargetCallback<String>(){
                    @Override
                    public void call(final String s) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                System.out.println("Engage Message : " + s);
                                if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                            }
                        });
                    }
                });
    }
```

SearchBusActivity에 Target 메서드를 방금 추가했으므로 클래스를 [!DNL Target] 가져와야 합니다.

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## 실시간 요청 추가

다음 요청은 감사 화면에서 실시간 요청이 됩니다. &quot;실시간&quot;은 두 요청이 모두 수행되고 응답이 즉시 적용됨을 의미합니다(나중에 캐시되지 않음). 다음 수업에서는 사용자의 여행 대상에 맞게 개인화된 이 요청을 사용하여 경험을 구축할 예정입니다.

이제 감사 화면에 실시간 요청을 추가해 보겠습니다. ThankYouActivity 파일에서, Adobe는 다음 빨간색으로 변경 사항을 만듭니다.
![감사 화면에 실시간 위치 추가](assets/thankyou.jpg)

ThankYouActivity 파일의 끝으로 스크롤합니다. 함수의 세 줄을 주석 `getRecommandations()` 으로 지정하고 함수 호출을 `targetLoadRequest()` 추가합니다.

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

함수에 이 코드 줄을 `getRecommandations()` 추가합니다.

```java
targetLoadRequest(recommandation.recommandations);
```

이제 `targetLoadRequest()` 기능을 정의해야 합니다.
![감사 화면에 실시간 위치 추가](assets/thankyou2.jpg)

함수 뒤에 이 코드 블록을 `filterRecommendationBasedOnOffer()` 추가합니다.

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
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
}
```

ThankYouActivity에 Target 메서드를 방금 추가했으므로 Target 클래스를 가져와야 합니다.

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### targetLoadRequest() 코드 설명

| 코드 | 설명 |
|--- |--- |
| `targetLoadRequest()` | SDK에 포함되지 않고 wetravel_context_dest 위치를 로드하여 표시하는 사용자 정의 함수 `Target.loadRequest()` |
| `Target.loadRequest()` | Target 서버에 요청을 하는 SDK 메서드 |
| Constant.wetravel_context_dest | 나중에 인터페이스에서 활동을 작성할 때 사용할 요청에 지정된 위치 [!DNL Target] 이름 |
| `filterRecommendationBasedOnOffer()` | Target 응답에서 위치 오퍼를 가져와 오퍼의 컨텐츠를 기준으로 앱이 변경되는 방법을 결정하는 앱에서 사용자 정의 함수 |
| `recommandations.addAll()` | ThankYou 화면이 로드될 때 기본적으로 실행되었던 앱의 사용자 정의 함수에서 이제 Target 응답을 수신하여 구문 분석한 후에 실행됩니다. `filterRecommendationBasedOnOffer()` |

이것은 우리가 그 앱에 대해 했던 더 정교한 업데이트였으며, 우리가 홈 화면에 추가한 요청과 함께, 우리가 했던 것을 잠시 동안 살펴봅시다.

1. 코드 줄을 주석 처리하여 3개의 기본 판촉 행사를 표시하는 앱의 이전 행동을 중단했습니다
1. 대신 앱에 새로운 함수를 실행하라고 지시했으며, 이 함수를 임의로 targetLoadRequest로 지정했습니다
1. Target.loadRequest 메서드를 사용하여 Target에 요청을 하고 오퍼 응답이 수신되면 즉시 `targetLoadRequest` 함수를 `filterRecommendationBasedOnOffer()` [!DNL Target] 실행하는 함수를 정의했습니다
1. 이 `filterRecommendationBasedOnOffer()` 함수는 응답을 해석하고 화면에 어떤 판촉을 적용할지 결정합니다

이는 모바일 앱에서 사용하는 경우 매우 일반적인 사용 패턴 [!DNL Target] 입니다.  모바일 앱의 거의 모든 측면을 개인화할 수 있는 강력한 솔루션입니다. 또한 앱 코드와 나중에 [!DNL Target] 인터페이스에서 정의할 오퍼 간에 조정이 필요합니다. 이러한 조정 때문에 일부 개인화 사용 사례에서는 활동을 실행하기 위해 앱 스토어에서 앱을 업데이트해야 할 수 있습니다.

### 실시간 요청 유효성 확인

Android 에뮬레이터를 열고 다음 단계에 따라 이동을 예약합니다. 홈 > 버스 검색 결과 > 시트 선택, 지불 옵션(빈 데이터가 있는 모든 지불 옵션)이 작동합니다.

마지막 감사 화면에서 Logcat에서 응답을 확인하십시오. &quot;wetravel_context_dest&quot;에 대해 기본 컨텐츠가 반환됨:

![감사 화면에 실시간 위치 추가](assets/thankyou_validation.jpg)

## 캐시에서 프리페치된 위치 지우기

세션 중에 프리페치된 위치를 지워야 하는 경우가 있을 수 있습니다. 예를 들어 예약이 발생하면 사용자가 &quot;참여&quot;되어 있고 예약 프로세스를 이해하므로 캐시된 위치를 지우는 것이 적절합니다. 또 다른 여행 예약을 할 경우 홈화면과 검색 결과 화면에서 기존 위치를 찾아 예약 안내를 받을 필요가 없게 된다. 캐시에서 위치를 지우고 새로운 오퍼를 프리페치하여 할인된 2차 예약 또는 기타 관련 시나리오를 수행하는 것이 더 적절합니다. 세션 중에 예약한 경우 새 위치를 미리 가져오기 위해 홈 화면 및 검색 결과 화면에 로직을 추가할 수 있습니다.

예를 들어 예약 시 세션의 프리페치된 위치를 지웁니다. 이 작업은 함수를 호출하여 `Target.clearPrefetchCache()` 수행됩니다. 함수 내에서 함수를 다음과 같이 `targetLoadRequest()` 설정합니다.

```java
Target.clearPrefetchCache()
```

![캐시에서 프리페치된 위치 지우기](assets/clearPrefetch.jpg)

축하합니다! 이제 앱에 개인화 프레임워크가 추가되었습니다. 다음 단원에서 이러한 위치에 매개 변수를 추가하여 개인화 기능을 개선하겠습니다.

**[다음: &quot;매개 변수 추가&quot; >](add-parameters.md)**
