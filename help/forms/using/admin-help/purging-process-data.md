---
title: 清除程式資料
description: 叫用長期程式時產生的程式資料可能會變得太大，導致AEM表單效能降低，並佔用不必要的磁碟空間。 瞭解如何永久刪除處理資料。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 53ce63a3-704a-4da6-b652-362a436f05a7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 清除程式資料 {#purging-process-data}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

叫用長期程式時產生的程式資料可能會變得太大，導致AEM表單效能降低，並佔用不必要的磁碟空間。 當不再需要記錄時，清除處理資料是很好的做法。 AEM forms提供數種清除流程資料的方法：

* 您可以使用管理主控台，執行一次性永久刪除與長期處理相關的過時記錄，或排程定期自動永久刪除。 （請參閱[從工作管理員資料庫](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)中清除記錄。）
* 您可以使用AEM表單Java API和Web服務API，以程式設計方式清除與長期流程相關的流程資料。 (請參閱[使用AEM表單](https://www.adobe.com/go/learn_aemforms_programming_63)進行程式設計中的「清除程式資料」。)
* 使用處理永久刪除工具，根據處理名稱和其他引數永久刪除處理。 如需詳細資訊，請參閱&#x200B;*[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt中的程式清除工具Readme檔案。
