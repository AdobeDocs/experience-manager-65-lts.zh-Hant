---
title: 使用智慧內容服務設定資產標籤
description: 瞭解如何使用智慧內容服務，在 [!DNL Adobe Experience Manager]中設定智慧標籤和增強智慧標籤。
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
exl-id: be7c294c-149b-4825-8376-573f9e2987e2
source-git-commit: 1cedead501597fb655c2c7b87336b29cbf048294
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 19%

---

# 準備[!DNL Assets]以進行智慧標籤 {#configure-asset-tagging-using-the-smart-content-service}

開始使用Smart Content Services標籤資產之前，請先將[!DNL Experience Manager Assets]與Adobe Developer Console整合，以使用[!DNL Adobe Sensei]的Smart Service。 設定之後，請使用一些影像和標籤來訓練服務。
在使用智慧內容服務之前，請先確定下列事項：

* [與Adobe Developer Console](#integrate-adobe-io)整合。
* [訓練智慧內容服務](#training-the-smart-content-service)。
* 安裝最新的[[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)。

>[!IMPORTANT]
>
>如需Assets 6.5中智慧標籤的設定，請參閱[準備AEM以進行智慧標籤](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/assets/administer/config-smart-tagging)。

**新使用者**

新的[!DNL Experience Manager Assets]內部部署使用者無法再使用智慧內容服務。

**現有使用者**

已啟用此功能的現有內部部署使用者可以繼續使用智慧內容服務。

## 整合Adobe Developer Console {#integrate-adobe-io}

當您與Adobe Developer Console整合時，[!DNL Experience Manager]伺服器會先透過Adobe Developer Console閘道驗證您的服務認證，再將您的要求轉送至智慧內容服務。 若要整合，您需要具有組織管理員許可權的Adobe ID帳戶，以及為貴組織購買並啟用的Smart Content Service授權。

若要設定智慧內容服務，請遵循下列最上層步驟：

1. 在[Adobe Developer Console](#create-adobe-io-integration)中建立整合。

1. 使用Adobe Developer Console的API金鑰和其他認證，建立[IMS技術帳戶設定](#create-ims-account-config)。

1. [設定智慧內容服務](#configure-smart-content-service)。

1. [測試設定](#validate-the-configuration)。

### 建立Adobe Developer Console整合 {#create-adobe-io-integration}

若要使用Smart Content Service API，請在Adobe Developer Console中建立整合，以取得[!UICONTROL 中雲端設定的]Assets智慧標籤服務設定[!UICONTROL 的]API金鑰[!UICONTROL &#x200B; (產生於Adobe Developer Console整合的]使用者端識別碼[!UICONTROL 欄位中)、]組織識別碼[!UICONTROL 以及]使用者端密碼[!DNL Experience Manager]。

1. 存取瀏覽器中的[https://developer.adobe.com](https://developer.adobe.com/)。 選取適當的帳戶，並確認關聯的組織角色是系統&#x200B;**管理員**。

1. 以任何所需的名稱建立專案。按一下&#x200B;**[!UICONTROL 「新增 API」]**。

1. 在&#x200B;**[!UICONTROL 新增 API]** 頁面上選取&#x200B;**[!UICONTROL 「Experience Cloud」]**，然後選取&#x200B;**[!UICONTROL 「智慧內容」]**。按一下&#x200B;**[!UICONTROL 下一步]**。

1. 選取&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**。 按一下&#x200B;**[!UICONTROL 下一步]**。
如需如何執行此設定的詳細資訊，請參閱Developer Console檔案（視您的需求而定）：

   * 概觀：
      * [伺服器對伺服器驗證](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

   * 建立新的 OAuth 認證：
      * [OAuth 伺服器對伺服器認證實作指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)

   * 將現有 JWT 認證移轉到 OAuth 認證：
      * [從服務帳戶 (JWT) 認證移轉至 OAuth 伺服器對伺服器認證](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration)


1. 在&#x200B;**[!UICONTROL 選取產品設定檔]**&#x200B;頁面中，選取&#x200B;**[!UICONTROL 智慧內容服務]**。 按一下&#x200B;**[!UICONTROL 儲存設定的API]**。

   此時會出現一個頁面，顯示更多關於設定的資訊。請保持此頁面開啟，以複製這些值，並將其新增至[!UICONTROL 中雲端設定的]Assets智慧標籤服務設定[!DNL Experience Manager]，以設定智慧標籤。

   ![Developer Console 的 OAuth 認證](assets/ims-configuration-developer-console.png)

### 建立IMS技術帳戶設定 {#create-ims-account-config}

您需要使用下列步驟建立IMS技術帳戶設定：

1. 在 [!DNL Experience Manager] 使用者介面中，存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS 設定」]**。

1. 按一下「**[!UICONTROL 建立]**」。

1. 在「 IMS技術帳戶設定」對話方塊中，使用以下值：

   ![Adobe IMS設定視窗](assets/adobe-ims-config.png)

   | 欄位 | 說明 |
   | -------- | ---------------------------- |
   | 雲端解決方案 | 從下拉式清單中選擇&#x200B;**[!UICONTROL 智慧標籤]**。 |
   | 標題 | 新增設定IMS帳戶的標題。 |
   | 授權伺服器 | 新增`https://ims-na1.adobelogin.com` |
   | 用戶端識別碼 | 將透過[Adobe Developer主控台](https://developer.adobe.com/console/)提供。 |
   | 用戶端密碼 | 將透過[Adobe Developer主控台](https://developer.adobe.com/console/)提供。 |
   | 範圍 | 將透過[Adobe Developer主控台](https://developer.adobe.com/console/)提供。 |
   | 組織 ID | 將透過[Adobe Developer主控台](https://developer.adobe.com/console/)提供。 |

1. 選取您已建立的組態，然後按一下&#x200B;**[!UICONTROL 檢查健康狀態]**。

1. 確認檢查健康情況對話方塊，並在設定處於健康狀態時按一下關閉。

### 建立新設定 {#configure-smart-content-service}

若要設定整合，請使用Adobe Developer Console整合中的[!UICONTROL 技術帳戶ID]、[!UICONTROL 組織識別碼]、[!UICONTROL 使用者端密碼]和[!UICONTROL 使用者端識別碼]欄位值。 建立智慧標籤雲端設定，可驗證來自[!DNL Experience Manager]部署的API要求。

1. 在[!DNL Experience Manager]中，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 智慧標籤]**&#x200B;以開啟[!UICONTROL 智慧標籤設定]。

1. 按一下&#x200B;**[!UICONTROL 建立]**&#x200B;以建立新組態。 否則，按一下&#x200B;**[!UICONTROL 屬性]**&#x200B;以更新現有的組態。

1. 填入下列欄位：

   ![智慧標籤設定](assets/smart-tags-config.png)

   | 欄位 | 說明 |
   | -------- | ---------------------------- |
   | 標題 | 新增設定IMS帳戶的標題。 |
   | 相關的 Adobe IMS 設定 | 從下拉式清單中選擇組態。 |
   | 服務 URL | `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`。例如 `https://smartcontent.adobe.io/apac`。您可以將`na`、`emea`或`apac`指定為代管Experience Manager作者執行個體的地區。 |

   >[!NOTE]
   >
   >如果在2022年9月1日之前布建Experience Manager Managed Service，請使用下列服務URL：
   >`https://mc.adobe.io/marketingcloud/smartcontent`

1. 按一下「**[!UICONTROL 儲存並關閉]**」。

### 驗證設定 {#validate-the-configuration}

完成設定後，您可以使用JMX MBean來驗證設定。 若要進行驗證，請按照以下步驟操作。

1. 在[!DNL Experience Manager]存取您的`https://[aem_server]:[port]`伺服器。

1. 移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**&#x200B;以開啟OSGi主控台。 按一下&#x200B;**[!UICONTROL 主要] > [!UICONTROL JMX]**。

<!--
1. Click `com.day.cq.dam.similaritysearch.internal.impl`. It opens **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.-->

1. 按一下「`com.day.cq.dam.similaritysearch.internal.impl (SCS)`」。

   ![Mbean視窗](assets/mbean.png)

1. 按一下 `validateConfigs()`。在&#x200B;**[!UICONTROL 驗證組態]**&#x200B;對話方塊中，按一下&#x200B;**[!UICONTROL 叫用]**。

驗證結果會顯示在相同的對話方塊中。

### 在[!UICONTROL DAM更新資產]工作流程中啟用智慧標籤（選用） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在[!DNL Experience Manager]中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。

1. 在「 **[!UICONTROL 工作流模型]** 」頁面上，選擇「**[!UICONTROL DAM 更新資產]** 」工作流模型。

1. 按一下工具列中的&#x200B;**[!UICONTROL 「編輯」]**。

1. 展開「側面板」以顯示步驟。拖 **[!UICONTROL 曳DAM Workflow]**  (DAM工作流程) 區段中可用的智慧型標籤資產步驟，並將其置於&#x200B;**[!UICONTROL 「處理縮 圖」]**&#x200B;步驟之後 。

   ![在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟](assets/smart-tag-in-dam-update-asset-workflow.png)

1. 開啟步驟的屬性以修改詳細資訊。 在「 **[!UICONTROL 進階設定]**」下，確定已選取 **[!UICONTROL 「處理常式進階]** 」選項。

   ![設定DAM更新資產工作流程並新增智慧標籤步驟](assets/smart-tag-step-properties-workflow1.png)

1. 在「參 **[!UICONTROL 數]** 」頁籤中，如果希望工作流完成，即使自動標籤步驟失敗，請選擇「忽略錯誤 **&#x200B;**&#x200B;」。

   此外，若無論是否對資料夾啟用智慧標籤，都要在資產上傳時標籤資產，請選取&#x200B;**[!UICONTROL 忽略智慧標籤旗標]**。

   ![設定DAM更新資產工作流程以新增智慧標籤步驟並選取處理常式進階](assets/smart-tag-step-properties-workflow2.png)

1. 按一下完成![完成圖示](assets/do-not-localize/check-ok-done-icon.png)以關閉程式步驟。

1. 按一下&#x200B;**[!UICONTROL 同步]**&#x200B;以儲存工作流程。

## 訓練智慧內容服務 {#training-the-smart-content-service}

若要讓智慧內容服務辨識您的企業分類，請在已包含與企業相關標籤的一組資產上執行它。 為了有效標籤您的品牌影像，智慧內容服務要求培訓影像符合特定准則。 訓練之後，此服務可以將相同的分類法套用至類似的資產集。

您可以訓練服務多次，以提高其套用相關標籤的能力。 在每個訓練週期後，執行標籤工作流程並檢查您的資產是否已正確標籤。

您可以定期或依需求訓練智慧內容服務。

>[!NOTE]
>
>訓練工作流程僅在資料夾中執行。

### 訓練准則 {#guidelines-for-training}

為達到最佳效果，訓練集中的影像需符合下列准則：

**&#x200B;**&#x200B;數量和大小：每個標籤至少30個影像。長邊至少500像素。

**Coherence**：用於特定標籤的影像在視覺上類似。

例如，將所有影像標籤為`my-party` （用於訓練）是不好的做法，因為這些影像在視覺上並不相似。

![說明性影像，以示範訓練准則](/help/assets/assets/do-not-localize/coherence.png)

**涵蓋範圍**：在訓練的影像中使用足夠的變化。 我們的想法是提供一些相當多元化的範例，讓Experience Manager學習如何聚焦於正確的事。 如果您要在視覺上相異的影像上套用相同的標籤，請至少包含每種型別的五個範例。

例如，對於標籤&#x200B;*模型向下姿態*，請包含更多與下方反白影像類似的訓練影像，以便服務在標籤期間更準確地識別類似影像。

![說明性影像，以示範訓練准則](/help/assets/assets/do-not-localize/coverage_1.png)

**干擾/阻撓**：此服務會針對干擾較少的影像（顯著的背景、不相關的伴侶，例如主主題的物件/人員）提供更好的訓練。

例如，對於標籤&#x200B;*休閒鞋*，第二個影像不是良好的訓練候選項。

![說明性影像，以示範訓練准則](/help/assets/assets/do-not-localize/distraction.png)

**&#x200B;**&#x200B;完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。例如，對於標籤（例如`raincoat`和`model-side-view`），請先在符合資格的資產上新增兩個標籤，然後再加入以進行訓練。

![說明性影像，以示範訓練准則](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>智慧型內容服務針對您的標籤進行培訓並將這些內容套用至其他影像的能力，取決於您用於培訓的影像品質。 為達到最佳效果，Adobe建議您使用視覺上相似的影像，針對每個標籤來訓練服務。

### 定期訓練 {#periodic-training}

您可以啟用智慧內容服務，定期訓練資料夾中的資產和關聯標籤。 開啟資產資料夾的[!UICONTROL 屬性]頁面，選取&#x200B;**[!UICONTROL 詳細資料]**&#x200B;標籤下的&#x200B;**[!UICONTROL 啟用智慧標籤]**，然後儲存變更。

![enable_smart_tags](assets/enable_smart_tags.png)

為資料夾選取此選項後，[!DNL Experience Manager]會自動執行訓練工作流程，以訓練資料夾資產及其標籤上的智慧內容服務。 根據預設，培訓工作流程每週於星期六凌晨12:30執行。

### 隨選培訓 {#on-demand-training}

您可以視需要從工作流程主控台訓練「智慧內容服務」。

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。
1. 從&#x200B;**[!UICONTROL 工作流程模型]**&#x200B;頁面，選取&#x200B;**[!UICONTROL 智慧標籤培訓]**&#x200B;工作流程，然後從工具列按一下&#x200B;**[!UICONTROL 開始工作流程]**。
1. 在&#x200B;**[!UICONTROL 執行工作流程]**&#x200B;對話方塊中，瀏覽至裝載資料夾，其中包含培訓服務的已標籤資產。
1. 指定工作流程的標題並新增註解。 然後，按一下&#x200B;**[!UICONTROL 執行]**。 資產和標籤會提交以進行訓練。

   ![工作流程對話方塊](assets/workflow_dialog.png)

>[!NOTE]
>
>一旦資料夾中的資產處理完畢，用於訓練後，後續訓練週期內將僅處理修改後的資產。

### 檢視訓練報告 {#viewing-training-reports}

若要檢查智慧型內容服務是否已針對您的資產培訓集中的標籤進行培訓，請從「報表」控制檯檢閱培訓工作流程報表。

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 報表]**。
1. 在&#x200B;**[!UICONTROL 資產報表]**&#x200B;頁面中，按一下&#x200B;**[!UICONTROL 建立]**。
1. 選取「**[!UICONTROL 智慧標籤培訓]**」報表，然後從工具列按一下「**[!UICONTROL 下一步]**」。
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。然後，從工具列按一下&#x200B;**[!UICONTROL 建立]**。
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。若要檢視報表，請按一下工具列中的&#x200B;**[!UICONTROL 檢視]**。
1. 檢閱報告的詳細資訊。

   報表會顯示您所訓練之標籤的訓練狀態。「培訓狀態」欄 **[!UICONTROL 中的綠色]** ，表示智慧型內容服務已接受標籤的培訓。黃色表示服務未針對特定標籤進行完整訓練。在這種情況下，請使用特定標籤新增更多影像，並執行培訓工作流程，以完全在標籤上訓練服務。

   如果您在此報告中未看到您的標籤，請再次執行這些標籤的培訓工作流程。

1. 若要下載報表，請從清單中選取報表，然後按一下工具列中的[下載]。 **&#x200B;**&#x200B;報表會下載為Microsoft Excel試算表。

## 限制 {#limitations}

* 增強型智慧標籤是以影像及其標籤的學習模型為基礎。 這些模型並非總能完美地識別標籤。 目前版本的智慧內容服務有下列限制：

   * 無法辨認影像中的細微差異。 例如，超薄襯衫和一般適合的襯衫。
   * 無法根據影像的微小模式/部分識別標籤。 例如，T恤上的標誌。
   * 支援[!DNL Experience Manager]的區域設定支援標籤。

* 若要搜尋具有智慧標籤（一般或增強功能）的資產，請使用[!DNL Assets] Omnisearch （全文檢索搜尋）。 智慧標籤沒有單獨的搜尋述詞。

>[!MORELIKETHIS]
>
>* [智慧標籤概觀及訓練方式](enhanced-smart-tags.md)
>* [疑難排解OAuth憑證的智慧標籤](config-oauth.md)
>* [有關智慧標籤的教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
