---
title: 使用用戶端資料庫
description: AEM 提供了用戶端庫資料夾，通過這些資料夾，您可以在存放庫中商店用戶端代碼，將其組織到類別中，並定義何時以及如何向用戶端提供每個代碼類別
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
exl-id: cafc7120-114e-487a-8b81-9c695318731e
source-git-commit: a061c19dcb883b94ee61be21459c46e21eaf696a
workflow-type: tm+mt
source-wordcount: '2791'
ht-degree: 1%

---

# 使用用戶端資料庫{#using-client-side-libraries}

現代網站嚴重依賴由複雜JavaScript和 CSS 代碼驅動的用戶端處理。 組織和優化此代碼的服務可能是個複雜的問題。

為協助處理此問題，AEM提供&#x200B;**使用者端程式庫資料夾**，可讓您將使用者端程式碼儲存在存放庫中、將其組織成類別，以及定義每個類別程式碼何時及如何提供給使用者端。 然後，使用者端程式庫系統會負責在最終網頁中產生正確的連結，以載入正確的程式碼。

## AEM中使用者端資料庫的運作方式 {#how-client-side-libraries-work-in-aem}

在頁面的 HTML 中包含 用戶端 資料庫（即 JS 或 CSS 文件）的標準方法是簡單地在該頁面的 JSP 中包含 或 `<script>` `<link>` 標記，其中包含相關文件的路徑。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

雖然此方法適用於AEM，但當頁面及其組成元件變得複雜時，它可以銷售機會問題。 在這種情況下，存在最終 HTML 輸出中可能包含同一 JS 資料庫的多個副本的危險。 若要避免此問題並允許邏輯組織用戶端資料庫AEM請使用 **用戶端資料庫資料夾**。

