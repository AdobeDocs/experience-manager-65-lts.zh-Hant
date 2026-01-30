---
title: 查詢產生器述詞參考
description: 查詢產生器API的完整述詞參考。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Developing,Search,Query Builder
role: Developer
exl-id: c044d541-24d6-4975-9b38-6a4317a16358
source-git-commit: a85b54d5a7c3b00f95f439941a390dcfee883187
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 1%

---

# 查詢產生器述詞參考{#query-builder-predicate-reference}

>[!CAUTION]
>
>此頁面上的資訊並非詳盡無遺。
>
>如需完整資訊，請參閱Query Builder Debugger主控台上&#x200B;**可用述詞**&#x200B;下的清單，例如：
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>例如，請參閱：
>
>* [http://localhost:4502/system/console/services？filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)

## 一般 {#general}

* [根](#root)
* [群組](#group)
* [orderby](#orderby)

## 述詞 {#predicates}

* [布林屬性](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [日期範圍](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [排除路徑](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [全文](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [語言](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [主要資產](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [路徑](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [屬性](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [相對日期範圍](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [相似](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [標籤](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [標籤ID](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [類型](/help/sites-developing/querybuilder-predicate-reference.md#type)

### `boolproperty` {#boolproperty}

符合JCR布林值屬性。 僅接受值&quot; `true`&quot;和&quot; `false`&quot;。 如果設為&quot; `false`&quot;，則符合屬性值是否為&quot; `false`&quot;或是否完全不存在。 對於檢查只在啟用時才會設定的布林值標幟很有用。

繼承的&quot; `operation`&quot;引數沒有意義。

其支援Facet擷取。 提供每個`true`或`false`值的值區，但僅限現有屬性。

#### 屬性 {#properties}

* **boolproperty**
屬性的相對路徑，例如`myFeatureEnabled`或`jcr:content/myFeatureEnabled`。

* **值**
要檢查「`true`」或「`false`」之屬性的值。

### `contentfragment` {#contentfragment}

將結果限制在內容片段。

不支援篩選。

不支援多面向擷取。

#### 屬性 {#properties-1}

* **contentfragment**
它可與任何值搭配使用，以檢查內容片段。

### `dateComparison` {#datecomparison}

比較兩個JCR DATE屬性彼此。 您可以測試這些值是否相等、不相等、大於或大於或等於。

僅限篩選的述詞，且無法使用搜尋索引。

#### 屬性 {#properties-2}

* **屬性1**

  第一個日期屬性的路徑。

* **屬性2**

  第二個日期屬性的路徑。

* **作業**

  `equals` （完全相符）、`!=` （不相等比較）、`greater` （屬性1大於屬性2）、`>=` （屬性1大於或等於屬性2）。 預設值為&quot; `equals`&quot;。

### `daterange` {#daterange}

比對JCR DATE屬性與日期和時間間隔。 使用ISO8601
日期和時間格式( `YYYY-MM-DDTHH:mm:ss.SSSZ`)，並允許部分表示，如`YYYY-MM-DD`。 或者，時間戳記也可以提供為UTC時區(UNIX®時間格式)自1970年以來的毫秒數。

您可以尋找兩個時間戳記之間的任何專案，或比指定日期新或舊的專案，也可以選擇介於包含間隔和開啟間隔之間的專案。

其支援Facet擷取。 提供值區「今天」、「本週」、「本月」、「最近3個月」、「今年」、「去年」和「比去年早」。

不支援篩選。

#### 屬性 {#properties-3}

* **屬性**

  `DATE`屬性的相對路徑，例如`jcr:lastModified`。

* **lowerBound**

  檢查屬性的日期下限，例如`2014-10-01`。

* **lowerOperation**

  「`>`」（較新）或「`>=`」（等於或較新）適用於`lowerBound`。 預設值為&quot; `>`&quot;。

* **上限**

  檢查屬性的上限，例如`2014-10-01T12:15:00`。

* **upperOperation**

  「`<`」（較舊）或「`<=`」（等於或較舊），適用於`upperBound`。 預設值為&quot; `<`&quot;。

* **時區**

  未指定為ISO-8601日期字串時要使用的時區ID。 預設為系統的預設時區。

### `excludepaths` {#excludepaths}

從結果中排除其路徑符合規則運算式的節點。

僅限篩選的述詞，且無法使用搜尋索引。

不支援多面向擷取。

#### 屬性 {#properties-4}

* **excludepaths**

  符合結果路徑的規則運算式，將符合的路徑排除在結果之外。

### `fulltext` {#fulltext}

搜尋全文檢索索引中的詞語。

不支援篩選。

不支援多面向擷取。

#### 屬性 {#properties-5}

* **全文**

  全文檢索搜尋詞。

* **relPath**

  在屬性或子節點中搜尋的相對路徑。 此屬性是選用的。

### `group` {#group}

允許建立巢狀條件。 群組可以包含巢狀群組。 查詢產生器查詢中的所有專案都以隱含方式位於根群組中，該根群組也可以有`p.or`和`p.not`引數。

比對兩個屬性中任一個與值的範例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

概念`(1_property`或`2_property)`。

巢狀群組的範例：

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

在&#x200B;**的頁面中或**&#x200B;的資產中搜尋字詞&quot;`/content/geometrixx/en`Management`/content/dam/geometrixx`&quot;。

概念`fulltext AND ( (path AND type) OR (path AND type) )`。 此類OR聯結需要良好的索引來提升效能。

#### 屬性 {#properties-6}

* **p.或**

  如果設為&quot; `true`&quot;，群組中只能有一個相符的述詞。 預設為&quot; `false`&quot;，表示所有專案都必須相符

* **p.not**

  若設為&quot; `true`&quot;，此專案會讓群組無效（預設為&quot; `false`&quot;）。

* **&lt;述詞>**

  新增巢狀述詞。

* **N_&lt;述詞>**

  新增多個相同的巢狀述詞，例如`1_property, 2_property, ...`。

### hasPermission {#haspermission}

將結果限製為目前工作階段具有指定[JCR許可權的專案。](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

僅限篩選的述詞，且無法使用搜尋索引。 不支援多面向擷取。

#### 屬性 {#properties-7}

* **hasPermission**

  目前使用者工作階段必須全部有問題節點的逗號分隔JCR許可權。 例如，`jcr:write`，`jcr:modifyAccessControl`。

### `language` {#language}

尋找特定語言的CQ頁面。 這會檢視頁面語言屬性和頁面路徑，後者通常包含頂層網站結構中的語言或地區設定。

僅限篩選的述詞，且無法使用搜尋索引。

其支援Facet擷取。 提供每個唯一語言代碼的貯體。

#### 屬性 {#properties-8}

* **語言**

  ISO語言代碼，例如&quot;`de`&quot;。

### `mainasset` {#mainasset}

檢查節點是否為DAM主要資產而非子資產。 基本上，每個節點不在「子資產」節點內。 不檢查`dam:Asset`節點型別。 若要使用此述詞，請設定&quot; `mainasset=true`&quot;或&quot; `mainasset=false`&quot;，沒有其他屬性。

僅限篩選的述詞，且無法使用搜尋索引。

它支援多面向擷取，並為主要和子資產提供兩個貯體。

#### 屬性 {#properties-9}

* **mainasset**

  布林值，主要資產為&quot; `true`&quot;，子資產為&quot; `false`&quot;。

### memberOf {#memberof}

尋找屬於特定[sling資源集合](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)成員的專案。

僅限篩選的述詞，且無法使用搜尋索引。 不支援多面向擷取。

#### 屬性 {#properties-10}

* **memberOf**

  Sling資源集合的路徑。

### `nodename` {#nodename}

符合JCR節點名稱。

其支援Facet擷取。 提供每個唯一節點名稱（檔案名稱）的貯體。

#### 屬性 {#properties-11}

* **nodename**

  允許萬用字元的節點名稱模式： `*` =任何或不含字元，`?` =任何字元，`[abc]` =僅括弧中的字元。

### `notexpired` {#notexpired}

透過檢查JCR DATE屬性是否大於或等於目前伺服器時間來比對專案。 可用來檢查`expiresAt` （如日期）屬性，並僅限尚未過期(`notexpired=true`)或已過期(`notexpired=false`)的屬性。

不支援篩選。

它以與日期範圍述詞相同的方式支援多面向擷取。

#### 屬性 {#properties-12}

* **notexpired**

  布林值，「`true`」代表尚未過期（未來日期或相等），「`false`」代表過期（過去的日期） （必要）。

* **屬性**

  要檢查的`DATE`屬性的相對路徑（必要）。

### `orderby` {#orderby}

可讓結果排序。 如果需要依多個屬性排序，則必須使用數字首碼多次新增此述詞，例如`1_orderby=first`、`2_oderby=second`。

#### 屬性 {#properties-13}

* **orderby**

  JCR屬性名稱由前導字元@表示，例如`@jcr:lastModified`或`@jcr:content/jcr:title`，或是查詢中要排序的另一個述詞，例如`2_property`。

* **排序**

  排序方向，`desc`代表遞減，`asc`代表遞增（預設）。

* **個案例**

  若設為`ignore`，排序會不區分大小寫，表示「a」在「B」之前；若為空白或省略，排序會區分大小寫，表示「B」在「a」之前

### `path` {#path}

在指定路徑內搜尋。

不支援多面向擷取。

#### 屬性 {#properties-14}

* **path**

  路徑模式。 當`exact=false` （預設）時，搜尋會比對指定路徑下的整個子樹狀結構 — 類似於XPath中附加`//*`，但不包含基底路徑本身。 當`exact=true`時，搜尋僅符合確切路徑，其中可包含`*`萬用字元。 如果已設定`self`，則搜尋會包含基底節點及其整個子樹狀結構。


* **完全**

  如果`exact`為true （開啟），則確切的路徑必須相符，但它可以包含簡單萬用字元( `*`)，這些萬用字元符合名稱，但不符合&quot; `/`&quot;；如果為false （預設），則包含所有子代（選擇性）。

* **平坦**

  僅搜尋直接子系（例如在`/*`中附加&quot; `xpath`&quot;） (僅在&#39;`exact`&#39;不是true （選用）時使用)。

* **self**

  搜尋子樹狀結構，但包含指定作為路徑的基本節點（無萬用字元）。

### `property` {#property}

符合JCR屬性及其值。

其支援Facet擷取。 為結果中的每個唯一屬性值提供值區。

#### 屬性 {#properties-15}

* **屬性**

  屬性的相對路徑，例如`jcr:title`。

* **值**

  要檢查屬性的值；遵循JCR屬性型別進行字串轉換。

* **N_value**

  使用`1_value`、`2_value`、...檢查多個值（預設會結合`OR`，若為`AND`，且為AND=TRUE） （自5.3起）。

* **和**

  設定為True以結合多個值( `N_value`)與AND （自5.3起）。

* **作業**

  使用`equals`進行完全比對（預設），使用`unequals`進行不相等比較。 使用`like`套用選用的`jcr:like` XPath函式。 使用`not`表示無相符專案（例如，XPath中的`not(@prop)`）；在此案例中，會忽略`value`引數。 使用`exists`檢查屬性是否存在： `true` （預設）需要屬性，而`false`相當於`not`。

* **深度**

  屬性與相對路徑可以存在的下層萬用字元層級。 例如，`property=size depth=2`會檢查節點和大小、節點/&amp;amp；ast；/size以及節點/&amp;amp；ast；/&amp;amp；ast；/size。

### `rangeproperty` {#rangeproperty}

比對JCR屬性與間隔。 套用至具有線性型別的屬性，例如`LONG`、`DOUBLE`和`DECIMAL`。 若為`DATE`，請參閱具有最佳化日期格式輸入的日期範圍述詞。

您可以定義下限與上限，或僅定義其中一個。 也可以分別針對下限與上限指定操作（例如「小於」或「小於或等於」）。

不支援多面向擷取。

#### 屬性 {#properties-16}

* **屬性**

  屬性的相對路徑。

* **lowerBound**

  檢查屬性的下限。

* **lowerOperation**

  「`>`」（預設）或「`>=`」適用於`lowerValue`

* **上限**

  檢查屬性的上限。

* **upperOperation**

  「`<`」（預設）或「`<=`」適用於`lowerValue`

* **decimal**

  如果核取的屬性型別為Decimal，則為&quot; `true`&quot;

### `relativedaterange` {#relativedaterange}

使用相對於目前伺服器時間的時間位移，以比對`JCR DATE`屬性與日期及時間間隔。 您可以使用毫秒值或bugzilla語法`lowerBound`來指定`upperBound`和`1s 2m 3h 4d 5w 6M 7y`。 前置詞為&quot; `-`&quot;，表示目前時間之前的負位移。 如果您只指定`lowerBound`或`upperBound`，則另一個預設為0，表示目前時間。

例如：

* `upperBound=1h` （沒有任何`lowerBound`）會在下一個小時選擇任何專案
* `lowerBound=-1d` （沒有任何`upperBound`）會選取過去24小時內的任何專案
* `lowerBound=-6M`和`upperBound=-3M`會選取任何6個月到3個月前的專案
* `lowerBound=-1500`和`upperBound=5500`會選取過去1500毫秒和未來5500毫秒之間的任何時間
* `lowerBound=1d`和`upperBound=2d`會選取後天的任何專案

這不考慮閏年，所有月份都是30天。

不支援篩選。

它以與日期範圍述詞相同的方式支援多面向擷取。

#### 屬性 {#properties-17}

* **上限**

  以毫秒為單位的上限日期或相對於目前伺服器時間的`1s 2m 3h 4d 5w 6M 7y` （一秒、兩分鐘、三小時、四天、五週、六個月、七年），使用「 — 」表示負位移。

* **lowerBound**

  以毫秒為單位或相對於目前伺服器時間的`1s 2m 3h 4d 5w 6M 7y` （一秒、兩分鐘、三小時、四天、五週、六個月、七年）為下限日期，使用「 — 」代表負位移。

### `root` {#root}

根述詞群組。 它支援群組的所有特徵，並可讓您設定全域查詢引數。

查詢中從未使用過名稱「root」，這是隱含的名稱。

#### 屬性 {#properties-18}

* **p.offset**

  表示結果頁面開始的數字，也就是要略過多少專案。

* **p.limit**

  表示頁面大小的數字。

* **p.guessTotal**

  為了避免計算完整結果總計的成本，請勿計算所有相符專案。 相反地，設定總計上限以計算（例如`1000`），讓使用者粗略估計小結果的粗略大小和精確總計。 或將其設定為`true`，以僅計算至所需的最小值： `p.offset + p.limit`。


* **p.excerpt**

  如果設為&quot; `true`&quot;，請在結果中包含全文摘錄。

* **p.hits**

  （僅適用於JSON servlet）選取將點選寫入為JSON的方式，並使用這些標準點選（可透過ResultHitWriter服務擴充）：

   * **簡單**：

     最小專案，例如`path`、`title`、`lastmodified`、`excerpt` （若已設定）。

   * **完整**：

     結果會呈現為每個節點的Sling JSON，`jcr:path`顯示點選路徑。 依預設，回應僅包含節點的直接屬性；使用`p.nodedepth=N`包含更深入的內容，其中`0`會傳回整個子樹狀結構。 設定`p.acls=true`以包含每個專案目前工作階段的JCR許可權(`create` = `add_node`，`modify` = `set_property`，`delete` = `remove`)。


   * **選擇性**：

     回應僅包含`p.properties`中列出的屬性，這是以空格分隔的相對路徑清單（在URL中使用`+`）。 如果相對路徑的深度大於1，則輸出會將其巢狀內嵌為子物件。 特殊`jcr:path`屬性一律包含點選路徑。


### `savedquery` {#savedquery}

它包含所有持續查詢產生器查詢的述詞，這些述詞作為子群組述詞放入目前的查詢。

它不會執行額外的查詢，但會擴充目前的查詢。

可以使用`QueryBuilder#storeQuery()`以程式設計方式保留查詢。 格式可以是多行String屬性，或是以Java™屬性格式將查詢作為文字檔案包含的`nt:file`節點。

不支援為已儲存查詢的述詞擷取Facet。

#### 屬性 {#properties-19}

* **savedquery**

  已儲存查詢的路徑（字串屬性或`nt:file`節點）。

### `similar` {#similar}

使用JCR XPath的`rep:similar()`進行相似性搜尋。

不支援篩選。 不支援多面向擷取。

#### 屬性 {#properties-20}

* **類似**
要尋找類似節點之節點的絕對路徑。

* **本機**
子系節點的相對路徑或目前節點的`.` （選擇性，預設為&quot; `.`&quot;）。

### `tag` {#tag}

透過指定標籤標題路徑，搜尋以一或多個標籤標籤標籤的內容。

其支援Facet擷取。 使用每個唯一標籤的目前標籤標題路徑，為其提供貯體。

#### 屬性 {#properties-21}

* **標籤**

  要尋找的標籤標題路徑，例如「資產屬性：方向/橫向」。

* **N_value**

  使用`1_value`、`2_value`、...來檢查多個標籤（預設會與`OR`結合，若為`AND`且為AND=TRUE） （自5.6起）。

* **屬性**

  要檢視的屬性（或屬性的相對路徑） （預設&quot; `cq:tags`&quot;）

### `tagid` {#tagid}

透過指定標籤ID來搜尋以一個或多個標籤標籤的內容。

其支援Facet擷取。 使用每個唯一標籤的目前標籤ID提供貯體。

#### 屬性 {#properties-22}

* **tagid**

  標籤ID，以便尋找&quot; `properties:orientation/landscape`&quot;之類的標籤。

* **N_value**

  使用`1_value`、`2_value`、...來檢查多個`tagids` （預設會與`OR`結合，若為`AND`且為=true） （自5.6起）。

* **屬性**

  要檢視的屬性（或屬性的相對路徑） （預設為&quot; `cq:tags`&quot;）。

### `tagsearch` {#tagsearch}

透過指定關鍵字，搜尋標籤有一或多個標籤的內容。 會先搜尋標題中包含這些關鍵字的標籤，然後將結果限製為僅限已標籤的專案。

不支援多面向擷取。

#### 屬性 {#Properties-1}

* **tagsearch**

  要在標籤標題中搜尋的關鍵字。

* **屬性**

  要檢視的屬性（或屬性的相對路徑） （預設`cq:tags`）。

* **lang**

  只搜尋特定當地語系化標籤標題（例如，`de`）。

* **全部**

  （布林值）搜尋整個標籤全文，也就是所有標題、說明等。 優先於「l `ang`」。

### `type` {#type}

將結果限製為特定的JCR節點型別（主要節點型別或mixin型別），並查詢該節點型別的子型別。 存放庫搜尋索引必須涵蓋節點型別，才能有效執行。

其支援Facet擷取。 為結果中的每個唯一型別提供值區。

#### 屬性 {#Properties-2}

* **型別**

  要搜尋的節點型別或mixin名稱，例如`cq:Page`。
