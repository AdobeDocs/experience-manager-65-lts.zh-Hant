---
title: AEM Forms伺服器甚至在所有服務啟動並執行之前就開始處理檔案。
description: 在所有服務啟動並在JEE伺服器和OSGi伺服器上執行之前，AEM Forms伺服器就會開始處理檔案。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 22dd8daa-b8c6-4e7d-bca3-3958a79fb4b5
source-git-commit: 402b42d8ce5539739205a85d99bcb035d382a036
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 3%

---

# AEM Forms伺服器甚至在所有服務啟動並執行之前就開始處理檔案{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## 問題 {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

在AEM Forms伺服器完全啟動且所有應用程式都啟動並執行之前，AEM Forms伺服器會開始處理檔案。


## 套用至 {#applies-to}

此解決方案適用於JEE伺服器上的AEM Forms和OSGi伺服器上的AEM Forms 。

## 解決方案 {#solution}

若要解決此問題，請在伺服器啟動期間將引數`Dcom.adobe.livecycle.dsc.deferServiceStart=true`新增至[批次檔](/help/sites-deploying/command-line-start-and-stop.md#windows-platform-start-bat-script-example)。
