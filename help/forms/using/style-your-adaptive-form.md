---
title: 設計您的自適應表單
description: 瞭解如何建立自訂主題、設定個別元件的樣式，以及在主題中使用Web Fonts。
topic-tags: introduction
feature: Adaptive Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 5b3beaa6-ca0a-454e-85ee-c3653dd423fe
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2038'
ht-degree: 8%

---

# 設計您的自適應表單 {#do-not-publish-style-your-adaptive-form}

瞭解如何建立自訂主題、設定個別元件的樣式，以及在主題中使用Web Fonts。

![hero-image](do-not-localize/08-style_your_adaptiveformmain.png)

本教學課程是[建立第一個最適化表單](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的步驟。 Adobe建議您依照時間順序來瞭解、執行和示範完整的教學課程使用案例。

## 關於教學課程  {#about-the-tutorial}

您可以使用主題來為最適化表單提供獨特的外觀和樣式。 您可以套用最適化表單編輯器隨附的現成主題，或是建立您自己的自訂主題。 AEM [!DNL Forms]提供[主題編輯器](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/themes.html)以建立自訂主題。 單一主題可為在行動裝置、平板電腦或桌上型電腦上開啟的相同最適化表單提供不同外觀。 使用主題編輯器不需要有CSS或LESS的任何先前知識，但這是必要的。

在本教學課程結束時，您應該能夠進行下列工作：

* 將立即可用的主題套用至最適化表單
* 使用主題編輯器建立最適化表單的主題
* 個別元件的樣式
* 額外章節：在自訂主題中使用Web Fonts

完成本教學課程後，您的表單應看起來類似下列內容：

![具有自訂主題的表單](assets/styled-adaptive-form.png)

## 開始之前 {#before-you-start}

在本機電腦上下載標題樣式和標誌影像（如下所示）。 `shipping-address-add-update-form`最適化表單的標題使用標題樣式和標誌影像。 頁首樣式影像會出現在頁首的右側。

[取得檔案](assets/header-style.png)

[取得檔案](assets/logo-1.png)

## 步驟1：將主題套用至最適化表單 {#step-apply-a-theme-to-your-adaptive-form}

調適型表單編輯器提供多個現成可用的主題。 如果您不打算將自訂樣式用於最適化表單，也可以使用現成可用的主題發佈最適化表單。 主題與調適型表單無關。 您可以將相同主題套用至多個最適化表單。

**若要將佈景主題套用至最適化表單：**

1. 開啟最適化表單進行編輯。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. 開啟&#x200B;**[!UICONTROL 最適化表單容器]**&#x200B;的屬性。 在屬性瀏覽器中，瀏覽至&#x200B;**[!UICONTROL 基本]** > **[!UICONTROL 最適化表單主題]**。 **[!UICONTROL 最適化表單主題]**&#x200B;欄位會列出所有現成可用的主題和自訂主題。 依預設，會套用畫布主題。
1. 從&#x200B;**[!UICONTROL 最適化表單主題]**&#x200B;欄位中選取主題。 例如，**問卷主題**。 選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)，以便套用選取的主題。

   ![具有預設主題的最適化表單](assets/default-adaptive-form.png)

   **圖：** *具有預設主題的最適化表單*

   ![含有調查主題的最適化表單](assets/adaptive-form-with-survey-theme.png)

   **圖：** *含有調查主題的最適化表單*

## 步驟2：更新最適化表單 {#step-update-your-adaptive-form}

以上顯示的設計需要變更您現有的最適化表單的預留位置文字和標誌。

**若要更新您的最適化表單：**

1. 變更頁首的現有標誌和文字。 若要移除標誌：

   1. 在表單編輯器中開啟表單。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. 選取[!UICONTROL 標題]元件中的標誌影像，並選取![cmppr](assets/cmppr.png) **[!UICONTROL 屬性]**。 在[!UICONTROL image]屬性中，選取X以移除現有的標誌影像。
   1. 選取&#x200B;**[!UICONTROL 上傳]**、選取logo.png，然後選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)以儲存變更。 在您開始[&#128279;](/help/forms/using/style-your-adaptive-form.md#before-you-start)之前，已在區段中下載影像。
   1. 選取標題文字`We.Retail`，然後選取![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**。 將標頭文字變更為`we retail`。 僅套用粗體格式至`we retail`中的`we`。

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. 移除標題並新增預留位置文字：

   1. 選取[客戶ID]欄位並選取![cmppr](assets/cmppr.png)屬性。
   1. 將&#x200B;**[!UICONTROL 標題]**&#x200B;欄位的內容複製到&#x200B;**[!UICONTROL 預留位置文字]**&#x200B;欄位。
   1. 刪除&#x200B;**[!UICONTROL Title]**&#x200B;欄位的內容並選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
   1. 對表單中的所有文字方塊、數值方塊和電子郵件欄位重複前三個步驟。

      ![已更新最適化表單](assets/updated-adaptive-form.png)

## 步驟3：建立最適化表單的自訂主題 {#step-create-a-custom-theme-for-your-adaptive-form}

您可以使用[主題編輯器](/help/forms/using/themes.md)來建立自訂主題。 主題編輯器是功能齊全的WYSIWYG編輯器。 這是一種將CSS套用至最適化表單各種元件的視覺方法。 它提供更細微的控制項，以便設定最適化表單的元件和面板的樣式。

佈景主題是獨立的實體，例如調適型表單。 它包含最適化表單之元件和面板的樣式(CSS)。 樣式包含CSS屬性，例如背景顏色、狀態顏色、透明度、對齊方式和大小。 套用主題時，指定的樣式會套用至最適化表單的對應元件。

在本教學課程中，您可為頁首與頁尾、文字與數值元件、附件元件及按鈕設定樣式。 讓我們從建立佈景主題開始：

### 建立主題 {#create-a-theme}

1. 登入AEM作者執行個體並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 主題]**。 預設URL為[http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes)。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;並選取&#x200B;**[!UICONTROL 主題]**。 [!UICONTROL 建立佈景主題]頁面，其中包含建立佈景主題所需的欄位。 **[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Name]**&#x200B;欄位是必要的：

   * **標題：**&#x200B;指定主題的標題。 例如，**全域主題。**&#x200B;標題可協助您從主題清單中識別主題。
   * **名稱：**&#x200B;指定主題的名稱。 例如，**Global-Theme。**&#x200B;在存放庫中建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議的值。名稱欄位只能包含字母數字字元、連字號和底線。所有無效的輸入都會以連字號取代。

1. 選擇 **[!UICONTROL 建立]**。主題隨即建立，並出現對話方塊以開啟表單進行編輯。 選取&#x200B;**[!UICONTROL 開啟]**&#x200B;以在新索引標籤中開啟新建立的主題。 主題會在主題編輯器中開啟。 對於樣式，主題編輯器使用AEM [!DNL Forms]隨附的現成最適化表單。

   如需有關使用主題編輯器UI的資訊，請參閱[關於主題編輯器](/help/forms/using/themes.md#aboutthethemeeditor)。

1. 選取&#x200B;**[!UICONTROL 主題選項]** ![主題選項](assets/theme-options.png) > **[!UICONTROL 設定]**。 在&#x200B;**[!UICONTROL 預覽表單]**&#x200B;欄位中，選取&#x200B;**shipping-address-add-update-form**&#x200B;最適化表單，選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)，選取&#x200B;**[!UICONTROL 儲存]**。 現在，主題編輯器已設定為使用您自己的最適化表單，而不是預設的最適化表單。 選取&#x200B;**[!UICONTROL 取消]**&#x200B;以返回主題編輯器。

   ![自訂佈景主題](assets/custom-theme.png)

   **圖：** *具有shipping-address-add-update-form最適化表單的主題編輯器*

   ![create-a-theme](assets/create-a-theme.png)

   **圖：** *使用預設表單的最適化表單*

### 樣式頁首與頁尾 {#style-header-and-footer}

頁首和頁尾提供最適化表單的一致且獨特外觀。 一般而言，頁首包含組織的標誌和名稱，頁尾包含版權資訊，而在組織的多個表單中，這些維持相同。 若要設定shipping-address-add-update-form最適化表單頁首與頁尾的樣式：

1. 瀏覽「選取器」面板中的&#x200B;**[!UICONTROL 標題]** > **[!UICONTROL 文字]**&#x200B;選項。 「選取器」面板位於主題編輯器的左側。 如果看不到面板，請選取![切換側面板](assets/toggle-side-panel.png)切換側面板。

1. 在&#x200B;**[!UICONTROL 文字]**&#x200B;摺疊式功能表中設定下列屬性，並選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 字體系列 | Arial® |
   | 字體顏色 | FFFFFF |
   | 字體大小 | 54畫素 |

1. 選取[!UICONTROL 標題] Widget並選取&#x200B;**[!UICONTROL 標題]**。 「頁首」Widget樣式的選項會顯示在左側。 展開&#x200B;**[!UICONTROL 維度與位置]**&#x200B;摺疊式功能表，將&#x200B;**[!UICONTROL 高度]**&#x200B;設定為`120px`，然後選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
1. 展開標頭Widget的&#x200B;**[!UICONTROL 背景]**&#x200B;摺疊式功能表，將&#x200B;**[!UICONTROL 背景色彩]**&#x200B;設定為`F6921E.`

   將游標停留在&#x200B;**[!UICONTROL 影像與漸層]** > **[!UICONTROL +新增]**&#x200B;上，選取&#x200B;**[!UICONTROL 影像]**。 設定下列屬性並選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 影像 | 上傳header-style.png。 在您開始[&#128279;](/help/forms/using/style-your-adaptive-form.md#before-you-start)之前，已在區段中下載影像。 |
   | 位置 | 右下 |
   | 並排顯示 | 不重複 |

1. 在主題編輯器中，選取標頭中的標誌，然後選取&#x200B;**[!UICONTROL 標頭標誌]**。 展開「維度與位置」設定追蹤器，設定下列屬性並選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>邊距</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>上： 1.5rem</li> 
        <li>下：-35px</li> 
        <li>左： 1rem<strong><br /> </strong></li> 
       </ul> <p><strong>秘訣：</strong>選取<img src="assets/link.png">連結圖示，為每個欄位提供不同的值。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高度</td> 
      <td>4.75雷姆</td> 
     </tr> 
    </tbody> 
   </table>

1. 選取頁尾Widget並選取&#x200B;**[!UICONTROL 頁尾]**。 展開&#x200B;**[!UICONTROL 背景]**&#x200B;摺疊式功能表，將&#x200B;**[!UICONTROL 背景色彩]**&#x200B;設定為`F6921E`，然後選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

### 設定資料擷取元件的樣式，並將背景套用至最適化表單 {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

您可以在調適型表單中使用多個元件來擷取資料。 例如，文字方塊和數值方塊。 您可以為所有資料擷取元件提供相同的樣式，或為每個元件提供個別的樣式。 在本教學課程中，相同的樣式會套用至數值方塊（客戶ID、郵遞區號）和文字方塊（客戶ID、名稱、送貨地址、州、電子郵件）。 設定資料擷取元件的樣式：

1. 選取&#x200B;**[!UICONTROL 客戶ID]**&#x200B;欄位並選取&#x200B;**[!UICONTROL 欄位Widget]**&#x200B;選項。 設定下列屬性並選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框顏色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框半徑 </td> 
      <td> 
       <ul> 
        <li>上： 7畫素<br /> </li> 
        <li>右： 7畫素<br /> </li> 
        <li>下： 7畫素<br /> </li> 
        <li>左： 7畫素<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字體系列</td> 
      <td>Arial®</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字體顏色</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字體大小</td> 
      <td>18畫素</td> 
     </tr> 
     <tr> 
      <td>尺寸與位置</td> 
      <td>寬度</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>尺寸與位置</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>左： 10個剩餘</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. 選取&#x200B;**[!UICONTROL 客戶識別碼]**&#x200B;欄位上方的空白區域，並選取&#x200B;**[!UICONTROL 回應式面板容器]**。 將&#x200B;**[!UICONTROL 背景]** > **[!UICONTROL 背景顏色]**&#x200B;設定為F1F2F2。 選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   ![回應式面板容器](do-not-localize/responsive-panel-container.png)

### 設定按鈕的樣式 {#style-the-buttons}

您可以使用自訂佈景主題，將相同的樣式套用至最適化表單的所有按鈕，並使用[內嵌樣式](/help/forms/using/inline-style-adaptive-forms.md)將樣式套用至特定按鈕。 設定按鈕的樣式：

1. 選取&#x200B;**[!UICONTROL Submit]**&#x200B;按鈕並選取&#x200B;**[!UICONTROL Button]**&#x200B;選項。 設定下列屬性並選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色彩</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>邊框<br /> </td> 
      <td>邊框顏色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框半徑 </td> 
      <td> 
       <ul> 
        <li>上： 7畫素<br /> </li> 
        <li>右： 7畫素<br /> </li> 
        <li>下： 7畫素<br /> </li> 
        <li>左： 7畫素</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>文字<br /> </td> 
      <td>字體系列</td> 
      <td>Arial®</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字體顏色</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字體大小</td> 
      <td>18畫素</td> 
     </tr> 
    </tbody> 
   </table>

1. [套用自訂佈景主題](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)，全域佈景主題，至您的最適化表單。 如果樣式沒有反映在自適應表單上，請清除瀏覽器快取並重試。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 步驟4：設定個別元件的樣式 {#step-style-individual-components}

某些樣式僅套用至特定元件。 這些元件會在最適化表單編輯器中設定樣式。

1. 開啟最適化表單進行編輯。 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 在頂端列上，選取&#x200B;**[!UICONTROL 樣式]**&#x200B;選項。

   ![style-option](assets/style-option.png)

1. 選取&#x200B;**[!UICONTROL 附加]**&#x200B;按鈕並選取![aem_6_3_edit](assets/aem_6_3_edit.png)圖示。 在&#x200B;**[!UICONTROL 維度和位置]**&#x200B;摺疊式功能表中設定下列屬性：

   | 屬性 | 值 |
   |---|---|
   | 浮點數 | 左 |
   | 寬度 | 10% |

1. 選取&#x200B;**[!UICONTROL 政府核准的地址校訂]**&#x200B;選項，並選取![aem_6_3_edit](assets/aem_6_3_edit.png)圖示。 設定下列屬性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>浮點數</td> 
      <td>左</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>寬度</td> 
      <td>73%</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>左： 10畫素</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>高度</td> 
      <td>40畫素</td> 
     </tr> 
     <tr> 
      <td>維度和位置<br /> </td> 
      <td>邊距</td> 
      <td><br /> 
       <ul> 
        <li>右：2剩餘</li> 
        <li>左： 10個剩餘 </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色彩</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框寬度</td> 
      <td>1畫素</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框樣式</td> 
      <td>堅固</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框顏色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框半徑</td> 
      <td>7畫素</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字體系列</td> 
      <td>Arial®</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字體顏色</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>字體大小</td> 
      <td>18畫素</td> 
     </tr> 
     <tr> 
      <td>文字</td> 
      <td>行高</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. 選取「**[!UICONTROL 提交]**」按鈕並選取「![aem_6_3_edit](assets/aem_6_3_edit.png)」圖示。 設定下列屬性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>折疊面板</b></td> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>尺寸與位置</td> 
      <td>浮點數</td> 
      <td>右</td> 
     </tr> 
     <tr> 
      <td>尺寸與位置</td> 
      <td>邊距</td> 
      <td> 
       <ul> 
        <li>上：5個剩餘</li> 
        <li>右：14分米</li> 
        <li>下： 20畫素</li> 
        <li>左： 20畫素<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色彩</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>邊框</td> 
      <td>邊框顏色</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## 步驟5：額外區段：在自訂主題中使用Web Fonts {#step-bonus-section-using-web-fonts-in-a-custom-theme}

您可以使用各種字型來設計最適化表單。 所有在其中檢視最適化表單的裝置可能沒有用來設計最適化表單的字型。 您可以使用Web字型服務，將所需的字型傳送至目標裝置。

[!DNL Adobe Fonts]是Web Fonts服務。 您可以透過最適化表單來設定和使用服務。 若要在最適化表單中使用[!DNL Adobe Fonts]：
1. 瀏覽Adobe字型的[資料庫](https://fonts.adobe.com/)，並選擇字型來設定表單的樣式。
<!--
>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] is now called Adobe Fonts and is included with Creative Cloud and other subscriptions. [Learn more](https://fonts.adobe.com/).-->

>[!NOTE]
>
> 您可以新增標籤或篩選器來調整字型清單。

1. 按一下&lt;/>按鈕，將系列新增至Web專案，以備您找到想要的字型時使用。

   ![select-font-from-font-library](assets/select-font-from-font-library.png)

   新增字型至Web專案對話方塊畫面隨即顯示。

   >[!NOTE]
   >
   > 只有在Web專案有&lt;/>按鈕可用時，您才能新增字型。

2. 為您的Web專案命名。
3. 選取核取方塊以選取要包含的字型粗細和樣式。

   ![新增字型庫](assets/add-a-font-window.png)

4. 選取&#x200B;**按一下**&#x200B;以建立專案。
5. 從畫面複製內嵌程式碼和URL。
   ![內嵌程式碼和URL](assets/font-add-url.png)

6. 按一下&#x200B;**完成**&#x200B;以關閉Web專案視窗。
7. 登入您的AEM執行個體並移至URL `http://server:port/crx/de/index.jsp#`
8. 在CRXDE中建立資料夾結構，例如`/apps/[fontslibrary]/[customlibrary(clientlibrary)]`。
9. 移至新建立的`clientlibs`資料夾並新增`allowProxy`和`categories`屬性。
10. 瀏覽至`/apps/[fontslibrary]/[customlibrary(clientlibrary)]`並建立css資料夾。
11. 移至已建立的CSS資料夾並建立檔案。 例如，將檔案建立為`fonts.css`並貼上內嵌程式碼以及URL。
    ![資料夾結構](/help/forms/using/assets/fonts-add-in-crxde.png)
12. 儲存變更。

>[!NOTE]
>
> 若要在最適化表單中使用新增的自訂字型，請確定&#x200B;**[!UICONTROL 使用者端資料庫類別]**&#x200B;中的使用者端資料庫名稱與clientlib資料夾的「類別」選項中指定的名稱一致。

最適化表單現在可透過下列自訂字型使用者端資料庫存取包含的字型。


<!--
Create Adobe Fonts Configuration

1. To create a API Token, go to **login** > **API Token** > **Make me a new API token**.

   ![API token](/help/forms/using/assets/fonts-api-token.png)

2. Once, you click **Make me a new API token**, a new token is generated. 
3. Copy the generated token for future use.
4. Now login to your AEM  author instance. On the author instance, go to **[!UICONTROL Tools]**>**[!UICONTROL Cloud Services]**> **[!UICONTROL Adobe Fonts]**.
5. Select the configuration container and click **Create**. **[UICONTROL Create Adobe Fonts Configuration]** screen appears.
    ![API token](/help/forms/using/adobe-font-configuration-screen.png)

6. Spceify the name and paste the API token in the **[!UICONTROL Kit ID]** textbox.
7. Click **Create**.



The fonts added to the **[!UICONTROL Adobe Fonts]** are available for selection in the **[!UICONTROL Text]** accordion of all the components.
1. In the theme editor, navigate to **[!UICONTROL Theme Options]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Configure]**. 
2. In the **[!UICONTROL Adobe Fonts Configuration]** field, select the kit, and click **[!UICONTROL Save]**.


1. Create an [Adobe Fonts](https://fonts.adobe.com/?ref=tk.com) account, create a kit, add font Myriad Pro to the kit, publish the kit, and obtain the Kit ID. It is required to use [!DNL Adobe Fonts] (Web Fonts) in an adaptive form. 
1. In the AEM [!DNL Forms] Server, navigate to ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. Now, open a configuration folder. If a configuration is already available, click the **[!UICONTROL Create]** button to create an instance.

   On the Create Configuration dialog, specify a **Title** for the configuration, and click **[!UICONTROL Create]**. You are redirected to the configuration page. In the [!UICONTROL Edit Component] dialog that appears, provide your **Kit ID** and click **[!UICONTROL OK]**. -->
