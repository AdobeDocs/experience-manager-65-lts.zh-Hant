---
title: 管理工作流程
description: 瞭解如何使用工作流程自動化Adobe Experience Manager活動。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
exl-id: 330f5cc5-1af4-4777-b386-b0755e6781df
source-git-commit: d37df3dc09122909adbb62ede6634939af105e06
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---

# 管理工作流程{#administering-workflows}

工作流程可讓您自動化Adobe Experience Manager (AEM)活動。 工作流程：

* 由一系列以特定順序執行的步驟組成。

   * 每個步驟都會執行不同的活動；例如等待使用者輸入、啟用頁面或傳送電子郵件訊息。

* 可與存放庫中的資產、使用者帳戶和AEM服務互動。
* 可以協調涉及AEM任何層面的複雜活動。

貴組織已建立的業務處理可以表示為工作流程。 例如，發佈網站內容的程式通常包括各種利害關係人的核准和簽核等步驟。 這些程式可以實作為AEM工作流程，並套用至內容頁面和資產。

* [開始工作流程](/help/sites-administering/workflows-starting.md)
* [管理工作流程例項](/help/sites-administering/workflows-administering.md)
* [管理工作流程存取權](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>如需進一步詳細資訊，請參閱：
>
>* 套用及參與工作流程： [使用工作流程](/help/sites-authoring/workflows.md)。
>* 正在建立工作流程模型並擴充工作流程功能： [開發和擴充工作流程](/help/sites-developing/workflows.md)。
>* 改善使用重要伺服器資源的工作流程效能： [並行工作流程處理](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)。
>

## 工作流程模型與例項 {#workflow-models-and-instances}

AEM中的[工作流程模型](/help/sites-developing/workflows.md#model)是商務程式的表示與實作：

* 它們通常會在頁面或資產上採取行動，以達到特定結果。
* 這些頁面和/或資產稱為工作流程裝載。
* 工作流程模型包含一系列執行特定任務的步驟。
* 當工作流程進行時，裝載會在不同步驟之間傳遞。

啟動（執行）工作流程模型時，會建立工作流程例項。 工作流程模型可多次啟動，每次都產生不同的工作流程例項。 對於每個例項，工作流程模型定義的步驟都會執行。

>[!CAUTION]
>
>執行的步驟是在產生執行個體時由工作流程模型&#x200B;*定義的步驟*。 如需詳細資訊，請參閱[開發和擴充工作流程 — 模型](/help/sites-developing/workflows.md#model)。

工作流程例項會進行下列生命週期：

1. 工作流程模型已啟動，且工作流程例項已建立並執行。

   1. 模型啟動時，會識別工作流程例項的裝載。
   1. 例項實際上是模型的副本（在建立時）。
   1. AEM作者、管理員或服務可以啟動工作流程模型。

1. 工作流程模型的第一個步驟就是執行。
1. 步驟已完成，且工作流程引擎會使用模型來決定下一個要執行的步驟。
1. 會執行並完成工作流程模型中的後續步驟。
1. 完成最後一個步驟時，工作流程例項即完成並封存。

AEM隨附許多實用的工作流程模型。 此外，您組織中的開發人員可以建立自訂工作流程模型，以針對您的業務流程的特定需求量身打造。

## 工作流程步驟 {#workflow-steps}

執行工作流程步驟時，它們會與工作流程例項相關聯。 工作流程執行個體的歷史記錄包含針對執行個體執行的每個步驟的相關資訊。 此資訊對於調查執行期間發生的問題很有用。

使用者或服務會根據步驟型別執行工作流程步驟：

* 當使用者執行步驟時，會為其指派放置在其收件匣中的工作專案。 使用者負責手動完成步驟，讓工作流程執行個體進行中。
* 服務執行步驟時，工作流程執行個體會在完成後自動進行到下一個步驟。

>[!NOTE]
>
>如果發生錯誤，服務/步驟實作應處理錯誤案例的行為。 工作流程引擎本身會重試工作，然後記錄錯誤並停止執行個體。

## 工作流程狀態和動作 {#workflow-status-and-actions}

工作流程可以有下列其中一種狀態：

* **正在執行**：工作流程執行個體正在執行。
* **已完成**：工作流程執行個體已成功結束。

* **已暫停**：將工作流程標示為已暫停。 不過，請參閱下面的注意事項來瞭解此狀態的已知問題。
* **已中止**：工作流程執行個體已終止。
* **過時**：工作流程執行個體的進度需要執行背景工作，但在系統中找不到工作。 當執行工作流程發生錯誤時，可能會發生這種情況。

>[!NOTE]
>
>當執行「程式步驟」導致錯誤時，該步驟會出現在管理員的「收件匣」中，且工作流程狀態為&#x200B;**正在執行**。

當您必須介入工作流程例項的正常進度時，根據狀態，您可以對執行中的工作流程例項執行動作：

* **暫停**：暫停會將工作流程狀態變更為已暫停。 請參閱下列警告：

>[!CAUTION]
>
>將工作流程狀態標示為「暫停」有已知問題。 在此狀態下，可以對收件匣中暫停的工作流程專案採取行動。

* **繼續**：使用相同的設定，在暫停的工作流程的執行點重新啟動暫停的工作流程。
* **終止**：結束工作流程執行並將狀態變更為&#x200B;**已中止**。 中止的工作流程執行個體無法重新啟動。
