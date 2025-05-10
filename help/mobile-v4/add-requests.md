---
title: Adobe Target 요청 추가
description: Adobe Mobile Services SDK(v4)는 다양한 사용자를 위해 다양한 경험으로 앱을 개인화할 수 있는 Adobe Target 메서드 및 기능을 제공합니다.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 88a5be3f-d61f-43e7-997a-574ef56122ed
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---

# Adobe Target 요청 추가

Adobe Mobile Services SDK(v4)는 다양한 사용자를 위해 다양한 경험으로 앱을 개인화할 수 있는 Adobe Target 메서드 및 기능을 제공합니다. 일반적으로 앱에서 Adobe Target으로 하나 이상의 요청을 하여 개인화된 콘텐츠를 검색하고 해당 콘텐츠의 영향을 측정합니다.

이 단원에서는 [!DNL Target] 요청을 구현하여 개인화를 위한 We.Travel 앱을 준비합니다.

## 전제 조건

[샘플 앱을 다운로드하고 업데이트](download-and-update-the-sample-app.md)하세요.

## 학습 목표

이 단원을 마치면 다음을 수행할 수 있습니다.

* 일괄 미리 가져오기 요청을 사용하여 여러 [!DNL Target] 오퍼(즉, 개인화된 콘텐츠) 캐시하기
* 미리 가져온 [!DNL Target]개 위치 로드
* 실시간으로 [!DNL Target] 위치 로드(미리 가져오지 않음)
* 캐시에서 프리페치된 위치 지우기
* 프리페치된 요청 및 실시간 요청의 유효성 검사

## Terminology

다음은 이 자습서의 나머지 부분에서 사용할 주요 Target 용어 중 일부입니다.

* Adobe Target 서버에 대한 **요청:** 네트워크 요청
* **Offer:** 사용자 인터페이스(또는 API)에 정의된 코드 또는 기타 텍스트 기반 콘텐츠 조각으로, 응답에서 전달됩니다. [!DNL Target] [!DNL Target]이(가) 기본 모바일 앱에서 사용되는 경우 일반적으로 JSON입니다.
* **위치:** 요청에 지정된 사용자 정의 이름으로, [!DNL Target] 인터페이스에서 오퍼를 특정 요청과 연결하는 데 사용됩니다.
* **일괄 처리 요청:** 여러 위치를 포함하는 단일 요청
* **미리 가져오기 요청:** 오퍼를 검색하고 나중에 앱에서 사용할 수 있도록 메모리에 캐시하는 단일 요청
* **일괄 미리 가져오기 요청:** 여러 위치에 대한 오퍼를 미리 가져오는 단일 요청
* **대상:** [!DNL Target] 인터페이스에 정의되어 있거나 다른 Adobe 응용 프로그램에서 [!DNL Target]과(와) 공유한 방문자 그룹(예: &quot;iPhone X 방문자&quot;, &quot;캘리포니아 방문자&quot;, &quot;첫 번째 앱 열기&quot;)
* **활동:** 개인화된 경험을 만들기 위해 위치, 오퍼 및 대상을 연결하는 [!DNL Target] 사용자 인터페이스(또는 API 포함)에 정의된 [!DNL Target] 구성입니다.

## 일괄 프리페치 요청 추가

We.Travel에서 구현할 첫 번째 요청은 홈 화면에 두 개의 [!DNL Target] 위치가 있는 일괄 미리 가져오기 요청입니다. 이후 단원에서는 예약 프로세스를 통해 신규 사용자를 안내하는 데 도움이 되는 메시지를 표시하는 이러한 위치에 대한 오퍼를 구성합니다.

미리 가져오기 요청은 Adobe Target 서버 응답(오퍼)을 캐시하여 가능한 한 최소한의 [!DNL Target] 콘텐츠를 가져옵니다. 배치 미리 가져오기 요청은 각각 다른 위치와 연관된 여러 오퍼를 검색하고 캐시합니다. 프리페치된 모든 위치는 사용자 세션에서 나중에 사용할 수 있도록 디바이스에 캐시됩니다. 홈 화면에서 여러 위치를 미리 가져오면 방문자가 앱을 탐색할 때 나중에 사용할 오퍼를 검색할 수 있습니다. 미리 가져오기 방법에 대한 자세한 내용은 [미리 가져오기 설명서](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=ko)를 참조하십시오.

