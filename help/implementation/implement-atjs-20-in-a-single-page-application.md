---
title: 단일 페이지 애플리케이션(SPA)에서 at.js 2.0을 구현하는 방법
description: Adobe Target의 at.js 2.0에서는 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다. SPA(단일 페이지 애플리케이션)에서 at.js 2.0을 구현하려면 다음 단계를 따르십시오.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 단일 페이지 애플리케이션(SPA)에서 Adobe Target의 at.js 2.0 구현

Adobe Target의 `at.js` 2.0은 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다. 이 버전은 단일 페이지 애플리케이션(SPA)과 조화로운 상호 작용을 하도록 `at.js`을(를) 업그레이드하는 데 중점을 두고 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/34780?quality=12&captions=kor)

## SPA에서 at.js 2.0을 구현하는 방법

* 단일 페이지 애플리케이션의 &lt;head>에서 `at.js` 2.0을 구현합니다.
* SPA에서 변경 내용을 볼 때마다 `adobe.target.triggerView()` 함수를 구현합니다. 이를 위해 URL 해시 변경 수신, SPA에서 실행된 사용자 지정 이벤트 수신, `triggerView()` 코드를 응용 프로그램에 직접 포함하기 등 다양한 기술을 사용할 수 있습니다. 특정 단일 페이지 애플리케이션에 가장 적합한 옵션을 선택해야 합니다.
* 보기 이름은 `triggerView()` 함수의 첫 번째 매개 변수입니다. Target의 시각적 경험 작성기에서 간단하고, 명확하고, 고유한 이름을 사용하여 쉽게 선택할 수 있습니다.
* 무한 스크롤링 페이지 중간에 있는 것과 같은 비 SPA 컨텍스트뿐만 아니라 작은 보기 변경 시 보기를 트리거할 수 있습니다.
* `at.js` 2.0 및 `triggerView()`은(는) Adobe Experience Platform Launch과 같은 태그 관리 솔루션을 통해 구현할 수 있습니다.

## at.js 2.0 제한 사항

업그레이드하기 전에 `at.js` 2.0의 다음 제한 사항에 유의하십시오.

* `at.js` 2.0에서는 도메인 간 추적이 지원되지 않습니다.
* mboxOverride.browserIp 및 mboxSession URL 매개 변수는 `at.js` 2.0에서 지원되지 않습니다.
* 이전 함수 mboxCreate, mboxDefine, mboxUpdate는 `at.js` 2.0에서 더 이상 사용되지 않습니다. 기본 콘텐츠가 표시되고 네트워크 요청이 수행되지 않습니다.

## 비디오에 사용되는 라이브러리 바닥글 코드

아래 코드는 비디오 재생 중에 `at.js` 라이브러리의 라이브러리 바닥글 섹션에 추가되었습니다. 이 메서드는 앱이 처음 로드되고 앱의 해시 변경 시 실행됩니다. 정리된 해시 버전을 보기 이름으로 사용하고, 해시가 비어 있으면 &quot;home&quot;을 사용합니다. SPA를 식별하기 위해 코드는 URL에서 &quot;react/&quot; 텍스트를 찾습니다. 이 텍스트는 사이트에서 업데이트해야 할 수 있습니다. 또한 SPA에서 사용자 지정 이벤트에서 `triggerView()`을(를) 실행하거나 코드를 앱에 직접 포함시켜 실행하는 것이 더 적절할 수 있습니다.

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
* [Adobe Target의 SPA VEC(단일 페이지 애플리케이션용 시각적 경험 작성기) 사용](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
