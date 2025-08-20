---
title: ' [!DNL Adobe Experience Manager] 6.5 LTS的發行說明'
description: 尋找 Adobe Experience Manager 6.5 LTS 的最新發行資訊。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 650c3659a451787539c8aac4aff38423a24262c3
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 95%

---

# Adobe Experience Manager 6.5 LTS 的最新發行說明 {#release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 LTS |
| 類型 | 主要版本 |
| 正式發佈日期 | 2025 年 3 月 7 日 |

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS 是 [!DNL Adobe Experience Manager] 6.5 程式碼基底的升級版本。此版本提供重要的客戶修正、高優先順序的客戶增強功能，以及針對產品穩定化的一般錯誤修正。還包括最高至 SP22 的 [!DNL Adobe Experience Manager] 6.5 Service Pack 版本。

下列清單為概觀內容，而後續頁面列出完整的詳細資訊。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS 平台是以更新版本的 OSGi 式框架 (Apache Sling 和 Apache Felix) 以及 Java™ 內容存放庫 (Apache Jackrabbit Oak 1.68.x) 為基礎進行建置。

Eclipse Jetty 11.0.x 做為快速入門的 servlet 引擎。

#### Java™ 支援  {#java-support}

* Java™ 17 和 Java™ 21 的支援。
* 為獲得最佳效能，請使用其他值覆寫預設的 GC 值。如需詳細資訊，請參閱[安裝與更新](/help/sites-deploying/custom-standalone-install.md)區段。
* 若是 Oracle 尚未正式推出，Adobe 會分發 Java™ 17 和 Java™ 21 維護更新供客戶在 AEM 相關專案中使用。

#### Uberjar 封裝 {#uber-jar-packaging}

