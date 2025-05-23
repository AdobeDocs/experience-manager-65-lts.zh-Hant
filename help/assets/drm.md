---
title: 資產的Digital Rights Management
description: 瞭解如何管理 [!DNL Experience Manager]中授權資產的資產到期狀態和資訊。
contentOwner: AG
role: User, Admin
feature: DRM,Asset Management
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 5870209f-9e0c-4e60-a083-e46edb707ae7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 8%

---

# 資產的 Digital Rights Management {#digital-rights-management-in-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/drm.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

數位資產通常與指定使用條款與期間的授權相關聯。 因為[!DNL Adobe Experience Manager Assets]已與[!DNL Experience Manager]平台完全整合，您可以有效率地管理資產到期資訊與資產狀態。 您也可以將授權資訊與資產建立關聯。

## 資產有效期 {#asset-expiration}

資產到期是強制執行資產授權要求的有效方式。 這可確保在已發佈資產過期時將其取消發佈，從而避免出現任何授權違規的可能性。 沒有管理員許可權的使用者無法編輯、複製、移動、發佈和下載過期的資產。

您可以在卡片檢視和清單檢視中，在[!DNL Assets]主控台中檢視資產的到期狀態。

![expired_flag_list](assets/expired_flag_list.png)

*圖：在清單檢視中，[!UICONTROL 狀態]欄顯示[!UICONTROL 已過期]橫幅。*

您可以在左側邊欄的[!UICONTROL 時間軸]中檢視資產的到期狀態。

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>對於不同時區的使用者，資產到期日的顯示方式會有所不同。

您也可以在&#x200B;**[!UICONTROL 參考]**&#x200B;邊欄中檢視資產的到期狀態。 它可管理資產到期狀態以及複合資產和參照的子資產、集合和專案之間的關係。

1. 導覽至您要檢視參照網頁和複合資產的資產。
1. 選取資產並在左側邊欄中開啟&#x200B;**[!UICONTROL 參考]**。 對於過期的資產，[!UICONTROL 參考]邊欄會在頂端顯示到期狀態&#x200B;**[!UICONTROL 資產已過期]**。

   ![chlimage_1-147](assets/chlimage_1-147.png)

   如果資產具有過期的子資產，[!UICONTROL 參考]邊欄會顯示狀態&#x200B;**[!UICONTROL 資產具有過期的子Assets]**。

   ![chlimage_1-148](assets/chlimage_1-148.png)

### 搜尋過期的資產 {#search-expired-assets}

您可以在「搜尋」面板中搜尋過期的資產，包括過期的子資產。

1. 在[!DNL Assets]主控台中，按一下工具列中的&#x200B;**[!UICONTROL 搜尋]**&#x200B;以顯示Omnisearch方塊。

1. 將游標放在Omnisearch方塊中，選取`Enter`鍵以顯示搜尋結果頁面。
1. 在左側邊欄中開啟搜尋面板。 按一下&#x200B;**[!UICONTROL 到期狀態]**&#x200B;選項以展開。

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 選擇&#x200B;**[!UICONTROL 過期]**。 篩選搜尋結果後，只會顯示已過期的資產。

當您選擇&#x200B;**[!UICONTROL 過期]**&#x200B;選項時，[!DNL Assets]主控台只會顯示複合資產所參考的過期資產和子資產。 參考過期子資產的複合資產不會在子資產過期後立即顯示。 而是在下次排程器執行時[!DNL Experience Manager]偵測到它們參照過期的子資產後，才會顯示。

如果您將已發佈資產的到期日修改為早於目前排程器週期的日期，排程仍會在下次執行時偵測此資產為已到期資產，並據此反映其狀態。

此外，如果故障或錯誤阻止排程器在目前週期中偵測到已到期的資產，排程器會在下一個週期中重新檢查這些資產，並偵測其已到期狀態。

若要啟用[!DNL Assets]主控台以顯示參照的複合資產以及過期的子資產，請在[!DNL Experience Manager] Configuration Manager中設定&#x200B;**[!UICONTROL Adobe CQ DAM Expiry Notification]**&#x200B;工作流程。

1. 開啟[!DNL Experience Manager]組態管理員。
1. 選擇&#x200B;**[!UICONTROL Adobe CQ DAM到期通知]**。 依預設，已選取&#x200B;**[!UICONTROL 以時間為基礎的排程器]**，排程工作以在特定時間檢查資產是否已過期的子資產。 工作完成後，具有過期子資產和參考資產的資產會在搜尋結果中顯示為過期。

1. 要定期運行作業，請清除「基於時 **[!UICONTROL 間的調度程式規則]** 」欄位，並在「定期調度程式」欄位中以秒為單 **[!UICONTROL 位修改時間]** 。例如，範例運算式`0 0 0 * * ?`會在00小時觸發工作。
1. 選取&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;以在資產過期時接收電子郵件。

   >[!NOTE]
   >
   >資產過期時，只有資產建立者（將特定資產上傳至[!DNL Assets]的人）會收到電子郵件。 如需有關在整體[!DNL Experience Manager]層級設定電子郵件通知的其他詳細資訊，請參閱[如何設定電子郵件通知](/help/sites-administering/notification.md)。

1. 在&#x200B;**[!UICONTROL 以秒為單位的先前通知]**&#x200B;欄位中，指定當您要接收有關資產到期的通知時，資產到期之前的時間（以秒為單位）。 資產建立者會在資產到期前收到訊息，通知您資產將在指定時間後到期。 資產過期後，您會收到另一則通知，確認資產已過期。 此外，過期資產也會停用。

1. 按一下「**[!UICONTROL 儲存]**」。

## 資產狀態 {#asset-states}

