---
title: 使用任務
description: 您可以在「工作搜尋」頁面，依使用者名稱或工作ID來搜尋工作。 進一步瞭解使用任務。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: d6a0caed-99fa-4121-ac2e-bc21626ff9e0
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# 使用任務 {#working-with-tasks}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以在「工作搜尋」頁面，依使用者名稱或工作ID來搜尋工作。 搜尋結果會顯示在「工作清單」頁面上，您可以在此頁面存取工作的歷史記錄。 如果使用者擁有太多工，或使用者收到錯誤的任務指派，您也可以重新指派任務。

>[!NOTE]
>
>執行工作搜尋不會傳回以數字元號(#)開頭的使用者名稱結果。 如果可能的話，請避免建立以數字元號開頭的使用者名稱。

## 搜尋與使用者相關聯的工作 {#search-for-tasks-associated-with-a-user}

1. 在管理控制檯中，按一下「服務>表單工作流程>任務搜尋」。
1. 在「搜尋依據」中，選取「使用者名稱」。 如果您知道要搜尋的部分使用者名稱，請在方塊中鍵入該名稱。 按一下「尋找使用者」。
1. 便會顯示「尋找使用者」頁面。 您可以依使用者名稱或電子郵件來搜尋，進一步縮小搜尋範圍。 當您找到要尋找的使用者時，請選取名稱旁的單選按鈕，然後按一下「確定」。
1. 依預設，任務搜尋會尋找目前指派給使用者的任務。 若要搜尋先前指派給使用者的工作，請選取「顯示未指派的工作」。 若要搜尋使用者已完成的工作，請選取「顯示已完成的工作」。
1. 按一下「搜尋」。 便會顯示「工作清單」頁面，列出搜尋結果。

## 知道任務識別碼時搜尋任務 {#search-for-a-task-when-you-know-its-task-id}

1. 在管理控制檯中，按一下「服務>表單工作流程>任務搜尋」。
1. 在搜尋依據中，選取工作ID，然後在方塊中輸入工作ID。
1. 按一下「搜尋」。 便會顯示「工作清單」頁面，列出搜尋結果。

## 使用任務清單 {#working-with-the-task-list}

作業搜尋結果會顯示在「作業清單」頁面上。 您可以選取工作以開啟「工作歷史記錄」頁面。 從那裡，您可以將任務指派給其他使用者。

這些任務會顯示以下資訊：

**任務識別碼：**&#x200B;當任務具現化（由使用者起始）時，表單工作流程所指派的正整數。 您可以使用此識別碼來追蹤整個生命週期中的任務。 按一下工作ID可檢視工作歷程記錄的詳細資訊，或將工作重新指派給其他使用者。

**狀態：**&#x200B;已指派表示任務目前已指派給使用者。 未指派表示任務先前已指派給使用者。 狀態也可以是「已完成」。

**活動：**&#x200B;顯示產生工作的初始作業或程式作業的表單和名稱。

**處理序識別碼：**&#x200B;當處理序具現化時（亦即，當使用者或自動化步驟起始處理序時），表單工作流程所指派的正整數。 您可以使用此識別碼來追蹤流程例證整個生命週期。

**處理序名稱 — 版本：**&#x200B;處理序的名稱（如Workbench中所定義）。

**應用程式：**&#x200B;處理序所屬的應用程式名稱（如Workbench中所定義）。

**建立日期：**&#x200B;建立工作的日期和時間。

## 檢視工作歷史記錄及重新指派工作 {#viewing-task-history-and-reassigning-tasks}

「作業歷史記錄」頁面會顯示已指派給特定作業的使用者和群組清單。

對於每個任務指派，清單會顯示下列資訊：

**名稱：**&#x200B;使用者的名稱。

**狀態：**&#x200B;已指派表示任務目前已指派給使用者。 未指派表示任務先前已指派給使用者。

**工作清單識別碼：**&#x200B;工作所屬使用者佇列的數值識別碼。 一個程式可以在多個使用者之間共用。

**型別：**&#x200B;表示工作已指派的方式：

**初始：**&#x200B;最初指派給使用者的是工作。

**轉寄：**&#x200B;原始任務擁有者已將任務指派給其他使用者。

**拒絕：**&#x200B;轉送的任務被拒絕，或任務在未完成的情況下傳回至工作清單。

**宣告：**&#x200B;使用者在共用工作清單中宣告工作。

**提升：**&#x200B;經過的預定時間（如Workbench中的使用者動作中所設定），使用者未進行互動，且另一個使用者已被指派此工作。

**諮詢：**&#x200B;工作擁有者已將此工作轉送給其他使用者，以諮詢使用者，他可以開啟表單、儲存資料、修改附件和附註，但無法完成此步驟。 使用者必須將任務傳回給與使用者諮詢的任務擁有者。

**管理員重新指派：**&#x200B;管理員已重新指派工作。

**指派日期：**&#x200B;指派工作給使用者的日期和時間。

### 指派新使用者給任務 {#assigning-a-new-user-to-a-task}

「指派使用者」頁面會列出可指派給任務的使用者。 您可以按一下「工作歷史記錄」頁面上的「指派新使用者」來存取「指派使用者」頁面。

1. 在「指派使用者」頁面的「搜尋」方塊中，輸入部分或所有必要的使用者名稱或電子郵件地址。
1. 在「使用」下，選取「名稱」或「電子郵件地址」，然後按一下「尋找」。 將顯示符合搜尋的使用者。
1. 從清單中選取使用者，然後按一下「確定」。 便會顯示「工作歷史記錄」頁面，其中包含新的使用者指派。
