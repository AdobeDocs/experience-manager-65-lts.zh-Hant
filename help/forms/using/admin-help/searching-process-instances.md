---
title: 搜尋程式執行個體
description: 您可以在「程式搜尋」頁面輸入搜尋條件，以尋找程式執行處理。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e358ee51-c23f-4737-9dcf-3193ed541bbb
source-git-commit: 51342861dd01e659999c19fbe0274e8d3cbcf8c4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 搜尋程式執行個體{#searching-for-process-instances}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以在「程式搜尋」頁面輸入搜尋條件，以尋找程式執行處理。 您可以從Forms Workflow頁面存取「程式搜尋」頁面。 或者，您可以按一下[處理執行個體]頁面上的&#x200B;**搜尋**。

您可以輸入執行一般搜尋的基本條件、執行詳細搜尋的特定屬性，或執行組合搜尋的基本條件和特定屬性的組合。

## 執行一般搜尋 {#perform-a-general-search}

如果您知道流程例項的流程ID，一般搜尋流程會是最合適的。 或者，如果您要尋找一組相關的程式執行個體，或者只有少數程式執行個體正在執行。

輸入執行一般搜尋的基本條件。 如果您輸入多個條件，則會以隱含的AND條件執行搜尋。

1. 在管理控制檯中，按一下「服務> Forms Workflow >程式搜尋」 。
1. 在「程式搜尋」頁面的「一般搜尋」底下，提供下列條件：

   * **處理序識別碼：**&#x200B;識別每個唯一處理序執行個體的正整數。
   * **處理狀態：**&#x200B;從清單中選取狀態。
   * **應用程式：**&#x200B;從清單中選取應用程式。 只會顯示已部署的應用程式。
   * **處理程式名稱 — 版本：**&#x200B;從功能表選取處理程式名稱。 只顯示已部署的流程。

1. 按一下&#x200B;**搜尋**。 便會顯示「處理執行處理」頁面，列出找到的執行處理。

## 執行流程的詳細搜尋 {#perform-a-detailed-search-for-a-process}

您可以輸入特定屬性來執行詳細搜尋。 如果您有許多執行中的程式執行個體，而且需要依特定條件縮小可能的搜尋範圍，則詳細搜尋是最合適的選擇。

1. 在管理控制檯中，按一下「服務> Forms Workflow >程式搜尋」 。
1. 在「程式搜尋」頁面的「詳細搜尋」底下，指定您的第一個條件集：

   * 在「屬性」清單中，選取屬性。
   * 在「篩選」清單中，選取運運算元。
   * 在「值」方塊中，鍵入適合所選屬性的值。

1. 若要新增其他列，請選取「更多篩選器」。 另一組「屬性」、「篩選」和「值」清單會出現，並出現一個「條件」清單。
1. 在「條件」下，選取AND或OR。 視需要重複步驟1到3，進一步縮小搜尋範圍。
1. 若要新增或移除列，請按一下「更多篩選器」或「更少篩選器」。 您可以有一到四列。
1. 按一下&#x200B;**搜尋**。 便會顯示「處理執行處理」頁面，列出找到的執行處理。

另請參閱[關於處理序執行個體狀態](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)。

## 執行流程的組合搜尋 {#perform-a-combined-search-for-a-process}

若要建立同時使用一般和詳細條件的搜尋，請在「程式搜尋」頁面的兩個區域中輸入值。 系統在這兩個區域之間套用隱含的`AND`。

如果搜尋太窄，則找不到例項。