* AEM 6.5 LTS 的 Uberjar 封裝略有不同。如需詳細資訊，請參閱[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

#### 升級 {#upgrade}

* 關於升級程序的詳細資訊，請參閱[升級文件](/help/sites-deploying/upgrade.md)。

## 安裝與更新 {#install-update}

關於設定要求，請參閱[安裝指示](/help/sites-deploying/custom-standalone-install.md)。

如需詳細說明，請參閱[升級文件](/help/sites-deploying/upgrade.md)。

>[!NOTE]
>
> 對於全新的 AEM 6.5 LTS 安裝，必須獨立安裝索引定義。如需詳細資訊，請參閱[本文章](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)。

## 受支援平台 {#supported-platforms}

尋找受支援平台的完整矩陣，包括 [AEM 6.5 LTS 技術要求](/help/sites-deploying/technical-requirements.md)的支援等級。

>[!NOTE]
>
>建議與 AEM 6.5 LTS 搭配使用的版本為 Java™ 17/Java™ 21。

## 已棄用和移除的功能 {#deprecated-and-removed-features}

Adobe 會持續審閱產品功能，藉由更新或取代舊功能，提高客戶價值。進行這些變更時，皆會仔細留意回溯相容性。

若要傳達即將移除或取代 Adobe Experience Manager (AEM) 功能的訊息，請套用下列規則：

1. 首先公告功能已棄用。雖已棄用，功能仍可繼續使用，但往後不會再進行增強。
1. 最早會於下一個主要版本中移除已棄用的功能。移除的實際目標日期依規劃稍後公告。

此程序讓客戶在實際移除功能之前，至少還有一個發行週期的時間可以調整其實施方案，使其適應已棄用功能的新版本或後續功能。

### 已棄用功能 {#deprecated-features}

此區段列出 Adobe 在 AEM 6.5 LTS 中已棄用的特點與功能。通常，在未來版本中移除某些功能之前，Adobe 會先將棄用該功能並提供替代方案。


建議客戶檢查其目前的部署中是否使用這些特點/功能，並規劃變更其實施方案，改用所提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
|---|---|---|---|
| Sites | [SPA 編輯器](/help/sites-developing/spa-overview.md) | AEM 中用於管理 Headless 內容的首選編輯器為：<br>- [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。<br>- [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。 | 6.5 LTS 正式發佈版 |

### 移除的功能 {#removed-features}

此區段列出 AEM 6.5 LTS 已移除的特點和功能。先前的版本已將這些功能標記為已棄用。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
|--- |--- |--- |--- |
| Commerce | 不支援 AEM CIF Classic。 | 移轉至 [AEM CIF](/help/commerce/cif/migration.md)。 | 6.5 LTS 正式發佈版 |
| 解決方案 | 不支援 Social/Communities。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Screens | 不支援 Screens。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Assets | 不支援 `dam-pim` 及 `dam-rating`，因為搭售方案需依賴 Social。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Assets | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` 已移除。 | 使用已新增的替代 API `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()`。 | 6.5 LTS 正式發佈版 |
| Portal | 不支援 AEM Portal Director。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Granite | 搭售方案 `com.adobe.granite.socketio` 已移除。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Granite | 不支援 `com.adobe.granite.crx-explorer`。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Granite | 不支援 `crx2oak`。 | 挑選相關版本的[Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) | 6.5 LTS 正式發佈版 |
| Adobe | 不支援 `com.adobe.cq.cq-searchpromote-integration`。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Guava | AEM 中所有的 guava 相依性都已移除，因此 `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` 搭售方案不再屬於 AEM 的一部分。 | 客戶若需依賴 guava，可以自行新增 guava，或在可能的情況下使用 Java 集合或其他替代方案取代 guava 程式碼。 | 6.5 LTS 正式發佈版 |
| `We.Retail` | 不支援`We-retail`範例網站。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | 不支援 `oak-solr-osgi` 搭售方案。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | 不支援 `org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom`，以及 `org.apache.sling.atom.taglib`。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | `org.apache.commons.io` 封裝現在從 `org.apache.commons.commons-io` 匯出。 | 不需要變更。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | `javax.mail` 封裝從 `com.sun.javax.mail` 搭售方案匯出。 | 不需要變更。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | `org.apache.jackrabbit.api` 封裝現在從 `org.apache.jackrabbit.oak-jackrabbit-api` 搭售方案匯出。 | 不需要變更。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | 不支援 `com.github.jknack.handlebars` | 選擇相關的[版本](https://mvnrepository.com/artifact/com.github.jknack/handlebars) | 6.5 LTS 正式發佈版 |

## 已知問題 {#known-issues}

### AEM 6.5.21-6.5.23 和 AEM 6.5 LTS 正式發佈版中的 JSP 指令碼搭售方案的問題

AEM 6.5.21、6.5.22、6.5.23 和 AEM 6.5 LTS 正式發佈版隨附 `org.apache.sling.scripting.jsp:2.6.0` 搭售方案，其中包含一個已知問題。通常在 AEM 實例同時處理許多請求而造成高負載的情況下，就會發生這個問題。

發生此問題時，錯誤記錄中可能會出現以下其中一項異常，並且參照 `org.apache.sling.scripting.jsp:2.6.0`：

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

可以使用 Hotfix [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) 解決此問題。

### 僅限 SSL 功能導致 Dispatcher 連線失敗 {#ssl-only-feature}

在 AEM 部署中啟用僅限 SSL 功能時，有一項已知問題會影響 Dispatcher 和 AEM 實例之間的連線。啟用此功能後，健康情況檢查可能會失敗，且 Dispatcher 和 AEM 實例之間的通訊可能會中斷。當客戶嘗試透過`https + IP`從Dispatcher連線到AEM執行個體時，就會發生此問題。 它與SNI （伺服器名稱指示）驗證問題有關。

**影響：**

* 健康情況檢查失敗，回應代碼為 HTTP 400
* Dispatcher 與 AEM 實例之間的流量中斷
* 無法透過 Dispatcher 正確地提供內容
* 利用 Dispatcher 設定中的 IP 位址進行 HTTPS 連線失敗
* 透過 HTTPS + IP 連線時出現 HTTP 400「無效 SNI」錯誤

**受影響的環境：**

* 具有 Dispatcher 設定的 AEM 部署
* 已啟用僅限 SSL 功能的系統
* 使用 `https + IP` 方法連線至 AEM 實例的 Dispatcher 設定

**解決方案：**
若您遇到此問題，請聯絡 Adobe 客戶支援。可以使用 Hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 解決此問題。在套用必要的 Hotfix 之前，請勿嘗試啟用僅限 SSL 功能。

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [在 licensing.adobe.com 下載產品](https://licensing.adobe.com/)
* [聯絡 Adobe 客戶支援](https://experienceleague.adobe.com/zh-hant/docs/customer-one/using/home)。

