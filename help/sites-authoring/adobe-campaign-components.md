---
title: 與Adobe Campaign元件整合
description: 與Adobe Campaign整合時，您擁有可在使用電子報和表單時使用的元件。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
exl-id: 20de763d-dd07-4ba6-a54d-a2b3b9b7e1ec
index: false
source-git-commit: 2edf37c2d6bb04b418618f2780f773ab37559114
workflow-type: tm+mt
source-wordcount: '2857'
ht-degree: 6%

---


# Adobe Campaign元件{#adobe-campaign-components}

與Adobe Campaign整合時，您擁有可在使用電子報和表單時使用的元件。 本檔案將說明這兩者。

>[!CAUTION]
>
>AEM電子郵件元件已淘汰。 由於電子郵件結合了內容和樣式，因此由AEM提供的現成可用電子郵件元件對於客戶的重複使用有限，因為需要將自訂樣式實作到專案所需的任何元件中。
>
>電子郵件元件可在專案層級實作，而過時的AEM電子郵件元件會說明如何實作。 不過，請勿在專案上使用這些已棄用的元件。

## Adobe Campaign Newsletter元件 {#adobe-campaign-newsletter-components}

所有Campaign元件都遵循[電子郵件範本最佳實務](/help/sites-administering/best-practices-for-email-templates.md)中概述的最佳實務，且以Adobe標籤語言[HTL](https://helpx.adobe.com/tw/experience-manager/htl/using/overview.html)為基礎。

當您開啟已設定為要與Adobe Campaign整合的新聞稿/電子郵件時，您應該會在&#x200B;**Adobe Campaign新聞稿**&#x200B;區段中看到下列元件：

* 標題 (行銷活動)
* 影像 (行銷活動)
* 連結 (行銷活動)
* Scene7 影像範本 (行銷活動)
* 目標參考 (行銷活動)
* 文字與影像 (行銷活動)
* 文字與個人化 (行銷活動)

下一節將說明這些元件。

元件顯示如下：

![chlimage_1-43](assets/chlimage_1-43.png)

### 標題 (行銷活動) {#heading-campaign}

標題元件可以：

* 將&#x200B;**標題**&#x200B;欄位保留空白以顯示目前頁面的名稱。
* 顯示您在&#x200B;**標題**&#x200B;欄位中指定的文字。

您直接編輯&#x200B;**標題（行銷活動）**&#x200B;元件。 留空將使用頁面標題。

![chlimage_1-44](assets/chlimage_1-44.png)

您可以設定下列專案：

* **標題**
如果您想使用頁面標題以外的名稱，請在此處輸入它。

* **標題層級(1， 2， 3， 4)**
根據HTML標題大小的標題層級1-4。

下列範例顯示正在顯示的標題（行銷活動）元件。

![chlimage_1-45](assets/chlimage_1-45.png)

### 影像 (行銷活動) {#image-campaign}

影像（行銷活動）元件會根據指定的引數顯示影像和隨附文字。

您可以上傳影像，然後編輯和處理影像（例如，裁切、旋轉、新增連結/標題/文字）。

您可以從[資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assetsbrowsertouchoptimizedui)將影像直接拖放到元件或其[設定對話方塊](/help/sites-authoring/editing-content.md#editconfigurecopycutdeletepastetouchoptimizedui)上。 您也可以從「設定」對話方塊上傳影像；此對話方塊也會控制影像的所有定義與操作：

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>在&#x200B;**替代文字**&#x200B;欄位中輸入資訊，否則無法儲存影像。

上傳影像後（而非之前），您可以視需要使用[就地編輯](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui)來裁切/旋轉影像：

![就地編輯工具列](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>就地編輯器在編輯時會使用影像的原始大小和外觀比例。 您也可以指定高度和寬度屬性。 儲存編輯變更時，會套用屬性中定義的任何大小和外觀比例限制。
>
>視您的執行個體而定，頁面[的](/help/sites-developing/designer.md)設計可能也會施加最小和最大限制；這些限制是在專案實作期間開發的。

全熒幕編輯模式中有數個其他選項可供使用；例如，地圖和縮放：

![全熒幕編輯模式](do-not-localize/chlimage_1-11.png)

載入影像時，您可以設定下列專案：

* **地圖**
若要對應影像，請選取「對應」。 您可以指定建立影像地圖（矩形、多邊形等）的方式以及區域應指向的位置。

* **裁切**
選取「裁切」以裁切影像。 使用滑鼠裁切影像。

* **旋轉**
若要旋轉影像，請選取「旋轉」。 重複使用，直到影像以您想要的方式旋轉。

* **清除**
移除目前的影像。

* 縮放列（僅傳統）
若要放大和縮小影像，請使用影像下方的滑動列（在「確定」和「取消」按鈕上方）
* **標題**
影像的標題。

* **替代文字**
建立無障礙內容時使用的替代文字。

* **連結至**
建立資產或網站內其他頁面的連結。

* **描述**
影像的說明。

* **大小**
設定影像的高度和寬度。

>[!NOTE]
>
>在&#x200B;**進階**&#x200B;索引標籤的&#x200B;**替代文字**&#x200B;欄位中輸入資訊，否則影像無法儲存，您會看到下列錯誤訊息：
>
>`Validation failed. Verify the values of the marked fields.`
>

下列範例顯示正在顯示的影像（行銷活動）元件。

![chlimage_1-47](assets/chlimage_1-47.png)

### 連結 (行銷活動) {#link-campaign}

連結（行銷活動）元件可讓您將連結新增至電子報。

您可以在&#x200B;**顯示**、**URL資訊**&#x200B;或&#x200B;**進階**&#x200B;索引標籤中設定下列專案：

* **連結標題**
連結的標題。 這是使用者看到的文字。

* **連結工具提示**
新增如何使用連結的其他資訊。

* **LinkType**
在下拉式清單中，選取&#x200B;**自訂URL**&#x200B;和&#x200B;**最適化檔案**。 此為必填欄位。 如果您選取「自訂URL」，可提供連結URL。 如果您選取「最適化檔案」，則可以提供檔案路徑。

* **其他URL引數**
新增任何其他URL引數。 按一下「新增專案」以新增多個專案。

>[!NOTE]
>
>在&#x200B;**URL資訊**&#x200B;索引標籤的&#x200B;**連結型別**&#x200B;欄位中輸入資訊，或元件無法儲存且您看到下列錯誤訊息：
>
>`Validation failed. Verify the values of the marked fields.`
>

下列範例顯示正在顯示的連結（行銷活動）元件。

![chlimage_1-48](assets/chlimage_1-48.png)

### Dynamic Media Classic (Scene7)影像範本（行銷活動） {#scene-image-template-campaign}

Dynamic Media Classic (Scene7)影像範本為圖層式影像檔案，其中的內容和屬性可以引數化為變動。 **[!UICONTROL 影像範本]**&#x200B;元件可讓您在電子報中使用Scene7範本，並變更範本引數的值。 此外，您可以在引數內使用Adobe Campaign中繼資料變數，讓每位使用者都能個人化地體驗影像。

![chlimage_1-49](assets/chlimage_1-49.png)

按一下&#x200B;**編輯**&#x200B;以設定元件。 您可以設定本節中所述的設定。 此Scene7影像範本在[Scene7影像範本元件](/help/assets/scene7.md#image-template)中有詳細說明。

此外，「引數」面板會列出已在Scene7中為範本定義的所有範本引數。 您可以針對這些引數調整值、插入變數或重設為預設值。

![chlimage_1-50](assets/chlimage_1-50.png)

### 目標參考 (行銷活動) {#targeted-reference-campaign}

目標參照（行銷活動）元件可讓您建立目標段落的參照。

在此元件中，您會導覽至目標段落以選取它。

按一下資料夾圖示以導覽至您要參考的段落。 完成後，按一下核取記號。

### 文字與影像 (行銷活動) {#text-image-campaign}

文字與影像（行銷活動）元件新增文字區塊和影像。

按一下以設定元件時，選取「文字」或「影像」。

![chlimage_1-51](assets/chlimage_1-51.png)

選取&#x200B;**文字**&#x200B;會顯示內嵌編輯器：

![文字工具列](do-not-localize/chlimage_1-12.png)

選取&#x200B;**影像**&#x200B;會顯示影像的就地編輯器：

![影像工具列](do-not-localize/chlimage_1-13.png)

如需使用影像的詳細資訊，請參閱[影像（行銷活動）元件](#image-campaign)。 如需使用文字的詳細資訊，請參閱[文字與Personalization （行銷活動）元件](#text-personalization-campaign)。

和文字與Personalization （行銷活動）及影像（行銷活動）元件一樣，您可以設定：

* **文字**
輸入文字。 使用工具列來修改格式、建立清單及新增連結。

* **影像**
從內容尋找器拖曳影像，或按一下以瀏覽影像。 視需要裁切或旋轉。

* **影像屬性** （**進階影像屬性**）
可讓您指定下列專案：

   * **標題**
區塊標題，由mouseover顯示。

   * **替代文字**
如果影像無法顯示，則會顯示替代文字。

   * **連結至**
建立資產或網站內其他頁面的連結。

   * **描述**
影像的說明。

   * **大小**
設定影像的高度和寬度。

>[!NOTE]
>
>需要&#x200B;**進階**&#x200B;索引標籤中的&#x200B;**替代文字**&#x200B;欄位，否則元件無法儲存，且您會看到下列錯誤訊息：
>
>`Validation failed. Verify the values of the marked fields.`
>

下列範例顯示正在顯示的文字與影像（行銷活動）元件。

![chlimage_1-52](assets/chlimage_1-52.png)

### 文字與個人化 (行銷活動) {#text-personalization-campaign}

文字與Personalization （行銷活動）元件可讓您使用WYSIWYG編輯器及[RTF編輯器](/help/sites-authoring/rich-text-editor.md)所提供的功能，輸入文字區塊。 此外，此元件可讓您使用Adobe Campaign中可用的內容欄位和個人化區塊；另請參閱[插入Personalization](/help/sites-authoring/campaign.md#inserting-personalization)。

選取圖示可讓您設定文字的格式，包括字型特性、對齊、連結、清單和縮排。 在[兩個UI](/help/sites-authoring/editing-content.md)中，功能基本相同，但外觀和感覺不同：

![chlimage_1-53](assets/chlimage_1-53.png)

在就地編輯器中，您可以新增文字、變更對齊、新增和移除連結、新增內容欄位或個人化區塊，以及進入全熒幕模式。 新增完文字/個人化後，請選取核取記號以儲存變更（或x以取消）。 如需詳細資訊，請參閱[就地編輯](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui)。

>[!NOTE]
>
>* 可用的個人化欄位取決於您電子報所連結的Adobe Campaign範本。
>* 從ContextHub選取角色後，個人化欄位會自動取代為所選設定檔的資料。
>
>請參閱[插入Personalization](/help/sites-authoring/campaign.md#inserting-personalization)。

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>只考慮&#x200B;**nms:seedMember**&#x200B;結構描述或其其中一個擴充功能中定義的欄位。 連結至&#x200B;**nms:seedMember**&#x200B;的資料表的屬性無法使用。

## Adobe Campaign表單元件 {#adobe-campaign-form-components}

您可以使用Adobe Campaign元件建立使用者填寫的表單，以訂閱電子報、取消訂閱電子報或更新其使用者設定檔。 如需詳細資訊，請參閱[建立Adobe Campaign Forms](/help/sites-authoring/adobe-campaign-forms.md)。

每個元件欄位都可以連結至Adobe Campaign資料庫欄位。 可用的欄位會依其包含的資料型別而有所不同，如區段[元件和資料型別](#components-and-data-type)所述。 如果您在Adobe Campaign中擴充收件者綱要，則資料型別相符的元件中將可使用新欄位。

當您開啟設定為要與Adobe Campaign整合的表單時，您會在&#x200B;**Adobe Campaign**&#x200B;區段中看到下列元件：

* 核取方塊 (行銷活動)
* 日期欄位（行銷活動）和日期欄位/HTML5 （行銷活動）
* 加密的主要金鑰 (行銷活動)
* 錯誤顯示 (行銷活動)
* 隱藏調和索引鍵 (行銷活動)
* 數值欄位 (行銷活動)
* 選項欄位 (行銷活動)
* 訂閱檢查清單 (行銷活動)
* 測試欄位 (行銷活動)

元件顯示如下：

![chlimage_1-55](assets/chlimage_1-55.png)

本節詳細說明每個元件。

### 元件和資料型別 {#components-and-data-type}

下表說明可顯示和修改Adobe Campaign設定檔資料的元件。 每個元件都可以對應至Adobe Campaign設定檔欄位，以顯示其值，並在提交表單時更新欄位。 不同的元件只能與適當資料型別的欄位相符。

<table>
 <tbody>
  <tr>
   <td><p><strong>元件</strong></p> </td>
   <td><p><strong>Adobe Campaign欄位的資料型別</strong></p> </td>
   <td><p><strong>範例欄位</strong></p> </td>
  </tr>
  <tr>
   <td><p>核取方塊 (行銷活動)</p> </td>
   <td><p>布林值</p> </td>
   <td><p>不再聯絡（透過任何管道）</p> </td>
  </tr>
  <tr>
   <td><p>日期欄位 (行銷活動)</p> <p>日期欄位/HTML 5 (行銷活動)</p> </td>
   <td><p>日期</p> </td>
   <td><p>出生日期</p> </td>
  </tr>
  <tr>
   <td><p>數值欄位 (行銷活動)</p> </td>
   <td><p>數值（位元組、短、長、雙）</p> </td>
   <td><p>年齡</p> </td>
  </tr>
  <tr>
   <td><p>選項欄位 (行銷活動)</p> </td>
   <td><p>具有關聯值的位元組</p> </td>
   <td><p>性別</p> </td>
  </tr>
  <tr>
   <td><p>測試欄位 (行銷活動)</p> </td>
   <td><p>字串</p> </td>
   <td><p>電子郵件</p> </td>
  </tr>
 </tbody>
</table>

### 大部分元件通用的設定 {#settings-common-to-most-components}

Adobe Campaign元件具有所有元件中通用的設定（加密的主要金鑰和隱藏的調解金鑰元件除外）。

在大多數元件中，您可以設定下列專案：

#### 標題和文字 {#title-and-text}

![chlimage_1-56](assets/chlimage_1-56.png)

* **標題**
如果您想使用元素名稱以外的名稱，請在此處輸入它。

* **隱藏標題**
如果您不想看到標題，請選取此核取方塊。

* **描述**
將說明新增至欄位，為使用者提供詳細資訊。

* **僅顯示值**
只顯示值（如果有）

#### Adobe Campaign {#adobe-campaign}

您可以設定下列專案：

* **對應**
選取Adobe Campaign個人化欄位（如適用）。

* **調解金鑰**
如果此欄位屬於調解金鑰，請選取此核取方塊。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 限制 {#constraints}

* **必要**&#x200B;選取此核取方塊即可讓此元件為必要；也就是說，使用者必須輸入值。
* **必要訊息**&#x200B;選擇性地新增訊息，說明欄位為必要欄位。

![chlimage_1-58](assets/chlimage_1-58.png)

#### 樣式 {#styling}

* **CSS**
輸入您要用於此元件的CSS類別。

![chlimage_1-59](assets/chlimage_1-59.png)

### 核取方塊 (行銷活動) {#checkbox-campaign}

核取方塊（行銷活動）元件可讓使用者修改布林資料型別的Adobe Campaign設定檔欄位。 例如，您可以有核取方塊（行銷活動）元件，讓收件者指定不想透過任何頻道聯絡他/她。

您可以[在核取方塊（行銷活動）元件中設定大部分Adobe Campaign元件通用的設定](#settings-common-to-most-components)。

下列範例顯示所顯示的Checkbox (Campaign)元件。

![chlimage_1-60](assets/chlimage_1-60.png)

### 日期欄位（行銷活動）和日期欄位/HTML 5 （行銷活動） {#date-field-campaign-and-date-field-html-campaign}

使用日期欄位可允許收件者指定日期；例如，您可能希望收件者指定其出生日期。 日期格式符合您在Adobe Campaign執行個體中使用的格式。

除了大部分Adobe Campaign元件通用的[設定](#settings-common-to-most-components)之外，您還可以設定下列專案：

* **限制 — 限制**&#x200B;下拉式清單
您可以選取 — **無**&#x200B;或&#x200B;**日期 —**&#x200B;來新增日期限制或無限制。 如果您選取日期，使用者在欄位中輸入的答案必須為日期格式。

* **限制訊息**&#x200B;此外，您可以新增限制訊息，讓使用者知道如何正確格式化他們的回答。
* **樣式 — 寬度**&#x200B;按一下或點選&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;圖示或輸入數字，以調整欄位的寬度。

下列範例顯示已調整寬度的日期欄位（行銷活動）元件。

![chlimage_1-61](assets/chlimage_1-61.png)

### 加密的主要金鑰 (行銷活動) {#encrypted-primary-key-campaign}

此元件定義將包含Adobe Campaign設定檔識別碼的URL引數名稱(分別為&#x200B;**主要資源識別碼**&#x200B;或Adobe Campaign Standard中的&#x200B;**加密主金鑰**&#x200B;和6.1)。

顯示和修改Adobe Campaign設定檔資料&#x200B;**的每個表單都必須**&#x200B;包含加密的主要金鑰元件。

您可以在加密的主要金鑰（行銷活動）元件中設定下列專案：

* **標題與文字 — 元素名稱**&#x200B;預設為encryptedPK。 當元素名稱與表單上其他元素的名稱衝突時，您只需要變更元素名稱。 沒有兩個表單欄位可以有相同的元素名稱。
* **Adobe Campaign - URL引數**&#x200B;新增EPK的URL引數。 例如，您可以使用值&#x200B;**epk**。

下列範例顯示正在顯示的加密主要金鑰（行銷活動）元件。

![chlimage_1-62](assets/chlimage_1-62.png)

### 錯誤顯示 (行銷活動) {#error-display-campaign}

此元件可讓您顯示後端錯誤。 需要將表單的錯誤處理設定為「前進」，元件才能正常運作。

下列範例顯示正在顯示的錯誤顯示（行銷活動）元件。

![chlimage_1-63](assets/chlimage_1-63.png)

### 隱藏調和索引鍵 (行銷活動) {#hidden-reconciliation-key-campaign}

「隱藏調解金鑰（行銷活動）」元件可讓您新增隱藏欄位，作為調解金鑰的一部分，以至表單。

您可以在隱藏調解金鑰（行銷活動）元件中設定下列專案：

* **標題與文字 — 元素名稱**&#x200B;預設為reconcilKey。 當元素名稱與表單上其他元素的名稱衝突時，您只需要變更元素名稱。 沒有兩個表單欄位可以有相同的元素名稱。
* **Adobe Campaign — 將**&#x200B;對應到Adobe Campaign個人化欄位。

下列範例顯示正在顯示的隱藏調解金鑰（行銷活動）元件。

![chlimage_1-64](assets/chlimage_1-64.png)

### 數值欄位 (行銷活動) {#numeric-field-campaign}

使用數值欄位可允許收件者輸入數字，例如年齡。

除了大部分Adobe Campaign元件通用的[設定](#settings-common-to-most-components)之外，您還可以設定下列專案：

* **限制 — 限制**&#x200B;下拉式清單
您可以選取 — **無**&#x200B;或&#x200B;**數值 —**&#x200B;來新增數值或無限制的限制。 如果您選取數字，使用者在欄位中輸入的答案必須是數字。

* **限制訊息**&#x200B;此外，您可以新增限制訊息，讓使用者知道如何正確格式化他們的回答。
* **樣式 — 寬度**&#x200B;按一下或點選&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;圖示或輸入數字，以調整欄位的寬度。

下列範例顯示已設定寬度的數值欄位（行銷活動）元件。

![chlimage_1-65](assets/chlimage_1-65.png)

### 選項欄位 (行銷活動) {#option-field-campaign}

此下拉式清單可讓您選取選項；例如，收件者的性別或狀態。

您可以在「選項欄位」 （行銷活動）元件中[設定大部分Adobe Campaign元件通用的設定](#settings-common-to-most-components)。 若要填入下拉式清單，請按一下或點選Adobe Campaign符號，並導覽至欄位，以在Adobe Campaign個人化欄位中選取適當的欄位。

![chlimage_1-66](assets/chlimage_1-66.png)

下列範例顯示正在顯示的選項欄位（行銷活動）元件。

![chlimage_1-67](assets/chlimage_1-67.png)

### 訂閱檢查清單 (行銷活動) {#subscriptions-checklist-campaign}

使用&#x200B;**訂閱檢查清單（行銷活動）**&#x200B;元件來修改與Adobe Campaign設定檔相關聯的訂閱。

當新增到表單時，此元件將所有可用的訂閱顯示為核取方塊，並允許使用者選取所需的訂閱。 使用者提交表單時，此元件會根據表單動作型別(**Adobe Campaign：訂閱服務**&#x200B;或&#x200B;**Adobe Campaign：取消訂閱服務**)，讓使用者訂閱或取消訂閱選取的服務。

>[!NOTE]
>
>元件不會檢查使用者已訂閱/取消訂閱的服務。

您可以[在訂閱檢查清單（行銷活動）元件中設定大部分Adobe Campaign元件通用的設定](#settings-common-to-most-components)。 (此元件沒有可用的Adobe Campaign設定。)

下列範例顯示正在顯示的訂閱檢查清單（行銷活動）元件。

![chlimage_1-68](assets/chlimage_1-68.png)

### 測試欄位 (行銷活動) {#text-field-campaign}

文字欄位（行銷活動）元件可讓您輸入字串型別資料，例如名字、姓氏、地址、電子郵件地址等。

除了大部分Adobe Campaign元件通用的[設定](#settings-common-to-most-components)之外，您還可以設定下列專案：

* **限制 — 限制**&#x200B;下拉式清單
您可以選取 — **無、** **電子郵件**&#x200B;或&#x200B;**名稱** （無變音） — 新增電子郵件地址、名稱或無限制的限制。 如果您選取電子郵件，使用者在欄位中輸入的答案必須是電子郵件地址。 如果您選取名稱，則它必須是名稱（不允許變音）。

* **限制訊息**&#x200B;此外，您可以新增限制訊息，讓使用者知道如何正確格式化他們的回答。
* **樣式 — 寬度**&#x200B;按一下或點選&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;圖示或輸入數字，以調整欄位的寬度。

下列範例顯示正在顯示的文字欄位（行銷活動）元件。

![chlimage_1-69](assets/chlimage_1-69.png)