### 배치 프리페치 요청 추가

app > main > java > com.wetravel > Controller 아래에 있는 HomeActivity 컨트롤러(홈 화면의 소스 코드)를 업데이트하겠습니다. 빨간색으로 표시된 두 코드 블록을 추가합니다.

app > main > java > com.wetravel > Controller 아래에 있는 HomeActivity 컨트롤러(홈 화면의 소스 코드)부터 시작하겠습니다.

빨간색으로 표시된 두 코드 블록을 추가합니다.

![HomeActivity 미리 가져오기 코드](assets/homeactivity.jpg)

HomeActivity 코드 끝으로 스크롤하여 `setHeader()` 함수 다음에 아래에 제공된 코드를 추가하고 *현재 `onResume()` 함수를*&#x200B;합니다.

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

파일에 가져온 [!DNL Target] 클래스가 없다는 경고가 IDE에 표시될 수 있습니다. 아래 빨간색으로 표시된 대로 HomeActivity 컨트롤러의 맨 위에 있는 [!DNL Target] 클래스를 가져와야 합니다.

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![대상 클래스 가져오기](assets/import.jpg)

또한 &quot;could find symbol variable wetravel_engage_home&quot; 및 &quot;could not find symbol variable wetravel_engage_search&quot;에 대한 오류가 표시될 수 있습니다. `Constant.java` 파일에 추가합니다(앱 > src > 기본 > java > com > wetravel > 유틸리티).

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![위치 이름을 Constant.java 파일에 추가](assets/constants.jpg)

### 일괄 프리페치 요청 코드 설명

| 코드 | 설명 |
|--- |--- |
| `targetPrefetchContent()` | [!DNL Target] 메서드를 사용하여 두 개의 [!DNL Target] 위치를 검색하고 캐시하는 사용자 정의 함수(SDK의 일부가 아님)입니다. |
| `prefetchContent()` | 미리 가져오기 요청을 보내는 [!DNL Target] SDK 메서드 |
| `Constant.wetravel_engage_home` | 홈 화면에 오퍼 컨텐츠를 표시하는 미리 가져온 [!DNL Target] 위치 이름 |
| `Constant.wetravel_engage_search` | 검색 결과 화면에 오퍼 컨텐츠를 표시하는 [!DNL Target] 위치 이름을 미리 가져왔습니다. 이 위치는 미리 가져오기의 두 번째 위치이므로 이 미리 가져오기 요청을 &quot;미리 가져오기 일괄 처리 요청&quot;이라고 합니다. |
| setUp() | [!DNL Target] 오퍼를 미리 가져온 후 앱의 홈 화면을 렌더링하는 사용자 정의 함수입니다 |

### 비동기 및 동기 정보

방금 구현한 코드를 사용하면 홈 화면이 렌더링되기 바로 전에 프리페치 요청이 동기식 차단 호출로 수행됩니다. 새 코드를 HomeActivity 컨트롤러에 붙여넣을 때 `onResume()` 함수에서 Target 요청 이후까지 `setUp()` 함수 실행을 이동했습니다. 이 기능은 앱이 처음 열릴 때 첫 번째 화면이 렌더링되기 전에 Target 서버의 개인화된 콘텐츠가 반환(또는 시간 초과)되었는지 확인하므로 콘텐츠를 개인화하려는 시나리오에서 유용할 수 있습니다. 요청이 백그라운드에서 비동기적으로 로드되도록 하려면 대신 `onCreate()` 함수 내에서 `setUp()`을(를) 호출하십시오.

### 배치 미리 가져오기 요청의 유효성 검사

