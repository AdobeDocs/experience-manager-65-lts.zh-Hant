---
title: Adobe Experience Manager 6.5 LTS目前發行說明
description: 尋找Adobe Experience Manager 6.5 LTS的最新發行資訊。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: abba652bb5d7eb9b5f902ce99c07f2186e313173
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 12%

---

# Adobe Experience Manager 6.5 LTS目前發行說明 {#release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5磅 |
| 類型 | 主要版本 |
| 正式發行日期 | 2025年3月7日 |

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS是[!DNL Adobe Experience Manager] 6.5程式碼基底的升級版本。 它提供重要的客戶修正、高優先順序的客戶增強功能，以及針對產品穩定化的一般錯誤修正。 其中也包含[!DNL Adobe Experience Manager]個6.5 Service Pack發行版本，最高至SP22。

下列清單提供概述，後續頁面則列出完整詳細資訊。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS的平台建置在OSGi架構的更新版本（Apache Sling和Apache Felix）以及Java™內容存放庫： Apache Jackrabbit Oak 1.68.x之上。

Eclipse Jetty 11.0.x作為Quickstart的servlet引擎使用。

#### Java™支援  {#java-support}

* 支援Java™ 17和Java™ 21。
* 為獲得最佳效能，請以其他值覆寫預設GC值。 如需詳細資訊，請參閱[安裝與更新](/help/sites-deploying/custom-standalone-install.md)區段。
* 當Oracle未公開提供客戶在AEM相關專案中使用時，Adobe會發佈Java™ 17和Java™ 21維護更新。

#### Uberjar封裝 {#uber-jar-packaging}

