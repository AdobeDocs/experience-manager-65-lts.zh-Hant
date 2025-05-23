---
title: 建立無障礙的最適化表單
description: AEM Forms為您提供工具，以及建立無障礙的最適化表格，並協助您遵循無障礙標準。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 8a0b276a-6020-4f48-95ab-4e7270e42e44
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2099'
ht-degree: 2%

---

# 建立無障礙的最適化表單{#creating-accessible-adaptive-forms}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/introduction)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文介紹使用基礎元件製作最適化Forms的舊方法。</span>

## 簡介 {#introduction}

可存取的表單是所有人都能使用的表單，包括有特殊需求的使用者。 最適化Forms包含多項功能，可提升不同功能使用者的可用性。 在最適化表單中建立協助工具，不僅可讓內容有儘可能廣泛的閱聽眾，而且在必須遵循協助工具標準的地理位置提供檔案時，這也是必要條件。 AEM Forms可協助表單開發人員遵守協助工具標準。

製作最適化表單時，作者應考量下列幾點，以建立無障礙的最適化表單：

* 使用協助工具名稱和說明檢查器(ANDI)協助工具測試工具檢查表單
* 為表單控制項提供適當的標籤
* 提供影像的對等文字
* 提供足夠的色彩對比
* 確保可使用鍵盤存取表單控制項

## 必備條件

您需要協助工具工具，例如&#x200B;**可存取的名稱和說明檢測器(ANDI)**，以及為解決協助工具相關問題而開發的&#x200B;**最適化表單主題**，以建立可存取的最適化表單。

### 下載並安裝協助工具測試工具

「可存取的名稱和說明檢測器」(ANDI)工具可協助您識別和修正網頁內容中與可存取性相容相關的問題。 這是國土安全部的Trusted Tester v5指引下建議的工具。 它是由美國社會安全管理&#x200B;部所開發，用於檢查網頁內容的Section 508合規性。 工具：

* 協助偵測網頁&#x200B;上的協助工具問題
* 提供改善協助工具的建議&#x200B;。
* 偵測鍵盤協助工具及色彩對比問題
* 清楚識別符合標準的熒幕助讀程式內容