앱을 다시 빌드하고 Android 에뮬레이터를 엽니다. (다음 스크린샷은 Android Q 버전 9+, API 레벨 29의 픽셀 2를 사용합니다.) 미리 가져오기 응답에는 &quot;미리 가져오기 응답 수신됨&quot;이 읽어야 합니다.

홈 화면이 렌더링될 때 미리 가져오기 요청을 로드해야 합니다. Logcat을 사용하여 [!DNL "Target"]을(를) 필터링하여 요청 및 응답을 봅니다.

![홈 화면에서 요청의 유효성 검사](assets/prefetch_validation.jpg)

성공적인 응답이 표시되지 않으면 `ADBMobileConfig.json` 파일의 설정과 HomeActivity 파일의 코드 구문을 확인하십시오.

이제 두 위치가 장치에 캐시됩니다. 위치 이름은 [!DNL Target] 인터페이스에 곧 소극적으로 로드되며, 활동에서 사용할 때 다양한 드롭다운 메뉴에서 선택할 수 있습니다.

### 캐시된 각 위치에 대한 로드 요청 추가

이제 위치를 미리 가져오고 해당 응답을 장치에 캐시했으므로, 응용 프로그램을 업데이트하는 데 사용할 수 있도록 캐시에서 오퍼 콘텐츠를 검색하는 `Target.loadRequest()` 메서드를 추가하겠습니다. 미리 가져오기 요청으로 실행할 `engageMessage()`(이)라는 새 사용자 지정 메서드를 추가합니다. `engageMessage()`이(가) `Target.loadRequest()`을(를) 호출합니다. `engageMessage()`은(는) 화면을 설정하기 전에 로드 요청이 호출되도록 `setUp()` 전에 실행됩니다.

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

이제 SearchBusActivity에서 wetravel_engage_search 위치에 대한 `engageMessage()` 호출 및 메서드를 추가합니다. `engageMessage()` 호출은 `setUpSearch()` 호출 전에 `onResume()` 메서드에 설정되어 있으므로 화면이 설정되기 전에 실행됩니다.

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

Target 메서드를 SearchBusActivity에 추가했으므로 [!DNL Target] 클래스를 가져와야 합니다.

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## 실시간 요청 추가

앱에 추가할 다음 요청은 감사 화면에서 실시간 요청이 됩니다. &quot;실시간&quot;은 요청이 모두 이루어지고 응답이 즉시 적용됨을 의미합니다(나중에 캐시되지 않음). 이후 단원에서는 이 요청을 사용하여 사용자의 여행 대상에 맞게 개인화된 경험을 구축하겠습니다.

그러면 감사 화면에 실시간 요청을 추가하겠습니다. ThankYouActivity 파일에서 빨간색으로 표시된 변경 사항을 수행합니다.
![감사 인사 화면에 실시간 위치 추가](assets/thankyou.jpg)

ThankYouActivity 파일의 끝으로 스크롤합니다. `getRecommandations()` 함수의 세 줄을 주석 처리하고 `targetLoadRequest()` 함수의 호출을 추가합니다.

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
![감사 인사 화면에 실시간 위치 추가](assets/thankyou2.jpg)

`filterRecommendationBasedOnOffer()` 함수 뒤에 이 코드 블록을 추가하십시오.

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

Target 메서드를 ThankYouActivity에 추가했으므로 Target 클래스를 가져와야 합니다.

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### targetLoadRequest() 코드 설명

| 코드 | 설명 |
|--- |--- |
| `targetLoadRequest()` | wetravel_context_dest 위치를 로드하고 표시하는 `Target.loadRequest()`을(를) 실행하는 사용자 정의 함수(SDK의 일부가 아님) |
| `Target.loadRequest()` | Target 서버에 요청하는 SDK 메서드입니다 |
| Constant.wetravel_context_dest | [!DNL Target] 인터페이스에서 활동을 빌드할 때 나중에 사용할 요청에 할당된 위치 이름 |
| `filterRecommendationBasedOnOffer()` | Target 응답에서 위치의 오퍼를 가져오고 오퍼의 콘텐츠를 기반으로 앱이 변경되는 방법을 결정하는 앱의 사용자 정의 함수입니다 |
| `recommandations.addAll()` | ThankYou 화면이 로드될 때 기본적으로 실행되던 앱의 사용자 정의 함수로, `filterRecommendationBasedOnOffer()`에서 Target 응답을 받고 구문 분석한 후 실행됩니다. |

