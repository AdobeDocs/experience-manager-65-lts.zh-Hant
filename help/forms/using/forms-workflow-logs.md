---
title: 登入AEM Forms工作流程
description: 瞭解如何偵錯AEM Forms工作流程問題並啟用AEM Forms工作流程的偵錯記錄以檢視記錄。
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 90a44cab-3ecf-4a71-95d4-e8ce2d996980
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 5%

---

# 登入AEM Forms工作流程{#logging-in-aem-forms-workflows}

Forms Workflow步驟提供詳細的記錄檔，可方便您偵錯工作流程相關問題。 啟用AEM Forms工作流程的偵錯記錄以檢視記錄。

依預設，所有記錄資訊都可在&#x200B;**error.log**&#x200B;檔案的&#x200B;*/crx-repository/logs/*&#x200B;目錄中取得。

表單工作流程的偵錯記錄包括：

* 每個工作流程步驟的輸入。 例如：\
  `[DEBUG] "Executing Invoke DDX Process step"`

* 結束每個工作流程步驟。 例如：\
  `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 服務呼叫訊息。 例如：\
  `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 服務結束訊息。 例如：\
  `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 從中繼資料對應讀取的變數。 例如：\
  `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* 以JCR存放庫撰寫的變數。 例如：

  ```verilog
     [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
  ```

* 具有完整棧疊追蹤的例外狀況訊息。 例如：\
  `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 動態步驟中繼資料引數。 例如：

  ```verilog
  [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
   [DEBUG] Locale to be used for Document of Record is <locale>
  ```

以下範例說明「簽署檔案」步驟的記錄：

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

使用記錄來評估：

* 您使用正確的Adobe Sign設定。
* Adobe Sign服務會在成功建立合約後結束。
* 「簽署檔案」步驟結束，並顯示成功訊息。

如果發生例外狀況，您可以檢視完整的棧疊追蹤，以評估錯誤的原因。

## 啟用AEM Forms工作流程的偵錯記錄 {#enable-debug-logging-for-aem-forms-workflows}

請執行以下動作，以啟用AEM Forms工作流程的偵錯記錄：

1. 前往AEM Web主控台設定管理員，網址：

   https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr

1. 選取&#x200B;**[!UICONTROL Sling]** > **[!UICONTROL 記錄檔支援]**。
1. 選取&#x200B;**[!UICONTROL 新增記錄器。]**
1. 選取&#x200B;**[!UICONTROL Debug]**&#x200B;做為&#x200B;**[!UICONTROL 記錄層級]**。
1. 指定記錄檔的位置。 記錄檔的預設位置為： *logs\error.log*
1. 在&#x200B;**[!UICONTROL 記錄器]**&#x200B;欄中指定封裝名稱為&#x200B;**com.adobe.granite.workflow.core**。

   執行這些步驟可儲存&#x200B;**com.adobe.granite.workflow.core**&#x200B;封裝的偵錯記錄檔。 選取&#x200B;**[!UICONTROL +]**&#x200B;並將下列封裝名稱新增至清單：

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