ANDI可與所有主要的網際網路瀏覽器搭配使用。 請參閱[ANDI檔案](https://www.ssa.gov/accessibility/andi/help/install.html)，以取得如何設定及使用此工具的詳細指示。

### 下載並安裝Ultraminary-Access主題

Ultraminary-Accessible主題是參考主題。 它有助於示範如何以最適化表單修正色彩對比和其他協助工具相關問題。 Adobe建議您根據組織核准的樣式來建立生產環境的自訂主題。 執行以下步驟，將主題上傳至您的AEM執行個體：

1. 下載主題套件。
1. 在您的AEM執行個體上導覽至&#x200B;**[!UICONTROL Experience Manager]** > **[!UICONTROL 導覽]** ![導覽](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Forms]**。
1. 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**。 選取並上傳x Ultramarine-Accessible-Theme.zip檔案。 它會上傳主題至您的AEM執行個體。

## 讓最適化表單可供存取

您應該關注四個關鍵方面：鍵盤導覽、色彩對比、有意義的影像替代文字，以及讓可存取調適型表單的表單控制項適用標籤。 執行以下步驟，讓您存取現有的最適化表單：

### 1.套用無障礙佈景主題並執行其他修正

將Ultraminary-Accessible主題套用至您現有的最適化表單。 若要套用主題：

1. 開啟最適化表單進行編輯。
1. 選取元件並選取父項圖示。 在內容功能表中，選取&#x200B;**[!UICONTROL 最適化表單容器]**，然後選取[設定]圖示。
1. 在屬性瀏覽器中選取Ultraminary-Accessible主題，然後選取&#x200B;**[!UICONTROL 儲存]**&#x200B;圖示。
1. 重新整理瀏覽器視窗。 主題會套用至最適化表單。

套用無障礙主題後，請執行以下列出的其他修正。 除了協助工具主題中涵蓋的協助工具修正之外，這些修正也包括：

1. 在最適化表單中為標誌影像新增有意義的替代文字。

   為最適化表單範本的頁首和頁尾元件中的影像提供有意義的替代文字。 當您修正範本並使用它建立調適型表單時，調適型表單會繼承套用至範本頁首和頁尾的所有協助工具相關修正。  若為現有的最適化表單，請在最適化表單層級進行變更。 對最適化表單範本進行的變更不會自動流入現有的最適化表單。

1. 將包含表單名稱的標題元件新增到最適化表單。 如果您的表單設計指定了公司名稱，請為公司名稱另外新增一個標題元件。

   大部分的協助工具都會通知使用者內容的階層，協助他們瞭解網頁的結構。 在最適化表單上，為組織名稱和表單名稱文字設定不同的標題層級，為這些文字提供階層結構。 此外，請在每個面板和區段之前使用文字元件（具有適當的標題層級）來建立階層。

   ![如何套用標頭樣式](assets/apply-style.gif)

1. 變更頁尾背景顏色，以根據協助工具標準使用適當的對比，以改善文字的可見度和可讀性。 您可以使用ANDI來尋找表單中的色彩對比問題。 此外，請勿使用非常小的字型。 小型字型很難閱讀。

1. 以選擇（選項式）元件取代現有最適化表單中的切換器和影像選擇元件。

1. 以數值方塊元件取代現有最適化表單中的數值步進器元件。

1. 以日期選擇器欄位取代日期輸入欄位。

1. 設定日期選擇器元件的顯示、驗證及編輯模式。 此外，設定自訂驗證錯誤訊息。 例如，您指定的日期無效。 正確的日期格式為YYYY-MM-DD。

1. 設定日期選擇器元件的自訂協助工具文字。 例如，輸入您的出生日期。 熒幕助讀程式會朗讀這些自訂協助工具文字。

1. 針對最適化表單元件，請使用簡短說明，而非詳細說明。 冗長的說明會新增說明按鈕。 請確定最適化沒有任何說明按鈕。

1. 新增自訂協助工具文字至表格的所有唯讀儲存格。 此外，也會停用表格的所有唯讀儲存格。

1. 移除最適化表單中的手寫簽名欄位（如果有的話）。 設定最適化表單以使用Adobe Sign，提供順暢的數位簽名體驗。

### 2.為表單控制項提供適當的標籤 {#provide-proper-labels-for-form-controls}

元件的標籤或標題可識別表單元件代表的意義。 例如，「名字」文字會告訴使用者他們必須在文字欄位中輸入名字。 為了方便熒幕閱讀程式存取，標籤會以程式設計方式與表單元件相關聯。 或者，表單控制項會設定其他協助工具資訊。

熒幕助讀程式感知到的標籤不需要與視覺註解相同。 在某些情況下，您可能會想要更明確說明控制項的用途。 對於表單中的每個欄位物件，協助工具選項可用於指定熒幕助讀程式為識別特定表單欄位所朗讀的內容。

若要使用「協助工具」選項，請遵循下列步驟：

1. 選取元件並選取![cmppr](assets/cmppr.png)。
1. 按一下側邊欄中的&#x200B;**[!UICONTROL 協助工具]**，選擇所需的協助工具選項。

### 表單元件中的協助工具選項 {#accessibility-options-in-form-components}

![表單元件中的協助工具選項](assets/accessibility-options.png)

**自訂文字**&#x200B;表單作者在協助工具選項[自訂文字]欄位中提供內容。 熒幕助讀程式等輔助技術會使用此自訂文字。 在大部分的案例中，使用「標題」設定是最佳選項。 只有在無法使用標題或簡短說明時，才考慮建立自訂畫面Reader文字。

**簡短描述**&#x200B;對於大多數元件，當使用者將指標暫留在元件上時，簡短描述會在執行階段顯示。 您可以在說明內容選項下方的簡短說明欄位中設定此選項。

**標題**&#x200B;使用此選項可讓AEM Forms使用與表單欄位相關聯的視覺標籤做為熒幕助讀程式文字。

**名稱**&#x200B;您可以在[繫結]索引標籤的[名稱]欄位中指定值。 名稱不能包含任何空格。

**無**&#x200B;選取「無」會導致表單物件在已發佈的表單中沒有名稱。 不建議對表單控制項使用「無」設定。

>[!NOTE]
>
>* Radio Button和Check-box只能有兩個協助工具選項，即Custom Text和Title。
>* 對於XFA型調適型表單，協助工具選項繼承自XDP中設定的協助工具選項。 XDP的工具提示會對應至簡短說明，而標題會對應至標題。 其他選項則可正常運作。

### 3.提供影像的等效文字 {#provide-text-equivalents-for-images}

影像有助於改善部分使用者的理解。 不過，對於使用熒幕助讀程式的使用者，影像會降低表單的協助工具。 如果您選擇使用影像，請為所有影像提供文字說明。

確定文字在表單中說明了物件及其用途。 熒幕助讀程式會在遇到影像時讀取此替代文字。 影像必須一律指定替代文字。

選取影像元件並選取![cmppr](assets/cmppr.png)。 在側邊欄中的「屬性」下方，指定影像的替代文字。

![影像的替代文字](assets/image-properties.png)

### 4.提供足夠的色彩對比 {#provide-sufficient-color-contrast}

協助工具設計涉及考慮色彩使用的其他准則。 表單作者可以使用顏色來改善表單的外觀，方法是反白顯示各種表單元件。 不過，若色彩使用不當，可能會使有不同能力的人難以或無法閱讀表格。

有視覺障礙的使用者需仰賴文字與背景的高對比才能閱讀數位內容。 如果沒有足夠的對比，某些使用者可能很難閱讀表單，甚至無法閱讀表單。

建議您使用預設字型和背景顏色 — 白色背景上的黑色內容。 如果您變更預設顏色，請在淺色背景顏色上選擇深色前景顏色，或反之。

請參閱[建立最適化表單的自訂主題](/help/forms/using/creating-custom-adaptive-form-themes.md)，以取得變更最適化表單色彩對比和主題的詳細資訊。

### 5.確認可使用鍵盤存取表單控制項 {#ensure-that-form-controls-are-keyboard-accessible}

可存取的表單僅能使用鍵盤或同等輸入裝置填入。 行動力下降或視力障礙的使用者可能別無選擇，只能使用鍵盤，而許多使用滑鼠的使用者則偏好使用鍵盤輸入。 透過允許各種輸入方法，您不僅可建立無障礙的表單，還可建立更適合所有使用者偏好設定的表單。

AEM Forms提供下列鍵盤快速鍵。

| 動作 | 鍵盤快速鍵 |
|---|---|
| 在表單中向前移動游標 | 定位符號 |
| 在表單中向後移動游標 | Shift+Tab鍵 |
| 移至下一個面板 | Alt+向右鍵 |
| 移至上一個面板 | Alt+向左鍵 |
| 重設表單中的填入資料 | Alt+R |
| 提交表單 | Alt+S |

此外，自適應Forms中的&#x200B;**[!UICONTROL 日期選擇器]**&#x200B;元件有各種可用的鍵盤快速鍵。 若要啟用快速鍵，請選取&#x200B;**[!UICONTROL 日期選擇器]**&#x200B;元件，然後選取![設定](assets/configure-icon.svg)以開啟屬性。 在&#x200B;**[!UICONTROL 模式]**&#x200B;區段中，使用&#x200B;**[!UICONTROL 型別]**&#x200B;和&#x200B;**[!UICONTROL 模式]**&#x200B;下拉式清單來選取顯示模式。 儲存屬性以啟用&#x200B;**[!UICONTROL 日期選擇器]**&#x200B;元件的快速鍵。

下列鍵盤快速鍵適用於Adaptive Forms中的日期選擇器元件：

| 動作 | 鍵盤快速鍵 |
|---|---|
| <ul><li>當索引標籤焦點反白標示行事曆圖示時，顯示日期選擇器元件選項</li><li>當索引標籤焦點反白某個選項時，執行點按事件</li> | 空格或Enter |
| 隱藏日期選擇器元件選項 | Esc 鍵 |
| <ul><li>在日期選擇器元件中可用的選項間向前移動游標。</li><li>當日期輸入欄位作用中時，將索引標籤焦點設定在行事曆圖示上</li> | 定位符號 |
| 在日期選擇器元件中可用的選項間向後移動游標 | Shift+Tab鍵 |
| <ul><li>當索引標籤焦點反白顯示日期輸入欄位時，顯示日期選擇器元件選項</li><li>在日期選擇器元件中可用的行事曆中，將游標向下移動</li> | 向下鍵 |
| 在日期選擇器元件中可用的行事曆中，將游標向上移動 | 向上鍵 |
| 在日期選擇器元件中可用的行事曆中，將游標向後移動 | 向左鍵 |
| 在日期選擇器元件中可用的行事曆中向前移動游標 | 向右鍵 |
| 針對行事曆中左右導覽箭頭之間可用的標題執行動作 | Shift +向上鍵 |
| 針對行事曆中可用的右導覽箭頭圖示![右箭頭](assets/right-navigation-icon.svg)執行動作 | Shift +向左鍵 |
| 執行行事曆中可用的向左導覽箭頭圖示![向左箭頭](assets/left-navigation-icon.svg)的動作 | Shift +向右鍵 |

## 使用協助工具來尋找剩餘的協助工具問題

可存取的名稱和說明檢查器(ANDI)可協助您在最適化表單中識別及修正可存取性法規遵循相關問題。 使用ANDI工具尋找最適化表單中的協助工具問題：

1. 在預覽模式中開啟最適化表單。
1. 按一下已建立書籤的ANDI工具圖示。 ANDI工具會分析最適化表單並顯示協助工具的問題。 如需有關如何使用工具的詳細資訊，請參閱[ANDI的檔案](https://www.ssa.gov/accessibility/andi/help/howtouse.html)。
1. 檢閱並修正ANDI回報的問題。
