---
title: 更新您的內容片段，以達到最佳化 GraphQL 篩選
description: 瞭解如何更新您的內容片段，以用於Adobe Experience Manager中最佳化的GraphQL篩選，以進行Headless內容傳送。
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
exl-id: 40211033-7084-4117-a3e2-73e504283266
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 49%

---

# 更新您的內容片段，以達到最佳化 GraphQL 篩選 {#updating-content-fragments-for-optimized-graphql-filtering}

若要最佳化 GraphQL 篩選器的效能，可執行一個程序來更新您的內容片段。

>[!NOTE]
>
>更新內容片段後，您可以依照[最佳化 GraphQL 查詢](/help/sites-developing/headless/graphql-api/graphql-optimization.md)的建議進行。

## 先決條件 {#prerequisites}

請確定您至少有6.5.17.0個AEM版本。

## 更新您的內容片段 {#updating-content-fragments}

若要執行此程式，請使用下列步驟：

1. [設定&#x200B;**內容片段移轉工作設定**&#x200B;的OSGi設定](/help/sites-deploying/configuring-osgi.md)：

   ![OSGi內容片段移轉工作設定](assets/cfm-graphql-update-01.png "OSGi內容片段移轉工作設定")

1. 在對話方塊中，設定這兩個引數如下：

   * **ContentFragmentMigration：Enabled** ： `1`
   * **ContentFragmentMigration：強制** ： `1`

1. **儲存**&#x200B;規格 — 更新程式開始。

1. 請等候程式完成。 當屬性`cfGlobalVersion`出現在`/content/dam`上且設定為`1`時，程式已完成。

1. 返回OSGi設定以停用程式。

   在&#x200B;**內容片段移轉工作設定**&#x200B;的對話方塊中，設定這兩個引數如下：

   * **ContentFragmentMigration：Enabled** ： `0`
   * **ContentFragmentMigration：強制** ： `0`

## 限制 {#limitations}

留意以下限制：

* GraphQL 篩選器的效能最佳化只有在完全更新所有內容片段後才有可能 (由 JCR 節點 `/content/dam` 的 `cfGlobalVersion` 屬性存在來表示)

* 如果在執行更新程序後從內容套組 (使用 `crx/de`) 匯入內容片段，則在再次執行更新程序之前，GraphQL 查詢結果中不會考慮這些內容片段。
