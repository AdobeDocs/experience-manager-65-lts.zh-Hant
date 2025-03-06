---
title: 記錄檔
description: 執行階段或啟動錯誤等事件會記錄到應用程式伺服器記錄檔中，這些記錄檔可使用任何文字編輯器開啟。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: ff4dce07-725e-4750-9e95-4261b50580bd
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 記錄檔 {#log-files}

執行階段或啟動錯誤等事件會記錄到應用程式伺服器記錄檔中。 如果部署到應用程式伺服器時發生任何問題，您可以使用記錄檔來協助您尋找問題。 您可以使用任何文字編輯器開啟記錄檔。

(JBoss)下列記錄檔位於`[appserver root]/server/'server'/log`目錄中：

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic)網域記錄檔位於`[appserverdomain]`目錄中，而伺服器記錄檔位於`[appserverdomain]/servers/[appserver name]/logs`目錄中：

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere)下列記錄檔位於`[appserver root]/profiles/default/logs/[appserver name]`目錄中：

* SystemErr.log
* SystemOut.log
* StartServer.log
