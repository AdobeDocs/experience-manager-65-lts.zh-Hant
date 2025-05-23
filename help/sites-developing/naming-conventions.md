---
title: Java內容存放庫中節點的命名慣例
description: 存放庫中的節點會遵守Java內容存放庫的命名慣例
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 36025dac-890e-45ba-adea-a230a5231a0b
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# 命名慣例 {#naming-conventions}

存放庫中的節點會遵循[Java內容存放庫](/help/sites-developing/the-basics.md#java-content-repository)的命名慣例。 不過，AEM對頁面節點名稱實施進一步的慣例。

## 頁面的命名慣例 {#naming-conventions-for-pages}

這些命名慣例會在不同的層級實作：

* JcrUtil： [JCR公用程式](#jcr-utilities)的AEM實作。
* PageManager： [頁面管理員](#page-manager)提供頁面層級作業的方法。
* 根據使用的UI：

   * [標準觸控式UI](#standard-ui)
   * [傳統 UI](#classic-ui)

### jcr公用程式 {#jcr-utilities}

[JcrUtil](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html)是JCR公用程式的AEM實作。 驗證名稱特別需要的是它控制的字元對應以及下列驗證：

* `isValidName`

   * 檢查名稱是否非空白且僅包含有效字元。
   * 可用來檢查建議的名稱是否有效。

* `createValidName`

   * 這會以任意字串建立有效的標籤。
   * 它可用來從標題建立名稱。

### 頁面管理員 {#page-manager}

[PageManager](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html)提供基於[JCRUtil](#jcr-utilities)的頁面層級作業方法。

### 標準 UI {#standard-ui}

標準的觸控式UI：

* 符合下列任一條件時，請根據PageManager的限制，驗證名稱：

   * 提供了頁面標題，以便轉換為節點名稱
   * 提供了明確的節點名稱

### 傳統 UI {#classic-ui}

傳統UI會實施更嚴格的限制：

* 在下列任一情況中，當節點名稱明確時驗證名稱：

   * 提供了頁面標題，以便轉換為節點名稱
   * 提供了明確的節點名稱

* 有效字元（從傳統UI中建立頁面時，即使`PageManagerImpl`允許其他字元，實際上只有這些字元有效）：

   * &#39;a&#39;至&#39;z&#39;
   * &#39;A&#39;至&#39;Z&#39;
   * &#39;0&#39;至&#39;9&#39;
   * _ （底線）
   * `-` （破折號/減號）
