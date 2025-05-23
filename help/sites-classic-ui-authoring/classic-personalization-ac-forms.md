---
title: 在AEM中建立Adobe Campaign Forms
description: AEM可讓您建立並使用與您網站上的Adobe Campaign互動的表單。 特定欄位可插入您的表單，並對應至Adobe Campaign資料庫。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
exl-id: 3a39c4ba-353a-41ee-bfe6-e7eb4323f170
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# 在AEM中建立Adobe Campaign Forms{#creating-adobe-campaign-forms-in-aem}

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

首先，檢查作者與發佈執行個體之間的連線，以及Adobe Campaign是否正常運作。 請參閱[與Adobe Campaign Standard整合](/help/sites-administering/campaignstandard.md)或[與Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md)整合。

>[!NOTE]
>
>當使用Adobe Campaign 6.1.x或Adobe Campaign Standard時，請確定頁面&#x200B;**jcr：content**&#x200B;節點上的&#x200B;**acMapping**&#x200B;屬性分別設為&#x200B;**mapRecipient**&#x200B;或&#x200B;**profile**
>

### 建立表單 {#creating-a-form}

1. 在siteadmin中開始。
1. 捲動檢視樹狀結構，以抵達您要在所選網站中建立表單的位置。
1. 選取&#x200B;**新增** > **新增頁面……**。
1. 選取&#x200B;**Adobe Campaign設定檔(AC 6.1)**&#x200B;或&#x200B;**Adobe Campaign設定檔(ACS)**&#x200B;範本，然後輸入頁面屬性。

   >[!NOTE]
   >
   >如果範本無法使用，請參閱[讓範本可用](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)區段。

1. 按一下&#x200B;**建立**&#x200B;以建立表單。

   ![chlimage_1-187](assets/chlimage_1-187.png)

   您可以[編輯並設定表單的內容](#editing-form-content)。

## 編輯表單內容 {#editing-form-content}

Adobe Campaign專用的Forms具有特定元件。 這些元件有選項可讓您將表單的每個欄位連結到Adobe Campaign資料庫中的欄位。

>[!NOTE]
>
>如果無法使用所需的範本，請參閱[讓範本可用](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)。

本節僅詳細說明Adobe Campaign的特定連結。 如需如何在Adobe Experience Manager中使用表單的一般概覽的詳細資訊，請參閱[編輯模式元件](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)。

1. 導覽至您要編輯的表單。
1. 在工具箱中，選取&#x200B;**頁面** > **頁面屬性……**，然後移至快顯視窗的&#x200B;**雲端服務**&#x200B;標籤。
1. 按一下&#x200B;**新增服務**，然後在服務的下拉式清單中選取與您的Adobe Campaign執行個體對應的設定，以新增Adobe Campaign服務。 此設定會在您設定執行個體之間的連線時執行。 如需詳細資訊，請參閱[將AEM連線到Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign)。

   >[!NOTE]
   >
   >如有必要，請按一下掛鎖圖示以解除鎖定設定，進而新增Adobe Campaign服務。

1. 使用表單開頭的&#x200B;**編輯**&#x200B;按鈕存取表單的一般引數。 **表單**&#x200B;索引標籤可讓您選取感謝頁面，使用者在驗證表單後將會重新導向該頁面。

   **進階**&#x200B;表單可讓您選取表單型別。 **張貼選項**&#x200B;欄位可讓您在三種型別的Adobe Campaign表單之間進行選擇：

   * **Adobe Campaign：儲存設定檔**：可讓您在Adobe Campaign中建立或更新收件者（預設值）。
   * **Adobe Campaign：訂閱服務**：可讓您在Adobe Campaign中管理收件者的訂閱。
   * **Adobe Campaign：取消訂閱服務**：可讓您取消Adobe Campaign中收件者的訂閱。

   **動作組態**&#x200B;欄位可讓您指定是否要在Adobe Campaign資料庫中建立收件者設定檔（如果尚未存在）。 若要這麼做，請核取&#x200B;**如果不存在，則建立使用者**&#x200B;選項。

1. 從工具箱中拖曳所選元件並放入表單，以新增這些元件。 如需有關可用的Adobe Campaign特定元件的詳細資訊，請參閱[Adobe表單元件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 連按兩下以設定新增的欄位。 **Adobe Campaign**&#x200B;索引標籤可讓您將欄位連結至Adobe Campaign收件者表格中的欄位。 您也可以指定欄位是否為調解金鑰的一部分，以允許辨識Adobe Campaign資料庫中已存在的收件者。

   >[!CAUTION]
   >
   >每個表單欄位的&#x200B;**專案名稱**&#x200B;必須不同。 如有需要，請加以變更。
   >
   >每個表單都必須包含&#x200B;**加密的主要金鑰**&#x200B;元件，才能正確管理Adobe Campaign資料庫中的收件者。

1. 選取工具箱中的&#x200B;**頁面** > **啟動頁面**，以啟動頁面。 頁面已在您的網站上啟動。 您可以前往AEM發佈執行個體來檢視它。 在驗證表單後，Adobe Campaign資料庫中的資料就會更新。

## 測試表單 {#testing-a-form}

建立表單並編輯表單內容後，您可能想要手動測試表單是否如預期般運作。

>[!NOTE]
>
>每個表單上都必須有&#x200B;**已加密的主索引鍵**&#x200B;元件。 在「元件」中選取Adobe Campaign ，只顯示元件。
>
>雖然您在此程式中手動輸入電話號碼，但實際上，使用者會在電子報中取得此頁面的連結（無論是取消訂閱、訂閱或更新您的設定檔）。 頁面會根據使用者自動更新。
>
>若要建立該連結，請使用變數&#x200B;**主要資源識別碼** (Adobe Campaign Standard)或&#x200B;**加密的識別碼** (Adobe Campaign 6.1) (例如，在&#x200B;**Text &amp; Personalization （行銷活動）**&#x200B;元件中)，其會連結至Adobe Campaign中的epk。

若要這麼做，您需要手動取得Adobe Campaign設定檔的EPK，然後將其附加至URL：

1. 若要取得Adobe Campaign設定檔的加密主要金鑰(EPK)：

   * 在Adobe Campaign Standard中 — 導覽至&#x200B;**設定檔與對象** > **設定檔**，其中會列出現有的設定檔。 請確定表格在欄中顯示&#x200B;**主要資源識別碼**&#x200B;欄位（這可以按一下/點選&#x200B;**設定清單**&#x200B;來設定）。 複製所需設定檔的主要資源識別碼。
   * 在Adobe Campaign 6.11中，前往&#x200B;**設定檔和目標** > **收件者**，這會列出現有的設定檔。 請確定資料表在資料行中顯示&#x200B;**加密識別碼**&#x200B;欄位（若要設定此專案，請在專案上按一下滑鼠右鍵，並選取&#x200B;**設定清單……**）。 複製所需設定檔的加密識別碼。

1. 在AEM中，開啟發佈執行個體上的表單頁面，並將步驟1中的EPK附加為URL引數：使用您在編寫表單時先前在EPK元件中定義的相同名稱（例如： `?epk=...`）
1. 此表單現在可用於修改與連結Adobe Campaign設定檔相關聯的資料和訂閱。 修改部分欄位並提交表單後，您可以在Adobe Campaign中驗證適當的資料是否已更新。

在驗證表單後，Adobe Campaign資料庫中的資料就會更新。
