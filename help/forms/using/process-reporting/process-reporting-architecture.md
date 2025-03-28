---
title: 程式報告的運作方式
description: 構成AEM Forms on JEE Process Reporting的服務說明和Process Reporting UI簡介
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: c59e5a1d-a066-48e7-a57e-c28cbb959719
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 程式報告的運作方式{#how-process-reporting-works}

程式報告是JEE上AEM Forms的報告模組。

程式報告可讓您執行AEM Forms程式和工作的報告。

Process Reporting使用內嵌的Process Reporting存放庫來發佈Forms資料。 然後使用該資料執行報表。

「程式報表」包含下列模組：

* [ProcessDataPublisher服務](#processdatapublisher-service-br-p)
* [ProcessDataStorage服務](#processdatastorageprovider-service-br-p)
* [OSGi服務](#osgi-service-br-p)
* [查詢資料servlet](#querydataservlet-service-br-p)
* [程式報告使用者介面](#process-reporting-user-interface-br-p)

## 程式報告架構 {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## 程式報告模組 {#process-reporting-modules}

### ProcessDataPublisher服務 {#processdatapublisher-service-br}

ProcessDataPublisher伺服器會定期在AEM Forms資料庫上執行，並擷取上次執行服務後變更的資料。 然後會將資料發佈至「程式資料儲存」服務。

如需設定服務的詳細資訊，請參閱[設定ProcessDataPublisher服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)。

### ProcessDataStorageProvider服務 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider服務會從ProcessDataPublisher服務接收處理作業資料，並將資料儲存到Process Reporting儲存庫。

如需設定服務的詳細資訊，請參閱[設定ProcessDataStorageProvider服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)。

### OSGi服務 {#osgi-service-br}

QueryDataServlet使用此服務從Process Reporting存放庫取得報表資料。

### QueryDataServlet服務 {#querydataservlet-service-br}

QueryDataServlet服務接受來自Process Reporting使用者介面的查詢。

然後，此服務會使用OSGi服務來取得相關報表資料、處理資料，並將資料傳回至使用者介面。

### 程式報告使用者介面 {#process-reporting-user-interface-br}

「程式報表」使用者介面是Web瀏覽器介面。 您可以使用此介面來檢視從AEM Forms資料庫發佈的程式與工作資訊。

如需程式報表使用者介面的簡介，請參閱[程式報表使用者介面](/help/forms/using/process-reporting/introduction-process-reporting.md)。

### QueryDataServlet服務 {#querydataservlet-service-br-1}

QueryDataServlet服務接受來自Process Reporting使用者介面的查詢。

然後，此服務會使用OSGi服務來取得相關報表資料、處理資料，並將資料傳回至使用者介面。

### 自訂報表 {#custom-reports-br}

您可以建立自己的自訂報表，並在「流程報表」使用者介面的「自訂報表」標籤中顯示這些報表。

如需建立自訂報表的步驟，請參閱文章[程式報表中的自訂報表](/help/forms/using/process-reporting/process-reporting-custom-reports.md)中的「建立自訂報表」。
