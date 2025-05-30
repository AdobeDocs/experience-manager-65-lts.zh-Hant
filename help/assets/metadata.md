---
title: 管理數位資產的中繼資料
description: 瞭解中繼資料的型別，以及如何管理資產的中繼資料，以輕鬆組織和處理資產。
contentOwner: AG
mini-toc-levels: 1
feature: Tagging, Metadata
role: Architect, Leader
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: dc231e6b-d656-4626-a800-ee66533b1c86
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2332'
ht-degree: 10%

---

# 管理數位資產的中繼資料 {#managing-metadata-for-digital-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-metadata.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, and so on, operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets]保留每個資產的中繼資料。 它可讓您更輕鬆地分類及組織資產，並協助尋找特定資產的人。 中繼資料管理可透過從上傳至[!DNL Experience Manager Assets]的檔案擷取中繼資料，與創意工作流程整合。 有了使用資產保留和管理中繼資料的功能，您可以根據資產的中繼資料自動組織和處理資產。

## 中繼資料及其來源 {#how-to-edit-or-add-metadata}

中繼資料是可搜尋資產的其他相關資訊。 它會新增至資產，並在您上傳資產時於[!DNL Experience Manager]中處理。 您可以編輯現有的中繼資料，將新的中繼資料屬性新增到現有欄位。 組織需要受控制且可靠的中繼資料辭彙。 因此，[!DNL Experience Manager Assets]不允許隨選新增新的中繼資料屬性。 只有管理員和開發人員可以新增包含中繼資料的新屬性或欄位。 使用者可以將中繼資料填入現有欄位。

下列方法可用於將中繼資料新增至數位資產：

