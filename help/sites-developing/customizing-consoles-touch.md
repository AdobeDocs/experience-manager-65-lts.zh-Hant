---
title: 自訂主控台
description: AEM提供多種機制，讓您能夠自訂編寫執行個體的主控台
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 2a94ea8d-2919-4f30-be31-ce559493805d
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 22%

---

# 自訂主控台 {#customizing-the-consoles}

>[!CAUTION]
>
>本檔案說明如何在現代、觸控式UI中自訂主控台，且不套用至傳統UI。

AEM提供多種機制，可讓您自訂編寫執行個體的主控台（以及[頁面編寫功能](/help/sites-developing/customizing-page-authoring-touch.md)）。

* Clientlibs
Clientlibs可讓您擴充預設實作以實現新功能，同時重複使用標準函式、物件和方法。 自訂時，您可以在`/apps.`下建立您自己的clientlib。例如，它可以儲存您自訂元件所需的程式碼。

* 覆蓋
覆蓋是以節點定義為基礎，可讓您以您自己的自訂功能（在`/apps`中）覆蓋標準功能（在`/libs`中）。 建立覆蓋時不需要原始的1:1副本，因為Sling資源合併器允許繼承。

您可以透過多種方式使用這些來擴充AEM主控台。 以下會涵蓋小範圍選區（高階）。

>[!NOTE]
>
>如需進一步詳細資訊，請參閱：
>
>* 正在使用和建立[clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用和建立[重疊](/help/sites-developing/overlays.md)。
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/index.html)
>


>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何專案。
>
>這是因為下次升級執行個體時，`/libs`的內容會被覆寫（當您套用Hotfix或Feature Pack時，這些內容很可能會被覆寫）。
>
>設定和其他變更的建議方法是：
>
>1. 在`/apps`下重新建立必要專案（亦即，它存在於`/libs`中）
>
>1. 在`/apps`中進行任何變更
>

例如，`/libs`結構內的下列位置可以重疊：

* 主控台（任何以Granite UI頁面為基礎的控制檯）；例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>請參閱知識庫文章[疑難排解AEM TouchUI問題](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-16935)，以取得進一步的秘訣和工具。

## 自訂主控台的預設檢視 {#customizing-the-default-view-for-a-console}

您可以自訂主控台的預設檢視 (欄、卡片、清單)：

1. 您可以從下列位置覆蓋所需專案，以重新排序檢視：

   `/libs/wcm/core/content/sites/jcr:content/views`

   第一個專案是預設值。

   可用的節點和可用的檢視選項相互關聯：

   * `column`
   * `card`
   * `list`

1. 例如，在清單的覆蓋中：

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   定義以下屬性：

   * **名稱**：`sling:orderBefore`
   * **類型**：`String`
   * **值**：`column`

### 將動作新增至工具列 {#add-new-action-to-the-toolbar}

1. 您可以建置自己的元件，並包含自訂動作對應的使用者端程式庫。 例如，在下列位置執行&#x200B;**促銷至Twitter**&#x200B;動作：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   然後，這可以連接至主控台上的工具列項目：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在選擇模式下：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 將工具列動作限制在特定群組 {#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自訂的轉譯條件來覆蓋標準動作，並在轉譯前強制實行必須滿足的特定條件。

   例如，建立元件以根據群組控制轉譯條件：

   `/apps/myapp/components/renderconditions/group`

1. 若要將這些專案套用至Sites主控台上的「建立網站」動作：

   `/libs/wcm/core/content/sites`

   建立覆蓋：

   `/apps/wcm/core/content/sites`

1. 然後新增動作的rendercondition：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此節點上的屬性，您可以定義被准許執行特定動作的 `groups`；例如，`administrators`

### 自訂清單檢視中的欄 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>此功能已針對文字欄位欄位進行最佳化；對於其他資料型別，可在`/apps`中覆蓋`cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer`。

若要自訂清單檢視中的欄：

1. 覆蓋可用欄的清單。

   * 在節點上：

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * 新增欄 — 或移除現有欄。

   如需詳細資訊，請參閱[使用覆蓋（以及Sling資源合併）](/help/sites-developing/overlays.md)。

1. 選擇性：

   * 如果您想要插入其他資料，您必須使用撰寫[PageInforProvider](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)

     `pageInfoProviderType`屬性。

   例如，請參閱底下的附加類別/套件（來自GitHub）。

1. 您現在可以在清單檢視的欄配置器中選取欄。

### 篩選資源 {#filtering-resources}

使用主控台時，常見的使用案例是使用者必須從資源（例如頁面、元件、資產等）中進行選取時。 例如，這可以採用清單的形式，作者必須從中選擇專案。

若要將清單保持為合理的大小並且和使用案例相關，可以以自訂述詞的形式實作篩選器。如需詳細資訊，請參閱[自訂頁面編寫 — 篩選資源](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources)。