使用者端程式庫資料夾是型別`cq:ClientLibraryFolder`的存放庫節點。 [CND表示法](https://jackrabbit.apache.org/node-type-notation.html)中的定義為

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

根據預設，`cq:ClientLibraryFolder`節點可以放置在存放庫的`/apps`、`/libs`和`/etc`子樹狀結構中的任何位置(這些預設值和其他設定可以透過[系統主控台](https://localhost:4502/system/console/configMgr)的&#x200B;**Adobe Granite HTML資料庫管理員**&#x200B;面板來控制)。

每個`cq:ClientLibraryFolder`都會填入一組JS和/或CSS檔案，以及一些支援檔案（請參閱下文）。 `cq:ClientLibraryFolder`的屬性設定如下：

* `categories`：識別此`cq:ClientLibraryFolder`中JS和/或CSS檔案集的類別。 `categories`屬性是多值屬性，可讓資料庫資料夾屬於多個類別（請參閱下方以瞭解其用處）。

* `dependencies`：這是此程式庫資料夾所依存之其他使用者端程式庫類別的清單。 例如，在指定`cq:ClientLibraryFolder`節點`F`和`G`的情況下，如果`F`中的檔案需要`G`中的另一個檔案才能正常運作，則`G`的`categories`中至少有一個`F`的`dependencies`中應該有。

* `embed`：用來內嵌其他程式庫中的程式碼。 如果節點F嵌入節點G和H，則產生的HTML將是節點G和H中的內容集。
* `allowProxy`：如果使用者端程式庫位於`/apps`之下，此屬性允許透過Proxy servlet存取它。 請參閱下方的[尋找使用者端資料庫資料夾及使用Proxy使用者端資料庫Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)。

## 參考使用者端程式庫 {#referencing-client-side-libraries}

由於HTL是開發AEM網站的偏好技術，因此HTL應該用於在AEM中包含使用者端程式庫。 不過，您也可以使用JSP執行此操作。

### 使用HTL {#using-htl}

在HTL中，使用者端程式庫是透過AEM提供的Helper範本載入，該範本可透過[`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use)存取。 此檔案中有三個範本可用，這些範本可透過[`data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call)呼叫：

* **css** — 僅載入參照的使用者端程式庫的CSS檔案。
* **js** — 僅載入參照的使用者端程式庫的JavaScript檔案。
* **all** — 載入參照的使用者端程式庫的所有檔案(CSS和JavaScript)。

每個 helper 範本都需要 `categories` 選項來參照所需的用戶端程式庫。 這個選項可以是字串值陣列，或是包含逗號分隔值清單的字串。

如需詳細資訊和使用範例，請參閱檔案[開始使用HTML範本語言](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)。

### 使用JSP {#using-jsp}

將`ui:includeClientLib`標籤新增至您的JSP程式碼，以在產生的HTML頁面中新增使用者端資料庫的連結。 若要參考資料庫，請使用`ui:includeClientLib`節點的`categories`屬性值。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如，`/etc/clientlibs/foundation/jquery`節點屬於型別`cq:ClientLibraryFolder`，類別屬性值為`cq.jquery`。 JSP檔案中的下列程式碼會參考程式庫：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

產生的HTML頁面包含下列程式碼：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

如需完整的資訊，包括篩選JS、CSS或主題資料庫的屬性，請參閱[ui：includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib)。

>[!CAUTION]
>
>`<cq:includeClientLib>`過去常用來包含使用者端資料庫，但自AEM 5.6起已淘汰。應改用[`<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib)，如上所述。

## 建立使用者端資源庫資料夾 {#creating-client-library-folders}

建立`cq:ClientLibraryFolder`節點以定義JavaScript和階層式樣式表程式庫，並讓它們可供HTML頁面使用。 使用節點的`categories`屬性來識別它所屬的程式庫類別。

節點包含一或多個在執行階段合併至單一JS和/或CSS檔案的來源檔案。 產生的檔案名稱是副檔名為`.js`或`.css`的節點名稱。 例如，名為`cq.jquery`的程式庫節點會產生名為`cq.jquery.js`或`cq.jquery.css`的檔案。

使用者端程式庫資料夾包含下列專案：

* 要合併的JS和/或CSS來源檔案。
* 支援CSS樣式的資源，例如影像檔案。

  **注意：**&#x200B;您可以使用子資料夾來組織來源檔案。
* 一個`js.txt`檔案和/或一個`css.txt`檔案，可識別產生的JS和/或CSS檔案中要合併的來源檔案。

![clientlibarch](assets/clientlibarch.png)

有關特定於小部件的用戶端資料庫要求的資訊，請參閱 [使用和擴展小部件](/help/sites-developing/widgets.md)。

Web使用者端必須擁有存取`cq:ClientLibraryFolder`節點的許可權。 您也可以從存放庫的安全區域公開程式庫（請參閱下方的從其他程式庫內嵌程式碼）。

### 覆寫/lib中的程式庫 {#overriding-libraries-in-lib}

位於`/apps`下方的使用者端資料庫資料夾優先於`/libs`中類似名稱的資料夾。 例如，`/apps/cq/ui/widgets`優先於`/libs/cq/ui/widgets`。 當這些資料庫屬於相同類別時，會使用`/apps`以下的資料庫。

### 查找用戶端庫檔案夾和使用代理用戶端庫 Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在以前的版本中，用戶端資料庫資料夾位於存放庫的下方 `/etc/clientlibs` 。 目前仍支援此功能，但建議將用戶端資料庫置於 `/apps`下。 這是為了將用戶端資料庫放置在其他腳本附近，這些腳本通常在下面 `/apps` 和 `/libs`中找到。

>[!NOTE]
>
>用戶端資料庫資料夾下的靜態資源必須位於名為資源的&#x200B;**&#x200B;資料夾中。如果資料夾 *資源*&#x200B;下沒有靜態資源（如圖像），則無法在發佈執行個體上引用該資源。 以下是範例： https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>為了更好地將代碼與內容和配置隔離開來，建議將用戶端資料庫置於 下`/apps`，並使用 屬性 公開它們`/etc.clientlibs` `allowProxy`。

為使客戶機 資料庫 下的 `/apps` 可存取，使用了 Proxy Servlet。 仍在客戶機資料庫資料夾上強制實施 ACL，但如果屬性設置為 ，`true`則 `allowProxy` servlet 允許通過`/etc.clientlibs/`讀取內容。

如果靜態資源位於用戶端資料庫資料夾下的資源下，則只能通過代理訪問靜態資源。

例如：

* 您有一個 clientlib 在 `/apps/myprojects/clientlibs/foo`
* 您有一個靜態圖像 `/apps/myprojects/clientlibs/foo/resources/icon.png`

然後您將`foo`上的`allowProxy`屬性設定為true。

* 您接著可以要求`/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然後，您可以通過以下方式參考圖像 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>使用代理用戶端資料庫時，AEM Dispatcher配置可能需要更新，以確保允許具有擴展用戶端庫的 URI。

>[!CAUTION]
>
>Adobe Systems 建議在 下 `/apps` 找到用戶端資料庫，並使用 Proxy Servlet 使其可用。 但是請記住，最佳實務仍然要求公共網站永遠不要包含直接通過 or `/libs` 路徑提供`/apps`的任何內容。

### 建立使用者端資源庫資料夾 {#create-a-client-library-folder}

1. 在網頁瀏覽器([https://localhost:4502/crx/de](https://localhost:4502/crx/de))中開啟CRXDE Lite。
1. 選取您要尋找使用者端程式庫資料夾的資料夾，然後按一下[建立] > [建立節點] **。**
1. 輸入程式庫檔案的名稱，然後在[型別]清單中選取`cq:ClientLibraryFolder`。 按一下[確定]&#x200B;**&#x200B;**，然後按一下[儲存全部]&#x200B;**&#x200B;**。
1. 若要指定程式庫所屬的類別，請選取`cq:ClientLibraryFolder`節點、新增下列屬性，然後按一下[儲存全部] **：**

   * 名稱：類別
   * 型別：字串
   * 值：類別名稱
   * 多個：選取

1. 以任何方式將來源檔案新增至程式庫資料夾。 例如，使用WebDav使用者端來複製檔案，或建立檔案並手動編寫內容。

   **注意：**&#x200B;您可以視需要在子資料夾中組織來源檔案。

1. 選取使用者端程式庫資料夾，然後按一下&#x200B;**建立>建立檔案**。
1. 在「檔案名稱」方塊中，輸入下列其中一個檔案名稱，然後按一下「確定」：

   * **`js.txt`：**&#x200B;使用此檔案名稱來產生JavaScript檔案。
   * **`css.txt`：**&#x200B;使用此檔案名稱產生階層式樣式表。

1. 開啟檔案並輸入下列文字，以識別來源檔案的路徑根目錄：

   `#base=*[root]*`

   取代 * `[root]`* 包含源檔的資料夾的路徑，相對於 TXT 檔。 例如，當源檔與 TXT 檔案位於同一資料夾中時，請使用以下文字：

   `#base=.`

   以下代碼將根設定為節點下 `cq:ClientLibraryFolder` 名為 mobile 的資料夾：

   `#base=mobile`

1. 在`#base=[root]`下方的行中，輸入來源檔案相對於根的路徑。 將每個檔案名稱放在單獨的一行上。
1. 按一下&#x200B;**「儲存全部」**。

### 連結到依賴項 {#linking-to-dependencies}

當用戶端資料庫資料夾中的代碼引用其他資料庫時，請將其他資料庫標識為依賴項。 在 JSP 中， `ui:includeClientLib` 引用客戶機資料庫資料夾的標記會導致 HTML 代碼包含對生成的資料庫文件和依賴項的連結。

相依項目必須是另一個 `cq:ClientLibraryFolder`。 若要標識依賴項，請使用以下屬性向節點添加 `cq:ClientLibraryFolder` 屬性：

* **名稱：** 依賴項
* **型別：**&#x200B;字串[]
* **值：**&#x200B;目前程式庫資料夾所依賴之cq：ClientLibraryFolder節點的categories屬性值。

例如，/ `etc/clientlibs/myclientlibs/publicmain`在`cq.jquery`資料庫上有相依性。 參考主要使用者端程式庫的JSP會產生HTML，其中包含下列程式碼：

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他程式庫內嵌程式碼 {#embedding-code-from-other-libraries}

您可以將使用者端程式庫的程式碼內嵌到另一個使用者端程式庫中。 在執行階段中，內嵌程式庫產生的JS和CSS檔案會包含內嵌程式庫的程式碼。

內嵌程式碼有助於提供對存放庫安全區域中的程式庫的存取權。

#### 應用程式專屬的使用者端資料庫資料夾 {#app-specific-client-library-folders}

最佳實務是將應用程式資料夾中的所有應用程式相關檔案保留在`/apps`以下。 拒絕網站訪客存取`/apps`資料夾也是最佳作法。 為滿足這兩個最佳實務，請在`/apps`下方建立使用者端程式庫資料夾，並透過[尋找使用者端程式庫資料夾及使用Proxy使用者端程式庫Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)中所述的Proxy Servlet存取該資料夾。

使用categories屬性來識別要內嵌的使用者端資料庫資料夾。 若要內嵌程式庫，請使用下列屬性將屬性新增至內嵌`cq:ClientLibraryFolder`節點：

* **名稱：** 嵌入
* **型別：**&#x200B;字串[]
* **值：**&#x200B;要內嵌`cq:ClientLibraryFolder`節點的categories屬性值。

#### 使用內嵌將請求最小化 {#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現發佈執行個體針對典型頁面產生的最終HTML包含相對大量的`<script>`元素，特別是如果您的網站正使用使用者端內容資訊來進行分析或鎖定目標時。 例如，在非最佳化專案中，您可能會在HTML中找到下列頁面的`<script>`元素系列：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在這種情況下，將所有必需的用戶端資料庫代碼合併到單個文件中非常有用，這樣可以減少載入頁面時的來回請求數。 為此，您可以使用 `embed` 節點的 `cq:ClientLibraryFolder` 嵌入屬性將所需的資料庫到特定于應用的用戶端資料庫中。

下列客戶資料庫類別包含 AEM。 您應該只嵌入執行您的特定網站所需的那些。 但是， **您應維持此處**&#x200B;列出的順序：

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### CSS 檔案中的路徑 {#paths-in-css-files}

嵌入 CSS 檔時，生成的 CSS 代碼使用相對於嵌入資料庫的資源路徑。 例如，可公開訪問的資料庫 `/etc/client/libraries/myclientlibs/publicmain` 嵌入用戶端資料庫 `/apps/myapp/clientlib` ：

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

該檔案 `main.css` 包含以下樣式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

節點生成的 CSS 文件 `publicmain` 包含以下樣式，使用原始圖像的URL：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 將資料庫用於特定行動群組 {#using-a-library-for-specific-mobile-groups}

`channels`使用用戶端資料庫資料夾的屬性來標識使用該資料庫的移動群組。當相同類別的程式庫是針對不同裝置功能而設計時，`channels`屬性很有用。

若要將使用者端程式庫資料夾與裝置群組建立關聯，請將屬性新增至具有下列屬性的`cq:ClientLibraryFolder`節點：

* **名稱：** 頻道
* **類型：** 字串[]
* **值：** 行動群組的名稱。 若要從群組中排除 資料庫 資料夾，請在名稱前面加上感嘆號 （“！”）。

例如，下表列出`cq.widgets`類別中每個使用者端程式庫資料夾的`channels`屬性值：

| 使用者端資料庫資料夾 | 管道屬性的值 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## 使用前置處理器 {#using-preprocessors}

AEM允許可插拔的前處理器，並隨附對CSS和JavaScript的[YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor)以及JavaScript的[Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/)的支援，並將YUI設為AEM的預設前處理器。

可插拔前處理器可彈性使用，包括：

* 定義可以處理指令碼來源的ScriptProcessors
* 處理器可設定選項
* 處理器可用於縮制，也可用於非縮制情況
* clientlib可以定義要使用哪個處理器

>[!NOTE]
>
>依預設，AEM使用YUI壓縮程式。 如需已知問題的清單，請參閱[YUI Compressor GitHub檔案](https://github.com/yui/yuicompressor/issues)。 切換至特定clientlibs的GCC壓縮程式可以解決使用YUI時觀察到的部分問題。

>[!CAUTION]
>
>請勿將縮制的程式庫放入使用者端程式庫中。 改為提供原始程式庫，如果需要縮制，請使用前置處理器的選項。

### 使用情況 {#usage}

您可以選擇為每個使用者端程式庫或系統範圍設定前置處理器組態。

* 在clientlibrary節點上新增多值屬性`cssProcessor`和`jsProcessor`

* 或透過&#x200B;**HTML資料庫管理員** OSGi設定來定義系統預設設定

用戶端庫節點上的預處理器配置優先於 OSGI 配置。

### 格式和範例 {#format-and-examples}

#### 格式 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### CSS縮制的YUI壓縮程式和JS的GCC {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Typescript可進行預先處理，然後使用GCC進行縮小及模糊化 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### 其他海灣合作委員會選項 {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

有關 GCC 選項的更多詳細資訊，請參閱 [GCC 文件](https://developers.google.com/closure/compiler/docs/compilation_levels)。

### 設定系統預設縮小器 {#set-system-default-minifier}

YUI 在 AEM 中設置為預設的縮小器。 若要將其更改為 GCC，請追隨以下步驟。

1. 轉到位於 https://localhost:4502/system/console/configMgr 的 [Apache Felix Config Manager](https://localhost:4502/system/console/configMgr)
1. 尋找並編輯&#x200B;**Adobe Granite HTML資料庫管理員**。
1. 啟用&#x200B;**最小化**&#x200B;選項（如果尚未啟用）。
1. 將&#x200B;**JS處理器預設組態**&#x200B;的值設定為`min:gcc`。

   如果以分號分隔，例如`min:gcc;obfuscate=true`，則可以傳遞選項。

1. 按一下「**儲存**」以儲存變更。

## 偵錯工具 {#debugging-tools}

AEM提供數種用於偵錯和測試使用者端程式庫資料夾的工具。

### 請參閱內嵌檔案 {#see-embedded-files}

若要追蹤內嵌程式碼的來源，或確保內嵌使用者端程式庫產生預期的結果，您可以檢視執行階段內嵌檔案的名稱。 若要檢視檔案名稱，請將`debugClientLibs=true`引數附加至網頁的URL。 產生的程式庫包含`@import`個陳述式，而非內嵌程式碼。

在先前[內嵌其他程式庫的程式碼](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)區段的範例中，`/etc/client/libraries/myclientlibs/publicmain`使用者端程式庫資料夾內嵌`/apps/myapp/clientlib`使用者端程式庫資料夾。 將該参数追加到 Web 頁面會在 Web 頁面 的原始程式碼中生成以下連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟`publicmain.css`檔案會顯示下列程式碼：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在網頁瀏覽器的位址方塊中，將下列文字附加至HTML的URL：

   `?debugClientLibs=true`
1. 頁面載入時，檢視頁面來源。
1. 按一下提供為連結元素href的連結，開啟檔案並檢視原始程式碼。

### 探索使用者端資料庫 {#discover-client-libraries}

該 `/libs/cq/granite/components/dumplibs/dumplibs` 元件生成有關系統上所有用戶端資料庫資料夾的信息頁面。 `/libs/granite/ui/content/dumplibs`節點將元件作為資源類型。若要打開頁面，請使用以下URL（根據需要更改主機和連接埠）：

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

這些資訊包括資料庫路徑和類型（CSS 或 JS）以及資料庫屬性（如類別和依賴項）的值。 頁面上的後續表格顯示了每個類別和通道中的資料庫。

### 請參閱已產生的Output {#see-generated-output}

該 `dumplibs` 元件包括一個測試選擇器，該显示為標記生成的 `ui:includeClientLib` 原始程式碼。 該頁面包括 js、css 和主題屬性不同組合的代碼。

1. 使用以下方法之一打開測試Output頁面：

   * 在 `dumplibs.html` 頁面中，按兩下按兩下 **此處獲取輸出測試** 文字中的連結。

   * 在您的網页瀏覽器中開啟下列URL （根據需要使用不同的主機和連接埠）：

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   默認頁面會顯示沒有類別屬性值的標記的輸出。

1. 若要查看類別的輸出，請鍵入用戶端資料庫屬性 `categories` 的值，然後按兩下提交 **查詢**”

## 為開發和生產設定程式庫處理 {#configuring-library-handling-for-development-and-production}

HTML程式庫管理員服務會在執行階段處理`cq:ClientLibraryFolder`標籤並產生程式庫。 環境、開發或生產的型別會決定您設定服務的方式：

* 提高安全性：停用偵錯
* 提升效能：移除空白並壓縮程式庫。
* 提高可讀性：包含空白字元且請勿壓縮。

如需設定服務的相關資訊，請參閱[AEM HTML資料庫管理員](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)。
