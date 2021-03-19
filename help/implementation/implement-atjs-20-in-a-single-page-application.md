---
title: 단일 페이지 응용 프로그램에서 at.js 2.0을 구현하는 방법(SPA)
description: Adobe Target의 at.js 2.0은 차세대 클라이언트측 기술에서 개인화를 실행할 수 있는 다양한 기능을 제공합니다. 다음 단계에 따라 단일 페이지 애플리케이션(SPA)에서 at.js 2.0을 구현합니다.
role: Developer
level: 중간
topic: SPA, 아키텍처, 개발
feature: 구현
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# 단일 페이지 애플리케이션(SPA)에서 Adobe Target at.js 2.0 구현

Adobe Target의 `at.js` 2.0은 차세대 클라이언트측 기술에서 개인화를 구현할 수 있는 다양한 기능을 제공합니다. 이 버전은 단일 페이지 애플리케이션(SPA)과의 상호 작용을 원활하게 하도록 `at.js`을 업그레이드하는 데 중점을 두고 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## SPA에서 at.js 2.0을 구현하는 방법

* 단일 페이지 애플리케이션의 &lt;head>에 `at.js` 2.0을 구현합니다.
* SPA에서 보기가 변경될 때마다 `adobe.target.triggerView()` 함수를 구현합니다. URL 해시 변경 내용 수신, SPA에서 실행하는 사용자 지정 이벤트 수신 또는 `triggerView()` 코드를 애플리케이션에 직접 임베드하는 등 다양한 기술을 사용하여 이를 수행할 수 있습니다. 특정 단일 페이지 애플리케이션에 가장 적합한 옵션을 선택해야 합니다.
* 보기 이름은 `triggerView()` 함수의 첫 번째 매개 변수입니다. 간단하고 명확하게 고유한 이름을 사용하여 Target의 시각적 경험 작성기에서 손쉽게 선택할 수 있습니다.
* 작은 보기 변경 내용뿐만 아니라 무한 스크롤 페이지 하단방향 등 SPA이 아닌 컨텍스트에서도 보기를 트리거할 수 있습니다.
* `at.js` 2.0 및 Adobe Experience Platform Launch과 같은 태그 관리 솔루션을 통해 구현할  `triggerView()` 수 있습니다.

## at.js 2.0 제한 사항

업그레이드하기 전에 `at.js` 2.0의 제한 사항에 유의하십시오.

* 도메인 간 추적은 `at.js` 2.0에서 지원되지 않습니다.
* mboxOverride.browserIp 및 mboxSession URL 매개 변수는 `at.js` 2.0에서 지원되지 않습니다.
* 기존 함수 mboxCreate, mboxDefine, mboxUpdate는 `at.js` 2.0에서 더 이상 사용되지 않습니다. 기본 컨텐츠가 표시되고 네트워크 요청이 수행되지 않습니다.

## 비디오에 사용된 라이브러리 바닥글 코드

아래 코드는 비디오 중에 `at.js` 라이브러리의 [라이브러리 바닥글] 섹션에 추가되었습니다. 앱이 처음 로드되고 앱에서 해시 변경 사항이 있을 때 실행됩니다. 해시의 정리 버전을 보기 이름으로 사용하고 해시가 비어 있으면 &quot;홈&quot;을 사용합니다. SPA을 식별하기 위해 코드는 URL에서 &quot;react/&quot; 텍스트를 찾습니다. 이 텍스트는 사이트에서 업데이트해야 합니다. SPA에서 사용자 지정 이벤트의 `triggerView()`을 실행하거나 코드를 앱에 직접 포함하여 실행하는 것이 더 적절할 수도 있습니다.

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## 추가 리소스

* [at.js 2.0의 작동 방식 이해(아키텍처 다이어그램)](understanding-how-atjs-20-works.md)
* [SPA VEC(Visual Experience Composer for Single Page Applications) 사용](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [at.js 1.x에서 at.js 2.0 설명서로 업그레이드](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)