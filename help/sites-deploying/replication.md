---
title: 複製
description: 瞭解如何在Adobe Experience Manager中設定和監控復寫代理。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: b840d970-9365-4df3-8467-e34abd940074
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '3270'
ht-degree: 2%

---

# 複製{#replication}

復寫代理程式是Adobe Experience Manager (AEM)的核心，因為此機制可用於：

* 從作者[發佈（啟動）](/help/sites-authoring/publishing-pages.md#activatingcontent)內容至發佈環境。
* 明確從Dispatcher快取排清內容。
* 將使用者輸入（例如表單輸入）從發佈環境傳回至作者環境（在作者環境的控制下）。

請求[已排入佇列](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler)給適當的代理程式處理。

>[!NOTE]
>
>使用者資料（使用者、使用者群組和使用者設定檔）不會在製作和發佈執行個體之間復寫。
>
>對於多個Publish執行個體，啟用[使用者同步處理](/help/sites-administering/sync.md)時，使用者資料會進行Sling散發。

## 從作者復寫至發佈 {#replicating-from-author-to-publish}

復寫至發佈執行個體或Dispatcher需要幾個步驟：

* 作者要求發佈（啟動）特定內容；這可以由手動要求或預先設定的自動觸發程式啟動。
* 此請求會傳遞至適當的預設復寫代理程式；一個環境可以有多個預設代理程式，這些代理程式一律會選取用於此類動作。
* 復寫代理程式會「封裝」內容，並將其置於復寫佇列中。
* 在[網站]索引標籤中，已為個別頁面設定[彩色狀態指示器](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus)。
* 內容會從佇列中提取，並使用設定的通訊協定傳輸至發佈環境；這通常是HTTP。
* 發佈環境中的servlet會接收要求並發佈接收的內容；預設servlet為`https://localhost:4503/bin/receive`。

* 可以設定多個作者和發佈環境。

![chlimage_1-21](assets/chlimage_1-21.png)

### 從發佈復寫至作者 {#replicating-from-publish-to-author}

部分功能可讓使用者在發佈執行個體上輸入資料。

有時候，需要有一種稱為反向復寫的復寫型別，將此資料傳回至製作環境，再從此處重新分配至其他發佈環境。 基於安全性考量，從發佈到製作環境的任何流量都必須受到嚴格控制。

反向復寫會在參照製作環境的發佈環境中使用代理程式。 此代理程式會將資料放入寄件匣。 此寄件匣與製作環境中的復寫接聽程式相符。 監聽器會輪詢寄件匣，以收集輸入的任何資料，然後視需要加以散發。 這可確保作者環境可控制所有流量。

### 復寫 — 立即可用 {#replication-out-of-the-box}

依照[建立及組織頁面](/help/sites-authoring/managing-pages.md)來建立頁面。

若要遵循此範例並使用預設的復寫代理程式，[安裝AEM](/help/sites-deploying/deploy.md)並包含：


* 連線埠`4502`上的作者環境
* 通訊埠`4503`上的發佈環境

系統會從製作環境執行下列動作來執行此復寫：

* **預設代理程式（發佈）**
此代理程式會將內容復寫至預設的發佈執行個體。
您可以從製作環境的「工具」主控台存取此專案的詳細資訊（設定和記錄）；或：
  `http://localhost:4502/etc/replication/agents.author/publish.html`。

>[!NOTE]
>
>預設為啟用：
>
>* 作者代理程式：預設代理程式（發佈），如果沒有，在繼續之前請務必啟用。
>
>預設會有效停用(自AEM 6.1起) ：
>
>* 製作代理程式：反向復寫代理程式(publish_reverse)
>* 發佈代理程式：反向復寫（寄件匣）
>
>若要檢查代理程式或佇列的狀態，請使用&#x200B;**工具**&#x200B;主控台。
>請參閱[監視您的復寫代理程式](#monitoring-your-replication-agents)。

#### 復寫（作者至發佈） {#replication-author-to-publish}

1. 導覽至作者環境上的支援頁面。
   **https://localhost:4502/content/site1/test.html** `<pi>`
1. 編輯頁面，以便新增一些文字。
1. **啟動頁面**，以便發佈變更。
1. 在發佈環境中開啟支援頁面：
   **https://localhost:4503/content/site1/test.html**
1. 您現在可以看到您在Author上輸入的變更。


#### 復寫代理程式 — 立即可用 {#replication-agents-out-of-the-box}

標準AEM安裝提供下列代理程式：

* [預設代理程式](#replication-author-to-publish)
用於從Author復寫至Publish。

* Dispatcher Flush
此項用於管理Dispatcher快取。 如需詳細資訊，請參閱[使編寫環境中的Dispatcher快取失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=zh-Hant#invalidating-dispatcher-cache-from-the-authoring-environment)和[使發佈執行個體中的Dispatcher快取失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=zh-Hant#invalidating-dispatcher-cache-from-a-publishing-instance)。

* [反向復寫](#configuring-reverse-replication)
用於從發佈復寫至作者。 反向復寫不適用於Communities功能，例如論壇、部落格和評論。 由於未啟用寄件匣，因此此功能實際上已停用。 使用反向復寫需要自訂設定。

* 靜態代理程式
這是「將節點的靜態表示儲存到檔案系統中的代理程式」。
例如，使用預設設定時，內容頁面和DAM資產會以HTML或適當資產格式的形式儲存在`/tmp`下。 檢視設定的`Settings`和`Rules`標籤。
已要求此專案，以便當直接從應用程式伺服器要求頁面時，可以看到內容。 這是專門的代理程式，（可能）在大多數執行個體中並非必要。

## 復寫代理程式 — 設定引數 {#replication-agents-configuration-parameters}

從「工具」控制檯設定復寫代理程式時，對話方塊中有四個索引標籤可用：

### 設定 {#settings}

* **名稱**

  復寫代理的唯一名稱。

* **說明**

  此復寫代理程式用途的說明。

* **已啟用**

  表示復寫代理程式是否已啟用。

  代理程式為&#x200B;**已啟用**&#x200B;時，佇列會顯示為：

   * 處理專案時&#x200B;**使用中**。
   * 佇列為空時&#x200B;**閒置**。
   * 專案在佇列中時&#x200B;**已封鎖**，但無法處理；例如，接收佇列已停用。

* **序列化型別**

  序列化的型別：

   * **預設**：設定是否自動選取代理程式。
   * **Dispatcher Flush**：如果要使用代理程式來排清Dispatcher快取，請選取此選項。

* **重試延遲**

  若發生問題，兩次重試之間的延遲（等待時間，以毫秒為單位）。

  預設： `60000`

* **代理程式使用者ID**

  根據環境，代理程式會使用此使用者帳戶來：

   * 從製作環境收集內容並封裝
   * 在發佈環境中建立和寫入內容

  將此欄位保留空白以使用系統使用者帳戶（在sling中定義為管理員使用者的帳戶；預設為`admin`）。

  >[!CAUTION]
  >
  >對於作者環境上的代理程式，此帳戶&#x200B;*必須*&#x200B;擁有您要復寫之所有路徑的讀取存取權。

  >[!CAUTION]
  >
  >對於發佈環境上的代理程式，此帳戶&#x200B;*必須*&#x200B;具有復寫內容所需的建立/寫入許可權。

  >[!NOTE]
  >
  >這可用來作為選取復製作業特定內容的機制。

* **記錄層級**

  指定用於記錄訊息的詳細資訊等級。

   * `Error`：僅記錄錯誤
   * `Info`：記錄錯誤、警告和其他資訊訊息
   * `Debug`：訊息中使用高層級的詳細資料，主要用於偵錯

  預設： `Info`

* **用於反向復寫**

  指出此代理程式是否用於反向復寫；從發佈環境傳回使用者輸入至製作環境。

* **別名更新**

  選取此選項可啟用Dispatcher的別名或虛名路徑失效請求。 另請參閱[設定Dispatcher Flush代理程式](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent)。

#### 傳輸 {#transport}

* **URI**

  這會指定目標位置的接收servlet。 尤其是，您可以在此處指定目標執行個體的主機名稱（或別名）和內容路徑。

  例如：

   * 預設代理程式可以復寫至`https://localhost:4503/bin/receive`
   * Dispatcher Flush代理程式可能會復寫至`https://localhost:8000/dispatcher/invalidate.cache`

  此處指定的通訊協定（HTTP或HTTPS）會決定傳輸方法。

  對於Dispatcher Flush代理程式，只有當您使用以路徑為根據的虛擬主機專案來區分陣列時，才會使用URI屬性，而您會使用此欄位來鎖定要失效的陣列。 例如，陣列 #1 的虛擬主機為 `www.mysite.com/path1/*`，而陣列 #2 的虛擬主機為 `www.mysite.com/path2/*`。您可以使用URL `/path1/invalidate.cache`來鎖定第一個伺服器陣列，並使用`/path2/invalidate.cache`來鎖定第二個伺服器陣列。

* **使用者**

  用於存取目標的帳戶使用者名稱。

* **密碼**

  用於存取目標的帳戶密碼。

* **NTLM網域**

  NTML驗證的網域。

* **NTLM主機**

  NTML驗證的主機。

* **啟用寬鬆SSL**

  如果您希望接受自我認證的SSL憑證，請啟用。

* **允許過期的憑證**

  若要接受過期的SSL憑證，請啟用。

#### Proxy {#proxy}

只有在需要Proxy時，才需要下列設定：

* **Proxy主機**

  用於傳輸的Proxy主機名稱。

* **代理主機連線埠**

  Proxy的連線埠。

* **Proxy使用者**

  要使用的帳戶使用者名稱。

* **Proxy密碼**

  要使用的帳戶密碼。

* **Proxy NTLM網域**

  代理NTLM網域。

* **Proxy NTLM主機**

  代理NTLM網域。

#### 延伸 {#extended}

* **介面**

  您可以在此處定義要繫結的通訊端介面。

  這會設定建立連線時要使用的本機位址。 如果未設定，則使用預設地址。 這對於指定要在多主伺服器或叢集化系統上使用的介面非常有用。

* **HTTP方法**

  要使用的HTTP方法。

  對於Dispatcher Flush代理程式，這幾乎永遠是GET且不應變更（POST是另一個可能的值）。

* **HTTP標頭**

  這些用於Dispatcher Flush代理程式，並指定必須清除的元素。

  若為Dispatcher Flush代理程式，三個標準專案不需要變更：

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

  在適當情況下，這些字元可用於指出排清控制代碼或路徑時要使用的動作。 子引數是動態的：

   * `{action}`表示復寫動作

   * `{path}`表示路徑

  這些變數會由與請求相關的路徑/動作取代，因此不需要「硬式編碼」：

  >[!NOTE]
  >
  >如果您已在非建議預設內容的內容中安裝AEM，則您必須在HTTP標頭中註冊該內容。 例如：
  >`CQ-Handle:/<*yourContext*>{path}`

* **關閉連線**

  啟用，以便您在每次請求後都可關閉連線。

* **連線逾時**

  嘗試建立連線時要套用的逾時（毫秒）。

* **通訊端逾時**

  建立連線後等待流量時所套用的逾時（毫秒）。

* **通訊協定版本**

  通訊協定的版本。 例如，HTTP/1.0為`1.0`。

#### 觸發器 {#triggers}

這些設定是用來定義自動復寫的觸發程式：

* **忽略預設值**

  如果勾選，代理將從預設復寫中排除；這意味著如果內容作者發出復寫動作，則不會使用代理。

* **修改**

  在此，當頁面修改時，將自動觸發此代理程式的復寫。 用於Dispatcher Flush代理程式，也用於反向復寫。

* **在散發中**

  如果勾選，代理程式會在修改內容時自動複製標籤為分發的任何內容。

* 已達到&#x200B;**開啟/關閉時間**

  當為頁面定義的時間或折扣發生時，就會觸發自動復寫（以視需要啟用或停用頁面）。 這主要用於Dispatcher Flush代理程式。

* 接收時&#x200B;**&#x200B;**

  如果勾選，代理會在接收到復寫事件時進行復寫。

* **無狀態更新**

  選取後，代理程式不會強制復寫狀態更新。

* **沒有版本設定**

  選取後，代理程式不會強制活動頁面的版本設定。

## 設定復寫代理 {#configuring-your-replication-agents}

### 從製作環境設定復寫代理 {#configuring-your-replication-agents-from-the-author-environment}

在製作環境的[工具]索引標籤中，您可以設定位於製作環境（**製作代理程式**）或發佈環境（**發佈代理程式**）中的復寫代理程式。 以下程式說明為Author環境設定代理程式，但可用於兩者。

>[!NOTE]
>
>當Dispatcher處理製作或發佈執行個體的HTTP請求時，來自復寫代理程式的HTTP請求必須包含PATH標頭。 除了下列程式外，您必須將PATH標頭新增到Dispatcher的使用者端標頭清單。 請參閱[/clientheaders (Client Headers)](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant#specifying-the-http-headers-to-pass-through-clientheaders)。
>

1. 存取AEM中的&#x200B;**工具**&#x200B;索引標籤。
1. 按一下&#x200B;**復寫** （左窗格以開啟資料夾）。
1. 在作者&#x200B;**上（左窗格或右窗格）連按兩下**&#x200B;代理程式。
1. 按一下適當的代理程式名稱（連結）以顯示該代理程式的詳細資訊。
1. 按一下&#x200B;**編輯**&#x200B;以開啟設定對話方塊：

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 提供的值應足以進行預設安裝。 若您進行變更，請按一下[確定] **&#x200B;**&#x200B;以儲存變更（如需個別引數的詳細資訊，請參閱[復寫代理程式 — 設定引數](#replication-agents-configuration-parameters)）。

>[!NOTE]
>
>AEM的標準安裝指定`admin`為預設復寫代理程式內傳輸認證的使用者。
>
>這應該變更為具有複製所需路徑之許可權的站台特定複製使用者帳戶。

### 設定反向復寫 {#configuring-reverse-replication}

反向復寫是用來將發佈執行個體上產生的使用者內容傳回作者執行個體。 這通常用於調查和登錄檔單等功能。

基於安全理由，大多數網路拓撲不允許連線&#x200B;*來自*&#x200B;的「非軍事區域」（將外部服務公開給不受信任的網路，例如網際網路的子網路）。

由於發佈環境通常位於DMZ，若要將內容取回製作環境，必須從製作執行個體起始連線。 這是透過下列專案完成的：

* 內容所在的發佈環境中的&#x200B;*寄件匣*。
* 製作環境中的代理程式（發佈），會定期輪詢寄件匣以尋找新內容。

若要這麼做，您需要：

**作者環境中的反向復寫代理程式** — 作為作用中元件，從發佈環境中的寄件匣收集資訊：

如果您想要使用反向復寫，請確定此代理程式已啟用。

![chlimage_1-23](assets/chlimage_1-23.png)

**發佈環境（寄件匣）中的反向復寫代理程式** — 當做寄件匣時的被動元素。 使用者輸入會放置在這裡，由代理程式在製作環境中收集。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### 為多個發佈執行個體設定復寫 {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>僅複製內容 — 不複製使用者資料（使用者、使用者群組和使用者設定檔）。
>
>若要同步處理多個發佈執行個體的使用者資料，請啟用[使用者同步處理](/help/sites-administering/sync.md)。

安裝後，已設定預設代理程式，以便將內容復寫至在localhost的連線埠4503上執行的發佈執行個體。

若要設定其他發佈執行個體的內容復寫，請建立並設定新的復寫代理程式：

1. 開啟AEM中的&#x200B;**工具**&#x200B;標籤。
1. 在左側面板中選取&#x200B;**復寫**，然後選取&#x200B;**作者代理程式**。
1. 選取&#x200B;**新增……**。
1. 設定&#x200B;**標題**&#x200B;和&#x200B;**名稱**，然後選取&#x200B;**復寫代理程式**。
1. 按一下[建立&#x200B;**&#x200B;**]以建立代理程式。
1. 連按兩下新代理程式專案，組態面板就會開啟。
1. 按一下&#x200B;**編輯** - **代理程式設定**&#x200B;對話方塊開啟 — **序列化型別**&#x200B;已定義為預設，必須保持此狀態。

   * 在&#x200B;**設定**&#x200B;索引標籤中：

      * 啟動&#x200B;**已啟用**。
      * 輸入&#x200B;**描述**。
      * 將&#x200B;**重試延遲**&#x200B;設定為`60000`。

      * 將&#x200B;**序列化型別**&#x200B;保留為`Default`。

   * 在&#x200B;**傳輸**&#x200B;索引標籤中：

      * 輸入新發佈執行個體的必要URI；例如，

        `https://localhost:4504/bin/receive`。

      * 輸入用於復寫的站台特定使用者帳戶。
      * 您可以視需要設定其他引數。

1. 按一下&#x200B;**「確定」**。

接著，您可以在作者環境中更新，然後發佈頁面，以測試操作。

更新會顯示在已依上述方式設定的所有發佈執行個體上。

如果您遇到任何問題，可以檢視Author執行個體上的記錄。 視所需的詳細程度而定，您也可以使用上述&#x200B;**代理程式設定**&#x200B;對話方塊，將&#x200B;**記錄層級**&#x200B;設定為`Debug`。

>[!NOTE]
>
>這可以結合使用[代理程式使用者ID](#agentuserid)來選取不同的內容，以復寫至個別的發佈環境。 對於每個發佈環境：
>
>1. 設定復寫代理以復寫至該發佈環境。
>1. 設定使用者帳戶；具有讀取復寫至該特定發佈環境的內容所需的存取許可權。
>1. 將使用者帳戶指派為復寫代理程式的&#x200B;**代理程式使用者識別碼**。
>

### 設定Dispatcher Flush代理程式 {#configuring-a-dispatcher-flush-agent}

預設代理程式會包含在安裝中。 不過，您仍需要特定設定，如果您定義新的代理程式，也同樣適用：

1. 開啟AEM中的&#x200B;**工具**&#x200B;標籤。
1. 按一下&#x200B;**部署**。
1. 選取&#x200B;**復寫**，然後選取發佈&#x200B;**上的**&#x200B;代理程式。
1. 連按兩下&#x200B;**Dispatcher Flush**&#x200B;專案以開啟概覽。
1. 按一下&#x200B;**編輯** - **代理程式設定**&#x200B;對話方塊開啟：

   * 在&#x200B;**設定**&#x200B;索引標籤中：

      * 啟動&#x200B;**已啟用**。
      * 輸入&#x200B;**描述**。
      * 將&#x200B;**序列化型別**&#x200B;保留為`Dispatcher Flush`，或是在建立代理程式時將其設為相同型別。

      * （選擇性）選取&#x200B;**別名更新**&#x200B;以啟用Dispatcher的別名或虛名路徑失效請求。

   * 在&#x200B;**傳輸**&#x200B;索引標籤中：

      * 輸入新發佈執行個體的必要URI；例如，

        `https://localhost:80/dispatcher/invalidate.cache`。

      * 輸入用於復寫的站台特定使用者帳戶。
      * 您可以視需要設定其他引數。

   對於Dispatcher Flush代理程式，只有當您使用以路徑為根據的虛擬主機專案來區分陣列時，才會使用URI屬性，而您會使用此欄位來鎖定要失效的陣列。 例如，陣列 #1 的虛擬主機為 `www.mysite.com/path1/*`，而陣列 #2 的虛擬主機為 `www.mysite.com/path2/*`。您可以使用URL `/path1/invalidate.cache`來鎖定第一個伺服器陣列，並使用`/path2/invalidate.cache`來鎖定第二個伺服器陣列。

   >[!NOTE]
   >
   >如果您已在非建議預設內容的內容中安裝AEM，請在&#x200B;**延伸**&#x200B;索引標籤中設定[HTTP標頭](#extended)。

1. 按一下&#x200B;**「確定」**。
1. 返回&#x200B;**工具**&#x200B;標籤，您可從這裡&#x200B;**啟用** **Dispatcher Flush**&#x200B;代理程式（**發佈上的代理程式**）。

**Dispatcher Flush**&#x200B;復寫代理程式在作者上未啟用。 您可以使用對等的URI （例如，`https://localhost:4503/etc/replication/agents.publish/flush.html`）在發佈環境中存取相同的頁面。

### 控制對復寫代理程式的存取 {#controlling-access-to-replication-agents}

使用`etc/replication`節點上的使用者和/或群組頁面許可權，即可控制用來設定復寫代理程式的頁面存取權。

>[!NOTE]
>
>設定這類許可權不會影響使用者復寫內容（例如，從網站主控台或Sidekick選項）。 復寫架構在復寫頁面時，不會使用目前使用者的「使用者工作階段」來存取復寫代理。

### 從CRXDE Lite設定復寫代理 {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>僅支援在`/etc/replication`存放庫位置中建立復寫代理。 必須具備此條件才能正確處理關聯的ACL。 在樹狀結構的其他位置建立復寫代理程式，可能會導致未經授權的存取。

您可以使用CRXDE Lite設定復寫代理的各種引數。

如果您導覽至`/etc/replication`，您會看到下列三個節點：

* `agents.author`
* `agents.publish`
* `treeactivation`

兩個`agents`保留適當環境的組態資訊，而且只有在環境執行時才有效。 例如，`agents.publish`僅用於發佈環境。 以下熒幕擷圖顯示製作環境中的Publish代理程式(包含在AEM WCM中)：

![chlimage_1-24](assets/chlimage_1-24.png)

## 監視復寫代理程式 {#monitoring-your-replication-agents}

監督復寫代理程式：

1. 存取AEM中的&#x200B;**工具**&#x200B;索引標籤。
1. 按一下&#x200B;**復寫**。
1. 連按兩下適當環境（左窗格或右窗格）代理程式的連結。 例如，作者&#x200B;**上的**&#x200B;代理程式。

   產生的視窗會顯示製作環境的所有復寫代理程式概觀，包括其目標和狀態。

1. 按一下適當的代理程式名稱（連結）以顯示該代理程式的詳細資訊：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   您可以在這裡進行以下作業︰

   * 檢視代理程式是否已啟用。
   * 檢視任何復寫的目標。
   * 檢視復寫佇列是否為使用中（已啟用）。
   * 檢視佇列中是否有任何專案。
   * **重新整理**&#x200B;或&#x200B;**清除**&#x200B;以更新佇列專案的顯示。 這可協助您檢視專案是否進入及離開佇列。

   * **檢視記錄檔**&#x200B;以存取復寫代理程式的任何動作記錄檔。
   * **測試目標執行個體的連線**。
   * 如有需要，對任何佇列專案強制重試&#x200B;**&#x200B;**。

   >[!CAUTION]
   >
   >請勿在發佈執行個體上的反向復寫寄件匣使用「測試連線」連結。
   >
   >
   >如果對Outbox佇列執行復寫測試，則任何早於測試復寫的專案都會透過每次反向復寫重新處理。
   >
   >
   >如果佇列中存有這類專案，可在下列XPath JCR查詢中找到並移除它們。
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## 批次復寫 {#batch-replication}

批次複製不會複製個別頁面或資產，但會根據時間或大小等待觸發兩者的第一個臨界值。

接著，它會將所有復寫專案封裝到一個封裝中，然後以單一檔案的形式復寫到發行者。

Publisher會解壓縮所有專案、儲存專案，並向作者回報。

### 設定批次複製 {#configuring-batch-replication}

1. 前往`http://serveraddress:serverport/siteadmin`
1. 按熒幕上方的&#x200B;**[!UICONTROL 工具]**&#x200B;圖示
1. 從左側導覽邊欄中，移至&#x200B;**[!UICONTROL 復寫 — 作者上的代理程式]**，然後按兩下&#x200B;**[!UICONTROL 預設代理程式]**。
   * 您也可以直接前往`http://serveraddress:serverport/etc/replication/agents.author/publish.html`，存取預設的發佈復寫代理程式
1. 按復寫佇列上方的&#x200B;**[!UICONTROL 編輯]**&#x200B;按鈕。
1. 在下列視窗中，移至&#x200B;**[!UICONTROL 批次]**&#x200B;標籤：
   ![批次復寫](assets/batchreplication.png)
1. 設定代理。

### 參數 {#parameters}

* `[!UICONTROL Enable Batch Mode]` — 啟用或停用批次復寫模式
* `[!UICONTROL Max Wait Time]` — 批次要求啟動前的等待時間上限（以秒為單位）。 預設值為2秒。
* `[!UICONTROL Trigger Size]` — 在此大小限制時開始批次復寫

## 其他資源 {#additional-resources}

如需疑難排解的詳細資訊，請參閱[疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md)頁面。
