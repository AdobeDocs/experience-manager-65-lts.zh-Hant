---
title: AEM檔案服務概觀
description: AEM檔案服務是一組OSGi服務，用於建立、彙編和保護PDF檔案。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services,Reader Extensions, Forms Service,PDF Generator
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 1%

---

# AEM檔案服務概觀{#overview-of-aem-document-services}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) |
| AEM 6.5 | 本文章 |


AEM檔案服務是一組OSGi服務，用於建立、彙編和保護PDF檔案。 檔案服務包含下列服務：

## 輸出服務 {#output-service}

「輸出」服務可讓您建立不同格式的檔案，包括PDF、雷射印表機格式和標籤印表機格式。 雷射印表機格式為PostScript和印表機控制語言(PCL)。 下列清單指定標籤印表機格式：

* 斑馬(ZPL)
* Intermec (IPL)
* Datamax (DPL)
* 東芝科技(TPCL)

檔案可以傳送到網路印表機、本機印表機或檔案系統上的檔案。 Output服務會合併XML表單資料與表單設計以產生檔案。 Output服務可以產生檔案，而無需將XML表單資料合併到檔案中。 不過，主要工作流程是將資料合併至檔案。

>[!NOTE]
>
>表單設計通常使用Designer來建立。 如需有關為Output服務建立表單設計的資訊，請參閱Designer說明。

使用Output服務將XML資料與表單設計合併時，結果會產生非互動式PDF檔案。 非互動式PDF檔案不允許使用者在其欄位中輸入資料。 相反地，您可以使用Forms服務建立互動式PDF表單，讓使用者在其欄位中輸入資料。

下列四個Output服務作業可供使用：

* **generatePDFOuput**：將表單設計與資料合併，以產生PDF檔案
* **generatePrintedOutput**：將表單設計與表單資料合併，以產生要傳送至雷射或標籤網路印表機的檔案

* **generatePDFOutputBatch**：在單一叫用中合併具有多個資料記錄的多個範本，以產生批次PDF檔案。 也可以合併所有PDF來產生單一PDF
* **generatePrintedOutputBatch**：在單一呼叫中合併含有多個資料記錄的多個範本，以產生一整批列印檔案(PS、PCL、ZPL、DPL、IPL、TPCL)。 也可以選擇產生單一列印檔案。

## 組合器服務 {#assembler-service}

Assembler服務可讓您組合、重新排列和增加PDF和XDP檔案，並取得有關PDF檔案的資訊。 提交至組合器服務的每個工作都包含檔案描述XML (DDX)檔案、來原始檔及外部資源（字串與圖形）。 DDX檔案提供如何使用來原始檔來產生一組結果檔案的指示。

除了上述功能以外，組裝程式服務也提供：

* 將PDF檔案轉換為PDF/A標準。
* 將PDF forms、XML表單(在Designer中建立)和PDF forms (在Acrobat中建立)轉換為PDF/A-1b、PDF/A-2b和PDFA/A-3b。
* 轉換已簽署或未簽署的PDF檔案（需要數位簽名）。
* 驗證PDF/A檔案的合規性，並視需要轉換它。

### 關於DDX {#about-ddx}

使用「組合器」服務時，請使用名為「檔案描述XML (DDX)」的XML語言來描述您想要的輸出。 DDX是一種宣告式標籤語言，其元素代表檔案的建置組塊。 這些建置區塊包括PDF檔案、XDP檔案、XDP表單片段和其他元素，例如註解、書籤和樣式化文字。

DDX檔案可以指定具有以下特性的結果檔案：

* 從多個PDF檔案組合的PDF檔案
* 多個PDF檔案與單一PDF檔案分離
* PDF Portfolio包含獨立使用者介面和多份PDF和非PDF檔案
* 從多個XDP檔案組合的XDP檔案
* 包含動態插入XDP檔案之XML片段的XDP檔案
* 封裝XDP檔案的PDF檔案
* 報告PDF檔案特性的XML檔案。 報告的特性包括文字、註釋、表單資料、檔案附件、用於PDF產品組合的檔案、書籤和PDF屬性。 PDF屬性包括表單屬性、頁面旋轉和檔案作者。

您可以使用DDX來增加PDF檔案，做為檔案組裝或拆解的一部分。 您可以指定下列效果的任意組合：

