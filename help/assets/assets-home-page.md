---
title: '[!DNL Assets]首頁體驗'
description: 個人化 [!DNL Experience Manager Assets] 首頁，以獲得豐富的歡迎畫面體驗，包括資產相關最近活動的快照。
contentOwner: AG
feature: Asset Management
role: Admin, User
solution: Experience Manager, Experience Manager Assets
exl-id: cdf1f56c-d9b2-456b-be05-e0394ea6204f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager Assets]首頁體驗 {#aem-assets-home-page-experience}

個人化[!DNL Adobe Experience Manager Assets]首頁，以獲得豐富的歡迎畫面體驗，包括資產相關最近活動的快照。

[!DNL Assets]首頁提供豐富且個人化的歡迎畫面體驗，其中包括最近活動的快照，例如最近檢視或上傳的資產。

[!DNL Assets]首頁預設為停用。 若要啟用此功能，請執行下列步驟：

1. 開啟[!DNL Experience Manager]組態管理員`https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟&#x200B;**[!UICONTROL Day CQ DAM事件記錄器]**&#x200B;服務。
1. 選取&#x200B;**[!UICONTROL 啟用此服務]**&#x200B;以啟用活動錄製。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 從&#x200B;**[!UICONTROL 事件型別]**&#x200B;清單中，選取要記錄的事件，並儲存變更。

   >[!CAUTION]
   >
   >啟用「已檢視資產」、「已檢視專案」和「已檢視集合」選項，會大幅增加已記錄事件的數量。

1. 從Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`開啟&#x200B;**[!UICONTROL DAM資產首頁功能標幟]**&#x200B;服務。
1. 選取`isEnabled.name`選項以啟用[!DNL Assets]首頁功能。 儲存變更。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 開啟&#x200B;**[!UICONTROL 使用者偏好設定]**&#x200B;對話方塊，然後選取&#x200B;**[!UICONTROL 啟用Assets首頁]**。 儲存變更。

   ![在使用者偏好設定對話方塊上啟用資產首頁](assets/Annotation-color.png)

啟用[!DNL Assets]首頁後，從導覽頁面導覽至[!DNL Assets]使用者介面，或直接從URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`存取。

![在Assets使用者介面上設定體驗連結](assets/config-experience-link.png)

按一下&#x200B;**[!UICONTROL 按一下這裡設定您的體驗連結]**&#x200B;以新增您的使用者名稱、背景影像和設定檔影像。

[!DNL Assets]首頁包含下列段落：

* 歡迎區段
* Widget區段

**歡迎區段**

如果您的設定檔存在，「歡迎」區段會顯示寄給您的歡迎訊息。 此外，它會顯示您的個人資料圖片和歡迎影像（如果已設定）。

如果您的設定檔不完整，「歡迎」區段會顯示一般歡迎訊息和設定檔圖片的預留位置。

**Widget區段**

此區段會顯示在「歡迎」區段下方，並在下列區段下顯示現成的Widget：

* 活動
* 最近
* 探索

**活動**：在此區段下，**[!UICONTROL 我的活動]** Widget會顯示登入使用者使用資產（包括沒有轉譯的資產）執行的最近活動，例如，資產上傳、下載、資產建立、編輯、註解、註解及共用。

**最近**：此區段下的&#x200B;**[!UICONTROL 最近檢視的]** Widget會顯示登入使用者最近存取的實體，包括資料夾、集合和專案。

**探索**：此區段下的&#x200B;**[!UICONTROL 新]** Widget會顯示最近上傳至[!DNL Assets]部署的資產和轉譯。

若要啟用清除使用者活動資料，請從Configuration Manager啟用&#x200B;**[!UICONTROL DAM事件清除服務]**。 啟用此服務後，系統會刪除登入使用者超過指定數目的活動。

「歡迎」畫面提供簡單的導覽協助，例如，工具列上的圖示可存取資料夾、集合和目錄。

>[!NOTE]
>
>啟用[!UICONTROL Day CQ DAM Event Recorder]和[!UICONTROL DAM Event Purge]服務會增加JCR的寫入作業和搜尋索引，大幅增加[!DNL Experience Manager]伺服器的負載。 [!DNL Experience Manager]伺服器上的額外負載可能會影響其效能。

>[!CAUTION]
>
>擷取、篩選及清除[!DNL Assets]首頁所需的使用者活動會對效能造成額外負荷。 因此，管理員應該為目標使用者有效地設定首頁。
>
>Adobe建議執行大量作業的管理員和使用者避免使用資產首頁功能，以防止使用者活動增加。 此外，管理員可以從[!UICONTROL 設定管理員]設定[!UICONTROL Day CQ DAM Event Recorder]，以排除特定使用者的錄製活動。
>
>如果使用功能，Adobe建議您根據伺服器負載排定清除頻率。
