---
title: 自訂任務的標籤
description: 如何在LiveCycle AEM Forms Workspace中自訂您工作的標簽名稱。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 88f5093c-f249-4e4b-900a-5897f47e513c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 自訂任務的標籤 {#customizing-tabs-for-a-task}

您可以在`Start Process` Uber檢視中自訂`Start Process`元件的標簽名稱，並在`ToDo` Uber檢視中自訂`Task Details`元件。

1. 執行[AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 變更`translation.json`檔案中`tabname`的值。

   例如，將英文的`/apps/ws/locales/en-US/translation.json`變更為下列內容。

   * 對於在啟動程式中啟動的工作，請使用`"startprocess" : {}`區塊中的下列程式碼片段。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 對於待辦事項中的工作，請使用`"todo" : {}`區塊中的下列程式碼片段。

   ```json
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >為所有支援的語言新增對應的機碼值組。
