---
title: 通用編輯器
description: 瞭解通用編輯器的彈性，以及如何協助您使用AEM 6.5 LTS強化Headless體驗。
feature: Developing
role: Developer
exl-id: 495df631-5bdd-456b-b115-ec8561f33488
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 9%

---

# 關於通用編輯器 {#universal-editor}

瞭解通用編輯器的彈性，以及如何協助您使用AEM 6.5 LTS強化Headless體驗。

## 概觀 {#overview}

通用編輯器是一個多功能視覺化編輯器，是 Adobe Experience Manager Sites 的一部分。它可讓作者對任何Headless體驗進行即席即得(WYSIWYG)編輯。

* 作者可受益於Universal Editor的彈性。 它支援針對所有形式的AEM Headless內容進行相同一致的視覺化編輯。
* 開發人員可受益於Universal Editor的多功能性，因為它也支援實作的真正分離。 它可讓開發人員使用幾乎任何他們選擇的架構或架構，而不需要施加任何SDK或技術限制。

如需詳細資訊，請參閱通用編輯器[上的](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)AEM as a Cloud Service檔案。

## 架構 {#architecture}

Universal Editor是一項與AEM搭配使用的服務，可讓您無頭製作內容。

* Universal Editor託管於`https://experience.adobe.com/#/aem/editor/canvas`，可編輯AEM 6.5 LTS轉譯的頁面。
* 通用編輯器會從AEM編寫執行個體透過Dispatcher讀取AEM頁面。
* 與Dispatcher在相同主機上執行的Universal Editor服務會將變更寫回AEM作者例項。

![使用通用編輯器的作者流程](assets/author-flow.png)

## 要求 {#requirements}

下列專案支援通用編輯器：

* AEM 6.5 LTS GA
   * 內部部署和Adobe Managed Services (AMS)託管均受支援。
