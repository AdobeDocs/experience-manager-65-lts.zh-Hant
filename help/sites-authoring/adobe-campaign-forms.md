---
title: 在Adobe Experience Manager中建立Adobe Campaign Forms
description: Adobe Experience Manager可讓您建立並使用與您網站上的Adobe Campaign互動的表單
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
exl-id: 6a72ba56-8222-4853-adc6-ee8f3d395d9d
source-git-commit: 2edf37c2d6bb04b418618f2780f773ab37559114
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 1%

---

# 在AEM中建立Adobe Campaign Forms {#creating-adobe-campaign-forms-in-aem}

AEM可讓您建立並使用與您網站上的Adobe Campaign互動的表單。 特定欄位可插入您的表單，並對應至Adobe Campaign資料庫。

您可以管理新的連絡人訂閱、取消訂閱和使用者設定檔資料，同時將其資料整合到您的Adobe Campaign資料庫中。

若要在AEM中使用Adobe Campaign表單，您必須依照本檔案所述的步驟操作：

1. 讓範本可供使用。
1. 建立表單。
1. 編輯表單內容。

預設提供三種特定於Adobe Campaign的表單型別：

* 儲存設定檔
* 訂閱服務
* 取消訂閱服務

這些表單會定義一個URL引數，此引數接受Adobe Campaign設定檔的加密主要金鑰。 表單會根據此URL引數更新相關Adobe Campaign設定檔的資料。

雖然您是獨立建立這些表單，但在典型的使用案例中，您會在電子報內容內產生表單頁面的個人化連結，讓收件者可以開啟連結，並調整其設定檔資料（無論是取消訂閱、訂閱或更新其設定檔）。

