---
title: 用於處理中繼資料、影像和影片的設定檔
description: 設定檔是一組規則，說明要套用至上傳至資料夾之資產的選項。 指定要套用至您上傳之視訊資產的中繼資料設定檔和視訊編碼設定檔。 針對影像資產，您也可以指定要套用至影像資產的影像設定檔，以正確裁切。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
docset: aem65
role: User, Admin
feature: Workflow,Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
exl-id: aa257d33-302c-4a01-be48-e4ff56700bfa
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# 用於處理中繼資料、影像和影片的設定檔{#profiles-for-processing-metadata-images-and-videos}

設定檔是將哪些選項套用至上傳至資料夾之資產的配方。 例如，您可以指定要套用至上傳之視訊資產的中繼資料設定檔和視訊編碼設定檔。 或者，套用至影像資產的影像設定檔，以正確裁切。

這些規則包括新增中繼資料、智慧型裁切影像或建立視訊編碼設定檔。 在Adobe Experience Manager中，您可以建立三種設定檔型別，下列連結將詳細介紹這些設定檔：

* [中繼資料設定檔](/help/assets/metadata-config.md#metadata-profiles)
* [影像設定檔](/help/assets/image-profiles.md)
* [視訊設定檔](/help/assets/video-profiles.md)

您需要管理員許可權才能建立、編輯和刪除中繼資料、影像或視訊設定檔。

建立中繼資料、影像或視訊設定檔後，請將其指派至一或多個資料夾，以作為新上傳資產的目的地。

在Experience Manager Assets中使用設定檔的重要概念是，設定檔會指派給資料夾。 設定檔中的設定為中繼資料設定檔的形式，以及視訊設定檔或影像設定檔。 這些設定會處理資料夾的內容及其任何子資料夾。 因此，您如何命名檔案和資料夾、如何排列子資料夾，以及如何處理這些資料夾中的檔案對於設定檔處理這些資產的方式有重大影響。
透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料做法，您可以充分利用數位資產集合，並確保由正確的設定檔處理正確的檔案。

>[!NOTE]
>
>您從某個資料夾移至另一個資料夾的Assets不會重新處理。 例如，假設您有已指派設定檔A的資料夾1和已指派設定檔B的資料夾2。 如果您將資產從「資料夾1」移至「資料夾2」，則已移動的資產會保留「資料夾1」的原始處理作業。
>
>即使在您將資產移動到具有相同設定檔的兩個資料夾之間時，也是如此。

## 重新處理資料夾中的資產 {#reprocessing-assets}

>[!NOTE]
>
>僅適用於Experience Manager 6.4.6.0或更新版本中的&#x200B;*Dynamic Media - Scene7模式*。

若資料夾中已有您後來加以變更的現有處理設定檔，您可以重新處理該資料夾中的資產。

例如，假設您建立了影像設定檔並將其指派至資料夾。 您上傳至資料夾的任何影像資產都會自動將影像設定檔套用至資產。 不過，您稍後會決定為輪廓新增智慧型裁切比例。 現在，您只需執行&#x200B;*Dynamic Media重新處理* <!-- *Scene7: Reprocess Assets* -->工作流程，而不需再次選取並重新上傳資產至資料夾。

您可以對首次處理失敗的資產執行重新處理工作流程。 因此，即使您尚未編輯處理設定檔或套用處理設定檔，您仍可隨時對資產的資料夾執行重新處理工作流程。

您可以選擇調整重新處理工作流程的批次大小，從預設的50個資產調整為1000個資產。 當您在資料夾上執行&#x200B;_Scene7：重新處理Assets_&#x200B;工作流程時，資產會依批次分組，然後傳送至Dynamic Media伺服器以供處理。 處理之後，整個批次集中每個資產的中繼資料會在Experience Manager上更新。 如果批次大小很大，您可能會遇到處理延遲的問題。 或者，如果批次大小太小，可能會導致Dynamic Media伺服器的往返次數過多。

請參閱[調整重新處理工作流程的批次大小](#adjusting-load)。

>[!NOTE]
>
>如果您正在將資產從Dynamic Media Classic大量移轉至Experience Manager，您必須在Dynamic Media伺服器上啟用移轉復寫代理程式。 移轉完成後，請務必停用代理程式。
>
>您必須在Dynamic Media伺服器上停用移轉發佈代理程式，才能讓重新處理工作流程如預期般運作。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job, and so on, until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**若要重新處理資料夾中的資產：**

1. 在Experience Manager中，從Assets頁面，導覽至已指派處理設定檔且您要套用&#x200B;**[!UICONTROL Dynamic Media重新處理]**&#x200B;工作流程的資產資料夾，

   在「卡片檢視」中，資料夾名稱正下方會顯示資料夾名稱，以指出已指派處理設定檔的資料夾。

1. 選取資料夾。

   * 工作流程會遞回考慮所選資料夾中的所有檔案。
   * 如果主要選取檔案夾中有一個或多個子檔案夾具有資產，工作流程會重新處理檔案夾階層中的每個資產。
   * 您最好避免在擁有超過1000個資產的資料夾階層上執行此工作流程。

1. 在頁面的左上角附近，從下拉式清單中選取&#x200B;**[!UICONTROL 時間表]**。
1. 在頁面的左下角附近，在「註解」欄位的右側，選取「克拉」圖示( **^** )。

   ![重新處理資產工作流程1](/help/assets/assets/reprocess-assets1.png)

1. 選取&#x200B;**[!UICONTROL 啟動工作流程]**。
1. 從&#x200B;**[!UICONTROL 開始工作流程]**&#x200B;下拉式清單中，選擇&#x200B;**[!UICONTROL Dynamic Media重新處理]**。
1. （選擇性）在&#x200B;**輸入工作流程的標題**&#x200B;文字欄位中，輸入工作流程的名稱。 如有必要，您可以使用名稱來參照工作流程例項。

   ![重新處理資產2](/help/assets/assets/reprocess-assets2.png)

1. 選取&#x200B;**[!UICONTROL 開始]**，然後選取&#x200B;**[!UICONTROL 確認]**。

   若要監視工作流程或檢查其進度，請從Experience Manager主控台頁面，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]**。 在「工作流程例項」頁面上，選取工作流程。 在功能表列上，選取&#x200B;**[!UICONTROL 開啟歷程記錄]**。 您也可以從同一個「工作流程例項」頁面終止、暫停或重新命名選取的工作流程。

### 調整重新處理工作流程的批次大小 {#adjusting-load}

（選用）重新處理工作流程中的預設批次大小是每個工作50個資產。 此最佳批次大小是由平均資產大小和執行重新處理的資產MIME型別所控制。 較高的值表示您在一個重新處理工作中擁有許多檔案。 因此，處理橫幅會在Experience Manager資產上停留較長時間。 不過，如果平均檔案大小很小（1 MB以下），Adobe建議您將值增加到數100，但絕不要超過1000。 如果平均檔案大小很大（例如數百個MB），Adobe建議您減少批次大小，上限為10。

**若要選擇性地調整重新處理工作流程的批次大小：**

1. 在Experience Manager中，選取&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;以存取全域導覽主控台，然後選取&#x200B;**[!UICONTROL 工具]** （槌子）圖示> **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。
1. 在「工作流程模型」頁面的「卡片檢視」或「清單檢視」中，選取「**[!UICONTROL Dynamic Media重新處理]**」。

   在卡片檢視中選取Dynamic Media重新處理工作流程的![工作流程模型頁面](/help/assets/assets-dm/reprocess-assets7.png)

1. 在工具列上，選取&#x200B;**[!UICONTROL 編輯]**。 新的瀏覽器標籤會開啟「Dynamic Media重新處理工作流程」模型頁面。
1. 在「動態媒體重新處理工作流程」頁面的右上角附近，選取「**[!UICONTROL 編輯]**」以「解除鎖定」工作流程。
1. 在工作流程中，選取Scene7批次上傳元件以開啟工具列，然後在工具列上選取「**[!UICONTROL 設定]**」。

   ![Scene7批次上傳元件](/help/assets/assets-dm/reprocess-assets8.png)

1. 在&#x200B;**[!UICONTROL 批次上傳至Scene7 — 步驟屬性]**&#x200B;對話方塊中，設定下列專案：
   * 在&#x200B;**[!UICONTROL 標題]**&#x200B;和&#x200B;**[!UICONTROL 描述]**&#x200B;文字欄位中，視需要輸入新的標題和描述。
   * 如果您的處理常式將進行到下一個步驟，請選取&#x200B;**[!UICONTROL 處理常式前進]**。
   * 在&#x200B;**[!UICONTROL 逾時]**&#x200B;欄位中，輸入外部處理序逾時（秒）。
   * 在&#x200B;**[!UICONTROL 期間]**&#x200B;欄位中，輸入輪詢間隔（秒），以測試外部處理序是否完成。
   * 在&#x200B;**[!UICONTROL 批次欄位]**&#x200B;中，輸入Dynamic Media伺服器批次處理上傳工作中要處理的資產數目上限(50-1000)。
   * 如果要在達到逾時時間時前進，請選取&#x200B;**[!UICONTROL 逾時時前進]**。 如果達到逾時時間時仍要進入收件匣，請取消選取專案。

   ![內容對話方塊](/help/assets/assets-dm/reprocess-assets3.png)

1. 在&#x200B;**[!UICONTROL 批次上傳到Scene7 — 步驟屬性]**&#x200B;對話方塊的右上角，選取&#x200B;**[!UICONTROL 完成]**。

1. 在「動態媒體重新處理工作流程」模型頁面的右上角，選取&#x200B;**[!UICONTROL 同步]**。 當您看到&#x200B;**[!UICONTROL 已同步]**&#x200B;時，工作流程執行階段模型已成功同步化，並準備好重新處理資料夾中的資產。

   ![同步處理工作流程模型](/help/assets/assets-dm/reprocess-assets1.png)

1. 關閉顯示「動態媒體重新處理」工作流程模型的瀏覽器標籤。

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.-->
