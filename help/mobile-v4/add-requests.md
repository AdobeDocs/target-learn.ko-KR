---
title: Adobe Target 요청 추가
description: 'Adobe Mobile Services SDK(v4)에서는 Adobe Target 메서드 및 기능을 제공하여 사용자가 다른 경험을 통해 앱을 개인화할 수 있도록 합니다.   '
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

Adobe Mobile Services SDK(v4)에서는 Adobe Target 방법과 기능을 제공하므로 다른 사용자를 위해 다양한 경험을 사용하여 앱을 개인화할 수 있습니다. 일반적으로 개인화된 컨텐츠를 검색하고 해당 컨텐츠의 영향력을 측정하기 위해 앱에서 Adobe Target으로 하나 이상의 요청이 수행됩니다.

이 단원에서는 [!DNL Target] 요청을 구현하여 개인화를 위한 We.Travel 앱을 준비합니다.

## 전제 조건

[샘플 앱](download-and-update-the-sample-app.md)을 다운로드하고 업데이트하십시오.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 일괄 프리페치 요청을 사용하여 여러 개의 [!DNL Target] 오퍼(즉, 개인화된 컨텐츠)를 캐시합니다.
* 프리페치된 [!DNL Target] 위치 로드
* 실시간으로 [!DNL Target] 위치를 로드합니다(프리페치 안 함).
* 캐시에서 프리페치된 위치 지우기
* 프리페치된 요청 및 실시간 요청 유효성 확인

## 용어

다음은 이 자습서의 나머지 부분에서 사용할 주요 Target 용어입니다.

* **요청:**  Adobe Target 서버에 대한 네트워크 요청
* **오퍼:**  사용자 인터페이스(또는 API를 사용하여)에 정의된 코드 또는 기타 텍스트 기반 컨텐트의  [!DNL Target] 조각이며 응답으로 전달됩니다. 일반적으로 기본 모바일 앱에서 [!DNL Target]이(가) 사용되는 JSON입니다.
* **위치:**  오퍼를 특정 요청과 연결하기 위해 인터페이스에서  [!DNL Target] 사용하는 요청에 지정된 사용자 정의 이름
* **일괄 요청:**  여러 위치를 포함하는 단일 요청
* **프리페치 요청:**  앱에서 나중에 사용할 수 있도록 오퍼를 검색하고 이를 메모리에 캐시하는 단일 요청
* **일괄 프리페치 요청:**  프리페치하는 단일 요청에서 여러 위치에 대한 오퍼를 제공합니다.
* **대상:**  인터페이스에 정의되거나  [!DNL Target] 다른 Adobe 응용 프로그램 [!DNL Target] 에서 공유되는 방문자 그룹(예:&quot;iPhone X 방문자&quot;, &quot;캘리포니아에 있는 방문자&quot;, &quot;첫 번째 앱 열기&quot;)
* **활동:**  사용자  [!DNL Target] 인터페이스(또는 API를 사용하여 위치, 오퍼 및 대상을 연결하여 개인화된 경험을 만드는  [!DNL Target] 구성

## 일괄 프리페치 요청 추가

We.Travel에서 구현하는 첫 번째 요청은 홈 화면에서 두 개의 [!DNL Target] 위치를 가진 일괄 프리페치 요청입니다. 이후 단원에서는 이러한 위치에 대한 오퍼를 구성하여 예약 프로세스를 안내하는 데 도움이 되는 메시지를 표시합니다.

프리페치 요청은 Adobe Target 서버 응답(오퍼)을 캐시하여 가능한 한 [!DNL Target] 컨텐츠를 페치합니다. 일괄 프리페치 요청은 각각 다른 위치에 연결된 여러 오퍼를 검색하고 캐시합니다. 나중에 사용자 세션에서 사용하기 위해 프리페치된 모든 위치가 장치에 캐시됩니다. 홈 화면에서 여러 위치를 프리페치함으로써 방문자가 앱을 탐색할 때 나중에 사용할 오퍼를 검색할 수 있습니다. 프리페치 방법에 대한 자세한 내용은 [프리페치 설명서](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html)를 참조하십시오.

### 일괄 프리페치 요청 추가

앱 > 기본 > java > com.wetrevel > 컨트롤러 아래에 있는 HomeActivity 컨트롤러(홈 화면의 소스 코드)를 업데이트하겠습니다. 빨간색으로 표시된 두 코드 블록을 추가합니다.

HomeActivity 컨트롤러(홈 화면의 소스 코드)부터 시작합니다. 이 코드는 앱 > 기본 > java > com.wetrevel > Controller 아래에 있습니다.

빨간색으로 표시된 두 코드 블록을 추가합니다.

![HomeActivity 프리페치 코드](assets/homeactivity.jpg)

HomeActivity 코드 끝까지 스크롤하고 `setHeader()` 함수 뒤에 아래 제공된 코드를 추가하고 *교체* 현재 `onResume()` 함수 뒤에 &lt;a1/>로 추가합니다.

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

IDE에서 파일에 가져온 [!DNL Target] 클래스가 없다는 경고 메시지가 나타날 수 있습니다. 아래 빨간색으로 표시된 대로 HomeActivity 컨트롤러 상단에 있는 [!DNL Target] 클래스를 가져와야 합니다.

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Target 클래스 가져오기](assets/import.jpg)