* 首先，建立資產的原生應用程式會新增一些中繼資料。 例如，[Acrobat將一些中繼資料](https://helpx.adobe.com/tw/acrobat/using/pdf-properties-metadata.html)新增至PDF檔案，或相機將一些基本中繼資料新增至像片。 產生資產時，您可以在原生應用程式本身中新增中繼資料。 例如，您可以[在Adobe Lightroom](https://helpx.adobe.com/tw/lightroom-classic/help/metadata-basics-actions.html)中新增IPTC中繼資料。

* 在將資產上傳到[!DNL Experience Manager]之前，您可以使用用於建立資產的原生應用程式或使用其他中繼資料編輯應用程式來編輯和修改中繼資料。 將資產上傳至Experience Manager時，系統會處理中繼資料。 例如，瞭解如何[在 [!DNL Adobe Bridge]](https://helpx.adobe.com/tw/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html)中使用中繼資料，並檢視[!DNL Adobe Exchange]中 [!DNL Adobe Bridge][&#128279;](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html)的標籤面板。

* 在[!DNL Experience Manager Assets]中，您可以在[!UICONTROL 屬性]頁面中手動新增或編輯資產的中繼資料。

* 當資產上傳至DAM時，您可以使用[!DNL Experience Manager Assets]的[中繼資料設定檔](/help/assets/metadata-config.md#metadata-profiles)功能來自動新增中繼資料。

## 在[!DNL Experience Manager Assets]中新增或編輯中繼資料 {#add-edit-metadata}

若要在[!DNL Assets]使用者介面中編輯資產的中繼資料，請遵循下列步驟：

1. 執行下列任一項作業：

   * 從[!DNL Assets]介面中，選取資產並按一下工具列中的&#x200B;**[!UICONTROL 檢視屬性]**。
   * 從資產縮圖中，選取&#x200B;**[!UICONTROL 檢視屬性]**&#x200B;快速動作。
   * 從資產頁面，按一下工具列中的&#x200B;**[!UICONTROL 檢視屬性]** ![Assets資訊圖示](assets/do-not-localize/info-circle-icon.png)。

   資產頁面會顯示所有資產的中繼資料。 將資產上傳（擷取）到[!DNL Experience Manager]時，會擷取中繼資料。

   ![選取資產的屬性以檢視其中繼資料](assets/asset-metadata.png)

   *圖：在資產[!UICONTROL 屬性]頁面上編輯或新增中繼資料。*

1. 視需要對各種標籤下的中繼資料進行編輯，在完成時，按一下工具列中的&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存您的變更。 按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;以返回[!DNL Assets]網頁介面。

   >[!NOTE]
   >
   >如果文字欄位為空，則沒有現有的中繼資料集。 您可以在欄位中輸入值，並將其儲存以新增該中繼資料屬性。

對資產中繼資料所做的任何變更，都會當作其XMP資料的一部分，回寫至原始二進位檔。 中繼資料的回寫工作流程會將中繼資料新增至原始二進位。 對現有屬性（例如`dc:title`）所做的變更會被覆寫，而新屬性（包括自訂屬性，例如`cq:tags`）會加入結構描述。

支援並啟用[技術要求中說明的平台與檔案格式的XMP回寫。](/help/sites-deploying/technical-requirements.md)

## 編輯多個資產的中繼資料屬性 {#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets]可讓您同時編輯多個資產的中繼資料，以便快速將常見的中繼資料變更大量傳播至資產。 您也可以大量編輯多個集合的中繼資料。 使用屬性頁面可對多個資產或集合執行中繼資料變更：

* 將中繼資料屬性變更為通用值
* 新增或修改標籤

若要自訂中繼資料屬性頁面，包括新增、修改、刪除中繼資料屬性，請使用[結構描述編輯器](metadata-config.md#folder-metadata-schema)。

>[!NOTE]
>
>大量編輯方法適用於資料夾或集合中可用的資產。 對於跨資料夾可用的資產，或符合共同條件的資產，可在搜尋[&#128279;](search-assets.md#metadataupdates)後大量更新中繼資料。

1. 在[!DNL Assets]使用者介面中，導覽至您要編輯之資產的位置。
1. 選取您要編輯其一般屬性的資產。
1. 在工具列中按一下&#x200B;**[!UICONTROL 屬性]**&#x200B;以開啟所選資產的屬性頁面。
1. 修改各種標籤下所選資產的中繼資料屬性。
1. 若要檢視特定資產的中繼資料，請取消選取清單中剩餘的資產。 如果您取消在[!UICONTROL 屬性]頁面上選取一些資產，這些資產的中繼資料不會更新。
1. 若要為資產選取不同的中繼資料結構，請從工具列按一下&#x200B;**[!UICONTROL 設定]**，然後選取結構。 按一下「**[!UICONTROL 儲存並關閉]**」。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。按一下「**[!UICONTROL 提交]**」。

![中繼資料結構描述大量套用至多個資產](assets/metadata-schema-bulk-edit.gif)

>[!CAUTION]
>
>對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 匯入中繼資料 {#import-metadata}

[!DNL Assets]可讓您使用CSV檔案大量匯入資產中繼資料。 您可以匯入CSV檔案，大量更新最近上傳的資產或現有資產。 您也可以以CSV格式從協力廠商系統大量擷取資產中繼資料。

中繼資料的匯入為非同步處理，不會阻礙系統效能。 如果勾選工作流程標幟，由於XMP回寫活動，同時更新多個資產的中繼資料可能會耗費大量資源。 在精益伺服器使用期間規劃這類匯入，以免影響其他使用者的效能。

>[!NOTE]
>
>若要在自訂名稱空間上匯入中繼資料，請先註冊名稱空間。

1. 導覽至[!DNL Assets]使用者介面，然後從工具列按一下&#x200B;**[!UICONTROL 建立]**。
1. 從功能表中選取&#x200B;**[!UICONTROL 中繼資料]**。
1. 在&#x200B;**[!UICONTROL 中繼資料匯入]**&#x200B;頁面中，按一下&#x200B;**[!UICONTROL 選取檔案]**。 選取包含中繼資料的CSV檔案。
1. 指定下列引數。 在[metadata-import-sample-file.csv](/help/assets/assets/metadata-import-sample-file.csv)檢視範例CSV檔案。

   | 中繼資料匯入引數 | 描述 |
   |:---|:---|
   | [!UICONTROL 批次大小] | 批次中要匯入中繼資料的資產數量。 預設值為50。 最大值為100。 |
   | [!UICONTROL 欄位分隔符號] | 預設值為`,` （逗號）。 您可以指定任何其他字元。 |
   | [!UICONTROL 多值分隔符號] | 中繼資料值的分隔符號。 預設值為`|`。 |
   | [!UICONTROL 啟動工作流程] | 預設為False。 設為`true`時，預設設定對[!UICONTROL DAM中繼資料WriteBack]工作流程有效(會將中繼資料寫入二進位XMP資料)。 啟用工作流程會拖慢系統速度。 |
   | [!UICONTROL 資產路徑資料行名稱] | 為含有資產的CSV檔案定義欄名稱。 |

1. 按一下工具列中的&#x200B;**[!UICONTROL 匯入]**。 匯入中繼資料後，[!UICONTROL 通知]收件匣中會顯示通知。

1. 若要驗證匯入是否正確，請瀏覽至資產的[!UICONTROL 屬性]頁面，然後驗證欄位中的值。

若要在匯入中繼資料時新增日期和時間戳記，請使用`YYYY-MM-DDThh:mm:ss.fff-00:00`格式作為日期和時間。 日期和時間以`T`分隔，`hh`是24小時格式的小時，`fff`是nanoseconds，而`-00:00`是時區位移。 例如，`2020-03-26T11:26:00.000-07:00`是2020年3月26日上午11:26:00:000 （太平洋標準時間）。

>[!CAUTION]
>
>如果日期格式不符合`YYYY-MM-DDThh:mm:ss.fff-00:00`，則不會設定日期值。 匯出的中繼資料CSV檔案的日期格式為`YYYY-MM-DDThh:mm:ss-00:00`。 如果您要匯入它，請加入由`fff`表示的nanoseconds值，將其轉換為可接受的格式。

## 匯出中繼資料 {#export-metadata}

您可以以CSV格式匯出多個資產的中繼資料。 中繼資料會以非同步方式匯出，不會影響系統效能。 若要匯出中繼資料，[!DNL Experience Manager]會遍訪資產節點`jcr:content/metadata`及其子節點的屬性，並將中繼資料屬性匯出為CSV檔案。

大量匯出中繼資料的一些使用案例包括：

* 移轉資產時，在第三方系統中匯入中繼資料。
* 與更廣大的專案團隊共用資產中繼資料。
* 測試或稽核中繼資料是否合規。
* 將中繼資料外部化，以個別進行當地語系化。

1. 選取包含您要匯出中繼資料之資產的資產資料夾。 從工具列中選取&#x200B;**[!UICONTROL 匯出中繼資料]**。

1. 在[!UICONTROL 中繼資料匯出]對話方塊中，指定CSV檔案的名稱。 若要匯出子資料夾中資產的中繼資料，請選取&#x200B;**[!UICONTROL 包含子資料夾中的資產]**。

   ![匯出資料夾中所有資產中繼資料的介面和選項](assets/export_metadata_page.png "匯出資料夾中所有資產中繼資料的介面和選項")

1. 選取所需的選項。 提供檔案名稱，並視需要提供日期。

1. 在&#x200B;**[!UICONTROL 要匯出的屬性]**&#x200B;欄位中，指定您是要匯出所有屬性還是特定屬性。 如果您選擇要匯出的「選擇性」屬性，請新增所需的屬性。

1. 在工具列中按一下&#x200B;**[!UICONTROL 匯出]**。 系統會顯示訊息，確認中繼資料已匯出。 關閉訊息。

1. 開啟導出作業的收件箱通知。選擇作業，然後從工具 **[!UICONTROL 欄中]** ，按一下「開啟」。若要下載含有中繼資料的CSV檔案，請從工具列按一下&#x200B;**[!UICONTROL CSV下載]**。 按一下&#x200B;**[!UICONTROL 關閉]**。

   ![用於下載包含大量匯出之中繼資料的CSV檔案的對話方塊](assets/csv_download.png)

   *圖：用於下載包含大量匯出之中繼資料的CSV檔案的對話方塊。*

## 編輯集合的中繼資料 {#collections-metadata}

如需詳細資訊，請參閱[檢視和編輯集合中繼資料](/help/assets/manage-collections.md#view-edit-collection-metadata)和[大量編輯多個集合的中繼資料](/help/assets/manage-collections.md#editing-collection-metadata-in-bulk)。

## 將中繼資料設定檔套用至資料夾 {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

將中繼資料描述檔指派給資料夾時，所有子資料夾都會自動從其父資料夾繼承描述檔。 這表示您只能將一個中繼資料設定檔指派至資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的資料夾結構。

如果您將不同的中繼資料描述檔指派給資料夾，則新的描述檔會覆寫先前的描述檔。 先前現有的資料夾資產保持不變。 新設定檔會套用至稍後新增至資料夾的資產。

在使用者介面中，會以卡片名稱中顯示的設定檔名稱來指出已指派設定檔的資料夾。

![卡片檢視顯示套用至資料夾](assets/metadata-profile-card-view-display.png)的中繼資料設定檔

您可以將中繼資料設定檔套用至特定資料夾，或全域套用至所有資產。

若資料夾中已有您後來加以變更的現有中繼資料設定檔，您可以重新處理該資料夾中的資產。 請參閱[在您編輯資料夾中資產的處理設定檔](processing-profiles.md#reprocessing-assets)之後，重新處理該資料夾中的資產。

您可以從「工具」菜單或者在資料夾內的「屬性」中，將元資料設定檔&#x200B;**[!UICONTROL 應用到資料夾]**&#x200B;**&#x200B;**。本節說明如何以兩種方式將中繼資料設定檔套用至資料夾。

已為其分配輪廓的資料夾將通過資料夾名稱正下方的輪廓名稱顯示來指示。

若資料夾中已有您後來加以變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 請參閱[在您編輯資料夾中資產的處理設定檔](processing-profiles.md#reprocessing-assets)之後，重新處理該資料夾中的資產。

### 從[!UICONTROL 設定檔]使用者介面將中繼資料設定檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

請依照以下步驟套用中繼資料設定檔：

1. 按一下[!DNL Experience Manager]標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料設定檔]**。
1. 選取您要套用至一或多個資料夾的中繼資料設定檔。
1. 按一下&#x200B;**[!UICONTROL 將中繼資料設定檔套用至資料夾]**，然後選取您要用來接收新上傳資產的資料夾或多個資料夾，並按一下&#x200B;**[!UICONTROL 完成]**。 已為其分配輪廓的資料夾將通過資料夾名稱正下方的輪廓名稱顯示來指示。

### 從[!UICONTROL 屬性]將中繼資料設定檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-properties}

1. 在左側邊欄中，按一下&#x200B;**[!UICONTROL Assets]**，然後導覽至您要套用中繼資料設定檔的資料夾。
1. 在資料夾上，按一下核取記號以選取資料夾，然後按一下&#x200B;**[!UICONTROL 內容]**。

1. 選取「**[!UICONTROL 中繼資料描述檔]**」標籤，然後從快顯功能表選取描述檔，然後按一下「**[!UICONTROL 儲存]**」。

已為其分配輪廓的資料夾將通過資料夾名稱正下方的輪廓名稱顯示來指示。

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### 從資料夾中移除中繼資料設定檔 {#removing-a-metadata-profile-from-folders}

當您從資料夾中移除中繼資料描述檔時，任何子資料夾都會自動繼承其父資料夾中描述檔的移除作業。 不過，在資料夾內發生的任何檔案處理作業都會維持不變。

您可以從&#x200B;**[!UICONTROL 工具]**&#x200B;功能表內的資料夾中移除中繼資料描述檔，或從資料夾內的&#x200B;**[!UICONTROL 屬性]**&#x200B;中移除中繼資料描述檔。

#### 透過設定檔使用者介面從資料夾中移除中繼資料設定檔 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. 按一下[!DNL Experience Manager]標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料設定檔]**。
1. 選取您要從資料夾或多個資料夾移除的中繼資料設定檔。
1. 按一下&#x200B;**[!UICONTROL 從資料夾移除中繼資料描述檔]**，然後選取您要用來從中移除描述檔的資料夾或多個資料夾，並按一下&#x200B;**[!UICONTROL 完成]**。

   您可以確認中繼資料描述檔不再套用至資料夾，因為資料夾名稱下方不再有該名稱。

#### 透過「屬性」從資料夾中移除中繼資料設定檔 {#removing-metadata-profiles-from-folders-via-properties}

1. 按一下[!DNL Experience Manager]標誌並導覽&#x200B;**[!UICONTROL Assets]**，然後移至您要從中移除中繼資料設定檔的資料夾。
1. 在資料夾上，按一下核取記號以選取資料夾，然後按一下&#x200B;**[!UICONTROL 內容]**。
1. 選擇&#x200B;**[!UICONTROL 「元資料設定檔」]**&#x200B;標籤，然後從下拉式選單中選 **[!UICONTROL 擇「無」]**，然後按一下&#x200B;**[!UICONTROL 「儲存」]**。已為其分配輪廓的資料夾將通過資料夾名稱正下方的輪廓名稱顯示來指示。

## 提示和限制 {#best-practices-limitations}

* 透過使用者介面更新中繼資料會變更`dc`名稱空間中的中繼資料屬性。 透過HTTP API所做的任何更新都會變更`jcr`名稱空間中的中繼資料屬性。 請參閱[如何使用HTTP API更新中繼資料](/help/assets/mac-api-assets.md#update-asset-metadata)。

* 用於匯入資產中繼資料的CSV檔案採用非常特定的格式。 為了節省時間和精力，並避免意外錯誤，您可以使用轉存的CSV檔案格式開始建立CSV。

* 使用CSV檔案匯入中繼資料時，所需的日期格式為`YYYY-MM-DDThh:mm:ss.fff-00:00`。 如果使用任何其他格式，則不會設定日期值。 匯出的中繼資料CSV檔案的日期格式為`YYYY-MM-DDThh:mm:ss-00:00`。 如果您要匯入它，請加入由`fff`表示的nanoseconds值，將其轉換為可接受的格式。

>[!MORELIKETHIS]
>
>* [中繼資料概念與瞭解](metadata-concepts.md)。
>* [編輯多個集合的中繼資料屬性](manage-collections.md#editing-collection-metadata-in-bulk)
>* [在Experience Manager Assets中匯入和匯出中繼資料](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html?lang=zh-Hant)

<!-- TBD: Try filling the available information in these topics to the extent possible. As and when complete, publish the sections live.

## Where to find metadata of an asset or folder {#find-metadata}

What all methods to access asset Properties. More Details option in column view. Select asset and click Properties. Keyboard shortcut `p`. What else?

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

* To begin with, assets come with some metadata. The applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some other metadata editing application. When you upload an asset to Experience Manager, the metadata is processed.

* Link to PS, ID, AI, PDF, and so on, metadata-related help articles.

* Link to XMP writeback.

* Manually add (or edit) metadata in AEM in Properties page.

* Metadata profiles

* Any workflows related to metadata?

* Advanced topic: Add, edit, modify, process and writeback metadata of subassets.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

Similarities and differences between metadata of asset and folder. 

Link to metadata handling of collections.

## Modify metadata of an asset, folder, or collection {#modify-metadata}

* While creating assets: Native application.

* Before ingesting assets: Metadata editors

* After ingesting assets: Properties of an asset, folder, collection, and so on.

* Any supported programmatic method to bulk edit metadata directly in JCR?

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value

* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the Properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

-->
