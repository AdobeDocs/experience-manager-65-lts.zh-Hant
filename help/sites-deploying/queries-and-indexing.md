---
title: Oak查詢與索引
description: 瞭解如何在Adobe Experience Manager (AEM) 6.5 LTS中設定索引。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 432fc767-a6b8-48f8-b124-b13baca51fe8
source-git-commit: 7584fa1c544f9dd499b4007a9158e25b783f620c
workflow-type: tm+mt
source-wordcount: '2594'
ht-degree: 1%

---

# Oak查詢與索引{#oak-queries-and-indexing}

>[!NOTE]
>
>本文會介紹如何在AEM 6.5 LTS中設定索引。 如需最佳化查詢和索引效能的最佳實務，請參閱[查詢和索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

## 簡介 {#introduction}

與Jackrabbit 2不同，Oak預設不會索引內容。 必要時必須建立自訂索引，就像傳統關聯式資料庫一樣。 如果特定查詢沒有索引，則可能會遍歷許多節點。 查詢可能仍然有效，但速度可能很慢。

如果Oak遇到沒有索引的查詢，則會列印WARN層級的記錄訊息：

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 支援的查詢語言 {#supported-query-languages}

Oak查詢引擎支援下列語言：

* XPath （建議）
* SQL-2
* SQL （已棄用）
* JQOM

## 索引子型態與成本計算 {#indexer-types-and-cost-calculation}

以Apache Oak為基礎的後端可將不同的索引器插入存放庫。

一個索引子是&#x200B;**屬性索引**，其索引定義儲存在存放庫本身中。

**Apache Lucene**&#x200B;的實作預設可用，支援全文檢索索引。

如果沒有其他索引器可用，則會使用&#x200B;**周遊索引**。 這表示內容未編制索引，系統會周遊內容節點以尋找與查詢相符的內容。

如果查詢有多個可用的索引器，則每個可用的索引器都會估計執行查詢的成本。 Oak接著會選擇預估成本最低的索引器。

![chlimage_1-148](assets/chlimage_1-148.png)

上圖是Apache Oak查詢執行機制的高層級表示。

首先，查詢會剖析為抽象語法樹狀結構。 然後，會檢查查詢並轉換為SQL-2 (Oak查詢的原生語言)。

接著，會參考每個索引來估計查詢的成本。 完成後，會擷取最便宜索引的結果。 最後，會篩選結果，以確保目前使用者具有結果的讀取許可權，以及結果符合完整查詢。

## 設定索引 {#configuring-the-indexes}

>[!NOTE]
>
>對於大型存放庫而言，建立索引是一項耗時的作業。 這適用於初始建立索引和重新建立索引（在變更定義後重建索引）。 另請參閱[疑難排解Oak索引](/help/sites-deploying/troubleshooting-oak-indexes.md)和[防止緩慢重新索引](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)。

如果大型存放庫需要重新索引，尤其是使用MongoDB和針對全文檢索索引時，請考慮文字預先擷取，並使用Oak-run建立初始索引和重新索引。

索引在&#x200B;**Oak：index**&#x200B;節點下的儲存庫中設定為節點。

索引節點的型別必須是&#x200B;**oak：QueryIndexDefinition。**&#x200B;每個索引器都有數個組態選項作為節點屬性使用。 如需詳細資訊，請參閱以下每個索引器型別的設定詳細資料。

### 屬性索引 {#the-property-index}

對於具有屬性限制但不是全文檢索的查詢，屬性索引非常有用。 可依下列程式進行設定：

1. 前往`http://localhost:4502/crx/de/index.jsp`開啟CRXDE
1. 在&#x200B;**oak：index**&#x200B;下建立節點
1. 為節點&#x200B;**PropertyIndex**&#x200B;命名，並將節點型別設定為&#x200B;**oak：QueryIndexDefinition**
1. 為新節點設定下列屬性：

   * **型別：** `property` （型別為String）
   * **propertyNames：** `jcr:uuid` （型別為Name）

   此特定範例會索引`jcr:uuid`屬性，其工作為公開其附加之節點的通用唯一識別碼(UUID)。

1. 儲存變更。

「屬性索引」有以下組態選項：

* **type**&#x200B;屬性指定索引的型別，在此情況下，它必須設定為&#x200B;**屬性**

* **propertyNames**&#x200B;屬性指出儲存在索引中的屬性清單。 如果遺失該節點，則會使用節點名稱作為屬性名稱參考值。 在此範例中，工作為公開其節點唯一識別碼(UUID)的&#x200B;**jcr：uuid**&#x200B;屬性會新增至索引。

* **唯一**&#x200B;旗標，如果設為&#x200B;**true**，會在屬性索引上新增唯一性限制。

* **declaringNodeTypes**&#x200B;屬性可讓您指定只套用索引的特定節點型別。
* **重新索引**&#x200B;旗標，若設為&#x200B;**true**，會觸發完整的內容重新索引。

### 有序索引 {#the-ordered-index}

Ordered索引是Property索引的延伸。 但是，它已被取代。 必須以[Lucene屬性索引](#the-lucene-property-index)取代此型別的索引。

### Lucene全文索引 {#the-lucene-full-text-index}

AEM 6.5 LTS提供以Apache Lucene為基礎的全文檢索器。

如果設定了全文檢索索引，則無論是否有其他條件已編制索引，也無論是否有路徑限制，所有具有全文檢索條件的查詢都會使用全文檢索索引。

如果未設定全文檢索索引，則具有全文檢索條件的查詢將無法如預期運作。

由於索引是以非同步背景執行緒的方式更新，因此在背景處理完成之前，某些全文檢索搜尋無法在很短的時間內完成。

您可以依照以下程式設定Lucene全文索引：

1. 開啟CRXDE並在&#x200B;**oak：index**&#x200B;下建立節點。
1. 為節點&#x200B;**LuceneIndex**&#x200B;命名，並將節點型別設定為&#x200B;**oak：QueryIndexDefinition**
1. 將下列屬性新增至節點：

   * **型別：** `lucene` （型別為String）
   * **非同步處理：** `async` （字串型別）

1. 儲存變更。

Lucene索引有下列設定選項：

* 指定索引型別的&#x200B;**type**&#x200B;屬性必須設定為&#x200B;**lucene**
* **非同步**&#x200B;屬性必須設定為&#x200B;**非同步**。 這會將索引更新程式傳送到背景執行緒。
* **includePropertyTypes**&#x200B;屬性定義索引中包含的屬性型別子集。
* 定義屬性名稱清單的&#x200B;**excludePropertyNames**&#x200B;屬性 — 應從索引中排除的屬性。
* 設定為&#x200B;**true**&#x200B;時，會觸發完整內容重新索引的&#x200B;**重新索引**&#x200B;旗標。

### 瞭解全文搜尋 {#understanding-fulltext-search}

例如，本節中的檔案適用於Apache Lucene、Elasticsearch，以及PostgreSQL、SQLite和MySQL的全文索引。 以下範例適用於AEM / Oak / Lucene。

<b>要編制索引的資料</b>

起點是必須編制索引的資料。 以下列檔案為例：

| <b>檔案識別碼</b> | <b>路徑</b> | <b>全文</b> |
| --- | --- | --- |
| 100 | /content/rubik | 「Rubik是芬蘭品牌。」 |
| 200 | /content/rubiksCube | 「魔方是在1974年發明的。」 |
| 300 | /content/cube | 「立方體是3維物件。」 |


<b>反轉索引</b>

索引機制會將全文分割成名為「Token」的字詞，並建置名為「inverted index」的索引。 此索引包含檔案清單，其中會針對每個單字顯示該索引。

簡短的一般字詞（也稱為「停用詞」）不會編制索引。 所有代號都會轉換為小寫，並套用字乾處理。

特殊字元（例如&#x200B;*&quot;-&quot;*）未編制索引。

| <b>Token</b> | <b>檔案識別碼</b> |
| --- | --- |
| 194 | ...， 200，... |
| 品牌 | ...， 100，... |
| 立方體 | ...、200、300、... |
| 維度 | 300 |
| 完成 | ...， 100，... |
| invent | 200 |
| 物件 | ...， 300，... |
| rubik | ...、100、200、... |

檔案清單已排序。 這在查詢時很方便。

<b>正在搜尋</b>

以下是查詢的範例。 請注意，所有特殊字元（例如&#x200B;*&#39;*）都已取代為空格：

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

這些字詞的標籤化和篩選方式與編制索引時的方式相同（例如，會移除單一字元字詞）。 因此在此案例中，搜尋的目標為：

```
+:fulltext:rubik +:fulltext:cube
```

索引會參考這些字的檔案清單。 如果檔案很多，清單可能會很大。 例如，假設它們包含下列內容：


| <b>Token</b> | <b>檔案識別碼</b> |
| --- | --- |
| rubik | 10， 100， 200， 1000 |
| 立方體 | 30、200、300、2000 |


Lucene在兩個清單（或循環配置資源`n`清單，搜尋`n`個字時）之間來回切換：

* 在「rubik」中讀取會取得第一個專案：它找到10
* 在「Cube」中讀取會取得第一個專案`>` = 10。 找不到10，則下一個是30。
* 在「rubik」中讀取會取得第一個專案`>` = 30：它找到100。
* 在「Cube」中讀取會取得第一個專案`>` = 100：它找到200。
* 在「rubik」中讀取會取得第一個專案`>` = 200。 找到200。 因此，檔案200符合兩個詞語。 記住這一點。
* 在「rubik」中讀取會取得下一個專案： 1000。
* 在「Cube」中讀取會取得第一個專案`>` = 1000：它找到2000。
* 在「rubik」中讀取會取得第一個專案`>` = 2000：清單結尾。
* 最後，您可以停止搜尋。

唯一包含這兩個詞的檔案是200，如下例所示：

| 200 | /content/rubiksCube | 「魔方是在1974年發明的。」 |
| --- | --- | --- |

找到多個專案時，會依分數排序。

>[!NOTE]
>
>本節中說明的搜尋機制使用Lucene索引，而非部份比對，如Linux `grep`命令。

### Lucene屬性索引 {#the-lucene-property-index}

由於&#x200B;**Oak 1.0.8**，因此Lucene可用來建立包含非全文檢索之屬性限制的索引。

若要取得Lucene屬性索引，**fulltextEnabled**&#x200B;屬性必須一律設定為false。

以下列範例查詢為例：

```xml
select * from [nt:base] where [alias] = '/admin'
```

若要為上述查詢定義Lucene屬性索引，您可以在&#x200B;**`oak:index`下建立節點，以新增下列定義：**

* **名稱：** `LucenePropertyIndex`
* **型別：** `oak:QueryIndexDefinition`

建立節點後，請新增下列屬性：

* **型別：**

  ```xml
  lucene (of type String)
  ```

* **非同步處理：**

  ```xml
  async (of type String)
  ```

* **全文檢索已啟用：**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames：** `["alias"] (of type String)`

>[!NOTE]
>
>相較於一般屬性索引，Lucene屬性索引一律設定為非同步模式。 因此，索引傳回的結果不一定能反映存放庫的最新狀態。

>[!NOTE]
>
>如需Lucene屬性索引的詳細資訊，請參閱[Apache Jackrabbit Oak Lucene檔案頁面](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### Lucene分析器 {#lucene-analyzers}

自1.2.0版開始，Oak支援Lucene分析器。

分析器在檔案編制索引時和查詢時都使用。 分析器會檢查欄位文字並產生權杖資料流。 Lucene分析器由一系列Tokenizer和篩選類別組成。

分析器可透過`oak:index`定義內的`analyzers`節點（型別為`nt:unstructured`）進行設定。

索引的預設分析器設定於分析器節點的`default`子系中。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>如需可用分析器的清單，請參閱您使用的Lucene版本的API檔案。

#### 直接指定分析器類別 {#specifying-the-analyzer-class-directly}

如果您要使用任何現成可用的分析器，可以依照下列程式進行設定：

1. 在`oak:index`節點下，找出您要與分析器搭配使用的索引。

1. 在索引下，建立名稱為`default`且型別為`nt:unstructured`的子節點。

1. 將屬性新增至具有下列屬性的預設節點：

   * **名稱：** `class`
   * **型別：** `String`
   * **值：** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   值是您要使用的分析器類別名稱。

   您也可以使用選擇性的`luceneMatchVersion`字串屬性，將分析器設定為與特定lucene版本搭配使用。 搭配Lucene 4.7使用的有效語法為：

   * **名稱：** `luceneMatchVersion`
   * **型別：** `String`
   * **值：** `LUCENE_47`

   如果未提供`luceneMatchVersion`，Oak會使用隨附的Lucene版本。

1. 如果您想要將stopwords檔案新增至分析器設定，可以在`default`節點下建立具有以下屬性的節點：

   * **名稱：** `stopwords`
   * **型別：** `nt:file`

#### 透過構成建立分析器 {#creating-analyzers-via-composition}

分析器也可以根據`Tokenizers`、`TokenFilters`和`CharFilters`組成。 您可以指定分析器並建立其選擇性代碼化工具的子節點，以及依列出的順序套用的篩選器，以達成此目的。

以這個節點結構為例：

* **名稱：** `analyzers`

   * **名稱：** `default`

      * **名稱：** `charFilters`
      * **型別：** `nt:unstructured`

         * **名稱：** `HTMLStrip`
         * **名稱：** `Mapping`

      * **名稱：** `tokenizer`

         * **屬性名稱：** `name`

            * **型別：** `String`
            * **值：** `Standard`

      * **名稱：** `filters`
      * **型別：** `nt:unstructured`

         * **名稱：** `LowerCase`
         * **名稱：** `Stop`

            * **屬性名稱：** `words`

               * **型別：** `String`
               * **值：** `stop1.txt, stop2.txt`

            * **名稱：** `stop1.txt`

               * **型別：** `nt:file`

            * **名稱：** `stop2.txt`

               * **型別：** `nt:file`

濾鏡、charFilters和tokenizers的名稱是透過移除原廠尾碼所組成。 因此：

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory`變成`standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory`變成`Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory`變成`Stop`

工廠所需的任何組態引數都會指定為相關節點的屬性。

對於必須載入外部檔案內容的載入停用字詞等情況，可透過為相關檔案建立`nt:file`型別的子節點來提供內容。

### AEM索引工具 {#aem-indexing-tools}

AEM 6.1也整合了AEM 6.0中存在的兩個索引工具，作為Adobe Consulting Services Commons工具集的一部分：

1. **說明Query**，此工具旨在協助管理員瞭解查詢的執行方式；
1. **Oak索引管理員**，維護現有索引的Web使用者介面。

您現在可以從AEM歡迎畫面前往&#x200B;**工具 — 作業 — 儀表板 — 診斷**&#x200B;來聯絡他們。

如需如何使用它們的詳細資訊，請參閱[操作儀表板檔案](/help/sites-administering/operations-dashboard.md)。

#### 透過OSGi建立屬性索引 {#creating-property-indexes-via-osgi}

ACS Commons套件也會公開可用於建立屬性索引的OSGi設定。

您可以搜尋&quot;**確定Oak屬性索引**&quot;，從Web主控台存取它。

![chlimage_1-150](assets/chlimage_1-150.png)

### 疑難排解索引問題 {#troubleshooting-indexing-issues}

可能會出現查詢執行時間很長，且一般系統回應時間很慢的情況。

本節提供一組必須執行哪些操作以追蹤這類問題原因的建議，以及解決這些問題的建議。

#### 正在準備偵錯資訊以供分析 {#preparing-debugging-info-for-analysis}

取得正在執行之查詢所需資訊的最簡單方式，是透過[說明查詢工具](/help/sites-administering/operations-dashboard.md#explain-query)。 這可讓您收集對緩慢查詢進行偵錯所需的精確資訊，而無需查閱記錄層級資訊。 如果您知道正在偵錯的查詢，這是您想要的。

如果由於任何原因而無法執行此操作，您可以將索引記錄收集到單一檔案中，並使用它來疑難排解您的特定問題。

#### 啟用記錄 {#enable-logging}

若要啟用記錄，您必須針對與Oak索引和查詢相關的類別啟用&#x200B;**DEBUG**&#x200B;層級記錄。 這些類別包括：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

**com.day.cq.search**&#x200B;類別僅適用於使用AEM提供的QueryBuilder公用程式。

>[!NOTE]
>
>請務必僅在您要進行疑難排解的查詢執行期間，將記錄檔設為DEBUG。 否則，許多事件會隨著時間在記錄中產生。 因此，在收集到所需的記錄後，請切換回上述類別的INFO層級記錄。

您可以依照下列程式來啟用記錄功能：

1. 將瀏覽器指向`https://serveraddress:port/system/console/slinglog`
1. 按一下主控台下方的&#x200B;**新增記錄器**&#x200B;按鈕。
1. 在新建立的列中，新增上述類別。 您可以使用&#x200B;**+**&#x200B;符號將多個類別新增至單一記錄器。
1. 從&#x200B;**記錄層級**&#x200B;下拉式清單中選擇&#x200B;**DEBUG**。
1. 將輸出檔案設定為`logs/queryDebug.log`。 這會將所有DEBUG事件關聯至單一記錄檔。
1. 執行查詢或轉譯正在使用您想要偵錯的查詢的頁面。
1. 執行查詢後，請返回記錄主控台，並將新建立的記錄器的記錄層級變更為&#x200B;**INFO**。

#### 索引設定 {#index-configuration}

查詢的評估方式很大程度上受索引設定影響。 重要的是，要分析索引設定或將其傳送給支援人員。 您可以以內容封裝的形式取得設定，或取得JSON轉譯。

索引設定通常儲存在CRXDE中的`/oak:index`節點下，您可在以下位置取得JSON版本：

`https://serveraddress:port/oak:index.tidy.-1.json`

如果索引設定在不同的位置，請相應地變更路徑。

#### MBean輸出 {#mbean-output}

有時候，提供索引相關MBean的輸出以進行偵錯會很有幫助。 您可以透過以下方式進行：

1. 前往位於的JMX主控台：
   `https://serveraddress:port/system/console/jmx`

1. 搜尋下列MBean：

   * Lucene索引統計資料
   * CopyOnRead支援統計資料
   * Oak查詢統計資料
   * 索引統計資料

1. 按一下每個MBean，即可取得效能統計資料。 建立熒幕擷圖或記下它們，以備需要提交支援時使用。

您也可以在下列URL取得這些統計資料的JSON變體：

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

您也可以透過`https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`提供合併的JMX輸出。 這會包括JSON格式的所有與Oak相關的MBean詳細資料。

#### 其他詳細資料 {#other-details}

您可以收集其他詳細資料來協助疑難排解問題，例如：

1. 執行個體所在的Oak版本。 您可以透過開啟CRXDE並檢視歡迎頁面右下角的版本來檢視此內容，或透過檢查`org.apache.jackrabbit.oak-core`套件組合版本來檢視。
1. 疑難查詢的QueryBuilder Debugger輸出。 可以存取偵錯工具： `https://serveraddress:port/libs/cq/search/content/querydebug.html`
