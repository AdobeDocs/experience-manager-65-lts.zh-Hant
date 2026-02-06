---
title: 使用xtype （傳統UI）
description: 瞭解Adobe Experience Manager提供的所有xtype
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4a78de53-33bf-4999-ba3c-7d0bc33196a4
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '3668'
ht-degree: 0%

---

# 使用xtype （傳統UI）{#using-xtypes-classic-ui}

本頁說明Adobe Experience Manager (AEM)可用的所有xtype。

在ExtJS語言中，xtype是指定給類別的符號名稱。 您可以閱讀ExtJS 2[的](https://docs.sencha.com/)總覽的「元件XTypes」段落，以取得有關什麼是xtype以及如何使用的詳細說明。

如需AEM中所有可用Widget的詳細資訊，請參閱[Widget API檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

若要找出指定xtype在AEM中使用的元件，您可以在CRXDE中使用下列`Xpath`查詢。 只需將「checkbox」取代為您感興趣的xtype：

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>本頁說明傳統UI中ExtJS xtypes的使用方式。
>
>Adobe建議您使用以[Coral UI](/help/sites-developing/touch-ui-concepts.md)和[Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)為基礎的標準、新式、[觸控式UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)。

## xtype {#xtypes}

以下列出Adobe Experience Manager中可用的xtype：

* `annotation`

  [CQ.wcm.Annotation](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Annotation`是一個特殊視窗。 其內文中有一個表單，其頁尾有一個按鈕群組。 它通常用於編輯內容，但也只能顯示資訊。

* `arraystore`

  [CQ.Ext.data.ArrayStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  先前稱為`SimpleStore`。

  小型Helper類別，可讓您更輕鬆地從Array資料建立[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 `ArrayStore`已自動設定為[CQ.Ext.data.ArrayReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `asseteditor`

  [CQ.dam.AssetEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Asset Editor`用於DAM管理員。

* `assetreferencesearchdialog`

  [CQ.wcm.AssetReferenceSearchDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `AssetReferenceSearchDialog`是一個對話方塊，會在頁面參考資產或標籤時彈出。

* `blueprintconfig`

  [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BlueprintConfig`提供面板來檢視Blueprint的即時副本及編輯此Blueprint屬性（同步觸發器和同步動作）。

* `blueprintstatus`

  [CQ.wcm.msm.BlueprintStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BlueprintStatus提供面板來檢視和編輯Blueprint及其即時副本關係。 透過[CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[CQ.wcm.msm.BlueprintStatus.Tree](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) Edition完成瀏覽。

* `box`

  [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  任何[元件](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的基底類別（使用寬度和高度），其大小為方塊。

  BoxComponent提供自動的方塊模型調整，以調整大小及定位，並在元件演算模型中正確運作。

* `browsedialog`

  [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BrowseDialog可讓使用者瀏覽存放庫以選取路徑。 它通常透過[BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)使用。

* `browsefield`

  [CQ.form.BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **已棄用：請改用[CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)**

* `bulkeditor`

  [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BulkEditor`提供搜尋引擎和格線來編輯搜尋結果。

  `BulkEditor`必須插入HTML表單（匯入功能所需）。 這完全適用於[CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `bulkeditorform`

  [CQ.wcm.BulkEditorForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BulkEditorForm提供HTML表單所包圍的[CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的獨立版本。 匯入按鈕需要HTML表單。

* `button`

  [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  簡單按鈕類別

* `buttongroup`

  [CQ.Ext.ButtonGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  按鈕群組的容器。

* `chart`

  [CQ.Ext.chart.Chart](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CQ.Ext.chart套件提供以Flash為基礎的圖表將資料視覺化的功能。 每個圖表都直接繫結至CQ.Ext.data.Store，以啟用圖表的自動更新。 若要變更圖表的外觀，請參閱[chartStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[extraStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)設定選項。

* `checkbox`

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  單一核取方塊欄位。 可用來直接取代傳統的核取方塊欄位。

* `checkboxgroup`

  [CQ.Ext.form.CheckboxGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)控制項的分組容器。

* `clearcombo`

  [CQ.form.ClearableComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ClearableComboBox為不可編輯的下拉式方塊，具有清除其值的觸發器。

* `colorfield`

  [CQ.form.ColorField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ColorField可讓使用者直接或使用[CQ.Ext.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)輸入顏色十六進位值。

* `colorlist`

  [CQ.form.ColorList](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ColorList可讓使用者從可編輯的清單中選擇顏色。

* `colormenu`

  [CQ.Ext.menu.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  包含[CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)元件的功能表。

* `colorpalette`

  [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  選擇顏色的簡單調色盤類別。 浮動視窗可呈現至任何容器。

* `combo`

  [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  可支援自動完成、遠端載入、分頁和許多其他功能的下拉式方塊控制項。

  ComboBox的運作方式與傳統HTML &lt;select>欄位類似。 不同之處在於，若要提交[valueField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，您必須指定[hiddenName](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)以建立隱藏的輸入。

* `component`

  [CQ.Ext.Component](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  所有`Ext`元件的基底類別。 元件的所有子類別都可以參與由`Ext`Container[類別提供的建立、演算和銷毀的自動化](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)元件生命週期。 建立容器時，元件可透過[專案](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)組態選項新增至容器。

* `componentextractor`

  [CQ.wcm.ComponentExtractor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ComponentExtractor可讓使用者從網站/頁面擷取元件。

* `componentselector`

  [CQ.form.ComponentSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  可用元件的分組、有序選擇。

* `componentstyles`

  [CQ.form.ComponentStyles](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `compositefield`

  [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基於面板的複雜表單欄位的基底類別，包括一個表單欄位或一組表單欄位。

* `container`

  [CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  任何可能包含其他元件的[CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的基底類別。 容器可處理包含專案的基本行為，即新增、插入和移除專案。

  最常使用的容器類別是[CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `contentfinder`

  [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinder是特殊化的兩欄[檢視區](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，它包含左邊的實際內容尋找器和右邊的內容框架。

* `contentfindertab`

  [CQ.wcm.ContentFinderTab](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinderTab是專用面板，提供用於[CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的標籤面板的功能。 通常會有搜尋表單（查詢方塊）和資料檢視來顯示搜尋。

* `cq.workflow.model.combo`

  [CQ.wcm.WorkflowModelCombo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelCombo是自訂的[CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，會顯示可用工作流程模型的清單。

* `cq.workflow.model.selector`

  [CQ.wcm.WorkflowModelSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelSelector會將WorkflowModelCombo與工作流程的縮圖影像，以及建立和編輯工作流程模型的按鈕結合在一起。

* `createsitewizard`

  [CQ.wcm.CreateSiteWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateSiteWizard是建立(MSM)網站的逐步精靈。

* `createversiondialog`

  [CQ.wcm.CreateVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateVersionDialog是允許建立頁面版本的對話方塊。

* `customcontentpanel`

  [CQ.CustomContentPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CustomContentPanel是用於[CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的特殊面板：其內容會從對話方塊中的其他欄位擷取並送出至不同的URL。

* `cycle`

  [CQ.Ext.CycleButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  專用的SplitButton，包含[CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)專案的功能表。 按鈕會在每次點按時自動循環每個功能表專案，引發作用中功能表專案的按鈕[變更](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)事件(或呼叫按鈕的[changeHandler](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)函式（如果提供）)。

* `dataview`

  [CQ.Ext.DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  使用自訂配置範本和格式來顯示資料的機制。 DataView使用[CQ.Ext.XTemplate](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)作為其內部範本化機制，並繫結至[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，以便在存放區中的資料變更時，檢視會自動更新以反映變更。

* `datefield`

  [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它提供具有[CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)下拉式清單和自動日期驗證的日期輸入欄位。

* `datemenu`

  [CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  包含[CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)元件的功能表。

* `datepicker`

  [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  快顯日期選擇器。 [DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)類別使用此類別來允許瀏覽及選取有效日期。

* `datetime`

  [CQ.form.DateTime](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DateTime可讓使用者結合[CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，以輸入日期和時間。

* `dialog`

  [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  對話方塊是一個特殊的視窗。 其內文中有一個表單，其頁尾有一個按鈕群組。 它通常用於編輯內容，但也只能顯示資訊。

* `dialogfieldset`

  [CQ.form.DialogFieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DialogFieldSet是用於[對話方塊](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `directstore`

  [CQ.Ext.data.DirectStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  小型helper類別可建立以[CQ.Ext.data.DirectProxy](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)設定的[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，以便更輕鬆地與[CQ.Ext.Direct](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)伺服器端[提供者](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)互動。

* `displayfield`

  [CQ.Ext.form.DisplayField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  未驗證且未提交的僅限顯示文字欄位。

* `editbar`

  [CQ.wcm.EditBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  EditBar可讓使用者使用列上的按鈕來編輯內容。

  雖然此處未列出，但EditBar擁有[CQ.wcm.EditBase](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的所有成員。

* `editor`

  [CQ.Ext.Editor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  處理隨選顯示/隱藏且具有某些內建調整大小和事件處理邏輯的基本編輯器欄位。

* `editorgrid`

  [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  此類別擴充[GridPanel類別](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，以在選取的[欄](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)上提供儲存格編輯。 可編輯的資料行是透過在[資料行組態](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)中提供[編輯器](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)來指定的。

* `editrollover`

  [CQ.wcm.EditRollover](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  「編輯」「滑鼠指向效果」可讓使用者透過按兩下來編輯內容，並透過快顯選單提供更多編輯動作。 當滑鼠滑過內容時，可編輯區域會以框架表示。

* `feedimporter`

  [CQ.wcm.FeedImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FeedImporter可讓使用者匯入RSS或Atom摘要，並為每個摘要專案建立頁面。

* `field`

  [CQ.Ext.form.Field](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  表單欄位的基底類別，提供預設事件處理、大小調整、值處理和其他功能。

* `fieldset`

  [CQ.Ext.form.FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  用於分組[表單](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)中專案的標準容器。

* `fileuploaddialogbutton`

  [CQ.form.FileUploadDialogButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadDialogButton會建立按鈕，開啟新的對話方塊，以透過FileUploadField上傳檔案。 可以在編輯對話方塊內使用，其中上傳必須以單獨的表單進行。

* `fileuploadfield`

  [CQ.form.FileUploadField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadField可讓使用者選取要上傳的單一檔案。

* `findreplacedialog`

  [CQ.wcm.FindReplaceDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FindReplaceDialog是尋找和取代頁面及其子頁面中的權杖的對話方塊。

* `flash`

  [CQ.Ext.FlashComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `grid`

  [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  此類別代表元件式網格控制項的主要介面，以表格格式的列與欄表示資料。

* `groupingstore`

  [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  提供依其中一個可用欄位來分組記錄的專用存放區實施。 與[CQ.Ext.grid.GroupingView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)搭配使用，以證明群組GridPanel的資料模型。

* `heavymovedialog`

  [CQ.wcm.HeavyMoveDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HeavyMoveDialog是用來移動頁面及其子頁面的對話方塊，也會考慮重新啟用先前啟動的頁面（「大幅」移動）。

* `hidden`

  [CQ.Ext.form.Hidden](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  在表單中儲存隱藏值的基本隱藏欄位，必須在表單提交中傳遞。

* `historybutton`

  [CQ.HistoryButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HistoryButton是小型的helper類別，可輕鬆提供後退和前進按鈕。 通常需要兩個相關的執行個體：前進按鈕執行個體是一個連結到後退按鈕執行個體的簡單按鈕，可處理歷史記錄。

* `htmleditor`

  [CQ.Ext.form.HtmlEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它提供輕量版HTML Editor元件。 Safari不支援某些工具列功能，因此系統會在需要時自動隱藏這些功能。 在適當的設定選項中註明。

  編輯器的工具列按鈕在[buttonTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)屬性中定義了工具提示。

* `iframedialog`

  [CQ.IframeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  顯示iframe內容並允許iframe中表單的純對話方塊。

* `iframepanel`

  [CQ.IframePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  包含iframe的面板。 它可讓您輕鬆建立iframe、iframe載入事件，並輕鬆存取iframe的內容。

* `inlinetextfield`

  [CQ.form.InlineTextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  InlineField是文字欄位，當不在焦點時會顯示為標籤。

* `jsonstore`

  [CQ.Ext.data.JsonStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  小型Helper類別，可讓您更輕鬆地從JSON資料建立[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 JsonStore已自動設定為[CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `label`

  [CQ.Ext.form.Label](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本標籤欄位。

* `languagecopydialog`

  [CQ.wcm.LanguageCopyDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LanguageCopyDialog是複製語言樹狀結構的對話方塊。

* `linkchecker`

  [CQ.wcm.LinkChecker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LinkChecker是檢查網站中外部連結的工具。

* `listview`

  [CQ.Ext.list.ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CQ.Ext.list.ListView是[網格式](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)檢視的快速輕量實作。

* `livecopyproperties`

  [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LiveCopyProperties提供可檢視和編輯即時副本屬性（關係繼承、同步觸發器和同步動作）的面板。

* `lvbooleancolumn`

  [CQ.Ext.list.BooleanColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  呈現布林資料欄位的Column定義類別。 如需詳細資訊，請參閱[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)組態選項。

* `lvcolumn`

  [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  此類別封裝要用於[ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)初始化的資料行組態資料。

* `lvdatecolumn`

  [CQ.Ext.list.DateColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  根據預設地區設定或設定的[格式](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)呈現通過日期的Column定義類別。 如需詳細資訊，請參閱[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)組態選項。

* `lvnumbercolumn`

  [CQ.Ext.list.NumberColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  根據[格式](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)字串呈現數值資料欄位的Column定義類別。 如需詳細資訊，請參閱[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的[xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)組態選項。

* `mediabrowsedialog`

  [CQ.MediaBrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **已棄用：請改用[內容尋找器](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)來瀏覽媒體。**

  MediaBrowseDialog是用來瀏覽媒體庫的對話方塊。

* `menu`

  [CQ.Ext.menu.Menu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  選單物件。 您可新增功能表專案的容器。 當您想要以其他元件（例如[CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)）為基礎的特殊功能表時，功能表也可以做為基底類別。

  功能表可包含[功能表專案](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)或一般[元件](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `menubaseitem`

  [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  呈現至功能表之所有專案的基底類別。 BaseItem提供預設呈現、啟動狀態管理，以及所有功能表元件共用的基本組態選項。

* `menucheckitem`

  [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  預設會新增包含核取方塊的功能表專案，但也可以是選項群組的一部分。

* `menuitem`

  [CQ.Ext.menu.Item](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  需要功能表相關功能（如子功能表）且不是靜態顯示專案的所有功能表專案的基底類別。 專案透過新增功能表特定的啟用和點按處理，來擴充[CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的基本功能。

* `menuseparator`

  [CQ.Ext.menu.Separator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它會在選單中新增分隔列，用來劃分選單專案的邏輯群組。 一般而言，您會在要新增()的呼叫或專案設定中使用「 — 」來新增專案，而非直接建立專案。

* `menutextitem`

  [CQ.Ext.menu.TextItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它會將靜態文字字串新增至功能表，作為標題或群組分隔符號使用。

* `metadata`

  [CQ.dam.form.Metadata](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Metadata`提供一組欄位，以決定如在Asset Editor頁面上使用之中繼資料欄位所需的資訊。

  它提供下列欄位：

* `multifield`

  [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `MultiField`是可編輯的表單欄位清單，用於編輯多值屬性。

* `mvt`

  [CQ.form.MVT](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Multivariate Testing元件可用來定義及編輯一組以交替橫幅顯示的影像。 每個橫幅會收集點進率統計資料。

* `notificationinbox`

  [CQ.wcm.NotificationInbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `NotificationInbox`可讓使用者訂閱WCM動作及管理通知。

* `numberfield`

  [CQ.Ext.form.NumberField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  提供自動按鍵篩選和數值驗證的數值文字欄位。

* `offlineimporter`

  [CQ.wcm.OfflineImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OfflineImporter`是將Microsoft® Word檔案匯入並轉換成AEM頁面的工具。 此功能允許使用文書處理器離線編輯內容。

* `ownerdraw`

  [CQ.form.OwnerDraw](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OwnerDraw`可以包含自訂HTML程式碼（直接輸入或從URL擷取）。

* `paging`

  [CQ.Ext.PagingToolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  隨著記錄數增加，瀏覽器轉譯記錄所需的時間也會增加。 分頁用於減少與使用者端交換的資料量。

* `panel`

  [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `panel`是一個容器，具有特定的功能和結構元件，使其成為應用程式導向使用者介面的完美建置區塊。

  依據面板的繼承，這些面板是來自[CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `paragraphreference`

  [CQ.form.ParagraphReference](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  段落參考欄位可讓您瀏覽頁面並選取其中一個段落。 它由觸發欄位和關聯的段落瀏覽對話方塊組成。

* `password`

  [CQ.form.Password](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Password`類似[CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，但會保留其私密值，讓使用者可以輸入敏感資料。

* `pathcompletion`

  [CQ.form.PathCompletion](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **已棄用：請改用[CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)**

* `pathfield`

  [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PathField`是專為路徑完成路徑設計的輸入欄位，以及開啟[CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)以瀏覽伺服器存放庫的按鈕。 它也可以瀏覽頁面段落以產生進階連結。

* `progress`

  [CQ.Ext.ProgressBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  可更新的進度列元件。 進度列支援兩種不同的模式：手動和自動。

  在手動模式中，您有責任顯示、更新（透過[updateProgress](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)）並視需要從您自己的程式碼中清除進度列。 若要顯示進度，此方法最適合。

* `propertygrid`

  [CQ.Ext.grid.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  專門化的網格實作，用來模擬開發IDE中通常看到的傳統屬性網格。 格線中的每一列代表某個物件的屬性，資料會在[CQ.Ext.grid.PropertyRecord](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s中儲存為一組名稱/值組。

* `propgrid`

  [CQ.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PropertyGrid`是用於顯示和編輯物件屬性的通用格線。

* `quicktip`

  [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `@xtype quicktip` — 工具提示的特殊工具提示類別，可在標籤中指定並由全域[CQ.Ext.QuickTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)執行個體自動管理。 如需其他使用方式的詳細資訊和範例，請參閱QuickTips類別標題。

* `radio`

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  單一`radio`欄位。 與Checkbox相同，但為了方便您自動設定輸入型別。 當群組中的每個選項按鈕使用相同的名稱時，瀏覽器會自動將選項按鈕分組。


* `radiogroup`

  [CQ.Ext.form.RadioGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)控制項的分組容器。

* `referencesdialog`

  [CQ.wcm.ReferencesDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `ReferencesDialog`是在頁面上顯示參考的對話方塊。

* `restoretreedialog`

  [CQ.wcm.RestoreTreeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RestoreTreeDialog`是用來還原樹狀結構先前版本的對話方塊。

* `restoreversiondialog`

  [CQ.wcm.RestoreVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  RestoreVersionDialog是用來還原先前版本頁面的對話方塊。

* `richtext`

  [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RichText`提供表單欄位，用於編輯樣式文字資訊(RTF)。

  `RichText`元件目前提供下列功能：

* `rolloutplan`

  [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  RolloutPlan會提供一個對話方塊，用來觀看頁面轉出進度。 [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)會啟動RolloutPlan。

* `rolloutwizard`

  [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RolloutWizard`提供轉出頁面的精靈。 RolloutWizard會啟動[CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

* `searchfield`

  [CQ.form.SearchField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SearchField`提供搜尋欄位，在可用來搜尋存放庫的下拉式清單中提供結果。

* `selection`

  [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Selection`可讓使用者在數個選項之間選擇。 選項可以是設定的一部分，或從JSON回應載入。 選取範圍可以呈現為下拉式（選取）或下拉式方塊（選取加上任意文字輸入）。

* `sidekick`

  [CQ.wcm.Sidekick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Sidekick`是浮動協助程式，為使用者提供用於編輯頁面的常用工具。

* `siteadmin`

  [CQ.wcm.SiteAdmin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteAdmin`是提供WCM管理功能的主控台。

* `siteimporter`

  [CQ.wcm.SiteImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteImporter`可讓使用者匯入完整的網站並建立初始專案。

* `sizefield`

  [CQ.form.SizeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SizeField`可讓使用者輸入寬度和高度（例如影像）。

* `slider`

  [CQ.Ext.Slider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  可支援垂直或水準方向、鍵盤調整、可設定的貼齊、軸點選和動畫的滑桿。 可將其新增為任何容器的專案。 例如，使用方式： ...

* `slideshow`

  [CQ.form.Slideshow](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  「投影片」元件可讓您定義及編輯一組影像和影像標題。 使用者可以投影片形式檢視集合。

  投影片元件是以[CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)元件為基礎。

* `smartfile`

  [CQ.form.SmartFile](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartFile是智慧型檔案上傳程式。

  如果已安裝Flash外掛程式（版本>= 9），則使用SWFupload程式庫執行上傳，提供處理上傳的便利方式。

* `smartimage`

  [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartImage是智慧型影像上傳程式。 它提供處理上傳影像的工具，例如定義影像地圖的工具和影像裁剪程式。

  此元件設計用於單獨的對話方塊索引標籤中。

* `spacer`

  [CQ.Ext.Spacer](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  用於提供版面配置中可擴充的空間。

* `spinner`

  [CQ.form.Spinner](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Spinner`是數值、日期或時間值的觸發欄位。 使用提供的上下觸發器、捲動輪或按鍵，可增加或減少值。

* `splitbutton`

  [CQ.Ext.SplitButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  提供內建下拉式箭頭的`splitbutton`，此箭頭可與按鈕的預設點按事件分開引發事件。 一般而言，這會用來顯示一個下拉式功能表，為主要按鈕動作提供其他選項，但任何自訂處理常式都可以提供`arrowclick`實作。

* `static`

  [CQ.Static](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Static`可用來顯示任意文字或HTML。

* `statistics`

  [CQ.wcm.Statistics](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Statistics`會將頁面印象顯示為圖表。 Widget可讓您選取應顯示統計資料的期間。

* `store`

  [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Store`類別封裝[Record](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)物件的使用者端快取，這些物件提供如[GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)或[DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)等元件的輸入資料。

* `suggestfield`

  [CQ.form.SuggestField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SuggestField`會根據使用者的輸入為其提供建議。

* `switcher`

  [CQ.Switcher](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Switcher`在主控台中提供標題列的按鈕群組，以便在網站、數位Assets、工具、工作流程和安全性之間切換。

* `tableedit`

  [CQ.form.TableEdit](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **已棄用：請改用[CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。**

* `tableedit2`

  [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TableEdit2`提供用來建立表格的Widget。

* `tabpanel`

  [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本頁簽容器。 TabPanels的使用方式與標準[CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)完全相同，可用於配置用途，但對於包含子元件([`items`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html))也有特殊的支援。

* `tags`

  [CQ.tagging.TagInputField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ```
  CQ.tagging.TagInputField
  ```

  是用於輸入標籤的表單Widget。 它有一個彈出式選單，可供您從現有標籤中選取，包括自動完成和許多其他功能。

* `textarea`

  [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  多行文字欄位。 可用來直接取代傳統`textarea`欄位，加上支援自動調整大小。

* `textbutton`

  [CQ.TextButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TextButton`提供具有[CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)功能的文字連結。

* `textfield`

  [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本文字欄位。 可用來直接取代傳統的文字輸入，或做為較複雜的輸入控制項（如[CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)）的基類別。

* `thumbnail`

  [CQ.form.Thumbnail](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `timefield`

  [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它提供時間輸入欄位，內含時間下拉式清單和自動時間驗證。 使用範例： ...

* `tip`

  [CQ.Ext.Tip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype提示：這是[CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[CQ.Ext.Tooltip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)的基底類別，提供所有提示類別所需的基本配置與定位。 此類別可直接用於簡單、靜態定位的提示。

* `titleseparator`

  [CQ.menu.TitleSeparator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它會在選單中新增分隔列，用來劃分選單專案的邏輯群組。 分隔符號也可以包含標題。

* `toolbar`

  [CQ.Ext.Toolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本`Toolbar`類別。 雖然工具列的[`defaultType`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)是[`button`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，但工具列元素（工具列容器的子專案）實際上可以是任何型別的元件。 工具列元素可透過其建構函式明確建立。

* `tooltip`

  [CQ.Ext.ToolTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  標準`tooltip`實作，可在游標停留在目標元素上時提供其他資訊。 @xtype一下工具提示。

* `treegrid`

  [CQ.tree.TreeGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype `treegrid`

* `treepanel`

  [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TreePanel`提供樹狀結構資料的UI表示法。

  新增至[的](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)TreeNode`TreePanel`可以包含您的應用程式在其[屬性](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)屬性中所使用的中繼資料。

* `trigger`

  [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  它為`TextFields`提供便利的包裝函式，可新增可點按的觸發按鈕（預設看起來像是下拉式方塊）。 觸發程式沒有預設動作，因此您必須透過覆寫[onTriggerClick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)，指派函式以實作觸發程式點選處理常式。 您可以直接建立`TriggerField`，因為它呈現的方式與下拉式方塊完全相同。

* `uploaddialog`

  [CQ.UploadDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `UploadDialog`可讓使用者上傳檔案到存放庫建立新的UploadDialog。

* `userinfo`

  [CQ.UserInfo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  工具列專案，顯示目前的使用者名稱並允許使用者動作，例如編輯使用者屬性和模擬。

* `viewport`

  [CQ.Ext.Viewport](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  代表可檢視應用程式區域（瀏覽器檢視區）的特殊容器。

  `Viewport`會將自身呈現至檔案內文，並自動調整自身大小以符合瀏覽器檢視區的大小並管理視窗大小調整。 只能建立一個檢視區。

* `window`

  [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  專用於作為應用程式視窗的面板。 Windows已浮動，預設為[可調整大小](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)和[可拖曳](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 Windows可以[最大化](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)以填滿檢視區，還原成先前的大小，也可以[最小化](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)天。

* `xmlstore`

  [CQ.Ext.data.XmlStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  小型協助程式類別，可讓您更輕鬆地從XML資料建立[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。 `XmlStore`已自動設定為[CQ.Ext.data.XmlReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)。

  `cqinclude` — 包含來自存放庫中不同路徑的Widget定義的偽xtype。 最常用於頁面對話方塊。 此xtype沒有實際的JavaScript Widget類別。 `CQ.Util`類別會使用`formatData()`函式來處理它。
