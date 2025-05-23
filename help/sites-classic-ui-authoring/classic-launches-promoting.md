---
title: 提升啟動
description: 您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。 提升啟動頁面時，來源頁面的對應頁面會取代為提升頁面的內容。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 1167735d-a13a-438e-bef8-205e27f59f4e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 3%

---

# 提升啟動{#promoting-launches}

您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。 提升啟動頁面時，來源頁面的對應頁面會取代為提升頁面的內容。 提升啟動頁面時，可使用下列選項：

* 僅提升目前頁面還是整個啟動。
* 是否要升級目前頁面的子頁面。
* 是要升級完整啟動項，還是隻升級已變更的頁面。

## 提升啟動頁面 {#promoting-launch-pages}

若要提升頁面，請在編輯要提升的啟動頁面時，執行下列步驟：

1. 在Sidekick的&#x200B;**頁面**&#x200B;索引標籤上，按一下&#x200B;**提升啟動**。
1. 指定要提升的頁面：

   * （預設）若要僅提升目前頁面，請選取&#x200B;**將頁面變更提升至生產版本**。
   * 若要同時提升目前頁面的子頁面，請選取&#x200B;**包含子頁面**。
   * 若要提升啟動項中的所有頁面，請選取&#x200B;**將完整啟動項提升至生產版本**。

1. 若要將生產頁面新增至工作流程封裝，請選取&#x200B;**新增至工作流程封裝**，然後選取工作流程封裝。
1. 按一下&#x200B;**升級**。

## 使用 AEM 工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型來對提升的「啟動」頁面執行大量處理：

1. 建立Workflow封裝。
1. 作者提升Launch頁面時，會將頁面儲存在Workflow套件中。
1. 使用封裝作為裝載啟動工作流程模型。

若要在頁面升級時自動啟動工作流程，請[為封裝節點設定工作流程啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers)。

例如，您可以在作者提升啟動頁面時自動產生頁面啟用請求。 設定工作流程啟動器，以便在修改封裝節點時啟動「請求啟用」工作流程。

![chlimage_1-136](assets/chlimage_1-136.png)