이 업데이트는 앱에 보다 정교하게 제공되었으며 홈 화면에 추가된 요청이므로 잠시 시간을 내어 수행한 작업을 검토해 보겠습니다.

1. 코드 행에 주석을 달아 세 개의 기본 프로모션을 표시하는 앱의 이전 동작을 중단했습니다
1. 대신 앱에 새 함수를 실행하라고 지시했으며, 이 함수를 임의로 targetLoadRequest라고 명명했습니다
1. [!DNL Target] 오퍼 응답을 받으면 Target.loadRequest 메서드를 사용하여 Target에 요청하고 `filterRecommendationBasedOnOffer()` 함수를 바로 실행하도록 `targetLoadRequest` 함수를 정의했습니다
1. `filterRecommendationBasedOnOffer()` 함수는 응답을 해석하고 화면에 적용할 프로모션을 결정합니다

이는 모바일 앱에서 [!DNL Target]을(를) 사용할 때 매우 일반적인 사용 패턴입니다.  모바일 앱의 거의 모든 측면을 개인화할 수 있다는 점에서 두 가지 모두 매우 강력합니다. 또한 앱 코드와 나중에 [!DNL Target] 인터페이스에서 정의할 오퍼 간의 조정이 필요합니다. 이러한 조정으로 인해 일부 개인화 사용 사례에서는 활동을 시작하기 위해 앱스토어에서 앱을 업데이트해야 할 수 있습니다.

### 실시간 요청의 유효성 검사

Android 에뮬레이터를 열고 여행을 예약하는 모든 단계를 거칩니다. 홈 > 버스 검색 결과 > 좌석 선택, 결제 옵션 (빈 데이터가 있는 모든 결제 옵션이 작동함).

마지막 감사 인사 화면에서 응답을 보려면 Logcat을 시청하십시오. 응답은 &quot;wetravel_context_dest&quot;에 대해 반환된 기본 컨텐츠입니다.

![감사 인사 화면에 실시간 위치 추가](assets/thankyou_validation.jpg)

## 캐시에서 프리페치된 위치 지우기

세션 중에 프리페치된 위치를 지워야 하는 상황이 있을 수 있습니다. 예를 들어, 예약이 발생하면 사용자가 이제 &quot;참여&quot;하고 예약 프로세스를 이해하므로 캐시된 위치를 지우는 것이 적절합니다. 만약 그들이 세션 중에 다른 여행을 예약한다면, 그들은 그들의 예약을 안내하기 위해 홈 화면과 검색 결과 화면에 원래 위치가 필요하지 않을 것이다. 캐시에서 위치를 지우고 할인된 두 번째 예약 또는 다른 관련 시나리오에 대한 새 오퍼를 미리 가져오는 것이 더 적절합니다. 세션 중에 예약이 이루어진 경우 홈 화면 및 검색 결과 화면에 논리를 추가하여 새 위치를 미리 가져올 수 있습니다.

이 예에서는 예약이 발생할 때 세션에 대해 미리 가져온 위치만 지웁니다. 이 작업은 `Target.clearPrefetchCache()` 함수를 호출하여 수행됩니다. 아래와 같이 `targetLoadRequest()` 함수 내에 함수를 설정합니다.

```java
Target.clearPrefetchCache()
```

![캐시에서 미리 가져온 위치 지우기](assets/clearPrefetch.jpg)

축하합니다! 이제 앱에 개인화를 위한 프레임워크가 있습니다. 다음 단원에서는 이러한 위치에 매개 변수를 추가하여 개인화 기능을 강화합니다.

**[다음 : &quot;매개 변수 추가&quot; >](add-parameters.md)**
