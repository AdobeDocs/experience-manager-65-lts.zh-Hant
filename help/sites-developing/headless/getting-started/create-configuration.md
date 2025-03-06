---
title: 建立設定Headless快速入門手冊
description: 建立設定，作為在AEM 6.5中開始使用Headless的第一步。
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
exl-id: 6792f5c0-074e-4465-9b84-8be78abd6b8f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 61%

---

# 建立設定Headless快速入門手冊 {#creating-configuration}

在AEM 6.5中開始使用Headless的第一步，是您必須建立設定。

## 什麼是設定？ {#what-is-a-configuration}

設定瀏覽器提供一般 API、內容結構、解析機制用於 AEM 中的設定。

在 AEM Headless 內容管理的環境中，將設定視為 AEM 中的工作區，您可以在其中建立內容模型，該內容模型定義未來內容和內容片段的結構。您可以有多個設定來將這些模型分開。

>[!NOTE]
>
>如果您熟悉[全堆疊 AEM 實作中的頁面範本](/help/sites-authoring/templates.md)，用於管理內容模型之設定的用法是類似的。

## 如何建立設定 {#how-to-create-a-configuration}

系統管理員一次只需建立一個設定，或者在需要新工作區來組織內容模型時建立，這個情況很少發生。出於本快速入門指南的目的，我們只需要建立一個設定。

1. 登入AEM，從主功能表選取&#x200B;**工具>一般>設定瀏覽器**。
1. 提供設定的&#x200B;**標題**。
   * 名稱將根據標題自動產生，並根據[AEM命名慣例進行調整。](/help/sites-developing/naming-conventions.md)。它會成為存放庫中的節點名稱。
1. 檢查以下選項：
   * **內容片段模型**
   * **GraphQL持續查詢**

   ![建立設定](assets/create-configuration.png)

1. 按一下「**建立**」。

如果需要，您可以建立多個設定。設定也可以是巢狀。

>[!NOTE]
>
>根據您的實作需求，除了&#x200B;**內容片段模型**&#x200B;和&#x200B;**GraphQL持續查詢**&#x200B;之外，可能還需要設定選項。

## 後續步驟 {#next-steps}

使用此設定，您現在可以繼續閱讀快速入門指南的第二部分，並[建立內容片段模型。](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
