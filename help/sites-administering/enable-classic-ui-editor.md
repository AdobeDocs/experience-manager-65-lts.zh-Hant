---
title: 編輯者
description: 瞭解如何切換回傳統UI編輯器。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 54a97ac0-db9e-4903-b395-b1af87cfd151
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---

# 編輯者{#editor}

依預設，從編輯器切換到傳統UI的功能已停用。

若要在&#x200B;**頁面資訊**&#x200B;功能表中重新啟用&#x200B;**在傳統UI中開啟**&#x200B;選項，請遵循下列步驟。

1. 使用CRXDE Lite尋找下列節點：

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例如

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 使用&#x200B;**覆蓋節點**&#x200B;選項建立覆蓋；例如：

   * **路徑**： `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **覆蓋位置**： `/apps/`
   * **符合節點型別**：作用中（選取核取方塊）

1. 將下列多值文字屬性新增至覆蓋的節點：

   `sling:hideProperties = ["granite:hidden"]`

1. 編輯頁面時，**頁面資訊**&#x200B;功能表中再次提供&#x200B;**在傳統UI中開啟**&#x200B;選項。

   從頁面資訊![在傳統UI中開啟選項](assets/syui-03-2019-02-27-15-19-48.png)
