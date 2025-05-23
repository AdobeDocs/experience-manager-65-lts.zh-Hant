---
title: 內容片段的元件
description: Adobe Experience Manager (AEM)內容片段會建立並管理為不受頁面影響的資產
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
exl-id: 2196af09-8053-49c3-8a23-caf03bb9a39d
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 內容片段的元件{#components-for-content-fragments}

## 片段編寫的元件 {#components-for-fragment-authoring}

>[!CAUTION]
>
>不建議擴充或變更片段編輯器中使用的實際元件，因為這些元件仍可能會變更。

請參閱[內容片段管理API — 使用者端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side)。

## 用於頁面編寫的元件 {#components-for-page-authoring}

>[!CAUTION]
>
>現在建議使用[內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hant)。 如需詳細資訊，請參閱[開發核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=zh-Hant)。
>
>本節詳細說明傳送用於內容片段的原始元件（**一般**&#x200B;群組中的&#x200B;**內容片段**）。

>[!NOTE]
>
>另請參閱[轉譯專用內容片段設定元件](/help/sites-developing/content-fragments-config-components-rendering.md)以取得進一步資訊。

Adobe Experience Manager (AEM)內容片段是[建立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。 它們可讓您建立管道中性內容，連同（可能特定於管道）變數。 [您接著可以在編寫內容頁面時，使用這些片段及其變數](/help/sites-authoring/content-fragments.md)。 您也可以[將現有內容片段資產從資產瀏覽器拖曳至頁面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （如同其他資產型元件，例如基礎元件影像）來使用現有內容片段資產。 現成可用的內容片段元件只會顯示參照內容片段的一個[元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。 使用元件對話方塊，您可以定義要在頁面上顯示的[元素、變數和片段段落](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)的範圍。

>[!NOTE]
>
>此內容片段元件已在AEM 6.2中作為文章元件的增強版本引入，但已遭淘汰。

>[!NOTE]
>
>傳統UI中不支援內容片段。

### 定義 {#definition}

**內容片段**&#x200B;元件是用來儲存內容片段資產的參考（有效地增強文字資產）。 內容片段的資源型別為：

`dam/cfm/components/contentfragment/contentfragment`

參照是在屬性中定義：

`fileReference`

只有觸控式UI的編輯器完全支援內容片段元件，其中包括使用者端程式庫：

`cq.authoring.editor.plugin.cfm`

此程式庫會將內容片段的特定功能新增到編輯器中。 例如，可支援在頁面上新增和設定內容片段的功能、在資產瀏覽器中搜尋內容片段資產的功能，以及側面板中的相關內容。

### 中間內容 {#in-between-content}

**內容片段** t元件可讓您在顯示的[元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)的不同段落之間放置額外的元件。 基本上，顯示的元素由不同的段落組成（每個段落都標有歸位字元）。 在每個段落之間，您可以使用其他元件來插入內容。

從技術觀點來看，所顯示元素的每個段落都位於其自身的parsys中，您在段落之間新增的每個元件都會（在機殼下）插入到parsys中。

換言之，如果內容片段元件的例項由三個段落組成，則元件在存放庫中會有三個不同的parsys。 所有新增至內容片段的中間內容實際上都位於這些parsys內。

在存放庫中，中間內容會相對於其在整體段落結構中的位置儲存，也就是說，它不會附加至實際的段落內容。

為了說明這一點，請考量您有以下事項：

* 由三個段落組成的內容片段例項
* 而且有些內容已經插入在第二段之後

   * 這表示內容會儲存在第二個parsys中。

基本上，如果此例項的段落結構有所變更（透過變更顯示的變化、元素或段落範圍），可能會影響內容片段內容時顯示的中間內容：

* 會進行編輯，並在第二段之前新增另一個段落：

   * 中間內容會顯示在新建的段落之後（第二個parsys現在會儲存新建的段落）。

* 已編輯並移除第二段：

   * 中間內容會顯示在先前為第三個的段落之後（第二個parsys現在會保留前一個第三個段落）。

* 設定為只顯示第一段：

   * 不會顯示中間內容（由於新設定，第二個parsys不再呈現）。

### 自訂內容片段元件 {#customizing-the-content-fragment-component}

若要使用現成的內容片段元件作為擴充的藍圖，您應遵守下列合約：

* 重複使用HTL演算指令碼及其關聯的POJO，以便檢視中間內容功能的實作方式。
* 重複使用內容片段節點： `cq:editConfig`

   * `afterinsert`/ `afteredit`/ `afterdelete`接聽程式是用來觸發JS事件。 這些事件會在`cq.authoring.editor.plugin.cfm`使用者端資料庫中處理，以在側面板中顯示關聯內容。
   * `cq:dropTargets`已設定為支援拖曳內容片段資產。
   * `cq:inplaceEditing`已設定為支援在頁面編輯器中編寫內容片段。 片段就地編輯器定義於`cq.authoring.editor.plugin.cfm`使用者端程式庫中，允許快速連結以在[片段編輯器](/help/assets/content-fragments/content-fragments-variations.md)中開啟目前的[元素/變數](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。

### 轉譯前的資產重新寫入 {#asset-rewriting-before-rendering}

內容片段管理會使用內部轉譯程式，為頁面產生最終HTML輸出。 這在內部供內容片段元件使用，同時也供在參考頁面上更新參考片段的背景程式使用。

在內部，Sling重寫程式會用於該轉譯。 在`/libs/dam/config/rewriter/cfm`找到個別的設定，必要時可加以調整。 如需詳細資訊，請參閱[Apache Sling重寫程式](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)。

>[!CAUTION]
>
>如果您確實調整/覆蓋重寫程式的設定：
>
>* `/libs/dam/config/rewriter/cfm`
>
>然後`serializerType` **必須**&#x200B;更新至：
>
>* `serializerType="html5-serializer"`

現成可用的組態使用下列轉換器：

* `transformer-cfm-payloadfilter` — 僅用於擷取片段HTML的`body`部分( `<body>...</body>`)

* `transformer-cfm-parfilter` — 如果指定了段落範圍，則篩選掉不需要的段落（與內容片段元件一樣）
* `transformer-cfm-assetprocessor` — 內部用於擷取內嵌於片段中的資產清單

轉譯程式透過[`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html)公開，如有需要，可由自訂元件使用（例如）。