&quot;symbol variable wetrevel_engage_home&quot;과 &quot;cannot find symbol variable wetrevel_engage_search&quot;에 대한 오류도 나타날 수 있습니다. 다음 항목을 `Constant.java` 파일에 추가합니다(앱 > src > main > java > com > wetlevel > Utils).

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Constant.java 파일에 위치 이름 추가](assets/constants.jpg)

### 일괄 프리페치 요청 코드 설명

| 코드 | 설명 |
|--- |--- |
| `targetPrefetchContent()` | [!DNL Target] 메서드를 사용하여 두 개의 [!DNL Target] 위치를 검색하고 캐시하는 사용자 정의 함수(SDK에 속하지 않음). |
| `prefetchContent()` | 프리페치 요청을 보내는 [!DNL Target] SDK 메서드 |
| `Constant.wetravel_engage_home` | 홈 화면에 오퍼 컨텐츠를 표시하는 [!DNL Target] 위치 이름을 프리페치했습니다. |
| `Constant.wetravel_engage_search` | 검색 결과 화면에 오퍼 컨텐츠를 표시하는 [!DNL Target] 위치 이름을 프리페치했습니다. 이 요청은 프리페치에서 두 번째 위치이므로 이 프리페치 요청을 &quot;프리페치 배치 요청&quot;이라고 합니다. |
| setUp() | [!DNL Target] 오퍼가 프리페치된 후 앱의 홈 화면을 렌더링하는 사용자 정의 함수 |

### 비동기 대 동기 정보

방금 구현한 코드를 사용하여 프리페치 요청은 홈 화면이 렌더링되기 바로 전에 동기 차단 호출로 수행됩니다. 새 코드를 HomeActivity 컨트롤러에 붙여넣을 때, Target 요청 이후로 `onResume()` 함수에서 `setUp()` 함수 실행을 이동했습니다. 첫 번째 화면이 렌더링되기 전에 Target 서버의 개인화된 컨텐츠가 반환되거나 시간 초과되었는지 확인하므로 앱을 처음 열 때 컨텐츠를 개인화하고자 하는 시나리오에서 이 기능이 유용할 수 있습니다. 요청이 비동기적으로(백그라운드에서) 로드되도록 하려면 대신 `onCreate()` 함수 내에서 `setUp()`만 호출하면 됩니다.

### 일괄 프리페치 요청 유효성 확인

앱을 다시 빌드하고 Android 에뮬레이터를 엽니다. (다음 스크린샷은 Android Q 버전 9+, API 레벨 29의 Pixel 2를 사용합니다.) 프리페치 응답에는 &quot;프리페치 응답 수신&quot; 메시지가 포함되어야 합니다.

