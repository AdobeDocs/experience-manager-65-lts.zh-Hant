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
hide: true
removedfrom6.5.2025: 'yes'
exl-id: ff4dce07-725e-4750-9e95-4261b50580bd
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '118'
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

* SystemEr.log
* SystemOut.log
* StartServer.log
