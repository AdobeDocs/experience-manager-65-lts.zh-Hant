---
title: 編輯器限制
description: 觸控式UI中的編輯器會使用覆蓋來與受限於iframe中的內容互動。 這個互動會對編輯器的使用以及開發人員造成一些限制。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 9f66c1c5-0fe7-47be-ad78-ef4548e4e26b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 6%

---

# 編輯器限制{#editor-limitations}

觸控式UI中的編輯器會使用覆蓋來與受限於iframe中的內容互動。 此互動會對編輯器的使用以及開發人員造成一些限制。 本頁面會概述這些限制，並儘可能提供解決方案或因應措施。

## 功能限制 {#functional-limitations}

使用編輯器編寫頁面時，作者可能會遇到下列功能限制。

### 連結未啟用 {#links-not-active}

當[編輯頁面](/help/sites-authoring/editing-content.md)時，連結未啟用。

* [切換到&#x200B;**預覽**&#x200B;模式](/help/sites-authoring/editing-content.md#preview-mode)以使用內容中的連結進行瀏覽。

### 結構頁面 {#structure-pages}

頁面不能命名為`structure`。 名稱為`structure`的頁面無法在頁面編輯器中編輯。

## CSS限制 {#css-limitations}

開發人員在編輯器與CSS的互動中可能會遇到下列限制。

### 絕對定位的元素 {#absolutely-positioned-elements}

絕對定位的元素可能會在覆蓋的位置造成問題。

* 如果發生這種狀況，請確定絕對位置元素的維度是否正確，因為編輯器會建立具有相同維度的覆蓋。

### vh單位 {#vh-units}

不支援`vh`個單位，因為iframe高度必須由Adobe Experience Manager (AEM)自動調整。

### 固定背景影像 {#fixed-background-images}

固定背景影像可能無法在捲動時顯示為固定影像，因為它內嵌於iframe中。

* 在標題列動作中選取&#x200B;**以發佈的形式檢視頁面**&#x200B;可正確顯示頁面。

### 100%高度 {#height}

頁面的內文元素不支援100%高度。

* 暫行解決方法是透過「拉伸」body元素來實施全熒幕主體，如下所示：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 邊界收合 {#margin-collapsing}

如果body元素的第一個子元素有邊界，則會出現邊界收合問題。

* 解決方法是在主體元素層級新增一個清除碼，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