홈 화면이 렌더링되면 프리페치 요청을 불러와야 합니다. Logcat에서 요청 및 응답을 보기 위해 [!DNL "Target"]에 대해 필터링합니다.

![홈 화면에서 요청 유효성 확인](assets/prefetch_validation.jpg)

성공적인 응답이 없으면 `ADBMobileConfig.json` 파일의 설정과 HomeActivity 파일의 코드 구문을 확인하십시오.

이제 두 위치가 장치에 캐시됩니다. 위치 이름은 [!DNL Target] 인터페이스에 잠시 지연되어 활동에서 사용할 때 다양한 드롭다운 메뉴에서 선택할 수 있습니다.

### 캐시된 각 위치에 대한 로드 요청 추가

이제 위치가 프리페치되고 해당 응답이 장치에 캐시되므로, 오퍼를 사용하여 응용 프로그램을 업데이트할 수 있도록 캐시에서 오퍼 컨텐츠를 검색하는 `Target.loadRequest()` 메서드를 추가하겠습니다. 프리페치 요청과 함께 실행되는 `engageMessage()`이라는 새 사용자 지정 메서드를 추가합니다. `engageMessage()` 전화드리겠습니다 `Target.loadRequest()`. `engageMessage()` 화면 `setUp()` 을 설정하기 전에 로드 요청이 호출되도록 하기 전에 실행됩니다.

먼저 HomeActivity에서 wetrevel_engage_home 위치에 대한 `engageMessage()` 호출 및 메서드를 추가합니다.

![첫 번째 로드 요청 추가](assets/wetravel_engage_home_loadRequest.jpg)

업데이트된 코드는 다음과 같습니다.

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

이제 SearchBusActivity에서 wetrevel_engage_search 위치에 대한 `engageMessage()` 호출 및 메서드를 추가합니다. `engageMessage()` 호출은 `setUpSearch()`에 대한 호출 전에 `onResume()` 메서드에 설정되므로 화면을 설정하기 전에 실행됩니다.

![두 번째 로드 요청 추가](assets/wetravel_engage_search_loadRequest.jpg)

업데이트된 코드는 다음과 같습니다.

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

SearchBusActivity에 Target 메서드를 방금 추가했으므로 [!DNL Target] 클래스를 가져와야 합니다.

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## 실시간 요청 추가

다음 요청은 감사 화면에서 실시간 요청이 됩니다. &quot;실시간&quot;은 두 요청이 모두 수행되고 응답이 즉시 적용됨을 의미합니다(나중에 캐시되지 않음). 다음 수업에서는 사용자의 여행 대상에 맞게 개인화된 이 요청을 사용하여 경험을 구축할 것입니다.

이제 감사 화면에 실시간 요청을 추가해 보겠습니다. 감사 인사 파일에서 다음 내용이 빨간색으로 표시됩니다.
![감사 화면의 실시간 위치 추가](assets/thankyou.jpg)

ThankYouActivity 파일의 끝으로 스크롤합니다. `getRecommandations()` 함수에 3개의 줄을 주석 처리하고 `targetLoadRequest()` 함수의 호출을 추가합니다.

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

이 코드 행을 `getRecommandations()` 함수에 추가합니다.

```java
targetLoadRequest(recommandation.recommandations);
```

이제 `targetLoadRequest()` 함수를 정의해야 합니다.
![감사 화면의 실시간 위치 추가](assets/thankyou2.jpg)

`filterRecommendationBasedOnOffer()` 함수 뒤에 이 코드 블록을 추가합니다.

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
| `targetLoadRequest()` | SDK의 일부가 아닌 사용자 정의 함수로, wetravel_context_dest 위치를 로드하여 표시하는 `Target.loadRequest()`을 실행합니다. |
| `Target.loadRequest()` | Target 서버에 요청을 하는 SDK 메서드 |
| Constant.wetravel_context_dest | [!DNL Target] 인터페이스에서 활동을 작성할 때 나중에 사용할 요청에 할당된 위치 이름 |
| `filterRecommendationBasedOnOffer()` | Target 응답에서 위치 오퍼를 가져와서 오퍼의 컨텐츠를 기준으로 앱이 변경되는 방식을 결정하는 앱에서 사용자 정의 함수 |
| `recommandations.addAll()` | ThankYou 화면을 로드할 때 기본적으로 실행되었던 앱의 사용자 정의 함수입니다. 그러나 이제 Target 응답을 수신하여 `filterRecommendationBasedOnOffer()`에 의해 구문 분석된 후 실행됩니다. |