* 在選取的頁面上新增或移除浮水印或背景。
* 在選取的頁面上新增或移除頁首與頁尾。
* 移除PDF套件或PDF Portfolio的結構和導覽功能。 結果會是單一PDF檔案。
* 重新編號頁面標籤。 頁面標籤通常用於頁碼編排。
* 從其他來原始檔匯入中繼資料。
* 新增或移除檔案附件、書籤、連結、註解和JavaScript。
* 設定初始檢視特性並最佳化以利在網頁上檢視。
* 設定加密PDF的許可權。
* 旋轉頁面或在頁面上旋轉和移動內容。
* 變更所選頁面的大小。
* 將資料與XFA型PDF合併。

您可以使用簡單的輸入對映來指定來源和結果檔案的位置。 您也可以使用下列外部資料URL型別：

* 檔案
* FTP
* HTTP/HTTPS

## 檔案Assurance服務 {#doc-assurance-service}

Doc Assurance服務可協助您加密和解密檔案、透過其他使用許可權擴充Adobe Reader的功能，以及在檔案中新增數位簽名。 您的使用者可以輕鬆與PDF forms和檔案互動，而您的組織則可改善安全性、封存和合規性。

Doc Assurance服務包含三項服務：簽名、加密和讀者延伸模組。

### 簽章服務 {#signature-service}

簽名服務可讓您在AEM伺服器上處理數位簽名和檔案。 例如，簽章服務通常用於以下情況：

* AEM伺服器會先認證表單，再傳送給使用者使用Acrobat或Adobe Reader開啟。
* AEM伺服器會使用Acrobat或Adobe Reader驗證已新增至表單的簽名。
* AEM伺服器代表公證人簽署表格。

簽章服務會存取儲存在信任存放區中的憑證和認證。

### 加密服務 {#encryption-service}

加密服務可讓您加密和解密檔案。 檔案加密後，其內容會變得無法讀取。 您可以加密整個PDF檔案（包括其內容、中繼資料和附件）、中繼資料以外的所有內容，或僅加密附件。 授權的使用者可以解密檔案以取得其內容的存取權。 如果PDF檔案已使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Acrobat中檢視檔案。 如果使用憑證加密PDF檔案，使用者必須使用私密金鑰（憑證）解密PDF檔案。 用於解密PDF檔案的私密金鑰必須與用於加密該檔案的公開金鑰相對應。

### Reader擴充功能服務 {#reader-extension-service}

Reader擴充功能服務可擴充Adobe Reader的功能，賦予您其他使用許可權，讓貴組織輕鬆共用互動式PDF檔案。 Reader擴充功能服務可與Adobe Reader 7.0或更新版本搭配使用。 此服務會將使用許可權新增至PDF檔案。 此動作會啟動使用Adobe Reader開啟PDF檔案時通常無法使用的功能，例如新增註釋至檔案、填寫表單及儲存檔案。 協力廠商使用者不需要其他軟體或外掛程式即可使用啟用許可權的檔案。

當PDF檔案新增了適當的使用許可權時，收件者可在Adobe Reader中執行下列活動：

* 線上上或離線完成PDF檔案和表單，讓收件者在本機儲存復本以做為記錄，同時仍完整保留新增的資訊
* 將PDF檔案儲存至本機硬碟，以保留原始檔案以及任何其他註解、資料或附件
* 將檔案和媒體剪輯附加至PDF檔案
* 使用業界標準的公開金鑰基礎架構(PKI)技術套用數位簽名，以簽署、認證和驗證PDF檔案
* 以電子方式提交已完成或附註的PDF檔案
* 使用PDF檔案和表單作為內部資料庫和Web服務的直覺式開發前端
* 與其他人共用PDF檔案，讓檢閱者可以使用直覺式的標籤工具來新增註解。 這些工具包括電子註解、印章、醒目提示和文字刪除線。 Acrobat提供相同功能。
* 支援條碼式表單解碼。

在Adobe Reader中開啟啟用許可權的PDF檔案時，會自動啟用這些特殊使用者功能。 當使用者使用完啟用許可權的檔案時，這些功能在Adobe Reader中會再次停用。 除非使用者收到其他已啟用許可權的PDF檔案，否則這些功能會維持停用狀態。

開箱即用的DocAssurance服務無法使用。 若要設定DocAssurance服務，請參閱[安裝和設定檔案服務](../../forms/using/install-configure-document-services.md)。

## 傳送至印表機服務 {#send-to-printer-service}

「傳送至印表機服務」提供API，可將檔案傳送至指定的印表機進行列印。
