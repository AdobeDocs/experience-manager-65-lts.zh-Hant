---
title: 列印管道和網頁管道
description: 匯入列印管道範本並建立及啟用網路管道範本
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: dca7f612-f505-414b-9326-90624be9db39
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 列印管道和網頁管道{#print-channel-and-web-channel}

互動式通訊可透過兩種通道提供：列印與網路。 列印管道用於建立PDF和書面通訊，例如作為保險費付款提醒的列印信函，而網路管道用於提供線上體驗，例如網站上的信用卡對帳單。

互動式通訊作者可重複使用檔案片段和影像等資產，以建立互動式通訊的列印和網頁版本。

[建立互動式通訊](../../forms/using/create-interactive-communication.md)的先決條件之一，是要在伺服器上提供列印和/或Web通道的範本。 範本作者在AEM中建立Web Channel範本時，列印管道範本XDP是在Adobe Forms Designer中建立並上傳至伺服器。

## 列印管道 {#printchannel}

互動式通訊的列印管道使用XFA表單範本XDP。 XDP是在Adobe Forms Designer中設計。 如需建立列印管道範本的詳細資訊，請參閱[版面設計](../../forms/using/layout-design-details.md)。 若要在互動式通訊中使用列印管道範本，您必須將範本上傳至AEM Forms伺服器。

### 上傳互動式通訊列印頻道範本 {#upload-interactive-communication-print-channel-template}

若要上傳範本，您必須是表單 — 使用者群組的成員。 使用以下步驟，將列印管道範本(XDP)上傳至AEM Forms：

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。

1. 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**。

   瀏覽並選取適當的列印管道範本(XDP)並選取&#x200B;**[!UICONTROL 開啟]**。

## 網路頻道 {#web-channel}

範本作者和管理員可以建立、編輯及啟用網頁範本。 若要允許其他使用者撰寫網頁範本，您必須授予他們許可權。 如需詳細資訊，請參閱[使用者、群組和存取許可權管理](/help/sites-administering/user-group-ac-admin.md)。

### 編寫Web Channel範本 {#authoring-web-channel-template}

若要建立Web Channel範本，您必須先建立範本資料夾。 在範本資料夾中建立Web範本後，您需要啟用範本以允許表單使用者根據範本建立互動式通訊的Web通道。

若要編寫Web Channel範本，請完成以下步驟：

1. 建立「範本」資料夾以保留互動式通訊Web範本（如果尚未建立）。 如需詳細資訊，請參閱[頁面範本 — 可編輯](/help/sites-developing/page-templates-editable.md)中的範本資料夾。

   1. 選取&#x200B;**[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 設定瀏覽器]**。
      * 如需詳細資訊，請參閱[設定瀏覽器](/help/sites-administering/configurations.md)檔案。
   1. 在組態瀏覽器頁面中，選取&#x200B;**[!UICONTROL 建立]**。
   1. 在[建立組態]對話方塊中，指定資料夾的標題，核取&#x200B;**[!UICONTROL 可編輯的範本]**，然後選取&#x200B;**[!UICONTROL 建立]**。

      資料夾隨即建立並列在「組態瀏覽器」頁面中。

1. 導覽至適當的範本資料夾並建立網站範本。

   1. 選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 範本]** > **`[Folder]`**，以導覽至適當的範本資料夾。
   1. 選取「**[!UICONTROL 建立]**」。
   1. 選取&#x200B;**[!UICONTROL 互動式通訊 — Web Channel]**&#x200B;並選取&#x200B;**[!UICONTROL 下一步]**。
   1. 輸入範本標題和說明，然後選取&#x200B;**[!UICONTROL 建立]**。

      範本隨即建立，並出現一個對話方塊。

   1. 選取&#x200B;**[!UICONTROL 開啟]**&#x200B;以開啟您在範本編輯器中建立的範本。

      「範本編輯器」即會出現。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      建立或編輯範本時，範本作者可以定義多個方面。 建立或編輯範本類似於頁面製作。 如需詳細資訊，請參閱[建立頁面範本](/help/sites-authoring/templates.md)中的「編輯範本 — 範本作者」。

1. 若要允許此範本用於建立互動式通訊，請啟用範本。

   1. 選取&#x200B;**[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 範本]**。
   1. 導覽至適當的範本，選取該範本，然後選取&#x200B;**[!UICONTROL 啟用]**，並在警示訊息中選取&#x200B;**[!UICONTROL 啟用]**。

      範本已啟用，其狀態會顯示為「已啟用」。 現在，您可以繼續建立互動式通訊，其中您可以使用新建立的Web Channel範本。

### 將Channel列印為Web channel的主版 {#print-channel-as-master-for-web-channel}

在製作互動式通訊時，作者可以選取此選項，以建立與列印管道同步的Web管道。 使用print channel做為web channel的主版，可確保從print channel衍生web channel的內容、繼承和資料繫結，並且在print channel中所做的變更可以反映在web channel中。 不過，互動式通訊作者可視需求中斷Web Channel中特定元件的繼承。

![Print channel as master](assets/create_ic_print_master_new.png) ![Web channel with print channel as master](assets/create_ic_print_master_web_new.png)
