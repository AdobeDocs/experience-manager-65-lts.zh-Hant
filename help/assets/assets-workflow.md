---
title: 使用工作流程處理資產
description: 資產處理可轉換格式、建立轉譯、管理資產、驗證資產並執行工作流程。
contentOwner: AG
feature: Workflow, Renditions
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: 06785380-07cc-4c8b-b11c-6005471bd058
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 處理數位資產 {#process-assets}

[!DNL Adobe Experience Manager Assets]可讓您以多種方式處理數位資產，以穩健的資產處理。 您可以使用預設或自訂的處理方法來確保端對端業務流程的完成、稽核與法規遵循、探索與發佈，以及數位資產的基本健全度。 您可以進行資產管理工作，同時達到所需的規模和自訂。

## 瞭解工作流程 {#understand-workflows}

為了進行資產處理，[!DNL Experience Manager]使用工作流程。 工作流程有助於自動化商業邏輯或活動。 預設會提供完成特定任務的精細步驟，開發人員可建立自己的自訂步驟。 這些步驟可以按邏輯順序組合，以建立工作流程。 例如，工作流程可以根據特定條件（例如上傳影像的資料夾、影像的解析度等），在上傳影像上套用浮水印。 另一個範例是工作流程設定，以浮水印並同時新增中繼資料、建立轉譯、新增智慧型標籤和發佈至資料存放區。

## [!DNL Experience Manager]中可用的預設工作流程 {#default-workflows}

依預設，所有上傳的資產都使用[!UICONTROL DAM更新資產]工作流程進行處理。 工作流程會針對每個上傳的資產執行，並完成基本資產管理任務，例如產生轉譯、中繼資料回寫、頁面擷取、媒體擷取和轉碼。

若要檢視預設可用的各種工作流程模型，請參閱[!DNL Experience Manager]中的&#x200B;**[!UICONTROL 工具>工作流程>模型]**。

![部分預設工作流程](assets/aem-default-workflows.png)

*圖： [!DNL Experience Manager].*&#x200B;中某些可用的預設工作流程

## 套用工作流程以處理資產 {#applying-workflows-to-assets}

將工作流程套用至數位資產的方式與套用至網站頁面相同。 如需如何建立及使用工作流程的完整指南，請參閱[開始工作流程](/help/sites-authoring/workflows-participating.md)。

在數位資產中使用工作流程來啟動資產或建立浮水印。 資產的許多工作流程都會自動開啟。 例如，在編輯影像後自動建立轉譯的工作流程會自動開啟。

>[!NOTE]
>
>如果傳統UI中可用的工作流程無法用於觸控式UI，例如[!UICONTROL 請求啟動]和[!UICONTROL 請求停用]，請參閱[建立工作流程模型](/help/sites-developing/workflows-models.md#classic2touchui)。

## 將工作流程套用至資產 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
若要將工作流程套用至資產，請遵循下列步驟：

1. 導覽至您要啟動工作流程的資產位置，然後按一下資產以開啟資產頁面。 從功能表選取&#x200B;**[!UICONTROL 時間表]**&#x200B;以顯示時間表。

   ![時間表–1](assets/timeline.png)

1. 按一下底部的&#x200B;**[!UICONTROL 動作]**&#x200B;以開啟資產可用的動作清單。

1. 按一下清單中的&#x200B;**[!UICONTROL 開始工作流程]**。

1. 在&#x200B;**[!UICONTROL 啟動工作流程]**&#x200B;對話方塊中，從清單中選取工作流程模型。

1. （選用）指定工作流程的標題，以用來參照工作流程的執行個體。

   ![選取工作流程，提供標題並按一下[開始]](assets/start-workflow.png)

1. 按一下&#x200B;**[!UICONTROL 開始]**，然後按一下&#x200B;**[!UICONTROL 繼續]**。 工作流程的每個步驟都會以事件的形式顯示在時間軸中。

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 將工作流程套用至多個資產 {#applying-a-workflow-to-multiple-assets}

1. 從[!DNL Assets]主控台，導覽至您要啟動工作流程的資產位置，然後選取資產。 從功能表選取&#x200B;**[!UICONTROL 時間表]**&#x200B;以顯示時間表。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 按一下底部的&#x200B;**[!UICONTROL 動作]** ![向上](assets/do-not-localize/chevron-up-icon.png) V形。
1. 按一下&#x200B;**[!UICONTROL 開始工作流程]**。 在&#x200B;**[!UICONTROL 啟動工作流程]**&#x200B;對話方塊中，從清單中選取工作流程模型。

   ![開始工作流程](assets/start-workflow.png)

1. （選用）指定工作流程的標題，可用來參考工作流程例項。
1. 按一 **[!UICONTROL 下「開始]** 」，然後按一 **[!UICONTROL 下對話方塊中的「確認]** 」。工作流程會在您選取的所有資產上執行。

## 將工作流程套用至多個資料夾 {#applying-a-workflow-to-multiple-folders}

將工作流程套用至多個資料夾的程式與將工作流程套用至多個資產的程式類似。 在[!DNL Assets]介面中選取資料夾，然後執行程式[將工作流程套用至多個資產](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets)的步驟2-7。

## 將工作流程套用至集合 {#applying-a-workflow-to-a-collection}

請參閱[在集合](/help/assets/manage-collections.md#running-a-workflow-on-a-collection)上套用工作流程。

## 自動啟動工作流程以有條件地處理資產 {#auto-execute-workflow-on-some-assets}

管理員可設定工作流程，以根據預先定義的條件自動執行及處理資產。 此功能對企業營運使用者和行銷人員非常有用，例如可在特定資料夾上建立自訂工作流程。 假設機構拍照時的所有資產都可加上浮水印，或是自由譯者上傳的所有資產都可經過處理，以建立特定轉譯。

對於工作流程模型，使用者可以建立執行它的工作流程啟動器。 工作流程啟動器會監視內容存放庫中的變更，並在符合預先定義的條件時執行工作流程。 管理員可向行銷人員提供存取權，以建立工作流程並設定啟動器。 使用者可以修改預設的[!UICONTROL DAM更新資產]工作流程，以新增處理特定資產所需的額外步驟。 工作流程會在所有新上傳的資產上執行。 使用下列其中一個方法，來限制在特定資產上執行額外的步驟：

* 製作[!UICONTROL DAM更新資產]工作流程的副本，並修改它以在特定資料夾階層上執行。 此方法對於某些資料夾相當實用。
* 額外處理步驟可以使用[OR分割](/help/sites-developing/workflows-step-ref.md#or-split)新增，視條件適用於所需的資料夾數量而定。

## 最佳作法和限制 {#best-practices-limitations-tips}

* 設計工作流程時，請考慮您對所有型別轉譯的需求。 如果您預計未來不需要轉譯，請從工作流程中移除其建立步驟。 之後無法大量刪除轉譯。 長時間使用[!DNL Experience Manager]後，不需要的轉譯可能會佔用儲存空間。 若為個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂[!DNL Experience Manager]以刪除特定轉譯，或刪除資產並重新上傳。
* 根據預設，[!UICONTROL DAM更新資產]工作流程包括建立縮圖和Web轉譯的部分步驟。 如果從工作流程移除任何預設轉譯，[!DNL Assets]的使用者介面將無法正確轉譯。

>[!MORELIKETHIS]
>
>* [套用並參與工作流程](/help/sites-authoring/workflows.md)
>* [建立工作流程模型並擴充工作流程功能](/help/sites-developing/workflows.md)
>* [執行工作流程的方法](/help/sites-administering/workflows-starting.md)
>* [工作流程最佳實務](/help/sites-developing/workflows-best-practices.md)
