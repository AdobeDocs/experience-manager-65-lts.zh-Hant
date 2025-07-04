---
title: 最適化表單片段
description: 調適型表單提供一種機制，可建立在任何調適型表單中使用的表單區段（例如面板或欄位群組）。 您也可以將現有面板儲存為片段。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 7da165ac-2039-4ac8-810d-fbe6f771453a
source-git-commit: c03b3e3e4526530715718b68804ac26d2562bdb8
workflow-type: tm+mt
source-wordcount: '2372'
ht-degree: 6%

---

# 最適化表單片段{#adaptive-form-fragments}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/adaptive-form-fragments-core-components.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

雖然每個表單都是為特定目的而設計，但大多數表單中都有一些常見的區段，例如提供個人詳細資訊，例如姓名和地址、家庭詳細資訊和收入詳細資訊。 每次建立新表單時，表單開發人員都必須建立這些通用區段。

調適型表單提供一種便利的機制，讓您只需建立一次表單區段（例如面板或欄位群組），即可在調適型表單中重複使用。 這些可重複使用的獨立區段稱為「最適化表單片段」。

>[!NOTE]
>
> 您可以使用[表單片段元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/adaptive-form-fragment)的「設定」對話方塊和「設計」對話方塊，輕鬆自訂使用者的片段體驗。

## 建立片段 {#create-a-fragment}

您可以從頭開始建立最適化表單片段，或將現有最適化表單中的面板儲存為片段。

### 從頭開始建立片段 {#create-fragment-from-scratch}

1. 在https://[*主機名稱*]：[*連線埠*]/aem/forms.html登入AEM Forms作者執行個體。
1. 按一下「**建立 > 自適應表單片段**」。
1. 指定片段的標題、名稱、說明和標籤。

   >[!NOTE]
   >
   >確保為片段指定唯一的名稱。如果存在另一個相同名稱的片段，則無法建立片段。

1. 按一下以開啟&#x200B;**表單模型**&#x200B;標籤，然後從&#x200B;**選取自**&#x200B;下拉式功能表中，為片段選取下列其中一個模型：

   * **無模型**：指定此選項，即可不使用任何表單模型，從頭開始建立表單。

     >[!NOTE]
     >
     > 在基於核心元件的最適化Forms中，您可以在表單中多次使用單一表單片段。 它支援無型和結構描述型表單片段。

   * **表單範本**：指定使用上傳至AEM Forms的XDP範本建立片段。 選取適當的XDP範本作為片段的表單模型。

   ![使用表單範本作為模型建立最適化表單](assets/form-template-model.png)

   所選表單範本中標籤為片段的子表單也會顯示。 您可以從下拉式清單中選取最適化表單片段的子表單。

   ![從指定的表單範本選取子表單](assets/fragment-subform.png)

   此外，您可以在下拉式方塊中指定子表單的SOM運算式，藉此使用未在表單範本中標示為片段的子表單建立最適化表單片段。

   * **XML結構描述**：指定使用上傳至AEM Forms的XML結構描述來建立片段。 您可以上傳或從可用的XML結構描述中選取作為片段的表單模型。

   ![根據XML結構描述建立最適化表單片段做為模型](assets/xml-schema-model.png)

   您也可以從下拉式方塊選取所選結構描述中存在的complexType，以建立最適化表單片段。

   ![從指定的XML結構描述模型選取複雜型別](assets/complex-type.png)

1. 按一下[建立]&#x200B;**&#x200B;**，然後按一下[開啟]&#x200B;**&#x200B;**，以編輯模式開啟具有預設範本的片段。

在編輯模式中，您可以將任何最適化表單元件從AEM sidekick拖放至片段上。 如需最適化表單元件的相關資訊，請參閱[製作最適化表單簡介](../../forms/using/introduction-forms-authoring.md)。

