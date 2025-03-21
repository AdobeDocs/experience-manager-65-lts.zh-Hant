---
title: 瞭解檔案夾結構
description: 如何瞭解AEM Forms工作區原始碼的檔案夾結構以自訂。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
exl-id: 08e6b25c-eef5-4f29-99fa-524f563e7f25
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 瞭解檔案夾結構 {#understanding-the-folder-structure}

AEM Forms工作區元件是使用Backbone在MVC架構上設計。 每個元件都有一個檔案，用於：

* 模型，包含商業邏輯。
* 範本，即包含介面控制項的HTML檔案。
* 作為範本的Controller類別的檢視。

所有元件的資產都會放置在如下所述的資料夾結構中。 若要存取資產，請登入CRXDE Lite並瀏覽至`/libs/ws/js/runtime/`。

**模型**&#x200B;包含骨幹模型。

**個檢視**&#x200B;包含主幹檢視。

**範本**&#x200B;僅包含元件的HTML範本。

**路由**&#x200B;包含通用路由。 路由內的範本資料夾包含HTML程式碼和元件的參考。

**服務**&#x200B;包含呼叫REST端點上Adobe Experience Manager伺服器API的服務介面。

**util**&#x200B;包含可由多個元件使用的一般公用程式。
