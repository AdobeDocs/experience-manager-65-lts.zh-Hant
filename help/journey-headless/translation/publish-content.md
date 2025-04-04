---
title: 發佈翻譯內容
description: 了解如何發佈翻譯的內容，並在內容更新時更新翻譯。
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Architect,Data Architect,Developer,User,Leader
exl-id: 1543c167-ca69-4481-835f-932d93850a53
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 80%

---

# 發佈翻譯內容 {#publish-content}

了解如何發佈翻譯的內容，並在內容更新時更新翻譯。

## 目前進度 {#story-so-far}

在 AEM Headless 歷程的上一個文件「[翻譯內容](configure-connector.md)」中，您已了解如何使用 AEM 翻譯專案來翻譯您的 Headless 內容。您現在應該：

* 了解什麼是翻譯專案。
* 能夠建立翻譯專案。
* 使用翻譯專案來翻譯您的 Headless 內容。

現在您的初始翻譯已完成，本文章將帶您完成發佈該內容的下一步，以及如何在語言根中的基礎內容變更時更新您的翻譯。

## 目標 {#objective}

本文件可協助您了解如何在 AEM 中發佈 Headless 內容，以及如何建立持續的工作流程以使您的翻譯保持最新。閱讀本文件後，您應該：

* 了解 AEM 的製作-發佈模型。
* 了解如何發佈翻譯的內容。
* 能夠為翻譯的內容實作持續更新模型。

## AEM 的製作-發佈模型 {#author-publish}

在發佈內容之前，最好了解 AEM 的製作-發佈模型。簡而言之，AEM 將系統使用者分成兩個群組。

1. 建立和管理內容和系統的人
1. 從系統取用內容的人

因此，AEM 實際上分成兩個執行個體。

1. **作者**&#x200B;執行個體是讓內容作者和管理員在其中建立和管理內容的系統。
1. **發佈**&#x200B;執行個體是將內容傳遞給取用者的系統。

在製作執行個體上建立內容後，必須將其傳輸到發佈執行個體才能供取用。從製作傳輸到發佈的流程稱之為&#x200B;**出版**。

## 發佈您的翻譯內容 {#publishing}

一旦您對翻譯內容的狀態感到滿意，就必須發佈內容，以便 Headless 服務可以取用。這項工作並非翻譯專家的職責，此處記錄以說明完整的工作流程。

>[!NOTE]
>
>通常，翻譯完成後，翻譯專家會通知內容所有者翻譯內容已準備好發佈。內容所有者接著會發佈。
>
>為了完整起見，提供了以下步驟。

最簡單的發佈翻譯方法是導覽到專案資產資料夾。

```text
/content/dam/<your-project>/
```

在此路徑下有每個翻譯語言的子資料夾，並且可以選擇要發佈的語言。

1. 前往「**導覽**」>「**資產**」>「**檔案**」並開啟專案資料夾。
1. 在這裡您可以看到語言根資料夾和所有其他語言資料夾。選擇本地化的語言或想要發佈的語言。
   ![選取語言資料夾](assets/select-language-folder.png)
1. 按一下&#x200B;**管理出版物**。
1. 在「**管理出版物**」視窗中，確保自動選取「**發佈**」(在「**動作**」之下)，而且已選取「**現在**」(在「**排程**」之下)。按一下「**下一步**」。
   ![管理發佈選項](assets/manage-publication-options.png)
1. 在下一個 **管理發佈**&#x200B;視窗中，確認正確的路徑已選取。點擊&#x200B;**發佈**。
   ![管理發佈範圍](assets/manage-publication-scope.png)
1. AEM會透過畫面頂端的快顯訊息來確認發佈動作。
   ![資源已發佈橫幅](assets/resources-published-message.png)

您翻譯的 Headless 內容現已發佈！現在您的 Headless 服務可以存取和使用。

>[!TIP]
>
>您可以在發佈時選取多個項目 (即多個語言資料夾)，以便一次發佈多個翻譯。

