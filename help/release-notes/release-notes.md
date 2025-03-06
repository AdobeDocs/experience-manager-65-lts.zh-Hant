---
title: Adobe Experience Manager 6.5 LTS目前發行說明
description: 以下是Adobe Experience Manager 6.5 LTS目前的發行說明。
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: f9fefb530e9cdcced664bede2e11556ab0345876
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 22%

---

# Adobe Experience Manager 6.5 LTS目前發行說明 {#release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5磅 |
| 類型 | 主要版本 |
| 正式發行日期 | 2025年3月7日 |

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS是[!DNL Adobe Experience Manager] 6.5程式碼基底的升級版本。 此版本提供全新的增強功能、重要客戶修正、高優先順序的客戶增強功能，以及針對產品穩定化的一般錯誤修正。其中也包含[!DNL Adobe Experience Manager]個6.5 Service Pack發行版本，最高至SP22。

下列清單提供概述，後續頁面則列出完整詳細資訊。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS的平台建置在OSGi架構的更新版本（Apache Sling和Apache Felix）以及Java™內容存放庫： Apache Jackrabbit Oak 1.68.x之上。

快速入門使用Eclipse Jetty 11.0.x作為servlet引擎。

#### Java™支援  {#java-support}

* 支援Java™ 17。
* 為獲得最佳效能，請以其他值覆寫預設GC值。 如需詳細資訊，請參閱[安裝與更新](/help/sites-deploying/custom-standalone-install.md)區段。
* Adobe會發佈Java™ 17維護更新，以供客戶在AEM相關專案中使用(若未從Oracle公開提供)。

#### Uberjar封裝 {#uber-jar-packaging}

* AEM 6.5 LTS的Uberjar封裝稍有不同。 如需詳細資訊，[請參考](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version-update-the-aem-uber-jar-version)。

#### 升級 {#upgrade}

* 如需有關升級程式的詳細資訊，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。

## 安裝與更新 {#install-update}

如需安裝需求，請參閱[安裝指示](/help/sites-deploying/custom-standalone-install.md)。

如需詳細指示，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。

## 支援平台 {#supported-platforms}

尋找支援平台的完整矩陣，包括[AEM 6.5 LTS技術需求](/help/sites-deploying/technical-requirements.md)的支援層級。

>[!NOTE]
>
>Java™ 17是搭配AEM 6.5 LTS使用的建議版本。

## 過時和移除的功能 {#deprecated-and-removed-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

若要傳達Adobe Experience Manager (AEM)功能即將移除或取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。雖然已棄用，功能仍可使用，但不會進一步增強。
1. 後續最新主要發行版本，則將最先移除已棄用的功能。 實際的目標移除日期將於稍後宣佈。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

### 已棄用的功能 {#deprecated-features}

本節提供AEM 6.5 LTS中標示為過時的功能。 通常，未來新發行版本預計移除的功能，將先設為過時並提供其他選項。

建議客戶檢閱是否在目前的部署中使用這些功能，並規劃變更實作，改用所提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本(SP) |
|---|---|---|---|
| Sites | [SPA 編輯器](/help/sites-developing/spa-overview.md) | AEM 中用於管理 Headless 內容的首選編輯器為：<br>- [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。<br>- [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。 | 6.5 LTS GA |

### 移除的功能 {#removed-features}

本節列出已從AEM 6.5 LTS移除的功能。 舊版將這些功能標籤為已過時。

| 區域 | 功能 | 替代方案 | 版本(SP) |
|--- |--- |--- |--- |
| Commerce | 不支援AEM CIF Classic。 | 您應該移轉至[AEM CIF](/help/commerce/cif/migration.md)。 | 6.5 LTS GA |
| 解決方案 | 不支援社交/社群。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Screens | 不支援Screens。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Assets | 不支援`dam-pim`和`dam-rating`，因為套件組合依存於social。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Assets | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()`已移除。 | 使用已新增的替代api `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()`。 | 6.5 LTS GA |
| 入口網站 | 不支援AEM Portal Director。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Granite | 組合`com.adobe.granite.socketio`已移除。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Granite | 不支援`com.adobe.granite.crx-explorer`。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Granite | 不支援`crx2oak`。 | 挑選相關的[Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade)版本 | 6.5 LTS GA |
| Adobe | 不支援`com.adobe.cq.cq-searchpromote-integration`。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| 瓜瓦 | 所有Guava相依性現在在AEM中移除，因此`com.adobe.granite.osgi.wrapper.guava-15.0.0-0002`套件組合並非AEM的一部分。 | 如果客戶依賴Guava，則可自行新增Guava，或儘可能以Java集合或其他替代專案取代Guava程式碼。 | 6.5 LTS GA |
| We.Retail | 不支援We-Retail範例網站。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| 開放原始碼 | 不支援`oak-solr-osgi`組合。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| 開放原始碼 | 不支援`org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom`和`org.apache.sling.atom.taglib`。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| 開放原始碼 | 已從`org.apache.commons.commons-io`匯出`org.apache.commons.io`個套件。 | 不需要變更。 | 6.5 LTS GA |
| 開放原始碼 | 正在從`com.sun.javax.mail`套件組合匯出`javax.mail`個套件。 | 不需要變更。 | 6.5 LTS GA |
| 開放原始碼 | `org.apache.jackrabbit.api`個套件現在已從`org.apache.jackrabbit.oak-jackrabbit-api`套件組合匯出。 | 不需要變更。 | 6.5 LTS GA |
| 開放原始碼 | 不支援`com.github.jknack.handlebars` | 挑選相關的[版本](https://mvnrepository.com/artifact/com.github.jknack/handlebars) | 6.5 LTS GA |

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [連絡Adobe客戶支援](https://experienceleague.adobe.com/en/docs/customer-one/using/home)。

