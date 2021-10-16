---
title: 단일 페이지 애플리케이션(SPA)에서 at.js 2.0을 구현하는 방법
description: Adobe Target의 at.js 2.0에서는 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다. 다음 단계에 따라 단일 페이지 애플리케이션(SPA)에서 at.js 2.0을 구현하십시오.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 단일 페이지 애플리케이션(SPA)에서 Adobe Target의 at.js 2.0 구현

Adobe Target의 `at.js` 2.0에서는 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다. 이 버전은 단일 페이지 애플리케이션(SPA)과 조화로운 상호 작용을 하도록 `at.js` 을 업그레이드하는 데 주력하고 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## SPA에서 at.js 2.0을 구현하는 방법

* 단일 페이지 애플리케이션의 &lt;head>에서 `at.js` 2.0을 구현합니다.
* SPA에서 보기가 변경될 때마다 `adobe.target.triggerView()` 함수를 구현합니다. URL 해시 변경 수신, SPA에서 실행한 사용자 지정 이벤트 수신 또는 `triggerView()` 코드를 애플리케이션에 직접 포함하는 등 다양한 기술을 사용하여 이를 수행할 수 있습니다. 특정 단일 페이지 애플리케이션에 가장 적합한 옵션을 선택해야 합니다.
* 보기 이름은 `triggerView()` 함수의 첫 번째 매개 변수입니다. 간단하고 명료하고 고유한 이름을 사용하여 Target의 시각적 경험 작성기에서 쉽게 선택할 수 있습니다.
* 작은 보기 변경 내용뿐만 아니라 무한 스크롤링 페이지 하단방향 등의 비 SPA 컨텍스트에서도 보기를 트리거할 수 있습니다.
* `at.js` 2.0 및  `triggerView()` 는 Adobe Experience Platform Launch 등의 태그 관리 솔루션을 통해 구현할 수 있습니다.

## at.js 2.0 제한 사항

업그레이드하기 전에 `at.js` 2.0의 다음 제한 사항을 알아 두십시오.

* 도메인 간 추적은 `at.js` 2.0에서 지원되지 않습니다
* mboxOverride.browserIp 및 mboxSession URL 매개 변수는 `at.js` 2.0에서 지원되지 않습니다
* 기존 함수 mboxCreate, mboxDefine, mboxUpdate는 `at.js` 2.0에서 더 이상 사용되지 않습니다. 기본 콘텐츠가 표시되고 네트워크 요청이 수행되지 않습니다.

## 비디오에 사용된 라이브러리 바닥글 코드

아래 코드가 비디오 중에 `at.js` 라이브러리의 라이브러리 바닥글 섹션에 추가되었습니다. 앱이 처음 로드되고 앱의 해시 변경 시 실행됩니다. 이 섹션에서는 해시의 정리된 버전을 보기 이름으로 사용하고 해시가 비어 있으면 &quot;home&quot;을 사용합니다. SPA을 식별하기 위해 코드는 URL에서 &quot;react/&quot; 텍스트를 찾으며, 이 텍스트는 사이트에서 업데이트해야 할 가능성이 높습니다. SPA에서 사용자 지정 이벤트의 `triggerView()`을 실행하거나 코드를 앱에 직접 포함시켜 실행하는 것이 더 적절할 수도 있음을 명심하십시오.

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

* [at.js 2.0 작동 방식 이해(아키텍처 다이어그램)](understanding-how-atjs-20-works.md)
* [단일 페이지 애플리케이션(SPA VEC)에 Adobe Target의 시각적 경험 작성기 사용](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [at.js 1.x에서 at.js 2.0으로 업그레이드 설명서](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/upgrading-from-atjs-1x-to-atjs-20.html?lang=en)