發佈內容時還有其他選項可用，例如排程發佈時間，這不在本歷程的討論範圍內。如需更多資訊息，請參閱文件結尾處的[其他資源](#additional-resources)區段。

## 更新您的翻譯內容 {#updating-translations}

翻譯很少是一次性的工作。通常，在初始翻譯完成後，內容作者會繼續在語言根中新增和修改內容。這表示您也必須更新翻譯的內容。

特定專案要求會定義您必須更新翻譯的頻率，以及執行更新前需遵循的決策程式。 在您決定更新翻譯後，AEM中的程式就會相當簡單。 由於初始翻譯是根據翻譯專案，因此任何更新也是如此。

但是，如同以往，根據您是選擇自動或手動建立翻譯專案，流程會略有不同。

### 更新自動建立的翻譯專案 {#updating-automatic-project}

1. 導覽至「**導覽**」>「**資產**」>「**檔案**」。請記住，AEM 中的 Headless 內容儲存成資產 (稱為內容片段)。
1. 選取專案的語言根。在此案例中，已選取`/content/dam/wknd/en`。
1. 按一下邊欄選取器並顯示&#x200B;**參考**&#x200B;面板。
1. 按一下&#x200B;**語言副本**。
1. 勾選&#x200B;**語言副本**&#x200B;核取方塊。
1. 展開參考面板底部的&#x200B;**更新語言副本**&#x200B;區段。
1. 在&#x200B;**專案**&#x200B;下拉選單中，選取&#x200B;**新增至現有翻譯專案**。
1. 在&#x200B;**現有翻譯專案**&#x200B;下拉選單中，選取為初始翻譯建立的專案。
1. 按一下&#x200B;**開始**。

![新增項目至現有翻譯專案](assets/add-to-existing-project.png)

內容已新增至現有翻譯專案中。若要檢視翻譯專案：

1. 導覽至「**導覽**」>「**專案**」。
1. 按一下您剛更新的專案。
1. 按一下該語言或您更新的語言之一。

您會看到新工作卡片已適當地新增到專案。

<!--
You see that a new job card was added to the project. In this example, another Spanish translation was added.

![Additional translation job added](assets/additional-translation-job.png)
-->

您可能會注意到新卡片上列出的統計資料 (資產和內容片段數量) 有所不同。這是因為 AEM 會識別自上次翻譯以來發生的變更，並且僅包括必須翻譯的內容。這包括更新內容的重新翻譯以及新內容的首次翻譯。

從這時開始，您[開始和管理您的翻譯工作，就像您最初的做法一樣。](translate-content.md#using-translation-project)

### 更新手動建立的翻譯專案 {#updating-manual-project}

若要更新翻譯，您可以將新工作新增至負責翻譯已更新內容的現有專案。

1. 導覽至「**導覽**」>「**專案**」。
1. 按一下您必須更新的專案。
1. 按一下視窗頂端的&#x200B;**新增**&#x200B;按鈕。
1. 在&#x200B;**新增拼貼**&#x200B;視窗中，按一下&#x200B;**翻譯工作**，然後按一下&#x200B;**提交**。

   ![新增圖磚](assets/add-translation-job-tile.png)

1. 在新翻譯工作的卡片上，按一下卡片頂端的>形箭號按鈕，然後選取&#x200B;**更新目標**&#x200B;以定義新工作的目標語言。

   ![更新目標](assets/update-target.png)

1. 在&#x200B;**選取目標語言**&#x200B;對話方塊中，使用下拉式清單來選取語言，然後按一下&#x200B;**完成**。

   ![選取目標語言](assets/select-target-language.png)

1. 設定好新翻譯工作的目標語言後，請按一下工作卡片底部的省略符號按鈕以檢視工作的詳細資訊。
1. 工作首次建立時是空的。點選或按一下&#x200B;**新增**&#x200B;按鈕並使用路徑瀏覽器[新增內容到工作，就像最初建立翻譯專案時的做法一樣。](translate-content.md#manually-creating)

>[!TIP]
>
>路徑瀏覽器強大的篩選器可以再次高效地只尋找已更新的內容。
>
>若要進一步了解路徑瀏覽器，請參閱[其他資源章節](#additional-resources)

從這時開始，您[開始和管理您的翻譯工作，就像您最初的做法一樣。](translate-content.md#using-translation-project)

## 歷程結尾？ {#end-of-journey}

恭喜！您已經完成 Headless 翻譯歷程！您現在應該：

* 大致了解什麼是 Headless 內容傳遞。
* 對 AEM Headless 功能有基本的了解。
* 了解 AEM 的翻譯功能及其與 Headless 內容的關係。
* 能夠開始翻譯您自己的 Headless 內容。

您現在已準備好在 AEM 中翻譯您自己的 Headless 內容。但是，AEM 是一個強大的工具，還有許多其他選項可用。查看[其他資源區段](#additional-resources)提供的一些其他資源，以詳細了解您在此歷程中看到的功能。

## 其他資源 {#additional-resources}

* [管理翻譯專案](/help/sites-administering/tc-manage.md) - 了解翻譯專案的詳細資料和其他功能，例如人工翻譯工作流程和多語言專案。
* [製作概念](/help/sites-authoring/author.md) - 詳細了解 AEM 的製作和發佈模型。本文件重點放在製作頁面而不是內容片段，但該理論仍然適用。
* [發佈頁面](/help/sites-authoring/publishing-pages.md) - 了解其他可用於發佈內容的功能。本文件重點放在製作頁面而不是內容片段，但該理論仍然適用。
* [製作環境和工具](/help/sites-authoring/author-environment-tools.md#path-selection) - AEM 提供各種機制來組織和編輯您的內容，包括強大的路徑瀏覽器。