[!DNL Assets]主控台可顯示資產的各種狀態。 根據特定資產的目前狀態，其卡片檢視會顯示描述其狀態的標籤，例如，已過期、已發佈、已核准、已拒絕等。

1. 在[!DNL Assets]使用者介面中，選取資產。
1. 按一下工具列中的&#x200B;**[!UICONTROL 發佈]**。 如果您在工具列上看不到&#x200B;**發佈**，請按一下工具列上的&#x200B;**[!UICONTROL 更多]**，並找到&#x200B;**[!UICONTROL 發佈]** ![發佈選項](assets/do-not-localize/publish-globe.png)選項。
1. 從功能表選擇&#x200B;**[!UICONTROL 發佈]**，然後關閉確認對話方塊。
1. 結束選取模式。 資產的發佈狀態會顯示在卡片檢視的資產縮圖底部。 在清單檢視中，「已發佈」欄會顯示資產的發佈時間。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 若要顯示其資產詳細資料頁面，請在[!DNL Assets]介面中選取資產，然後按一下&#x200B;**[!UICONTROL 屬性]** ![檢視屬性](assets/do-not-localize/info-circle-icon.png)。

1. 在[!UICONTROL 進階]索引標籤中，從&#x200B;**[!UICONTROL 過期]**&#x200B;欄位設定資產的到期日。

   ![在[過期]欄位中設定資產到期日期和時間](assets/asset-properties-advanced-tab.png)

   *圖：資產[!UICONTROL 屬性]頁面中的[!UICONTROL 進階]索引標籤以設定資產有效期。*

1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;以顯示資產主控台。
1. 資產的發佈狀態會指出卡片檢視中資產縮圖底部的過期狀態。 在清單檢視中，資產的狀態會顯示為&#x200B;**[!UICONTROL 已過期]**。

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. 在[!DNL Assets]主控台中，選取資料夾並在該資料夾上建立稽核工作。
1. 檢閱並核准/拒絕檢閱任務中的資產，然後按一下&#x200B;**[!UICONTROL 完成]**。
1. 導覽至您建立稽核任務的資料夾。 您核准/拒絕的資產狀態會顯示在卡片檢視的底部。 在清單檢視中，核准和到期狀態會顯示在適當的欄中。

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. 若要根據資產的狀態來搜尋資產，請按一下&#x200B;**[!UICONTROL 搜尋]** ![搜尋選項](assets/do-not-localize/search_icon.png)以顯示Omnisearch列。
1. 選取`Return`並按一下[!DNL Experience Manager]以顯示搜尋面板。
1. 在搜尋面板中，按一下&#x200B;**[!UICONTROL 發佈狀態]**&#x200B;並選取&#x200B;**[!UICONTROL 已發佈]**，以在[!DNL Assets]中搜尋已發佈的資產。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 按一下&#x200B;**[!UICONTROL 核准狀態]**，然後按一下適當的選項以搜尋已核准或已拒絕的資產。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 若要根據資產的過期狀態來搜尋資產，請在「搜尋」面 **[!UICONTROL 板中選取「過期狀態]** 」，然後選擇適當的選項。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 您也可以根據各種搜尋面向下的狀態組合來搜尋資產。 例如，您可以在搜尋Facet中選取適當的選項，以搜尋已在稽核任務中核准且尚未過期的已發佈資產。

   ![chlimage_1-166](assets/chlimage_1-166.png)

## [!DNL Assets]中的Digital Rights Management {#digital-rights-management-in-assets-1}

此功能強制接受授權合約，然後才能從[!DNL Adobe Experience Manager Assets]下載授權資產。

如果您選取受保護的資產並按一下[下載]，系統會將您重新導向至授權頁面，讓您接受授權合約。 **&#x200B;**&#x200B;如果您不接受授權合約，將無法使用&#x200B;**[!UICONTROL 下載]**&#x200B;選項。

如果選取範圍包含多個受保護的資產，請一次選取一個資產、接受授權合約，然後繼續下載資產。

如果符合下列任一條件，資產即視為受保護：

* 資產中繼資料屬性`xmpRights:WebStatement`指向包含資產授權合約的頁面的路徑。
* 資產中繼資料屬性`adobe_dam:restrictions`的值是指定授權合約的原始HTML。

>[!NOTE]
>
>已棄用舊版[!DNL Experience Manager]中用來儲存授權的位置`/etc/dam/drm/licenses`。
>
>若您建立或修改授權頁面，或將其從先前的[!DNL Experience Manager]發行版本移轉，Adobe建議您將其儲存在`/apps/settings/dam/drm/licenses`或`/conf/&ast;/settings/dam/drm/licenses`下。

### 下載受DRM保護的資產 {#downloading-drm-assets}

1. 在卡片檢視中，選取您要下載的資產，然後按一下&#x200B;**[!UICONTROL 下載]**。
1. 在「版 **[!UICONTROL 權管理]** 」頁面中，從清單中選取您要下載的資產。
1. 在[!UICONTROL 授權]窗格中，選擇&#x200B;**[!UICONTROL 同意]**。 資產旁會出現核取標籤。 按一下&#x200B;**[!UICONTROL 下載]**&#x200B;選項。

   >[!NOTE]
   >
   >**[!UICONTROL 下載]**&#x200B;選項只有在您選擇同意受保護資產的授權合約時才啟用。 但是，如果您的選擇同時包含受保護和未受保護的資產，則窗格中只會列出受保護的資產，並且會啟用「**[!UICONTROL 下載]**」選項來下載未受保護的資產。 若要同時接受多個受保護資產的授權合約，請從清單中選取資產，然後選擇「同 **[!UICONTROL 意」]**。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 在對話方塊中，按一下&#x200B;**[!UICONTROL 下載]**&#x200B;以下載資產或其轉譯。