* [AEM 6.5](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * 支援內部部署和AMS託管。
* [AEM as a Cloud Service](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) （版本`2023.8.13099`或更新版本）

本檔案著重於通用編輯器的AEM 6.5 LTS支援。 若要搭配AEM 6.5 LTS使用通用編輯器，您需要下列專案：

* AEM 6.5 LTS GA
* Dispatcher已正確設定

## 設定 {#setup}

若要使用通用編輯器，請執行下列動作：

1. [在您的AEM編寫執行個體上設定服務。](#configure-aem)
1. [設定本機通用編輯器服務。](#set-up-ue)
1. [調整您的Dispatcher以允許Universal Editor服務。](#update-dispatcher)

完成設定之後，您可以[檢測應用程式以使用通用編輯器。](#instrumentation)

### 設定服務 {#configure-aem}

Universal Editor依賴許多必須設定的服務。

#### 設定`login-token` Cookie的SameSite屬性。 {#samesite-attribute}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Adobe Granite Token Authentication Handler**，然後按一下&#x200B;**變更組態值**。
1. 在對話方塊中，將登入權杖cookie **(**)值的`token.samesite.cookie.attr`SameSite屬性變更為`Partitioned`。
1. 按一下&#x200B;**儲存**。

#### 移除`SAMEORIGIN`標題X-Frame選項。 {#sameorigin}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Apache Sling主要Servlet**，然後按一下&#x200B;**編輯設定值**。
1. 刪除`X-Frame-Options=SAMEORIGIN`其他回應標頭&#x200B;**屬性(**)中的`sling.additional.response.headers`值（如果存在）。
1. 按一下&#x200B;**儲存**。

#### 設定Adobe Granite查詢引數驗證處理常式 {#query-parameter}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Adobe Granite查詢引數驗證處理常式**，然後按一下&#x200B;**編輯組態值**。
1. 在&#x200B;**路徑**&#x200B;欄位(`path`)中新增`/`以啟用。
   * 空值會停用驗證處理常式。
1. 按一下&#x200B;**儲存**。

#### 定義在通用編輯器中開啟的內容路徑或`sling:resourceTypes` {#paths}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到「**通用編輯器 URL 服務**」，然後按一下「**編輯設定值**」。
1. 定義應開啟通用編輯器的內容路徑或`sling:resourceTypes`。
   * 在「**通用編輯器開啟對應**」欄位中，提供通用編輯器的開啟路徑。
   * 在&#x200B;**Sling:resourceTypes （應由通用編輯器**&#x200B;欄位開啟）中，輸入通用編輯器直接開啟的資源清單。
1. 按一下&#x200B;**儲存**。
1. 檢查您的[外部器組態](/help/sites-developing/externalizer.md)，並確定您至少有本機、作者和發佈環境設定，如下列範例所示：

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

完成這些設定步驟後，AEM會依下列順序開啟頁面的通用編輯器：

1. AEM會檢查`Universal Editor Opening Mapping`底下的對應，如果內容位於此處定義的任何路徑下，則會為其開啟Universal Editor。

1. 針對`Universal Editor Opening Mapping`中定義路徑以外的內容，AEM會檢查內容`resourceType`是否符合&#x200B;**Sling:resourceTypes中的專案，此專案應由Universal Editor**&#x200B;開啟。 如果相符，AEM會在`${author}${path}.html`的通用編輯器中開啟內容。
1. 否則，AEM會開啟頁面編輯器。

下列變數可用來定義`Universal Editor Opening Mapping`下的對應。

* `path`：要開啟的資源內容路徑
* `localhost`： `localhost`的Externalizer專案沒有結構描述，例如`localhost:4502`
* `author`：沒有結構描述的作者的Externalizer專案，例如`localhost:4502`
* `publish`：用於沒有結構描述的發行的Externalizer專案，例如`localhost:4503`
* `preview`：預覽的外部化程式專案，不含結構描述，例如`localhost:4504`
* `env`：`prod`、`stage`、`dev`，根據所定義的 Sling 執行模式
* `token`：`QueryTokenAuthenticationHandler` 所需的查詢權杖

範例對應：

* 在 AEM Author 上開啟 `/content/foo` 之下的所有頁面：
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * 結果開啟`https://localhost:4502/content/foo/x.html?login-token=<token>`
* 在遠端NextJS伺服器上開啟`/content/bar`下的所有頁面，提供所有變數作為資訊
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 結果開啟`https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### 設定Universal Editor服務 {#set-up-ue}

更新並設定AEM後，您就可以設定本機通用編輯器服務，以供您自己的本機開發和測試使用。

1. 安裝Node.js version >=20。
1. 從[Software Distribution](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud/software-distribution/home)下載並解除封裝最新的Universal Editor服務
1. 透過環境變數或`.env`檔案設定Universal Editor Service。
   * [如需詳細資訊，請參閱AEM as a Cloud Service Universal Editor檔案。](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * 請注意，如果需要內部IP重寫，您可能需要使用`UES_MAPPING`選項。
1. 執行`universal-editor-service.cjs`

### 更新Dispatcher {#update-dispatcher}

設定AEM且執行本機Universal Editor Service時，您需要在Dispatcher中允許新服務[的反向Proxy。](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-dispatcher/using/dispatcher)

1. 調整編寫執行個體的vhost檔案，以包含反向Proxy。

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080是預設連線埠。 如果您使用`UES_PORT`您的[檔案，`.env`中的](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)引數變更此專案，您必須在此相應地調整連線埠值。

1. 重新啟動Apache。

## 檢測您的應用程式 {#instrumentation}

更新AEM並執行本機Universal Editor Service後，您就可以使用Universal Editor開始編輯Headless內容。

不過，您的應用程式必須經過檢測才能使用通用編輯器。 其中涉及加入中繼標籤，以指示編輯器如何以及在何處儲存內容。 此檢測的詳細資訊可在AEM as a Cloud Service的[通用編輯器檔案中取得。](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

請注意，在針對AEM as a Cloud Service通用編輯器編寫以下檔案時，將其與AEM 6.5 LTS搭配使用時套用以下變更。

* 中繼標籤中的通訊協定必須是`aem65`而非`aem`。

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* 必須透過meta標籤公告Universal Editor服務端點。

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* 在元件定義的`plugins`區段中，必須使用`aem65`而非`aem`。

>[!TIP]
>
>如需通用編輯器的完整開發人員指南，請參閱AEM as a Cloud Service檔案中的[AEM開發人員通用編輯器概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview)。 請注意本節所述的AEM 6.5 LTS變更。

## AEM 6.5 LTS與AEM as a Cloud Service的差異 {#differences}

AEM 6.5 LTS中的通用編輯器與AEM as a Cloud Service中的通用編輯器運作方式大致相同，包括UI和大部分設定。 不過，您應留意兩者間的差異。

* 6.5 LTS中的Universal Editor僅支援Headless使用案例。
* 通用編輯器的設定對6.5 LTS稍有不同（[如目前檔案所述](#setup)）。
* 6.5 LTS中的Universal Editor使用與AEM as a Cloud Service不同的資產選擇器和內容片段選擇器。