表單會根據使用者自動更新。 如需詳細資訊，請參閱[編輯表單內容](#editing-form-content)。

## 讓範本可供使用 {#making-a-template-available}

您必須先在AEM應用程式中提供不同的範本，才能建立Adobe Campaign專用的表單。

若要這麼做，請參閱[範本檔案](/help/sites-developing/templates.md#template-availability)。

## 建立表單 {#creating-a-form}

首先，檢查作者與發佈執行個體之間的連線，以及Adobe Campaign是否正常運作。 請參閱[整合Adobe Campaign Standard](/help/sites-administering/campaignstandard.md)或[整合Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md)。

>[!NOTE]
>
>當使用Adobe Campaign Classic或Adobe Campaign Standard時，請確定頁面&#x200B;**jcr**&#x200B;節點上的&#x200B;**acMapping:content**&#x200B;屬性分別設為&#x200B;**mapRecipient**&#x200B;或&#x200B;**profile**
>

1. 在AEM的Sites中，導覽至您要建立頁面的位置。
1. 建立頁面並選取&#x200B;**Adobe Campaign Classic設定檔**&#x200B;或&#x200B;**Adobe Campaign Standard設定檔**，然後按一下&#x200B;**下一步**。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果無法使用所需的範本，請參閱[範本可用性](/help/sites-developing/templates.md#template-availability)。

1. 在&#x200B;**名稱**&#x200B;欄位中，新增頁面名稱。 必須為有效的JCR名稱。
1. 在&#x200B;**標題**&#x200B;欄位中輸入標題，然後按一下&#x200B;**建立**。
1. 開啟頁面並選取&#x200B;**開啟屬性**，然後在雲端服務中新增Adobe Campaign設定並選取核取記號以儲存您的變更。

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. 在頁面的&#x200B;**表單開始**&#x200B;元件中，選取它的表單型別 — **訂閱、取消訂閱、**&#x200B;或&#x200B;**儲存設定檔**。 每個表單只能有一個型別。 您現在可以[編輯表單內容](#editing-form-content)。

## 編輯表單內容 {#editing-form-content}

Adobe Campaign專用的Forms具有特定元件。 這些元件有選項可讓您將表單的每個欄位連結到Adobe Campaign資料庫中的欄位。

>[!NOTE]
>
>如果無法使用所需的範本，請參閱[讓範本可用。](/help/sites-authoring/campaign.md)

本節僅詳細說明Adobe Campaign的特定連結。 如需如何在Adobe Experience Manager中使用表單的一般概覽的詳細資訊，請參閱[編輯模式元件](/help/sites-authoring/default-components-foundation.md)。

1. 選取「**開啟屬性**」，然後在Cloud Services中新增Adobe Campaign設定，並選取核取記號以儲存變更。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 在頁面上的&#x200B;**表單開始**&#x200B;元件中，按一下「設定」圖示。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 按一下「**進階**」標籤，並選取它的表單型別 — **訂閱、取消訂閱、**&#x200B;或&#x200B;**儲存設定檔**，然後按一下「**確定」。**&#x200B;每個表單只能有一個型別。

   * **Adobe Campaign：儲存設定檔**：可讓您在Adobe Campaign中建立或更新收件者（預設值）。
   * **Adobe Campaign：訂閱服務**：可讓您在Adobe Campaign中管理收件者的訂閱。
   * **Adobe Campaign：取消訂閱服務**：可讓您取消Adobe Campaign中收件者的訂閱。

1. 每個表單上都必須有&#x200B;**加密的主要金鑰**&#x200B;元件。 此元件會定義哪個URL引數用於接受Adobe Campaign設定檔的加密主要金鑰。 在「元件」中選取Adobe Campaign ，只顯示元件。
1. 將元件&#x200B;**加密的主要金鑰**&#x200B;拖曳至表單（任何位置），然後按一下&#x200B;**組態**&#x200B;圖示。 在&#x200B;**Adobe Campaign**&#x200B;索引標籤中，指定URL引數的任何名稱。 按一下核取記號以儲存變更。

   產生的此表單連結需要使用此URL引數，並指派給Adobe Campaign設定檔的加密主要金鑰。 加密的主要金鑰必須正確以URL （百分比）編碼。

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. 視需要新增元件至表單，例如文字欄位、日期欄位、核取方塊欄位、選項欄位等。 如需每個元件的詳細資訊，請參閱[Adobe Campaign表單元件](/help/sites-authoring/adobe-campaign-components.md)。
1. 按一下「組態」圖示以開啟元件。 例如，在&#x200B;**文字欄位（行銷活動）**&#x200B;元件中，變更標題和文字。

   按一下&#x200B;**Adobe Campaign**，將表單欄位對應至Adobe Campaign中繼資料變數。 當您提交表單時，對應的欄位會在Adobe Campaign中更新。 變數選擇器中僅提供具有相符型別的欄位（例如，文字欄位的字串變數）。

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >您可以依照下列指示，新增/移除顯示在收件者表格中的欄位： [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. 按一下&#x200B;**發佈頁面**。 頁面已在您的網站上啟動。 您可以前往AEM發佈執行個體來檢視它。 您也可以[測試表單](#testing-a-form)。

   >[!CAUTION]
   >
   >您需要提供雲端服務匿名使用者的讀取許可權，才能在發佈上使用表單。 但是，請注意向匿名使用者提供讀取許可權的潛在安全性問題，並務必透過例如設定Dispatcher來緩解此問題。

## 測試表單 {#testing-a-form}

建立表單並編輯表單內容後，您可能想要手動測試表單是否如預期般運作。

>[!NOTE]
>
>每個表單上都必須有&#x200B;**已加密的主索引鍵**&#x200B;元件。 在「元件」中選取Adobe Campaign ，只顯示元件。
>
>雖然您在此程式中手動輸入電話號碼，但實際上，使用者會在電子報中取得此頁面的連結（無論是取消訂閱、訂閱或更新您的設定檔）。 頁面會根據使用者自動更新。
>
>若要建立該連結，請使用變數&#x200B;**主要資源識別碼** (Adobe Campaign Standard)或&#x200B;**加密的識別碼** (Adobe Campaign Classic) (例如，在&#x200B;**Text &amp; Personalization （行銷活動）**&#x200B;元件中)，其會連結至Adobe Campaign中的epk。

若要這麼做，您需要手動取得Adobe Campaign設定檔的EPK，然後將其附加至URL：

1. 若要取得Adobe Campaign設定檔的加密主要金鑰(EPK)：

   * 在Adobe Campaign Standard中 — 導覽至&#x200B;**設定檔與對象** > **設定檔**，其中會列出現有的設定檔。 請確定表格在欄中顯示&#x200B;**主要資源識別碼**&#x200B;欄位（這可以按一下/點選&#x200B;**設定清單**&#x200B;來設定）。 複製所需設定檔的主要資源識別碼。
   * 在Adobe Campaign Classic中，移至&#x200B;**設定檔和目標** > **收件者**，其中會列出現有的設定檔。 請確定資料表在資料行中顯示&#x200B;**加密識別碼**&#x200B;欄位（若要設定此專案，請在專案上按一下滑鼠右鍵，並選取&#x200B;**設定清單……**）。 複製所需設定檔的加密識別碼。

1. 在AEM中，開啟發佈執行個體上的表單頁面，並將步驟1中的EPK附加為URL引數：使用您在編寫表單時先前在EPK元件中定義的相同名稱（例如： `?epk=...`）
1. 此表單現在可用於修改與連結Adobe Campaign設定檔相關聯的資料和訂閱。 修改部分欄位並提交表單後，您可以在Adobe Campaign中驗證適當的資料是否已更新。

在驗證表單後，Adobe Campaign資料庫中的資料就會更新。