* AEM 6.5 LTS的Uberjar封裝稍有不同。 如需詳細資訊，請參閱[更新AEM Uber Jar版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

#### 升級 {#upgrade}

* 如需有關升級程式的詳細資訊，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。

## 安裝與更新 {#install-update}

如需安裝需求，請參閱[安裝指示](/help/sites-deploying/custom-standalone-install.md)。

如需詳細指示，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。

## 支援平台 {#supported-platforms}

尋找支援平台的完整矩陣，包括[AEM 6.5 LTS技術需求](/help/sites-deploying/technical-requirements.md)的支援層級。

>[!NOTE]
>
>Java™ 17/Java™ 21是搭配AEM 6.5 LTS使用的建議版本。

## 過時和移除的功能 {#deprecated-and-removed-features}

Adobe會持續審視產品功能，以透過更新或取代舊功能來提升客戶價值。 進行這些變更時，會留意回溯相容性。

若要傳達Adobe Experience Manager (AEM)功能即將移除或取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。雖然已棄用，功能仍可使用，但不會進一步增強。
1. 後續最新主要發行版本，則將最先移除已棄用的功能。 實際的目標移除日期計畫稍後公告。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

### 已棄用的功能 {#deprecated-features}

本節列出Adobe在AEM 6.5 LTS中已棄用的功能。 在未來版本中移除功能之前，Adobe通常會先淘汰這些功能，並提供替代方案。


建議客戶檢閱是否在目前的部署中使用這些功能，並規劃變更實作，改用所提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本(SP) |
|---|---|---|---|
| Sites | [SPA 編輯器](/help/sites-developing/spa-overview.md) | AEM 中用於管理 Headless 內容的首選編輯器為：<br>- [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。<br>- [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。 | 6.5 LTS GA |

### 移除的功能 {#removed-features}

本節列出已從AEM 6.5 LTS移除的功能。 舊版將這些功能標籤為已過時。

| 區域 | 功能 | 替代方案 | 版本(SP) |
|--- |--- |--- |--- |
| Commerce | 不支援AEM CIF Classic。 | 移轉至[AEM CIF](/help/commerce/cif/migration.md)。 | 6.5 LTS GA |
| 解決方案 | 不支援社交/社群。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Screens | 不支援Screens。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Assets | 不支援`dam-pim`和`dam-rating`，因為套件組合依存於social。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Assets | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()`已移除。 | 使用已新增的替代api `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()`。 | 6.5 LTS GA |
| 入口網站 | 不支援AEM Portal Director。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Granite | 組合`com.adobe.granite.socketio`已移除。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Granite | 不支援`com.adobe.granite.crx-explorer`。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| Granite | 不支援`crx2oak`。 | 挑選相關版本的[Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) | 6.5 LTS GA |
| Adobe | 不支援`com.adobe.cq.cq-searchpromote-integration`。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| 瓜瓦 | 所有Guava相依性現在在AEM中移除，因此`com.adobe.granite.osgi.wrapper.guava-15.0.0-0002`套件組合並非AEM的一部分。 | 如果客戶依賴Guava，則可自行新增Guava，或儘可能以Java集合或其他替代專案取代Guava程式碼。 | 6.5 LTS GA |
| We.Retail | 不支援We-Retail範例網站。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| 開放原始碼 | 不支援`oak-solr-osgi`組合。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| 開放原始碼 | 不支援`org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom`和`org.apache.sling.atom.taglib`。 | 沒有可用的替代專案。 | 6.5 LTS GA |
| 開放原始碼 | 已從`org.apache.commons.commons-io`匯出`org.apache.commons.io`個套件。 | 不需要變更。 | 6.5 LTS GA |
| 開放原始碼 | 正在從`com.sun.javax.mail`套件組合匯出`javax.mail`個套件。 | 不需要變更。 | 6.5 LTS GA |
| 開放原始碼 | `org.apache.jackrabbit.api`個套件現在已從`org.apache.jackrabbit.oak-jackrabbit-api`套件組合匯出。 | 不需要變更。 | 6.5 LTS GA |
| 開放原始碼 | 不支援`com.github.jknack.handlebars` | 挑選相關的[版本](https://mvnrepository.com/artifact/com.github.jknack/handlebars) | 6.5 LTS GA |

## 已知問題 {#known-issues}

### AEM 6.5.21-6.5.23和AEM 6.5 LTS GA**中的JSP指令碼套件組合問題

AEM 6.5.21、6.5.22、6.5.23和AEM 6.5 LTS GA隨附`org.apache.sling.scripting.jsp:2.6.0`套件，其中包含已知問題。 AEM執行個體處理許多並行請求時，高負載下通常會發生問題。

發生此問題時，下列其中一個例外可能會與對`org.apache.sling.scripting.jsp:2.6.0`的參考一起出現在錯誤記錄中：

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

發生此錯誤時，唯一的復原方法是重新啟動AEM執行個體。

請聯絡Adobe客戶支援，並參閱此版本注意事項以尋求解決方案。

### 僅SSL功能的Dispatcher連線失敗 {#ssl-only-feature}

在AEM部署中啟用SSL專用功能時，有一個已知問題會影響Dispatcher與AEM執行個體之間的連線。 啟用此功能後，健康情況檢查可能會失敗，而Dispatcher與AEM執行個體之間的通訊可能會中斷。

**影響：**

* HTTP 500回應代碼的健康情況檢查失敗
* Dispatcher與AEM執行個體之間的流量中斷
* 無法透過Dispatcher正確提供內容

**受影響的環境：**

* AEM部署搭配Dispatcher設定
* 已啟用僅SSL功能的系統

**解決方案：**
如果您遇到此問題，請聯絡Adobe客戶支援。 Hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.0.zip)可用來解決此問題。 在套用必要的Hotfix之前，請勿嘗試啟用僅限SSL的功能。

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是客戶且需要存取權，請聯絡您的Adobe客戶經理。

* [產品下載網址為licensing.adobe.com](https://licensing.adobe.com/)
* [連絡Adobe客戶支援](https://experienceleague.adobe.com/en/docs/customer-one/using/home)。