此外，如果您選取XML結構描述或XDP表單範本作為片段的表單模型，內容尋找器中會出現一個顯示表單模型階層的新索引標籤。 它可讓您將表單模型元素拖放至片段上。 新增的表單模型元素會轉換為表單元件，同時保留關聯XDP或XSD的原始屬性。

### 將面板另存為片段 {#save-panel-as-a-fragment}

1. 開啟包含您要另存為最適化表單片段的面板的最適化表單。
1. 在面板工具列中按一下&#x200B;**[!UICONTROL 另存為片段]**。 另存為片段對話方塊隨即開啟。

   >[!NOTE]
   >
   >如果您儲存為片段的面板包含子面板，則產生的片段會包含這些面板。

1. 在「片段建立」對話方塊中，指定下列資訊：

   * **名稱**：片段的名稱。 預設值為面板的元素名稱。 這是必填欄位。

     >[!NOTE]
     >
     >確保為片段指定唯一的名稱。如果存在另一個相同名稱的片段，則無法建立片段。

   * **Title**：片段的標題。 預設值為面板的標題。

   * **描述**：片段的描述。

   * **標籤**：片段的標籤中繼資料。

   * **目標路徑**：儲存片段的存放庫路徑。 若您未指定路徑，則會在包含最適化表單的節點旁建立與片段名稱相同的節點。 片段會儲存在此節點中。

   * **表單模型**：根據最適化表單的表單模型，此欄位會顯示&#x200B;**XML結構描述**、**表單範本**&#x200B;或&#x200B;**無**。 這是不可編輯的欄位。

   * **片段模型根**：僅出現在XSD型最適化表單中。 它會指定片段模型的根。 您可以從下拉式清單中選擇&#x200B;**/**&#x200B;或XSD複雜型別。 只有在選取複雜型別作為片段模型根時，才能在另一個最適化表單中重複使用片段。
如果您選擇&#x200B;**/**&#x200B;作為片段模型根目錄，則最適化表單資料模型標籤中會顯示根目錄的完整XSD樹狀結構。 對於複雜型別片段模型根，在調適型表單資料模型標籤中只會顯示所選複雜型別的子系。 如果您建立片段並選擇複雜型別做為&#x200B;**片段模型根**，則您可以在使用該複雜型別的地方使用它，無論是在相同表單中還是在多個表單中。

   * **XSD Ref**：僅出現在XSD型最適化表單中。 它顯示XML綱要的位置。

   * **XDP Ref**：僅出現在XDP型最適化表單中。 它顯示XDP表單範本的位置。

   ![儲存片段](assets/save-fragment.png)

   另存為片段對話方塊

1. 按一下&#x200B;**「確定」**。

   面板會儲存在存放庫中的指定或預設位置。 在最適化表單中，面板會由片段的快照取代。 如下所示，「一般資訊」面板及其子面板「個人資訊和地址」會儲存為片段。

   若要編輯片段，請按一下面板工具列中的&#x200B;**[!UICONTROL 編輯資產]**。 片段會在編輯模式的新標籤或視窗中開啟。

   ![正在編輯片段](assets/edit-fragment.png)

## 使用片段 {#working-with-fragments}

### 設定片段外觀 {#configure-fragment-appearance}

您在調適型表單中插入的任何片段都會顯示為預留位置影像。 預留位置最多可在片段中顯示十個子面板的標題。 您可以設定AEM Forms顯示完整的片段，而非預留位置影像。

請執行以下步驟，讓您可以在表單中顯示完整的片段：

1. 移至https：[*主機*]：[*連線埠*]/system/console/configMgr的AEM Web主控台設定頁面。

1. 搜尋並選取&#x200B;**[!UICONTROL 最適化表單和互動式通訊Web Channel設定]**，以在編輯模式中開啟它。
1. 停用&#x200B;**[!UICONTROL 啟用預留位置來取代片段]**&#x200B;核取方塊，以便您可以顯示完整的片段，而非預留位置影像。

### 在最適化表單中插入片段 {#insert-a-fragment-in-an-adaptive-form}

