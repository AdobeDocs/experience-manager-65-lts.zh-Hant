---
title: 參與工作流程
description: 工作流程通常包括需要人員在頁面或資產上執行活動的步驟。 工作流程會選取執行活動的使用者或群組，並將工作專案指派給該人員或群組。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: aea2daf6-c1e2-4e17-8c3f-6b25c693a45c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 4%

---

# 參與工作流程{#participating-in-workflows}

工作流程通常包括需要人員在頁面或資產上執行活動的步驟。 工作流程會選取執行活動的使用者或群組，並將工作專案指派給該人員或群組。

## 正在處理您的工作專案 {#processing-your-work-items}

您可以執行下列動作以處理工作專案：

* **完成**

  您可以完成專案以允許工作流程進行到下一個步驟。

* **代理人**

  如果已將步驟指派給您，但由於任何原因您無法採取動作，則可以將步驟委派給其他使用者或群組。

  可委派的使用者取決於工作專案的指派者：

   * 如果工作專案已指派給群組，則群組成員可供使用。
   * 如果工作專案已指派給群組，然後又委派給使用者，則群組成員和群組可供使用。
   * 如果工作專案已指派給單一使用者，則無法委派工作專案。

* **後退**

  如果您發現某個步驟或一系列步驟需要重複，您可以後退。 這可讓您選取工作流程中先前發生的步驟，以便重新處理。 工作流程會回到您指定的步驟，然後從那裡繼續。

## 參與工作流程 {#participating-in-a-workflow}

### 已指派工作流程動作的通知 {#notifications-of-assigned-workflow-actions}

當您被指派工作項目時(例如「核准內 **容**」)，會出現各種警報和/或通知：

* 「網站」主控台的&#x200B;**狀態**&#x200B;欄指出頁面在工作流程中：

  ![workflowstatus-1](assets/workflowstatus-1.png)

* 當您或您所屬的群組被指派工作專案作為工作流程的一部分時，該工作專案會出現在您的AEM工作流程收件匣中。

  ![工作流程收件匣](assets/workflowinbox.png)

### 完成參與者步驟 {#completing-a-participant-step}

採取指示的動作後，您可以完成工作專案，讓工作流程繼續進行。 使用以下程式完成工作專案。

1. 選取工作流程步驟，然後按一下頂端導覽列中的&#x200B;**完成**&#x200B;按鈕。
1. 在產生的對話方塊中，選取&#x200B;**下一個步驟**；也就是下一個要執行的步驟。 下拉式清單會顯示所有適當的目的地。 也可以輸入&#x200B;**註解**。

   ![workflowcomplete](assets/workflowcomplete.png)

   列出的步驟數取決於工作流程模型的設計。

1. 按一下&#x200B;**確定**&#x200B;以確認動作。

### 委派參與者步驟 {#delegating-a-participant-step}

使用下列程式委派工作專案。

1. 按一下頂端導覽列中的&#x200B;**委派**&#x200B;按鈕。
1. 在對話方塊中，使用下拉式清單來選取要委派工作專案的&#x200B;**使用者**。 您也可以新增&#x200B;**註解**。

   ![workflowdelegate](assets/workflowdelegate.png)

1. 按一下&#x200B;**確定**&#x200B;以確認動作。

### 對參與者步驟執行後退 {#performing-step-back-on-a-participant-step}

請使用下列步驟來後退。

1. 按一下頂端導覽列中的「後退」按鈕。
1. 在產生的對話方塊中，選取「上一步」；也就是說，要執行的下一個步驟 — 即使該步驟發生在工作流程的前面。 下拉式清單會顯示所有適當的目的地。

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. 按一下「確定」以確認動作。
