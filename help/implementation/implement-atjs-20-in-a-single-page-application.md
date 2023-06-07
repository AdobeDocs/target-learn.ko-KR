---
title: 단일 페이지 애플리케이션(SPA)에서 at.js 2.0을 구현하는 방법
description: Adobe Target의 at.js 2.0에서는 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다. 다음 단계에 따라 SPA(단일 페이지 애플리케이션)에서 at.js 2.0을 구현합니다.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# 단일 페이지 애플리케이션(SPA)에서 Adobe Target의 at.js 2.0 구현

Adobe Target `at.js` 2.0은 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다. 이 버전은 업그레이드에 중점을 둡니다. `at.js` 단일 페이지 애플리케이션(SPA)과 조화로운 상호 작용을 할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## SPA에서 at.js 2.0을 구현하는 방법

* 구현 `at.js` 2.0인치 &lt;head> 단일 페이지 애플리케이션
* 구현 `adobe.target.triggerView()` SPA에서 보기 변경 사항이 있을 때마다 작동합니다. 이를 위해 URL 해시 변경 수신, SPA에서 실행하는 사용자 지정 이벤트 수신 또는 포함 등 다양한 기법을 사용할 수 있습니다. `triggerView()` 를 애플리케이션에 바로 추가합니다. 특정 단일 페이지 애플리케이션에 가장 적합한 옵션을 선택해야 합니다.
* 보기 이름은 의 첫 번째 매개 변수입니다. `triggerView()` 함수. Target의 시각적 경험 작성기에서 간단하고, 명확하고, 고유한 이름을 사용하여 쉽게 선택할 수 있습니다.
* 무한 스크롤링 페이지 중간에 있는 것과 같은 비 SPA 컨텍스트뿐만 아니라 작은 보기 변경 시 보기를 트리거할 수 있습니다.
* `at.js` 2.0 및 `triggerView()` Adobe Experience Platform Launch과 같은 태그 관리 솔루션을 통해 구현할 수 있습니다.

## at.js 2.0 제한 사항

의 다음 제한 사항을 숙지하십시오. `at.js` 업그레이드 전 2.0:

* 도메인 간 추적이 지원되지 않음 `at.js` 2.0
* mboxOverride.browserIp 및 mboxSession URL 매개 변수는에서 지원되지 않습니다. `at.js` 2.0
* mboxCreate, mboxDefine, mboxUpdate 레거시 함수는에서 더 이상 사용되지 않습니다. `at.js` 2.0. 기본 컨텐츠가 표시되고 네트워크 요청이 수행되지 않습니다.

## 비디오에 사용되는 라이브러리 바닥글 코드

아래 코드가 의 라이브러리 바닥글 섹션에 추가되었습니다. `at.js` 비디오가 재생되는 동안 라이브러리가 표시됩니다. 이 메서드는 앱이 처음 로드되고 앱의 해시 변경 시 실행됩니다. 정리된 해시 버전을 보기 이름으로 사용하고, 해시가 비어 있으면 &quot;home&quot;을 사용합니다. SPA을 식별하기 위해 코드는 URL에서 &quot;react/&quot; 텍스트를 찾으며 이 텍스트를 사이트에서 업데이트해야 할 수 있습니다. SPA을 실행하는 것이 더 적합할 수 있다는 것도 염두에 두십시오 `triggerView()` 사용자 지정 이벤트에서 제외하거나 코드를 앱에 직접 포함시켜 제외합니다.

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
* [단일 페이지 애플리케이션용 Adobe Target 시각적 경험 작성기 사용(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
