---
title: 翻譯增強功能
description: AEM翻譯管理功能的漸進式增強和細化。
topic-tags: site-features
content-type: reference
feature: Language Copy
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 59b4d716-37a2-4f67-88eb-68c93359242c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 翻譯增強功能{#translation-enhancements}

本頁介紹AEM翻譯管理功能的遞增增強功能和細化。

## 翻譯專案自動化 {#translation-project-automation}

已新增選項，以提升使用翻譯專案的生產力，例如自動提升和刪除翻譯啟動，以及排程翻譯專案的週期性執行。

1. 在您的翻譯專案中，按一下&#x200B;**翻譯摘要**&#x200B;方塊底部的省略符號。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切換至&#x200B;**進階**&#x200B;標籤。 您可以在底部選取&#x200B;**自動提升翻譯啟動**。

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. 或者，您可以選擇在收到翻譯內容後，是否應該自動提升和刪除翻譯啟動。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 若要選取重複執行翻譯專案，請在&#x200B;**重複翻譯**&#x200B;下方的下拉式清單中選取頻率。 週期性專案執行將在指定的時間間隔內自動建立和執行翻譯工作。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多語言翻譯專案 {#multilingual-translation-projects}

您可以在翻譯專案中設定多種目標語言，以減少建立的翻譯專案總數。

1. 在您的翻譯專案中，按一下&#x200B;**翻譯摘要**&#x200B;方塊底部的點。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切換至&#x200B;**進階**&#x200B;標籤。 您可以在&#x200B;**目標語言**&#x200B;下新增多種語言。

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 或者，如果您要透過Sites中的參考邊欄啟動翻譯，請新增您的語言並選取&#x200B;**建立多語言翻譯專案**。

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 翻譯工作將在專案中針對每種目標語言建立。 您可以在專案中逐一啟動，或透過在專案管理員中全域執行專案來一次啟動。

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 翻譯記憶更新 {#translation-memory-updates}

翻譯內容的手動編輯可以同步回翻譯管理系統(TMS)，以訓練其翻譯記憶庫。

1. 從Sites主控台，更新已翻譯頁面中的文字內容後，選取&#x200B;**更新翻譯記憶庫**。

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 清單檢視會顯示每個已編輯文字元件的來源與翻譯的並排比較。 選取應將哪些翻譯更新同步處理到翻譯記憶庫，然後選取&#x200B;**更新記憶庫**。

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM會更新已設定TMS之翻譯記憶庫中現有字串的翻譯。

* 動作會更新已設定TMS的翻譯記憶庫中現有字串的翻譯。
* 它不會建立新的翻譯工作。
* 它會透過AEM翻譯API （請參閱下文）將翻譯傳回TMS。

若要使用此功能：

* TMS必須設定為可與AEM搭配使用。
* 聯結器需要實作方法[`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html)。
   * 此方法中的程式碼會決定翻譯記憶體更新請求的情況。
   * AEM翻譯架構會透過此方法實作，將字串值配對（原始和更新的翻譯）傳回TMS。

在使用專有翻譯記憶庫的情況下，可以攔截翻譯記憶庫更新並傳送到自訂目的地。

## 多個層級的語言副本 {#language-copies-on-multiple-levels}

語言根現在可以在節點下分組（例如，按區域），同時仍被識別為語言副本的根。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>只允許一個層級。 例如，下列專案不會允許&quot;es&quot;頁面解析為語言副本：
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>將不會偵測到此`es`語言副本，因為它距離`en`節點有2個層級（美洲/中美洲）。

>[!NOTE]
>
>語言根可以有任何頁面名稱，而不僅僅是語言的ISO程式碼。 AEM一律會先檢查路徑和名稱，但如果頁面名稱未識別語言，AEM會檢查頁面的cq：language屬性以取得語言識別。

## 翻譯狀態報表 {#translation-status-reporting}

現在，您可以在網站清單檢視中選取屬性，以顯示頁面是否已翻譯、正在翻譯或尚未翻譯。 若要顯示它：

1. 在網站中，切換至&#x200B;**清單檢視。**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. 按一下&#x200B;**檢視設定**。

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. 核取&#x200B;**翻譯**&#x200B;下的&#x200B;**已翻譯**&#x200B;核取方塊，然後按一下&#x200B;**更新**。

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

您現在可以看到&#x200B;**已翻譯**&#x200B;欄，其中顯示頁面的翻譯狀態。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