您建立的自適應表單片段會顯示在AEM內容尋找器的「自適應表單片段」標籤中。 若要以最適化表單插入最適化表單片段：

1. 以編輯模式開啟最適化表單，您要在其中插入最適化表單片段。
1. 按一下側邊欄中的&#x200B;**Assets** ![assets-browser](assets/assets-browser.png)。 在資產瀏覽器中，從下拉式清單中選取&#x200B;**最適化表單片段**。

   您也可以選擇顯示所有最適化表單片段，或根據其表單模式進行篩選 — 表單範本、XML結構描述或基本。

1. 將最適化表單片段拖放至最適化表單上。

   >[!NOTE]
   >
   >未啟用最適化表單片段來從最適化表單內進行製作。 此外，您無法在JSON型最適化表單中使用XSD型片段，反之亦然。

最適化表單片段會以參考方式插入最適化表單中，並與獨立的最適化表單片段同步。 這表示當您更新最適化表單片段時，這些變更會反映在使用該片段的所有最適化表格中。

### 在自適應表單中嵌入片段 {#embed-a-fragment-in-adaptive-form}

您可以選擇在新增片段的面板工具列上按一下「**內嵌資產： &lt;*fragmentName*>**」按鈕，在自適應表單中內嵌自適應表單片段，如下列範例影像所示。

![將表單片段內嵌於最適化表單](assets/embed-fragment.png)

>[!NOTE]
>
>嵌入的片段不再與獨立片段連結。 您可以從最適化表單內編輯內嵌片段中的元件。

### 在片段中使用片段 {#using-fragments-within-fragments}

您可以建立巢狀自適應表單片段，這表示您可以將片段拖放到另一個片段中，而且可以有巢狀片段結構。

### 變更片段 {#change-fragments}

您可以使用自適應表單片段面板的「編輯」元件對話方塊中的&#x200B;**選取片段資產**&#x200B;屬性，以其他片段取代或變更自適應表單片段。

### 產生最適化表單片段的記錄檔案 {#generate-DOR-for-fragments}

記錄檔案(DOR)可協助您以列印或檔案格式保留表單資訊。 有鑑於此，它有助於您之後隨時追蹤客戶的相關資訊，您也可以使用記錄檔案，以PDF格式將表單與內容一起封存。 [瞭解如何產生最適化表單片段的記錄檔案](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)。

### 在最適化表單中多次使用表單片段 {#using-form-fragment-mutiple-times-in-af}

您可以在調適型表單中多次使用結構描述型表單片段，以唯一儲存每個表單片段欄位的資料。 例如，您可以使用地址表單片段來收集地址詳細資訊，以便永久性、通訊和在貸款申請表中呈現有效地址。

![在最適化表單中使用多個片段](/help/forms/using/assets/using-multiple-fragment-af.gif)

>[!NOTE]
>
> * 如果您在適用性表單中多次使用無架構表單片段，則會發生片段欄位之間的資料同步。 核心元件型表單片段中不會發生資料同步問題，您可以在表單中多次使用結構描述型或無型片段。

## 自動對應資料繫結的片段 {#auto-mapping-of-fragments-for-data-binding}

當您使用XFA表單範本或XSD複雜型別建立最適化表單片段，並將片段拖放至最適化表單時，XFA片段或XSD複雜型別會自動被對應的最適化表單片段取代，其片段模型根已對應至XFA片段或XSD複雜型別。

您可以從「編輯元件」對話方塊變更片段資產及其連結。

>[!NOTE]
>
>您也可以從AEM內容尋找器中的最適化表單片段資料庫拖放已繫結的最適化表單片段，並在最適化表單片段面板的「編輯」元件對話方塊中提供正確的繫結參考。

## 管理片段 {#manage-fragments}

您可以使用AEM Forms UI對最適化表單片段執行數個操作。

1. 前往 `https://[hostname]:'port'/aem/forms.html`。

