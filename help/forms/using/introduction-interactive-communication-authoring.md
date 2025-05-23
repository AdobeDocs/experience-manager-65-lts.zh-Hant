---
title: 互動式通訊編寫UI簡介
description: 介紹您可以用來編寫互動式通訊的各種使用者介面元素
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 595f8d31-f297-48be-8ead-f171a60891b8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 10%

---

# 互動式通訊編寫UI簡介{#introduction-to-interactive-communication-authoring-ui}

編寫[互動式通訊](/help/forms/using/interactive-communications-overview.md)的使用者介面是直覺式的，並提供下列內容來編寫互動式通訊的列印和Web管道：

* WYSIWYG拖放檔案編輯器
* 整合式資產存放庫 — 您可透過互動式通訊編寫介面的資產瀏覽器，使用上傳至伺服器並在其上建立的資產

當您[建立或編輯現有的互動式通訊](../../forms/using/create-interactive-communication.md)時，請使用下列使用者介面元素：

* [側邊欄](#sidebar)
* [頁面工具列](#page-toolbar)
* [元件工具列](#component-toolbar)
* 內容區域

![互動式通訊編寫使用者介面](assets/form-editor.png)

**A.**&#x200B;側欄&#x200B;**B.**&#x200B;頁面工具列&#x200B;**C.**&#x200B;內容區域

## 側邊欄 {#sidebar}

![側邊欄](assets/sidebar-comps-2.png)

**A.**&#x200B;頻道瀏覽器&#x200B;**B.**&#x200B;內容瀏覽器&#x200B;**C.**&#x200B;屬性瀏覽器&#x200B;**D.**&#x200B;資產瀏覽器&#x200B;**E.**&#x200B;元件瀏覽器&#x200B;**F.**&#x200B;資料來源瀏覽器 — 資料模型&#x200B;**G.**&#x200B;資料來源瀏覽器 — 主要內容

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

側邊欄包含下列專案：

* **頻道瀏覽器**

Channel瀏覽器可協助您在互動式通訊的列印與網頁通道之間切換。 根據您在管道瀏覽器中選取的管道，「內容」和「元件」等瀏覽器會顯示選項。

* **內容瀏覽器**
在內容瀏覽器中，您可以看到所選管道檔案的物件階層。 作者可以在檔案物件樹中點選特定元件，以導覽至該元件。 作者可以在Web Channel中搜尋物件，並從此樹狀結構重新排列物件。

* **屬性瀏覽器**

  可讓您編輯元件的屬性。屬性會根據元件而變更。 例如，若要檢視檔案容器的屬性：
選取元件，然後選取![欄位層級](assets/field-level.png) > **檔案容器**，然後選取![cmppr](assets/cmppr.png)。

* **Assets瀏覽器**
區隔不同型別的內容，例如版面片段、影像、檔案、頁面、影片。 作者可以將資產拖放至互動式通訊中。

* **元件瀏覽器**
包含可用來建置檔案的列印和Web管道的元件。 您可以將元件拖曳至互動式通訊以新增元素，並依需求設定新增的元素。 下表說明「元件」瀏覽器中針對列印和Web通道列出的元件：

| **Component** | **列印管道** | **Web Channel** | **功能** |
|---|---|---|---|
| 圖表 | ✓ | ✓ | 新增可在互動式通訊中使用的圖表，以視覺化呈現從表單資料模型集合專案中擷取的二維資料。 |
| 文件片段 | ✓ | ✓ | 可讓您將可重複使用的元件、文字、清單或條件新增至互動式通訊。 您新增至互動式通訊的可重複使用元件，可以是表單資料模型式或不含表單資料模型。 |
| 影像 | ✓ | ✓ | 可讓您插入影像。 |
| 面板 | - | ✓ | Panel元件是將其他元件分組在一起的預留位置，可控制一組元件在互動式通訊中的配置方式。 面板元件也可讓您讓一組元件可供一般使用者重複，例如在填寫教育憑證所需的多個專案中。 同時，在多重索引標籤的互動式通訊的索引標籤中，也應使用各面板。 |
| 表格 | &#42; | ✓ | 新增表格以整理行和欄中的資料。 |
| 目標區域 | &#42;&#42; | ✓ | 在Web Channel中插入目標區域，以整理Web Channel專用元件。 |
| 文字 | - | ✓ | 新增文字至互動式通訊的Web channel。 文字可以使用表單資料模型物件，讓內容成為動態的。 |

&#42;在Print channel中使用佈局片段來新增表格。

&#42;&#42;在Print channel中，目標區域已在XDP/print範本中預先定義。 您無法使用互動式通訊編寫UI新增目標區域。

* **資料來源瀏覽器**
資料來源瀏覽器會以您建立互動式通訊時選取的表單資料模型，顯示可用的資料來源。

### 使用元件的要點 {#key-points-for-working-with-components}

使用互動式通訊元件時的要點如下：

* 每個元件都有相關的屬性，這些屬性控制其外觀和功能。 若要設定元件的屬性，請選取元件，然後選取![cmppr](assets/cmppr.png)，以在[屬性]瀏覽器中開啟元件屬性。
* 以元件的元素名稱來識別元件。 選取![cmppr](assets/cmppr.png)時，您可以變更屬性瀏覽器中的「元素名稱」欄位值來變更元件名稱。 「元素名稱」欄位僅接受字母、數字、連字型大小(-)和底線(_)。 不允許使用其他特殊字元，元素名稱應以字母開頭。
* 只要互動式通訊的標題可見，您就可以修改編輯器中內嵌的互動式通訊元件的Title屬性，而不需開啟Properties瀏覽器。 若要這麼做：

   1. 選取此選項可選取具有Title屬性且已停用Hide title屬性的元件。
   1. 選取![aem_6_3_edit](assets/aem_6_3_edit.png)讓標題可編輯。

   1. 修改標題並選取Return鍵，或選取元件之外的任意位置以儲存變更。 選取Esc鍵以捨棄變更。

## 元件工具列 {#component-toolbar}

![元件工具列標籤](do-not-localize/component_toolbar_labels_new.png)

選取元件時，您會看到可讓您使用元件的工具列。 您可以選擇剪下、貼上、移動和指定元件屬性。您的選項有：

A.**設定**：當您選取&#x200B;**設定**&#x200B;時，元件屬性會顯示在側邊欄中。

B.**編輯規則**：當您選取編輯規則時，規則編輯器會出現，您可以在其中編輯和建立所選元件的規則。 在規則編輯器中，您也可以選取其他表單物件（元件）並編輯/建立這些表單物件的規則。

C.**複製**：您可以使用複製選項來複製元件，並將其貼到互動式通訊的其他位置。

D.**剪下**：您可以在互動式通訊中使用剪下選項將元件從一個位置移動到另一個位置。

E. **刪除**：可讓您從互動式通訊中刪除元件。

F. **插入元件**：可讓您在選取的元件上方插入元件。

G. **貼上**：可讓您使用上述選項貼上您剪下或複製的元件。

H. **群組**：如果您想要一起剪下、複製或貼上多個元件，可讓您選取多個元件。

I. **父系**：可讓您選取元件的父系。

J. **檢視SOM運算式：**&#x200B;可讓您檢視元件的[SOM運算式](../../forms/using/using-som-expressions-adaptive-forms.md)。

K： **面板中的群組物件：**&#x200B;可讓您將面板中的元件群組起來，以便同時對這些元件執行作業。 如需詳細資訊，請參閱[面板中的群組物件](create-interactive-communication.md#groupobjectspanel)。

L. **新增子面板** （僅適用於面板）：可讓您新增子面板至面板。

M： **新增面板工具列** （僅適用於面板）：可讓您新增面板元件的工具列。 您接著可以在工具列上執行進一步的動作。

此外，工具列上的&#x200B;**取代**&#x200B;選項可讓您以替代元件取代現有元件。 選項不適用於面板元件。

## 頁面工具列 {#page-toolbar}

上方的「頁面」工具列提供可讓您預覽互動式通訊並變更其屬性的選項。 您可以在編寫互動式通訊時加以預覽，並據以進行變更。 在頁面工具列中，您會看到：

* 切換側面板![切換側面板](assets/toggle-side-panel.png)：可讓您顯示或隱藏側欄。
* 頁面資訊![pageinformationad](assets/pageinformationad.png)：可讓您檢視頁面屬性。
* 模擬器![尺規](assets/ruler.png)：可讓您針對不同的顯示大小（例如平板電腦和手機），模擬互動式通訊的外觀。
* 編輯：可讓您選取其他模式，例如：編輯、樣式、開發人員和設計。

   * 編輯：可讓您編輯互動式通訊及其元件的屬性。 例如，新增元件、放置影像以及指定必填欄位。
   * 樣式：可讓您為互動式通訊的元件外觀設定樣式。 例如，在樣式模式下，您可以選取面板並指定其背景顏色。
   * 開發人員：讓開發人員：

      * 探索互動式通訊由哪些部分組成。
      * 找出狀況及其發生的時間和位置，這反過來有助於解決問題。

   * Target：可讓您啟用或停用自訂元件，或是側邊欄中未列出的現成可用元件。

* 預覽：可讓您預覽互動式通訊在發佈時的外觀。
