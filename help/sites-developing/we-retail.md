---
title: We.Retail參考實作
description: We.Retail是參考實作的技術預覽，說明使用AEM設定線上存在的建議方式
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 71a49353-5273-46ee-a1ff-5bbfe5b6b0b4
source-git-commit: c0bf6864bb344e582c4f88371c892d401ce2827c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 7%

---

# `We.Retail`參考實作{#we-retail-reference-implementation}

## 簡介 {#introduction}

`We.Retail`頁面是參考實作和範例內容，說明使用Adobe Experience Manager設定線上存在的建議方式。

`We.Retail`網站使用最新的Adobe Experience Manager (AEM)技術，例如HTL、回應式版面、可編輯的範本、核心元件等。

雖然它說明的是零售垂直專案，但網站設定方式可套用至任何垂直專案，而且只有產品目錄和購物車功能是零售專用的。

## 功能 {#features}

作為AEM的標準參考實作，`We.Retail`會展示AEM的一些最強大功能。

| **功能** | **說明** | **有興趣？** |
|---|---|---|
| [全域化網站結構](/help/sites-administering/tc-bp.md) | `We.Retail`包含即時複製到特定國家/地區網站的主要語言頁面。 | [試試看！](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [回應式配置](/help/sites-authoring/responsive-layout.md) | 所有頁面都具備回應式版面，可動態調整以符合熒幕和裝置大小。 | [試試看！](/help/sites-developing/we-retail-responsive-layout.md) |
| [可編輯的範本](/help/sites-developing/page-templates-editable.md) | 所有頁面都以可編輯的範本為基礎，可讓非開發人員調整及自訂範本。 | [試試看！](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML範本語言](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-htl/content/overview) | 所有元件都以HTL為基礎 |  |
| [核心元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/introduction) | 所有元件均以新的核心元件為基礎，且更易於使用及使用者設定 | [試試看！](/help/sites-developing/we-retail-core-components.md) |
| [內容片段](/help/assets/content-fragments/content-fragments.md) | `We.Retail`體驗區段會展示透過內容片段重複使用內容的力量。 | [試試看！](/help/sites-developing/we-retail-content-fragments.md) |
| [體驗片段](/help/sites-authoring/experience-fragments.md) | 體驗片段是一組一或多個元件，包括可在頁面中參考的內容和版面。 | [試試看！](/help/sites-developing/we-retail-experience-fragments.md) |

## 快速入門 {#getting-started}

`We.Retail`網站會傳遞為AEM的範例內容。 若要使用，只需[啟動AEM （如同您平常一樣）](/help/sites-deploying/deploy.md#getting-started)，並確定未停用範例內容。

>[!CAUTION]
>
>請勿在生產執行個體上安裝`We.Retail`。 生產執行個體應在`nosamplecontent` [執行模式](/help/sites-deploying/configure-runmodes.md)中啟動。

>[!CAUTION]
>
>`We.Retail`網站是以最新的AEM技術為基礎，因此不支援[傳統UI編寫](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md)。

### 最新版本 {#latest-version}

雖然`We.Retail`是隨AEM發行版本發行，但在發行版本之後可能會進行內容及其功能的更新。 因此，可以從GitHub [下載最新版本](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)，然後[上傳](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)並[將其安裝為AEM執行個體上的套件](/help/sites-administering/package-manager.md#installing-packages)。

### 首要步驟 {#first-steps}

1. 啟動AEM （和/或安裝`We.Retail`）後，**`We.Retail`**&#x200B;網站主控台[即可使用網站](/help/sites-authoring/basic-handling.md#global-navigation)。
1. 例如，可以開啟下列頁面，它應該會如下列[附錄](#appendix)中所示：

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## `We.Retail`與Geometrixx {#we-retail-geometrixx}

Geometrixx及其許多化身可作為舊版AEM的範例內容。 自6.3版開始，`We.Retail`一直是AEM提供的範例內容，可作為新的標準參考實作。

`We.Retail`網站在技術上更健全，利用最新的AEM技術更靈活、更可擴充，同時展示產品的最新功能。

### 功能比較 {#feature-comparison}

下表概略說明`We.Retail`中相較於Geometrixx可用的主要功能。

* **可用**&#x200B;表示在範例內容中找到該功能的範例。
* **無法使用**&#x200B;表示範例內容沒有功能範例，但功能仍可使用。


| **功能** | **`We.Retail`** | **Geometrixx** |
|---|---|---|
| 全域化網站結構 | 主要語言頁面會即時複製到特定國家的網站 | 無法使用 |
| 內容片段 | 可使用 | 無法使用 |
| 體驗片段 | 可使用 | 無法使用 |
| 回應式版面 | 針對所有頁面 | 僅限Geometrixx Media |
| 可編輯的範本 | 針對所有頁面 | 無法使用 |
| HTL | 所有元件 | 有限 |
| 目標定位 | 針對所有頁面 | 僅限Geometrixx Outdoors |
| 手稿 | 無法使用 | 可使用 |
| 轉盤檢視器、下載和圖表元件 | 無法使用 | 可使用 |
| 欄控制項 | 由版面容器取代 | 可使用 |
| Forms | 無法使用 | 可使用 |
| Campaign | 無電子郵件範例 | 可使用 |

>[!NOTE]
>
>此清單力求完整，但不應視為詳盡無遺。

## Contribute {#contribute}

`We.Retail`網站已發行為開放原始碼專案，而最新版本的原始程式碼可從GitHub下載。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼。

* 在GitHub上[開啟aem-sample-we-retail專案](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 將專案下載為[ZIP檔](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/zip/refs/heads/master)

最新版本也可以是[直接下載](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/tag/we.retail.reactor-4.0.0)作為可安裝的套件。

如果發生問題，請提出[GitHub問題](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues)。

您可以隨意使用[提取請求](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)來建立分支或協助撰寫。

## 預覽 {#preview}

`We.Retail`歡迎頁面預覽：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
