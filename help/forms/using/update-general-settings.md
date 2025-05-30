---
title: 更新一般設定
description: 更新AEM Forms應用程式設定（例如首頁畫面）並擷取「起點」和「附件」選項
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 735e4c4a-6580-4698-a1bf-75c4b1e47b5b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# 更新一般設定{#updating-general-settings}

AEM Forms應用程式的一般設定可讓您指定設定，例如擷取附件、離線模式、登陸畫面、預設類別和自動儲存頻率。

## 更新應用程式中的「一般」設定 {#working-with-the-form}

當您將應用程式與AEM Forms伺服器同步時，所有表單和已定義的工作都會下載到您的行動裝置。

現成可用的AEM Forms應用程式解決方案不會在應用程式同步處理時，下載與每個表單相關聯的附件。

在「一般」標籤中，變更下載附件、離線模式、登陸畫面、自動儲存和同步化設定。 您可以變更應用程式的[主畫面](../../forms/using/home-screen.md)。

**瀏覽至[設定]畫面上的[一般]索引標籤**

1. 若要移至[設定]畫面，請選取[首頁]畫面左上角的[功能表]按鈕，然後選取[選取&#x200B;**設定**]。
1. 在「設定」畫面中，選取「一般」標籤。

   ![AEM Forms應用程式中的一般設定](assets/gen-settings-1.png)

   一般設定畫面

   >[!NOTE]
   >
   >選項在不同行動裝置上的顯示方式可能有所不同。

### 一般設定 {#general-settings}

您可以對應用程式的設定進行下列變更。

* **擷取工作附件**：指定每個工作下載至您的應用程式時，是否要下載關聯的附件。
* **離線模式**：若要啟用或停用AEM Forms應用程式的離線服務。 如需詳細資訊，請參閱[在離線模式](/help/forms/using/work-offline-mode.md)中工作。
* **登陸畫面**：設定應用程式的開始位置（[主畫面](../../forms/using/home-screen.md)）。
可用選項：

   * Forms
   * 任務
   * 我的最愛

* **預設類別**：可讓您選取要在主畫面中顯示的表單類別。 選取「全部」時，您可在首頁畫面中看到所有表單。 系統會根據應用程式中載入的表單填入類別。 根據AEM Forms伺服器中指定的表單設定，可在應用程式中使用Forms。

* **自動儲存頻率**：設定您的[行動應用程式在本機儲存表單資料](../../forms/using/autosave-data-app.md)的頻率。
* **同步處理頻率**：設定您的[行動應用程式以線上模式與AEM Forms伺服器同步處理的頻率](../../forms/using/sync-app.md)。
  **清除本機資料**：從裝置清除資料庫，包括所有使用者的設定和本機資料，以及檔案儲存空間。

>[!NOTE]
>
>清除快取將會立即將您登出應用程式。
>
>但是，系統會提示您確認清除快取作業。
