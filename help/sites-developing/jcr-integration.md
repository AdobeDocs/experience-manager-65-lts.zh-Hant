---
title: JCR整合
description: 瞭解您需要在JCR層級整合Adobe Experience Manager時的一些提示。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6c5715f8-ff7e-47c3-8469-f97b6ea6fe03
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# JCR整合{#jcr-integration}

## 與JCR API相比，偏好Sling Resource API {#prefer-the-sling-resource-api-to-jcr-api}

Sling API在比JCR API更高、更抽象的層級上運作。 這可讓您的程式碼可重複使用且獨立於基礎儲存空間。 這可讓您視需要透過ResourceProvider機制納入外部虛擬資料較為容易。

## 儘可能避免查詢 {#avoid-queries-wherever-possible}

導覽存放庫以擷取資料的速度永遠比執行查詢快。 在某些情況下需要查詢，例如一般使用者查詢或需要從整個存放庫尋找結構化內容，但對於所有其他情況，最好導覽至必要的節點。 轉譯器邏輯中應一律避免查詢，例如導覽元件、「最近專案清單」、專案計數等。 在這些情況下，最好逐步瀏覽階層或預先快取結果，以便在轉譯時可直接使用。

## 限制JCR觀察的範圍 {#restrict-the-scope-of-jcr-observation}

在監聽存放庫中的事件時，請務必儘可能縮小範圍。 例如，在`/etc/mycompany`聆聽事件比在`/etc`聆聽要好得多。 永遠不要接聽存放庫根目錄中的事件。 此外，請確定回呼方法會在沒有其他可做的事情時儘快執行。

## 不再使用JCR管理員存取權 {#eliminate-use-of-jcr-admin-access}

自AEM 6起，已棄用登入管理，亦不建議從ResourceResolverFactory取得管理工作階段。 而是應該為需要這種存取型別的後台作業建立服務帳戶，並且可以使用ResourceResolverFactory來取得此帳戶的ResourceResolver。