이것은 앱에 대한 더 정교한 업데이트였고, 홈 화면에 추가된 요청과 함께, Adobe가 한 일을 잠시 살펴보도록 하겠습니다.

1. 코드 줄을 주석 처리하여 3개의 기본 판촉 행사를 표시하는 앱의 이전 행동을 중단했습니다
1. 대신 앱에 새로운 함수를 실행하라고 지시했으며, 이 함수를 임의로 targetLoadRequest라고 지정했습니다
1. Target.loadRequest 메서드를 사용하여 Target에 요청하도록 `targetLoadRequest` 함수를 정의하고 [!DNL Target] 오퍼 응답이 수신되면 즉시 `filterRecommendationBasedOnOffer()` 함수를 실행합니다.
1. `filterRecommendationBasedOnOffer()` 함수는 응답을 해석하고 화면에 적용할 프로모션을 결정합니다

이는 모바일 앱에서 [!DNL Target]을(를) 사용할 때 매우 일반적인 사용 패턴입니다.  모바일 앱의 거의 모든 측면을 개인화할 수 있다는 점에서 두 가지 모두 매우 강력합니다. 또한 앱 코드와 나중에 [!DNL Target] 인터페이스에서 정의할 오퍼 간의 조정이 필요합니다. 이러한 조정을 통해 일부 개인화 사용 사례에서는 활동을 실행하기 위해 앱 스토어에서 앱을 업데이트해야 할 수 있습니다.

### 실시간 요청 유효성 확인

Android 에뮬레이터를 열고 다음 단계를 통해 이동을 예약합니다.홈 > 버스 검색 결과 > 시트 선택, 지불 옵션(빈 데이터가 있는 모든 지불 옵션이 작동합니다.)

마지막 감사 화면에서 Logcat에서 응답을 확인하십시오. &quot;wetravel_context_dest&quot;에 대해 기본 컨텐츠가 반환되었습니다.

![감사 화면에 실시간 위치 추가](assets/thankyou_validation.jpg)

## 캐시에서 프리페치된 위치 지우기

세션 중에 프리페치된 위치를 지워야 하는 경우가 있을 수 있습니다. 예를 들어 예약이 발생하면 사용자가 &quot;참여&quot;되어 있고 예약 프로세스를 이해하므로 캐시된 위치를 지우는 것이 적절합니다. 세션 중에 다른 여행을 예약할 경우 홈 화면에서 원래 위치 및 검색 결과 화면이 예약에 필요한 것이 아닙니다. 캐시에서 위치를 지우고 할인된 2차 예약 또는 기타 관련 시나리오에 대해 새로운 오퍼를 미리 가져오는 것이 더 이치에 좋습니다. 세션 중에 예약한 경우 홈 화면 및 검색 결과 화면에 논리를 추가하여 새 위치를 미리 가져올 수 있습니다.

예를 들어 예약 시 세션의 프리페치된 위치를 지웁니다. 이 작업은 `Target.clearPrefetchCache()` 함수를 호출하여 수행합니다. 아래와 같이 `targetLoadRequest()` 함수 내의 함수를 설정합니다.

```java
Target.clearPrefetchCache()
```

![캐시에서 프리페치된 위치 지우기](assets/clearPrefetch.jpg)

축하합니다! 이제 앱에 개인화를 위한 프레임워크가 있습니다. 다음 단원에서는 이러한 위치에 매개 변수를 추가하여 개인화 기능을 개선해 보겠습니다.

**[다음:&quot;매개 변수 추가&quot; >](add-parameters.md)**