1. 按一下AEM Forms UI工具列中的&#x200B;**選取**，然後選取最適化表單片段。 工具列會顯示您可對所選最適化表單片段執行的下列操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>開啟</p> </td>
   <td><p>在編輯模式中開啟選取的自適應表單片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>檢視屬性</p> </td>
   <td><p>開啟屬性面板。 從「屬性」面板中，您可以檢視和編輯屬性、產生預覽，以及上傳所選片段的縮圖影像。 如需詳細資訊，請參閱<a href="../../forms/using/manage-form-metadata.md" target="_blank">管理中繼資料</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>複製</p> </td>
   <td><p>複製所選片段。 「貼上」按鈕會出現在工具列中。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>下載</p> </td>
   <td><p>下載所選片段。<br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>預覽</p> </td>
   <td><p>提供以HTML預覽片段的選項，或透過合併XML檔案中的資料與片段來自訂預覽。 如需詳細資訊，請參閱<a href="/help/forms/using/previewing-forms.md" target="_blank">預覽表單</a>。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>開始評論/管理評論</p> </td>
   <td><p>允許啟動和管理所選片段的審查。 如需詳細資訊，請參閱<a href="../../forms/using/create-reviews-forms.md" target="_blank">建立和管理評論</a>。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>建立字典</p> </td>
   <td><p>產生字典以將選取的片段本地化。 如需詳細資訊，請參閱<a href="/help/forms/using/lazy-loading-adaptive-forms.md" target="_blank">將最適化表單當地語系化</a>。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>發佈/取消發佈</p> </td>
   <td><p>發佈/取消發佈所選片段。<br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>刪除</p> </td>
   <td><p>刪除所選片段。<br /><br /> </p> </td>
  </tr>
 </tbody>
</table>

## 本地化包含片段的自適應表單 {#localizing-adaptive-form-containing-fragments}

若要將包含自適應表單片段的自適應表單本地化，您必須分別將片段和表單本地化。 其構想是將片段本地化一次，並在多個最適化表單中重複使用。

>[!NOTE]
>
>片段中的本地化索引鍵不會出現在最適化表單的XLIFF檔案中。

## 使用片段時要記住的關鍵點 {#key-points-to-remember-when-working-with-fragments}

* 確認片段使用唯一的名稱。如果現有片段擁有相同的名稱，則無法建立片段。
* 在XDP型最適化表單中，如果您將面板儲存為包含其他XDP片段的片段，則產生的片段會自動與子XDP片段繫結。 如果存在XSD型最適化表單，則產生的片段會與結構描述根繫結。
* 建立最適化表單片段時，會建立片段節點，這類似於CRXDE Lite中最適化表單的guideContainer節點。
* 不支援使用不同表單資料模型的最適化表單中的片段。 例如，XSD型最適化表單中不支援XDP型片段，反之亦然。
* 最適化表單片段可透過AEM內容尋找器中的最適化表單片段標籤使用。
* 透過參考插入或嵌入自適應表單時，獨立自適應表單片段中的任何運算式、指令碼或樣式都會保留。
* 您無法從最適化表單中編輯依參考插入的最適化表單片段。 若要編輯，請編輯獨立的自適應表單片段，或將片段嵌入自適應表單中。
* 發佈最適化表單時，您必須發佈在最適化表單中透過參考插入的獨立最適化表單片段。
* 當您重新發佈更新的自適應表單片段時，變更會反映在使用片段的自適應表單的已發佈例項中。
* 包含Verify元件的調適型表單不支援匿名使用者。 此外，不建議在自適應表單片段中使用驗證元件。
* (**僅限Mac**)若要確保表單片段功能在所有案例中都能完美運作，請將下列專案新增至/private/etc/hosts檔案：
  `127.0.0.1 <Host machine>` **主機電腦**：部署AEM Forms的Apple Mac電腦。

## 參考片段 {#reference-fragments}

您可以使用參考的最適化表單片段來建立您的表單。 如需詳細資訊，請參閱[參考片段](../../forms/using/reference-adaptive-form-fragments.md)。
