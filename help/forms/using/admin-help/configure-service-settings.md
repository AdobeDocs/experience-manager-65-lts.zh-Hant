---
title: 設定服務設定
description: 瞭解如何設定服務設定。 您可以使用「服務管理」頁面來設定AEM表單中各服務的設定。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Workbench
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a2586a1e-0e7f-4ea4-87ec-fbd82df3ec4c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '10836'
ht-degree: 0%

---

# 設定服務設定 {#configure-service-settings}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以使用「服務管理」頁面，為AEM表單中的每項服務設定設定。 可用的設定會依所設定的服務而有所不同。

1. 在Administration Console中，按一下「服務>應用程式和服務>服務管理」。
1. 請先停止服務，再進行變更。 （請參閱[啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)。）
1. 按一下要設定的服務名稱。
1. 如果服務有「組態」標籤，請使用它來變更服務的設定。 如需詳細資訊，請參閱下列連結清單。

   >[!NOTE]
   >
   >並非所有列在「服務管理」頁面上的服務都有組態頁簽。 對於您已建立的處理，只有在您已在Workbench中為處理新增組態引數時，才會顯示「組態」標籤。 （請參閱[Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63)中的「設定引數」。）


1. 按一下「安全性」標籤，然後設定服務的安全性設定。 請參閱[修改服務的安全性設定](configure-service-settings.md#modifying-security-settings-for-a-service)。
1. 如果服務有「端點」標籤，請使用它來變更端點設定。 請參閱[管理端點](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md)。
1. 按一下「共用」標籤並設定共用設定。 請參閱[為服務設定集區](configure-service-settings.md#configuring-pooling-for-a-service)。
1. 按一下[儲存]儲存變更，或按一下[取消]捨棄變更。
1. 選取服務名稱旁的核取方塊，然後按一下啟動以重新啟動服務。

## 稽核工作流程服務設定 {#audit-workflow-service-settings}

Workbench提供在執行階段執行處理序執行個體時加以記錄，然後播放它們以觀察處理序行為的功能。 （請參閱[Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63)。）若要節省Forms伺服器的檔案系統空間，您可以限制儲存的處理程式記錄資料量。 您可以設定Audit Workflow Service ( `AuditWorkflowService`)的下列屬性：

**maxNumberOfRecordingInstances：**&#x200B;儲存的錄製數目上限。 當儲存最大記錄數時，建立新記錄時將從檔案系統中移除最舊的記錄。 如果您想要建立許多錄製，而且您想要自動移除舊的錄製，則此屬性很有用。 預設值為 50。

**MaxNumberOfRecordingEntries：**&#x200B;每個錄製可以儲存的最大資料專案數。 資料專案是處理程式中作業的相關資訊。 每個作業執行都會儲存數個專案，例如作業是否已開始、作業是否已完成，以及通向作業的路由是否已完成。 當處理程式可以包含許多作業執行時（例如，遇到無盡的回圈時），此屬性會很有用。 預設值為 50。

## 條碼式表單服務設定 {#barcoded-forms-service-settings}

條碼式表單服務`(BarcodedFormsService)`會從掃描的影像中擷取條碼資料。 此服務接受條碼式(TIFF或PDF)作為輸入，並擷取由條碼編碼之資料的電腦表示法。

條碼式表單服務可使用下列設定。

**向左讀取：**&#x200B;選取時，條碼影像會從右到左水準掃描。

**向右讀取：**&#x200B;選取時，條碼影像會從左到右水準掃描。

**向上讀取：**&#x200B;選取時，條碼影像會從下到上垂直掃描。

**向下讀取：**&#x200B;選取時，條碼影像會從上到下垂直掃描。

>[!NOTE]
>
>依預設，會選取所有選項。 只有在您確定表單上不會出現條碼時，才取消選取選項。

**基本檔案路徑：**&#x200B;相對於執行XML檔案工作和執行一般檔案工作作業之批次輸入與輸出檔案引數的檔案路徑。 在叢集組態中，基本檔案路徑必須是所有叢集節點都具備讀取/寫入存取權的共用檔案系統位置。

**資料Source名稱：**&#x200B;用來維護批次處理作業相關狀態與歷程記錄資訊的資料來源名稱。 指定的資料來源必須支援全域(XA)交易。

## 中央移轉Bridge服務（已棄用）設定 {#central-migration-bridge-service-settings}

中央移轉Bridge服務( `CentralMigrationBridge`)會叫用Adobe Central Pro Output Server （中央）功能的子集，包括JFMERGE、JFTRANS和XMLIMPORT命令。 中央移轉Bridge服務作業可讓您在AEM表單中重複使用下列中央資產：

* 範本設計(&amp;amp；ast；.ifd)
* 輸出範本(&amp;amp；ast；.mdf)
* 資料檔案（&amp;amp；ast；.dat檔案）
* 序言檔案（&amp;amp；ast；.pre檔案）
* 資料定義檔案(&amp;amp；ast；.tdf)

下列設定適用於中央移轉Bridge服務。

**中央安裝目錄：** Adobe Central 5.7的安裝目錄。

## EMC Documentum的Content Repository Connector服務設定 {#content-repository-connector-for-emc-documentum-service-settings}

Content Repository Connector for EMC Documentum服務( `EMCDocumentumContentRepositoryConnector`)可讓您建立與儲存在Documentum存放庫中的內容互動的程式。

下列設定適用於EMC Documentum服務的Content Repository Connector。

**Asset Link物件預設路徑：** Documentum存放庫中用於儲存Asset Link物件的路徑預設部分。 實際路徑由預設路徑及表單範本在AEM表單存放庫中的位置組成。

例如，如果預設路徑設為`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`，而表單範本儲存在資料夾`/Docbase/forms/`中，則Asset Link物件會儲存在下列位置：

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

此設定的預設值為`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`。

## IBM FileNet服務設定的內容存放庫聯結器 {#content-repository-connector-for-ibm-filenet-service-settings}

IBM FileNet的內容存放庫聯結器可讓您建立與儲存在IBM FileNet存放庫中的內容互動的流程。

下列設定適用於IBM FileNet服務的內容存放庫聯結器。

**資產連結物件預設路徑：** IBM FileNet存放庫中用於儲存資產連結物件的預設路徑部分。 實際路徑由預設路徑及表單範本在AEM表單存放庫中的位置組成。

例如，如果預設路徑設為`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`，而表單範本儲存在資料夾`/Docbase/forms/`中，則Asset Link物件會儲存在下列位置：

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

此設定的預設值為`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`。

## 轉換PDF服務設定 {#convert-pdf-service-settings}

轉換PDF服務( `ConvertPdfService`)會將PDF檔案轉換為PostScript和多種影像格式(JPEG、JPEG 2000、PNG和TIFF)。 將PDF檔案轉換為PostScript對於任何PostScript印表機上的自動伺服器式列印都很有用。 在不支援PDF檔案的內容管理系統中封存檔案時，將PDF檔案轉換為多頁TIFF檔案是可行的。

轉換PDF服務可使用下列設定。

**交易型別：**&#x200B;指定交易內容應如何傳播至作業。

**必要：**&#x200B;支援交易內容（如果有的話）；否則，會建立新的交易內容。 這是預設值。

**需要新的：**&#x200B;永遠建立新的交易內容。 如果作用中交易內容存在，則會暫停它。

**交易逾時（秒）：**&#x200B;基礎交易提供者在復原正在包裝此作業的交易之前應等待的秒數。 如果傳播現有的交易內容，則會忽略此值。 預設值為 180。

**平滑化的臨界值解析度（以dpi表示）：**&#x200B;如果已經為文字、線條圖及影像選取「將平滑化套用至」選項，則套用至平滑（或消除鋸齒）的影像解析度下方。

**套用平滑處理至文字：**&#x200B;控制文字的消除鋸齒。 若要停用文字平滑化，並使用熒幕放大鏡讓文字更銳利且更容易閱讀，請清除此核取方塊。

**將平滑套用至線條圖：**&#x200B;套用平滑以移除線條中的銳角。

**套用平滑至影像：**&#x200B;套用平滑以最小化影像中的突然變更。

## Distiller服務設定 {#distiller-service-settings}

Distiller服務( `DistillerService`)透過網路將PostScript、Encapsulated PostScript (EPS)和PRN檔案轉換為PDF檔案。

下列設定適用於Distiller服務。

**Adobe PDF設定：**&#x200B;下列預先設定的設定已套用至產生的PDF：

* 高品質列印
* 超大頁面
* PDFA1b 2005 CMYK
* PDFA1b 2005 RGB
* PDFX1a 2001
* PDFX3 2002
* 新聞品質
* 最小檔案大小
* 標準

新設定可透過PDF Generator使用者介面建立。

**安全性設定：**&#x200B;預先設定的安全性設定已套用至產生的PDF檔案。 預設值為No Security。 使用PDF Generator建立安全性設定，然後在這裡輸入設定。

**集區大小：**&#x200B;集區的初始大小。 部署Distiller服務時，此數字可用來決定已建立並配置給等待呼叫要求之可用集區的服務實作執行個體數量。 然後，服務容器可以立即回應呼叫要求，而不需要先初始化服務執行個體。

## 檔案管理服務設定 {#document-management-service-settings}

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES （已淘汰）是隨LiveCycle安裝的內容管理系統。 它可讓使用者設計、管理、監控及最佳化以人為中心的流程。 內容服務（已棄用）支援將於2014年12月31日終止。 請參閱[Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。

檔案管理服務(`DocumentManagementService`)可讓處理程式使用內容服務（已棄用）所提供的內容管理功能。 檔案管理作業提供在內容管理系統中維護空間與內容所需的基本工作。 這類工作的範例包括複製、刪除、移動、擷取和儲存內容、建立空間和關聯，以及取得和設定內容屬性。

Document Management服務可使用下列設定。

**存放區配置：**&#x200B;內容所在存放區的配置。 預設值為workspace。

**HTTP連線埠：**&#x200B;用來存取內容服務的連線埠（已棄用）。 預設值為 8080。

## 電子郵件服務設定 {#email-service-settings}

電子郵件常用於發佈內容或提供狀態資訊，以作為自動化程式的一部分。 電子郵件服務(`EmailService`)可讓處理程式從POP3或IMAP伺服器接收電子郵件訊息，並傳送電子郵件訊息至SMTP伺服器。

例如，某個程式使用電子郵件服務來傳送包含PDF表單附件的電子郵件訊息。 電子郵件服務會連線至SMTP伺服器，以傳送包含附件的電子郵件訊息。 PDF表單的設計可讓收件者在完成表單後按一下「提交」 。 動作會導致表單以附件形式傳回至指定的電子郵件伺服器。 電子郵件服務會擷取傳回的電子郵件訊息，並將完成的表單儲存在流程資料表單變數中。

電子郵件服務可使用下列設定。

**SMTP主機：**&#x200B;用於傳送電子郵件之SMTP伺服器的IP位址或URL。

**SMTP連線埠號碼：**&#x200B;用來連線至SMTP伺服器的連線埠。

**SMTP驗證：**&#x200B;如果連線到SMTP伺服器需要使用者驗證，請選取此選項。

**SMTP使用者：**&#x200B;用來登入SMTP伺服器的使用者帳戶使用者名稱。

**SMTP密碼：**&#x200B;與SMTP使用者帳戶關聯的密碼。

**SMTP傳輸安全性：**&#x200B;用來連線至SMTP伺服器的安全性通訊協定：

* 若未使用任何通訊協定，則選取無（資料會以純文字傳送）
* 若使用安全通訊端層通訊協定，請選取SSL。
* 若使用傳輸層安全性，請選取TLS。

**POP3/IMAP主機：**&#x200B;用來傳送電子郵件之POP3或IMAP伺服器的IP位址或URL。

**POP3/IMAP使用者名稱：**&#x200B;用來登入POP3或IMAP伺服器的使用者帳戶使用者名稱。

**POP3/IMAP密碼：**&#x200B;與POP3或IMAP使用者帳戶關聯的密碼。

**POP3/IMAP連線埠號碼：**&#x200B;用來連線至POP3或IMAP伺服器的連線埠。

**POP3/IMAP：**&#x200B;用來傳送及接收電子郵件的通訊協定。

**接收傳輸安全性：**&#x200B;用來連線至SMTP伺服器的安全性通訊協定：

* 若未使用任何通訊協定，則選取無（資料會以純文字傳送）。
* 若使用安全通訊端層通訊協定，請選取SSL。
* 若使用傳輸層安全性，請選取TLS。

## 加密服務設定 {#encryption-service-settings}

加密服務( `EncryptionService`)可讓您加密和解密檔案。 檔案加密後，其內容會變得無法讀取。 授權的使用者可以解密檔案以取得內容的存取權。 如果PDF檔案已使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Adobe Acrobat中檢視檔案。 同樣地，如果使用憑證加密PDF檔案，使用者必須使用與用來加密PDF檔案的憑證（私密金鑰）相對應的公開金鑰來解密PDF檔案。

加密服務可使用下列設定。

**要連線的預設LDAP伺服器：**&#x200B;用來擷取檔案加密憑證之LDAP伺服器的主機名稱。

**要連線至LDAP伺服器的**&#x200B;連線埠號碼的預設LDAP連線埠。

**預設LDAP使用者名稱：**&#x200B;如果LDAP伺服器需要驗證，請指定用來連線至LDAP伺服器的使用者名稱。

**預設LDAP密碼：**&#x200B;如果LDAP伺服器需要驗證，請指定與用來連線至LDAP伺服器的使用者名稱對應的密碼。

>[!NOTE]
>
>只有在透過SSL （使用LDAPS）保護連線時才使用簡單驗證（使用者名稱和密碼）。

<!-- **Compatibility Mode:**-->

## FTP服務設定 {#ftp-service-settings}

FTP服務( `FTP`)可讓處理程式與FTP伺服器互動。 FTP服務作業可以從FTP伺服器擷取檔案、將檔案放在FTP伺服器上，以及從FTP伺服器刪除檔案。 例如，從程式產生的報告等檔案可能會儲存在FTP伺服器上以分發。 或者，外部系統可能會根據流程中先前的步驟產生某些檔案。 在程式中的後續步驟中，可將檔案傳輸到遠端位置。

FTP服務可使用下列設定。

**預設主機：** FTP伺服器的IP位址或URL。

**預設連線埠：**&#x200B;用來連線至FTP伺服器的連線埠。 預設值為 21。

**預設使用者名稱：**&#x200B;您可以用來存取FTP伺服器的使用者帳戶名稱。 使用者帳戶必須擁有足夠的許可權，才能執行此服務所需的FTP作業。

**預設密碼：**&#x200B;要與指定的使用者名稱搭配使用以透過FTP伺服器驗證的密碼。

## 產生PDF服務設定 {#generate-pdf-service-settings}

產生PDF服務( `GeneratePDFService`)會將各種原生格式的檔案轉換為PDF檔案，並將PDF檔案轉換為多種檔案格式。

產生PDF服務可使用下列設定。

**Adobe PDF設定：**&#x200B;預先設定要套用至轉換工作的Adobe PDF設定名稱（如果這些設定未指定為API叫用引數的一部分）。 Adobe PDF設定是透過按一下「服務> PDF Generator > Adobe PDF設定」在管理控制檯中設定。 這些設定僅適用於PDFMaker型轉換。

**安全性設定：**&#x200B;要套用至轉換工作的預先設定安全性設定的名稱（如果這些設定未指定為API叫用引數的一部分）。 您可以在管理控制檯中按一下「服務> PDF Generator >安全性設定」來設定安全性設定。

**檔案型別設定：**&#x200B;預先設定要套用至轉換工作的檔案型別設定名稱（如果這些設定未指定為API叫用引數的一部分）。 檔案型別設定是透過按一下「服務> PDF Generator>檔案型別設定」在管理控制檯中進行設定。

**使用WebCapture （僅限Windows）：**&#x200B;當此設定為true時，產生PDF服務會使用Acrobat進行所有HTML到PDF的轉換。 這可改善從HTML產生的PDF檔案品質，但效能可能會稍微降低。 預設值為false。

**HTML到PDF轉換的主要轉換工具：**「產生PDF」服務提供多種將HTML檔案轉換為PDF檔案的途徑： Webkit、WebCapture （僅限Windows）和WebToPDF。 此設定可讓使用者選取主要轉換工具，以便將HTML轉換為PDF。 依預設，會選取WebToPDF。

**HTML到PDF轉換的遞補轉換工具：**&#x200B;如果主要轉換工具失敗，請指定HTML到PDF轉換的轉換工具。 依預設，會選取WebCapture （僅限Windows）。

**使用Acrobat影像轉換（僅限Windows）：**&#x200B;當此設定為true時，產生PDF服務會使用Acrobat進行所有影像到PDF的轉換。 只有當預設的純Java轉換機制無法成功轉換大部分的輸入影像時，此設定才有用。 預設值為false。

**啟用以Acrobat為基礎的AutoCAD轉換（僅限Windows）：**&#x200B;當此設定為true時，產生PDF服務會使用Acrobat進行所有DWG到PDF的轉換。 只有當伺服器上未安裝AutoCAD或AutoCAD轉換機制無法成功轉換檔案時，此設定才有用。

**尋找禁止的特殊的規則運算式
使用者名稱中的字元（僅限Windows）：**&#x200B;指定當字元出現在使用者名稱中時，會干擾Export PDF和最佳化PDF作業的字元。

**ImageToPDF集區大小：**&#x200B;產生PDF服務中預設（純Java） Image-to-PDF轉換器的集區大小。 此設定可控制「產生PDF」服務可同時執行的最大影像到PDF轉換次數。 此設定的預設值（建議用於單處理器系統）為3，您可以在多處理器系統上增加此值。

**HTML至PDF集區大小：**&#x200B;產生PDF服務中HTML至PDF轉換器的集區大小。 此設定可控制「產生HTML」服務可同時執行的PDF對PDF的最大轉換次數。 此設定的預設值（建議用於單處理器系統）為3，您可以在多處理器系統上增加此值。

**OCR集區大小：** PDF Generator用於OCR的PaperCaptureService集區大小。 此設定的預設值（建議用於單處理器系統）為3，您可以在多處理器系統上增加此值。 此設定僅在Windows系統上有效。

**ImageToPDF在記憶體中用於TIFF轉換的最大頁數：**&#x200B;此設定決定了TIFF影像在轉換成PDF期間可保留在記憶體中的最大頁數。 此設定的預設值為500，如果為ImageToPDF轉換程式配置額外的記憶體，則會增加此值。

**HTML到PDF轉換的遞補字型系列：**&#x200B;當原始HTML中使用的字型無法供PDF伺服器使用時，AEM Forms檔案中要使用的字型系列名稱。 如果要轉換使用無法使用字型的HTML頁面，請指定字型系列。 例如，以地區語言撰寫的頁面可能會使用無法使用的字型。

**原生轉換的重試邏輯**&#x200B;管理PDF產生重試（如果第一次嘗試轉換失敗）：

* **無重試**

  如果首次轉換嘗試失敗，請勿重試PDF轉換

* **重試**

  不論是否已達到逾時臨界值，都請重試PDF轉換。 第一次嘗試的預設逾時期間為270秒。

* **如果時間允許，請重試**

  如果首次轉換嘗試所花費的時間少於指定的逾時期間，請重試PDF轉換。 例如，如果逾時期間為270秒，而第一次嘗試耗用200秒，PDF Generator將會重新嘗試轉換。 如果首次嘗試本身耗用270秒，則不會重試轉換。

## 指南ES4公用程式服務設定 {#guides-es4-utilities-service-settings}

當您建立指南時，某些資源（例如指南定義）會內嵌在指南中。 資源也可作為儲存在本機或AEM Forms伺服器上的應用程式資產的參考而存在。 指南不包含資料，且提交位置和輸入的值不適合所有外部環境。

在大多數情況下，預設的Guides轉譯服務就足以準備要用於Workspace或其他外部環境的指南。 (在「服務」檢視中，Workbench的預設服務為「指南（系統）/程式/轉譯器指南 — 1.0」。) 指南公用程式服務( `GuidesUtility`)可讓您建立自訂程式，以視需要呈現指南。

「參考線公用程式」作業可讓您將下列「參考線」演算任務新增至處理序：

* 判斷是否有資料可用來將指南填入
* 內嵌節目表資料或將其轉換為連結
* 將參照的內容轉換為外部可存取的URL
* 取代HTML檔案或其他包裝函式中的值，或將其轉換為可從外部存取的URL
* 設定提交位置
* 指定輸入值
* 建立引數以代表參考的內容
* 如果有變化，請設定變化

「指南公用程式」服務的預設值支援大部分的使用案例。 不過，如有需要，您可以變更下列值。

**publicPaths：**&#x200B;此選項已過時。 請勿在AEM表單中使用此選項。

**pathInfoExpiryInSeconds：**&#x200B;使用者端路徑資訊要求到期的間隔。 預設值為1。

**collateralExpiryInSeconds：**&#x200B;使用者端的附屬專案要求過期的時間間隔。 預設為315576000。

**mismatchExpiryInSeconds：**&#x200B;當eTag （實體標籤）不相符時，使用者端附屬專案的要求到期的間隔。 （eTag是HTTP回應標頭。） 預設值為1。

**guideContext：** Guides Web應用程式的內容根目錄。 符合使用Guides網頁應用程式設定的值。 預設值為/Guides/。

**secureRandomAlgorithm：**&#x200B;產生金鑰和識別碼時使用的演演算法。 此值會傳遞給SecureRandom Java類別的getInstance方法。 預設為SHA1PRNG。

**idBytes：**&#x200B;用來作為金鑰識別碼的隨機位元組數目。 預設值為6。

**macAlgorithm：**&#x200B;用於附屬專案URL驗證的MAC （訊息驗證碼）演演算法。 此方法會傳遞至Mac類別的getInstance方法。 預設為HmacSHA1。

**macRefreshIntervalInMinutes：**&#x200B;金鑰作用中的時間量。 當此間隔的金鑰處於作用中狀態時，就會產生新的金鑰。 新鍵會成為使用中鍵。 先前作用中的金鑰會保留10%的重新整理間隔。 此行為可讓使用舊金鑰產生的URL在金鑰開關中繼續運作。 預設為144000。

**macOverlapIntervalInMinutes：**&#x200B;產生新金鑰後上一個金鑰將維持有效的時間長度。 預設值為1440分鐘（1天）。

**macKeySeed：**&#x200B;產生安全URL的種子值。 如果此選項為的話，索引鍵永遠不會重新整理。 在不同的伺服器上設定相同的種子，會導致這些伺服器產生相容的安全URL。 如果在負載平衡器後使用多個表單伺服器，這可能很有用。 輸入字元和數字的隨機序列作為種子。

### 在伺服器叢集中使用指南 {#using-guides-in-a-server-cluster}

在不使用粘性工作階段的伺服器叢集中轉譯參考線失敗，並產生NullPointerException。 Guides請求會使用安全URL，這些URL在預設情況下在其產生所在的伺服器中是唯一的。 在使用粘性工作階段的叢集中，當請求點選叢集中的節點後，該工作階段或使用者的所有後續請求都只路由到該伺服器，一切正常。 在不使用粘性工作階段的叢集中，後續請求可能會點選叢集中的任何伺服器。 如果請求點選的伺服器不是原始伺服器，則無法解析安全URL。

如果您在不使用粘性工作階段的伺服器叢集中使用Guides，請為GuidesUtility服務設定macKeySeed值，然後停止並啟動叢集。

macKeySeed值是用於產生安全URL的隨機數產生器的種子。 設定此值會讓每個叢集節點以相同的方式初始化隨機數字產生器，並存取相同的安全URL。 您可以對此種子值使用任何隨機字串。

需要重新整理安全URL時，請變更macKeySeed值。 重新整理安全URL取決於您的安全性原則，與變更伺服器主根密碼的重新整理原則類似。 macSeedValue類似於安全URL的主密碼，因為它用於產生新的唯一隨機數，以用於安全URL的產生和擷取。

重新啟動叢集，因為macSeedValue在系統啟動時是唯讀的。 所有節點都需要重新啟動才能讀取值，因為它們會單獨使用它，以種子值初始化其內部隨機數。

## JDBC服務設定 {#jdbc-service-settings}

JDBC服務(`JdbcService`)可讓處理程式與資料庫互動。

下列設定適用於JDBC服務。

**datasourceName：**&#x200B;字串值，代表要用來連線至資料庫伺服器的資料來源的JNDI名稱。 資料來源必須在託管Forms伺服器的應用程式伺服器上定義。 預設值是AEM表單資料庫的資料來源的JNDI名稱。

## JMS服務設定 {#jms-service-settings}

JMS服務(`JMS`)可與Java Messaging System (JMS)提供者互動，這些提供者同時實作點對點訊息和發佈/訂閱訊息。

使用預設特性設定JMS服務，讓服務作業可以連線並與JMS提供者及關聯的JNDI服務互動。 根據JBoss Application Server，服務屬性的值會設定為預設值。 如果您使用不同的應用程式伺服器來託管AEM表單，請變更這些值。

JMS服務可使用下列設定。

**提供者URL：** JNDI服務提供者的URL。 預設值是以JBoss Application Server為基礎。 下列URL是AEM表單支援之應用程式伺服器的預設值：

**JBoss：** `<server name>:1099`

**WebLogic：** `<server name>:7001`

**WebSphere：** `<server name>:2809`

**JNDI使用者名稱：**&#x200B;要用來向用來查詢佇列和主題名稱的JNDI服務提供者進行驗證的帳戶使用者名稱。 預設值為guest。

**JNDI密碼：**&#x200B;與JNDI使用者名稱指定的使用者名稱關聯的密碼。 預設值為guest。

**Initial Context Factory：**&#x200B;要做為初始Context Factory使用的Java類別。 JMS服務會使用此類別來建立初始前後關聯，這是解析主題和佇列名稱的起點。 預設值是JBoss上JMS服務的初始前後關聯處理站。 下列類別是AEM表單支援之應用程式伺服器的初始內容處理站：

**JBoss：** org.jnp.interfaces.NamingContextFactory

**WebLogic：** weblogic.jndi.WLInitialContextFactory

**WebSphere：** com.ibm.websphere.naming.WsnInitialContextFactory

**連線使用者名稱：**&#x200B;與為連線使用者名稱指定的使用者名稱相關聯的密碼。 預設值為guest。

**連線密碼：**&#x200B;與連線使用者名稱指定的使用者名稱關聯的密碼。 預設值為guest。

**其他內容：**&#x200B;您可以傳遞至JNDI服務提供者的內容名稱和值配對。 這些屬性取決於您使用之提供者的實作和設定。

屬性名稱和值組之間以分號&#x200B;**；**&#x200B;分隔。 例如，下列文字顯示將針對名為name1和name2的兩個屬性指定的值，其值分別為value1和value2：

`name1=value1;name2=value2`

## LDAP服務設定 {#ldap-service-settings}

LDAP服務( `LDAPService`)提供查詢LDAP目錄的操作。 LDAP目錄通常用來儲存組織中人員、群組及服務的相關資訊。

下列設定適用於LDAP服務。

**Initial Context Factory：**&#x200B;要做為內容工廠的Java類別。 此類別用來建立與LDAP伺服器的連線。 預設值為com.sun.jndi.ldap.LdapCtxFactory，適用於大多數LDAP伺服器。

**提供者URL：**&#x200B;用來連線至LDAP服務的URL。 值的格式為`ldap://server name:port`

*伺服器名稱*&#x200B;是裝載LDAP伺服器的電腦名稱

*連線埠*&#x200B;是LDAP服務使用的通訊連線埠。 預設值為389，這是用於LDAP連線的標準連線埠。

**使用者名稱：**&#x200B;用來登入LDAP伺服器的使用者帳戶使用者名稱。 使用者帳戶需要擁有許可權才能連線到伺服器並讀取LDAP目錄中的資訊。

根據LDAP伺服器的不同，使用者名稱可能是簡單使用者名稱（例如`myname`）或DN （例如`cn=myname,cn=users,dc=myorg`）。

**密碼：**&#x200B;與使用者名稱設定對應的密碼。

**其他屬性：**&#x200B;字串值，代表您可以提供給LDAP伺服器的其他屬性及其對應值。 該值為以下格式：

`property=value;property=value;...`

## Microsoft SharePoint組態服務設定 {#microsoft-sharepoint-configuration-service-settings}

Microsoft SharePoint設定服務`(MSSharePointConfigService)`可讓您為具有模擬許可權的AEM表單使用者指定認證。 如需模擬許可權的相關資訊，請參閱[設定Microsoft SharePoint的聯結器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。

Microsoft SharePoint組態服務可使用下列設定：

* 具有模擬許可權的使用者使用者名稱
* 上述使用者的密碼

**啟用SSL (HTTPS)：**

**存留時間：**&#x200B;此布建設定檔在使用者端上有效並快取的時間長度（以秒為單位）。 預設值為86400 （24小時）。 當使用者端應用程式與伺服器同步且經過指定的時間量時，使用者端應用程式會向伺服器要求新的布建設定檔。

**加密：**&#x200B;指定是否加密行動裝置上儲存的資料。

**Forms應用程式：**&#x200B;在行動使用者端應用程式中啟用Forms功能。 選取此選項時，使用者可以從行動裝置開啟表單及起始程式。

**工作應用程式：**&#x200B;啟用行動使用者端應用程式中的工作功能。 選取此選項時，使用者可以從行動裝置存取其工作清單並完成工作。

**Content Services應用程式：**&#x200B;啟用行動使用者端應用程式中的Content Services功能。 此功能僅適用於iOS。 選取此選項時，iPhone和iPad使用者可以存取儲存在您組織的WebDAV伺服器中的檔案。

**離線支援：**&#x200B;可讓使用者繼續使用行動使用者端應用程式，即使他們未連線到伺服器（例如，當他們超出儲存格範圍或處於飛航模式時）。 使用者也必須在其行動裝置上啟用離線支援設定。 此功能適用於Android和iOS裝置。 此功能預設為關閉。

>[!NOTE]
>
>如果已啟用離線支援，然後您將其停用，則使用者的布建設定檔會立即更新，或線上上時立即更新。 如果使用者一直在離線工作，所有擱置的任務都會傳回至其「任務」清單，而其「佇列」中的所有專案（包括擱置的表單、任務以及包含驗證錯誤的表單）都會從「佇列」中刪除。

**Android：**&#x200B;允許Android裝置連線到伺服器。

**Apple iOS：**&#x200B;允許iPhone和iPad連線至伺服器。

**AIR：**&#x200B;允許執行以Adobe AIR®為基礎的應用程式的裝置連線到伺服器。

**BlackBerry：**&#x200B;允許BlackBerry裝置連線到伺服器。

**需要Android Microsoft Exchange ActiveSync：**&#x200B;指定Android裝置上是否必須安裝並啟用Microsoft Exchange ActiveSync原則管理員(EAS)。 選取此選項時，必須在Android裝置上強制執行EAS。 如果未選取此選項，則不會執行檢查，但會強制執行其他需求。

**Android最小PIN長度：** Android裝置必須具有全域設定，以強制使PIN或密碼至少為此長度。 僅具有指定長度的PIN是不夠的。 系統必須強制執行PIN長度，以便使用者稍後無法移除或縮短PIN。 預設值為 4。

擦去前&#x200B;**Android最大密碼重試次數：** Android裝置具有全域設定，可在指定次數的無效密碼嘗試後擦去系統。 此全域設定已啟用且等於或低於此處指定的值。 預設值為 5。

**移除時Android擦除：**&#x200B;指定當Android裝置上發生原則違規時會發生什麼情況。 選取此選項時，會刪除帳戶。 未選取此選項時，會刪除儲存的帳戶密碼和快取資料。 除非使用者修正原則違規，否則不會再嘗試同步處理。

## 輸出服務設定 {#output-service-settings}

Output服務`(OutputService)`可讓您將XML表單資料與AEM forms Designer中建立的表單設計合併，以以下列格式之一建立檔案輸出資料流：

* PDF或PDF/A檔案輸出資料流。
* Adobe PostScript輸出資料流。
* 印表機控制語言(PCL)輸出資料流。
* Zebra程式設計語言(ZPL)輸出資料流。

輸出資料流可以傳送到網路印表機、本機印表機或磁碟檔案。 當您使用Output服務做為處理作業的一部分時，也可以將輸出資料流作為檔案附件傳送給電子郵件收件者。

下列設定適用於Output服務。

**交易型別：**&#x200B;指定交易內容應如何傳播至作業：

**必要：**&#x200B;支援交易內容（若已存在）；否則，會建立新的交易內容。 這是預設值。

**需要新的：**&#x200B;永遠建立新的交易內容。 如果作用中交易內容存在，則會暫停它。

**交易逾時（秒）：**&#x200B;基礎交易提供者在復原正在包裝此作業的交易之前等待的秒數。 如果傳播現有的交易內容，則會忽略此值。

處理大型資料檔案或在繁忙的伺服器上作業時，可能需要增加Output服務逾時。 若要變更逾時值，請確定硬體伺服器有足夠的記憶體，而且記憶體可供Java Application Server棧積使用。 預設值為 `180`。

## PDFG組態服務設定 {#pdfg-config-service-settings}

下列設定適用於PDFG設定服務( `PDFGConfigService`)。

**使用者工作選專案錄：**&#x200B;檔案系統資料夾的路徑，c服務會在此資料夾中寫入Acrobat Pro Extended可存取的工作選項檔案。 預設值為[user.home]/Application Data/Adobe/Adobe PDF/Settings。

**PS啟動目錄：**&#x200B;儲存了Adobe Acrobat Distiller所需啟動檔案的檔案系統資料夾路徑。 預設值為[user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup。

**PS啟動檔案：** Adobe Acrobat Distiller所需的啟動檔案名稱。 預設值為example.ps。

**伺服器轉換逾時：**&#x200B;產生PDF服務和Distiller服務的最大工作轉換逾時（以秒為單位）。 此設定會限制可在config.xml檔案和PDF Generator的管理主控台頁面中指定的轉換逾時上限。 預設值為 270。

**伺服器全域逾時：**&#x200B;執行PDF轉換時，Forms伺服器會考慮逾時限制。 設定逾時值以解決問題。

**工作選項首碼：**&#x200B;產生PDF服務用來在暫時建立供Acrobat Distiller使用的工作選項檔案前面加上簡短字串的前置詞。 預設值為pdfg。

**非Unicode應用程式：**&#x200B;已知不支援Unicode的應用程式名稱清單（以逗號分隔）。 此清單預先填入了數個應用程式的名稱，這些應用程式的支援已在PDF Generator中預先設定。 如果您選擇透過其他不支援Unicode的協力廠商應用程式來新增對PDF轉換的支援，則必須將新增至此清單。 預設值為Autocad、Excel、PowerPoint、Project、Publisher、Visio、Word、WordPerfect。

**伺服器執行緒集區計數：**&#x200B;控制「產生PDF」服務在內部使用的執行緒集區大小，以服務涉及串連的HTML到PDF轉換要求（轉換可從首頁面存取的連結頁面）。 預設值為 20。

**PDFG清理掃描秒數：**&#x200B;如需詳細資料，請參閱[工作到期秒數]區段。

**工作到期秒數：**&#x200B;產生PDF服務會在轉換輸入檔案後立即刪除這些檔案。 它會暫時儲存輸出檔案，儲存時間長度由「PDFG清理掃描秒數」和「作業過期秒數」設定決定。

工作到期秒數設定指定檔案或空資料夾在符合刪除資格之前必須達到的年齡。 PDFG清理掃描秒數設定指定清理執行緒掃描暫存資料夾以找出可刪除檔案的頻率。

例如，如果「工作到期秒數」設為100，而「PDFG清除掃描秒數」設為200，則清除執行緒會每隔200秒執行一次，並刪除超過100秒的檔案。

PDFG清理掃描秒數的預設值為`43200` （12小時）。 工作到期秒數的預設值為`86400` （24小時）。

**預設地區設定：**&#x200B;用於覆寫部署產生PDF服務之伺服器的預設地區設定（國家/地區+語言）。 如果未指定此引數，則會從部署服務的作業系統決定預設地區設定。 此引數會控制將錯誤訊息傳回API所用的語言。

## 表單工作流程資料服務設定 {#forms-workflow-data-services-service-settings}

下列服務可擴充資料服務，並公開Workspace用來與伺服器通訊的組合器。 請勿變更這些服務的設定選項，除非Adobe支援指示您這麼做。 這些服務不適合直接存取：

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## 遠端服務設定 {#remoting-service-settings}

大部分服務都已設定完成，因此您可透過AEM Forms Remoting (AEM表單已棄用)存取這些服務。 如需(AEM表單已棄用) AEM表單遠端處理的相關資訊，請參閱[使用AEM表單程式設計](https://adobe.com/go/learn_aemforms_programming_63)。

下列設定可供遠端服務使用。

**Flex使用者端驗證方法：**&#x200B;決定當所叫用的服務已啟用安全性、叫用的作業不支援匿名叫用，且使用者端傳入的認證無效或無效時，伺服器傳回給使用者端的回應型別。 從「自訂」或「基本」中選擇。 預設值為「基本」。

**允許非序列化類別的序列化：**&#x200B;大部分AEM表單端點只允許使用可序列化類別來進行引動。 在舊版中，Remoting端點允許非序列化類別用於從Flex使用者端叫用。 為了防止APS11-15中說明的安全性弱點，已變更此設定。 如果要繼續將不可序列化的類別與Flex遠端端點搭配使用，請選取此核取方塊。

## 存放庫服務設定 {#repository-service-settings}

存放庫服務( `RepositoryService`)為AEM表單提供資源儲存和管理服務。 開發人員建立應用程式時，可以將資產部署在存放庫中，而不是部署在檔案系統上。 資產可包括任何型別的附屬資料，包括XML表單、PDF forms (包括Acrobat表單)、表單片段、影像、設定檔、原則、SWF檔案、DDX檔案、XML結構描述、WSDL檔案和測試資料。

您可以使用AEM表單隨附的預設存放庫，或使用協力廠商存放庫(EMC Documentum Content Server、IBM FileNet Content Manager或IBM Content Manager)。

存放庫提供者服務是一種服務委派，充當提供者服務的介面。 這可讓您連線至通用API，而不需知道哪個提供者服務正在實作儲存功能。 儲存區域提供者服務提供儲存區域服務資源的資料庫儲存空間。

下列設定可供存放庫服務使用。

**提供者服務：**&#x200B;用來作為儲存提供者之服務的名稱。 預設值為RepositoryProviderService。

## 簽名服務設定 {#signature-service-settings}

簽章服務( `SignatureService`)可讓您的組織保護其散發與接收之Adobe PDF檔案的安全性與隱私權。 此服務使用數位簽名和憑證來確保檔案不會遭到更改。 變更檔案會破壞其簽名。 由於安全性功能會套用至檔案本身，因此檔案在其整個生命週期內皆會保持安全及受控制；在防火牆之外，當檔案離線下載時，以及當檔案送回您的組織時。

下列設定可供簽名服務使用。

**遠端HSM SPI服務的名稱：**&#x200B;此選項適用於將HSM安裝在遠端電腦上。 當AEM表單安裝在64位元Windows上，且您使用HSM裝置進行簽署時，請指定此選項。

**遠端HSM Web服務的URL：**&#x200B;當AEM Forms安裝在64位元Windows上，而且您正在使用HSM裝置進行簽署時，請指定此選項。

**包含表單載入變更的認證：**&#x200B;選取此選項時，除了XFA範本之外，還會認證XFA表單狀態。 請注意，啟用此選項可能會對效能產生負面影響。 預設值為true。

**執行檔案JavaScript指令碼：**&#x200B;指定是否要在簽名作業期間執行檔案JavaScript指令碼。 預設值為false。

**處理具有Acrobat 9相容性的檔案：**&#x200B;指定是否啟用Acrobat 9相容性。 例如，選取此選項時，會啟用動態PDF中的「可見認證」。 預設值為false。

**簽署時嵌入撤銷資訊：**&#x200B;指定簽署PDF檔案時是否嵌入撤銷資訊。 預設值為false。

**認證時嵌入撤銷資訊：**&#x200B;指定認證PDF檔案時是否嵌入撤銷資訊。 預設值為false。

**強制嵌入所有憑證的撤銷資訊
簽署/憑證期間：**&#x200B;指定若未內嵌所有憑證的有效撤銷資訊，簽署或憑證作業是否失敗。 請注意，如果憑證未包含任何CRL或OCSP資訊，即使未擷取任何撤銷資訊，也會被視為有效。 預設值為false。

**撤銷檢查順序：**&#x200B;指定透過憑證撤銷清單(CRL)和線上憑證狀態通訊協定(OCSP)機制進行檢查時，撤銷檢查的順序。 預設值為OCSPFirst。

**撤銷封存資訊的大小上限：**&#x200B;撤銷封存資訊的大小上限（以KB為單位）。 AEM forms會嘗試在不超過限制的情況下儲存儘可能多的撤銷資訊。 預設值為10 KB。

**支援從發行前組建建立的簽章
Adobe產品：**&#x200B;選取此選項時，使用Adobe產品發行前版本建立的簽名將可正確驗證。 預設值為false。

**驗證時間選項：**&#x200B;指定簽署者憑證的驗證時間。 預設值為安全時間或目前時間。

**使用在簽名中封存的撤銷資訊
驗證：**&#x200B;指定是否使用以簽章封存的撤銷資訊進行撤銷檢查。 預設值為true。

**使用儲存在檔案中的驗證資訊
簽章驗證：**&#x200B;選取此選項時，會使用檔案中內嵌的驗證資訊（包括撤銷和時間戳記資訊）來驗證簽章。 預設值為true。

**允許的巢狀驗證工作階段數上限：**&#x200B;允許的巢狀驗證工作階段數上限。 當OCSP或CRL憑證設定不正確時，AEM Forms會在驗證OCSP或CRL簽署者憑證時使用此值來防止無限回圈。 預設值為 10。

**驗證時脈歪斜上限：**&#x200B;簽署時間可在驗證時間之後的最長時間（以分鐘為單位）。 如果時鐘歪斜大於此值，則簽章將無效。 預設值為65分鐘。

**憑證存留期快取：**&#x200B;線上或透過其他方法擷取的憑證存留期快取中。 預設值為1天。

### 傳輸選項 {#transport-options}

**Proxy主機：** Proxy主機的URL。 僅在提供某些有效值時使用。 無預設值。

**Proxy連線埠：** Proxy連線埠。 輸入從0到65535的任何有效連線埠號碼。 預設值為 80。

**Proxy登入使用者名稱：** Proxy登入使用者名稱。 只有在為Proxy主機和Proxy連線埠提供某些有效值時才使用。 無預設值。

**Proxy登入密碼：** Proxy登入密碼。 只有在為Proxy主機、Proxy連線埠和Proxy登入使用者名稱提供某些有效值時才使用。 無預設值。

**最大下載限制：**&#x200B;每個連線可接收的最大資料量(MB)。 最小值為1 MB，最大值為1024 MB。 預設值為16 MB。

**連線逾時：**&#x200B;建立新連線的等候時間上限（以秒為單位）。 最小值為1，最大值為300。 預設值為 5。

**通訊端逾時：**&#x200B;發生通訊端逾時（等待資料傳輸時）前的等待秒數時間上限。 最小值為1，最大值為3600。 預設值為 30。

### 路徑驗證選項 {#path-validation-options}

**需要明確原則：**&#x200B;指定路徑是否對至少一個與簽署者憑證的信任錨點關聯的憑證原則有效。 預設值為false。

**Inhibit ANY原則：**&#x200B;指定如果原則物件識別碼(OID)包含在憑證中，是否應該處理它。 預設值為false。

**禁止原則對應：**&#x200B;指定憑證路徑中是否允許原則對應。 預設值為false。

**檢查所有路徑：**&#x200B;指定是否應該驗證所有路徑，或是否在找到第一個有效路徑後停止驗證。 選取true或false。 預設值為false。

**LDAP伺服器：** LDAP伺服器用來查詢憑證以進行路徑驗證。 無預設值。

**追蹤憑證AIA中的URI：**&#x200B;指定在路徑探索期間是否處理憑證AIA中的統一資源識別碼(URI)。 預設值為false。

**CA憑證中需要的基本條件約束延伸：**&#x200B;指定CA憑證是否必須有憑證授權單位(CA)的基本條件約束憑證延伸。 某些早期的德國認證根憑證（7及更早版本）不符合RFC 3280，並且不包含基本限制延伸。 如果已知使用者的EE憑證鏈結到這樣的德文根，請取消選取此核取方塊。 預設值為true。

**鏈結建立期間需要有效的憑證簽章：**&#x200B;指定鏈結建立器是否需要在用來建立鏈結的憑證上需要有效的簽章。 如果選取此核取方塊，鏈產生器將不會在憑證上建置具有無效RSA簽章的鏈。 考慮鏈結CA > ICA > EE，其中CA在ICA上的簽名無效。 如果此設定為true，則鏈結建立將停止在ICA，並且CA將不會包含在鏈結中。 如果此設定為false，則會產生完整的3憑證鏈。 此設定不會影響DSA簽章。 預設值為false。

### 時間戳記提供者選項 {#timestamp-provider-options}

**TSP伺服器網址：**&#x200B;預設時間戳記提供者的URL。 僅在提供某些有效值時使用。 無預設值。

**TSP伺服器使用者名稱：**&#x200B;使用者名稱（如果時間戳記提供者需要）。 只有在為URL提供某些有效值時才使用。 無預設值。

**TSP伺服器密碼：**&#x200B;上述使用者名稱的密碼（如果時間戳記提供者需要的話）。 只有在為URL和使用者名稱提供某些有效值時才使用。 無預設值。

**要求雜湊演演算法：**&#x200B;指定在建立時間戳記提供者的要求時要使用的雜湊演演算法。 預設值為SHA1。

**撤銷檢查樣式：**&#x200B;指定用來從觀察到的撤銷狀態判斷時間戳記提供者憑證之信任狀態的撤銷檢查樣式。 預設值為BestEffort。

**傳送Nonce：**&#x200B;指定是否隨時間戳記提供者要求傳送Nonce。 Nonce可以是時間戳記、網頁上的造訪計數器，或是用來限制或防止未經授權重播或重製檔案的特殊標籤。 預設值為true。

**驗證期間使用過期時間戳記：**&#x200B;選取此選項時，可以使用過期時間戳記來擷取簽章的驗證時間。 預設值為true。

**TSP回應大小：** TSP回應的預估大小（位元組）。 此值應代表設定的時間戳記提供者可傳回的時間戳記回應大小上限。 除非您非常確定，否則請勿變更此設定。 最小值為60B，最大值為10240B。 預設值為4096B。

**忽略時間戳記伺服器延伸模組**：選取&#x200B;**忽略時間戳記伺服器延伸模組**&#x200B;選項，以停止AEM Forms伺服器連絡指定的時間戳記伺服器。 選取選項有助於避免因為AEM Forms與時間戳記伺服器之間的連線逾時而發生的處理作業失敗。

### 憑證撤銷清單選項 {#certificate-revocation-list-options}

**請先查閱本機URI：**&#x200B;指定在本機URI或CRL查詢中提供的CRL位置是否應該優先於憑證內指定的任何位置，以進行撤銷檢查。 預設值為false。

**CRL查閱的本機URI：**&#x200B;本機CRL提供者的URL。 只有當「諮詢本機URI優先」設定設為true時，才會查閱此值。 無預設值。

**撤銷檢查樣式：**&#x200B;指定撤銷檢查樣式，用來從觀察到的撤銷狀態判斷CRL提供者憑證的信任狀態。 預設值為BestEffort。

**CRL查閱的LDAP伺服器：**&#x200B;用來取得CRL的LDAP伺服器(如www.ldap.com)。 CRL的所有DN型查詢都將導向此伺服器。 無預設值。

**上線：**&#x200B;指定是否要上線以擷取CRL。 若為false，則僅會查閱快取的CRL （位於本機磁碟上或內嵌簽名的CRL）。 預設值為true。

**忽略有效日期：**&#x200B;指定是否忽略回應的thisUpdate和nextUpdate時間，以免這些時間對回應有效期間產生負面影響。 預設值為false。

**CRL中需要AKI副檔名：**&#x200B;指定CRL中是否必須包含授權金鑰識別碼副檔名。 預設值為false。

### 線上憑證狀態通訊協定選項 {#online-certificate-status-protocol-options}

**OCSP伺服器URL：**&#x200B;預設OCSP伺服器的URL。 是否使用透過此URL指定的OCSP伺服器取決於「諮詢選項」設定的URL。 無預設值。

**諮詢選項：**&#x200B;控制用於執行狀態檢查的OCSP伺服器清單和順序。 預設值為UseAIAInCert。

**撤銷檢查樣式：**&#x200B;指定驗證OCSP伺服器憑證時所使用的撤銷檢查樣式。 預設值為CheckIfAvailable。

**傳送Nonce：**&#x200B;指定Nonce是否隨OCSP要求傳送。 Nonce可以是時間戳記、網頁上的造訪計數器，或是用來限制或防止未經授權重播或重製檔案的特殊標籤。 預設值為true。

**最大時鐘歪斜時間：**&#x200B;回應時間與本機時間之間允許的最大歪斜（分鐘）。 最小值為0，最大值為2147483647m。 預設值為5m。

**回應時效性時間：**&#x200B;預先建構的OCSP回應被視為有效的最長時間（分鐘）。 最小值為1m，允許的最大值為2147483647。 預設值為525600 （一年）。

**簽署OCSP要求：**&#x200B;指定是否應簽署OCSP要求。 預設值為false。

**要求簽署者認證別名：**&#x200B;指定在啟用簽署功能時，用於簽署OCSP要求的認證別名。 僅在啟用OCSP要求簽署時使用。 無預設值。

**上線：**&#x200B;指定是否上線以進行撤銷檢查。 預設值為true。

**忽略回應的thisUpdate和nextUpdate時間：**&#x200B;指定是否忽略回應的thisUpdate和nextUpdate時間，以避免這些時間對回應有效性的負面影響。 預設值為false。

**允許OCSPNoCheck延伸模組：**&#x200B;指定回應簽署憑證中是否允許OCSPNoCheck延伸模組。 預設值為true。

**需要OCSP ISIS-MTT CertHash延伸模組：**&#x200B;指定OCSP回應中是否必須包含憑證公開金鑰雜湊延伸模組。 預設值為false。

### 偵錯的錯誤處理選項 {#error-handling-options-for-debugging}

**在下次API呼叫時清除憑證快取：**&#x200B;指定是否要在呼叫下次簽章服務作業時清除憑證快取。 呼叫作業後，此選項會設回false。 預設值為false。

**在下次API呼叫時清除CRL快取：**&#x200B;指定是否要在呼叫下次簽章服務作業時清除CRL快取。 呼叫作業後，此選項會設回false。 預設值為false。

**在下次API呼叫時清除OCSP快取：**&#x200B;指定是否要在呼叫下次簽章服務作業時清除OCSP快取。 呼叫作業後，此選項會設回false。 預設值為false。

## Watched資料夾服務設定 {#watched-folder-service-settings}

Watched資料夾服務(`WatchedFolder`)會設定所有watched資料夾端點通用的屬性。 它也會提供watched資料夾端點的預設值。 （請參閱[設定Watched資料夾端點](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)。）外部使用者端應用程式不會叫用它，或在Workbench中建立的程式中使用它。

下列設定適用於Watched資料夾服務。

**Cron運算式：** Quartz用來排程輪詢輸入目錄的Cron運算式。

**重複計數：**&#x200B;輪詢輸入目錄的次數。 如果未在端點設定中指定此值，則使用預設的重複計數。 值為–1表示無限掃描目錄。 預設值為 -1。

**重複間隔：**&#x200B;每個輪詢之間的預設秒數。 除非在watched資料夾端點設定中指定不同的值，否則此值會用作重複間隔。 預設值為 5。如需詳細資訊，請參閱「批次大小」設定的說明。

**非同步：**&#x200B;將呼叫型別識別為非同步或同步。 暫時和同步處理程式只能同步叫用。 預設值為非同步。

**等候時間：**&#x200B;從輸入資料夾擷取檔案之前的時間預設值（以秒為單位）。 如果檔案或資料夾早於等待時間中指定的時間，則會擷取該檔案或資料夾進行處理。 預設值為 0。

**批次大小：**&#x200B;每次掃描處理的檔案或資料夾數目的預設值。 預設值為 2。

「重複間隔」和「批次大小」設定決定了Watched Folder在每次掃描中擷取的檔案數。 Watched資料夾使用Quartz執行緒集區來掃描輸入資料夾。 執行緒集區與其他服務共用。 如果掃描間隔很小，執行緒會經常掃描輸入資料夾。 如果檔案經常被拖放到watched資料夾中，請將掃描間隔維持在較小的範圍內。 如果檔案不常捨棄，請使用較大的掃描間隔，讓其他服務可以使用執行緒。

如果有大量檔案被捨棄，請讓批次大小變大。 例如，如果由watched資料夾端點叫用的服務每分鐘可以處理700個檔案，而且使用者以相同的速率將檔案放入輸入資料夾，則將「批次大小」設定為350，並將「重複間隔」設定為30秒，將有助於Watched資料夾的效能，而不會產生經常掃描watched資料夾的成本。

當檔案被放入watched資料夾時，它會列出輸入中的檔案，如果每秒都進行掃描，這會降低效能。 增加掃描間隔可以改善效能。 如果捨棄的檔案量很小，請相應地調整「批次大小」和「重複間隔」。 例如，如果每秒丟棄10個檔案，請嘗試將「重複間隔」設定為1秒，並將「批次大小」設定為10。

在叢集設定中，觀察資料夾端點的批次大小不會縮放至多個叢集節點。 例如，如果雙節點叢集的批次大小設為`2`，且選取了Throttle選項，則節點會集體處理兩個批次的檔案，而不是每個節點一次處理兩個檔案。

**覆寫重複的檔案名稱：**&#x200B;布林值字串，指定是否覆寫watched資料夾的重複結果檔案名稱，以及是否應覆寫保留的同名檔案。

**保留資料夾：**&#x200B;保留資料夾的預設值。 如果成功處理輸入，則會使用此資料夾將來源檔案複製到中。 此值可以是具有檔案模式的空白、相對或絕對路徑，如「結果資料夾」設定所述。

**失敗資料夾：**&#x200B;複製失敗檔案的資料夾名稱。 此值可以是具有檔案模式的空白、相對或絕對路徑，如「結果資料夾」設定所述。

**結果資料夾：**&#x200B;結果資料夾的預設名稱。 此資料夾用於將結果檔案複製到中。 此值可以是具有下列檔案模式的空白、相對或絕對路徑。

* %F =檔案名稱前置詞
* %E =副檔名
* %Y =年（完整）
* %y =年（最後兩位數）
* %M =月
* %D =日期
* %d =一年中的第幾天
* %H =小時（24小時時鐘）
* %h =小時（12小時時鐘）
* %m =分鐘
* %s =秒
* %l =毫秒
* %R =隨機數字（從0到9）
* %P =處理程式或工作識別碼

例如，如果是2009年7月17日晚上8點，而您指定`C:/Test/WF0/failure/%Y/%M/%D/%H/`，則結果資料夾為`C:/Test/WF0/failure/2009/07/17/20`。

如果路徑不是絕對路徑而是相對路徑，則會在watched資料夾內建立資料夾。 如需檔案模式的詳細資訊，請參閱[關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。

>[!NOTE]
>
>結果資料夾的大小越小，Watched資料夾的效能就越好。 例如，如果watched資料夾的估計負載為每小時1000個檔案，請嘗試類似`result/%Y%M%D%H`的模式，以便每小時建立新的子資料夾。 如果負載較小（例如，每天1000個檔案），您可以使用類似`result/%Y%M%D`的模式。

**舞台資料夾：** watched資料夾內舞台資料夾的預設名稱。

**輸入資料夾：** watched資料夾內輸入資料夾的預設名稱。

**失敗時保留：**&#x200B;如果為True，則失敗時會將原始檔案保留在失敗資料夾中。

**節流：**&#x200B;選取此選項時，它會限制AEM在任何指定時間處理之watched資料夾工作的數目。 「批次大小」值決定作業的最大數量（請參閱關於節流）。

## Web服務設定 {#web-service-service-settings}

Web服務服務(`WebService`)可讓處理序呼叫Web服務作業。

Web服務可讓處理序呼叫Web服務作業。 例如，組織可能想要整合程式，以透過叫用服務提供者公開的Web服務來儲存和擷取資訊，例如聯絡人和帳戶詳細資訊。 Web服務會叫用指定的Web服務，並傳遞其每個引數的值。 然後，它會將操作的傳回值儲存到流程內的指定變數中。

Web服務會透過傳送和接收SOAP訊息來與Web服務互動。 此服務也支援使用WS-Attachment通訊協定，以SOAP訊息傳送MIME、MTOM和SwaRef附件。 Web服務互動與SAP系統和.NET Web服務相容。

Web服務可使用下列設定。

**金鑰存放區：**&#x200B;包含用於驗證的私密金鑰之金鑰存放區檔案的完整路徑。 Forms伺服器必須能夠存取檔案。

**金鑰庫密碼：**&#x200B;金鑰庫檔案的密碼。

**金鑰存放區型別：**&#x200B;金鑰存放區的型別。 不提供使用針對執行Forms伺服器的JVM所設定的預設金鑰存放區型別的值。 否則，請提供下列其中一個值：

* jks
* pkcs12
* cms
* jceks

**信任存放區：**&#x200B;包含Web服務伺服器公開金鑰的信任存放區檔案的完整路徑。

**信任存放區密碼：**&#x200B;信任存放區檔案的密碼。

**信任存放區型別：**&#x200B;信任存放區的型別。 不提供使用針對執行Forms伺服器的JVM所設定的預設金鑰存放區型別的值。 否則，請提供下列其中一個值：

* jks
* pkcs12
* cms
* jceks

## XSLT轉換服務設定 {#xslt-transformation-service-settings}

XSLT轉換服務(`XSLTService`)可讓處理程式在XML檔案上套用可延伸樣式表語言轉換(XSLT)。

下列設定適用於XSLT轉換服務。

**Factory名稱：**&#x200B;用來執行XSLT轉換的Java類別的完整名稱。 如果未指定值，則會使用在執行Forms伺服器的Java虛擬機器器中設定的預設處理站。

## 修改服務的安全性設定 {#modifying-security-settings-for-a-service}

Forms Server可讓您為每個服務設定安全性設定，讓您逐個服務層級設定微調存取控制。

預設安全性設定檔已安裝，然後可加以設定以符合您的系統需求。 每個安全性設定檔都有一個關聯的網域，並在使用者層級或群組層級建立。

### 修改服務的安全性設定 {#modify-security-settings-for-a-service}

1. 在Administration Console中，按一下「服務>應用程式和服務>服務管理」。
1. 在「服務管理」頁面上，按一下要設定的服務。
1. 按一下「安全性」標籤。
1. 在「需要呼叫者驗證」清單中，選取「是」或「否」以指定是否可使用認證來叫用服務。

   如果您選取[是]，必須驗證服務的呼叫者，而且必須授權該呼叫者的使用者主體來呼叫服務；否則，將會拒絕呼叫嘗試。

   如果您選取[否]，則服務的呼叫者可能會或不會通過驗證。 因為沒有授權檢查，所以服務的呼叫一律會成功。

1. 對於包含一或多個標籤為匿名存取之操作的服務，請選取或取消選取「允許匿名存取」。 啟用匿名存取時，系統內的任何使用者都可以叫用服務上的作業。 如果停用匿名存取，則必須授予使用者呼叫服務及叫用作業的許可權。 使用者可以直接獲得這些許可權，或作為具有這些許可權的群組的一部分被授予。
1. 對於某些服務，執行作業的使用者帳戶會影響結果。 例如，在Content Services （已棄用）中，儲存內容的使用者會成為內容的所有者，而這會影響後續可存取內容的使用者。 如果您使用程式來儲存內容，請考慮使用哪個使用者來執行Document Management服務，因為該使用者將擁有儲存的內容。

   若要指定服務用來執行作業的執行階段識別，請選取指定執行身分，從相關清單中選取選項，然後按一下儲存。 從下列選項中選擇：

   **叫用者：**&#x200B;使用與叫用服務之使用者相同的身分。

   **系統：**&#x200B;使用系統使用者以完整許可權執行服務。

   **具名使用者：**&#x200B;可讓您以特定使用者的身分執行服務。 選取此選項時，按一下「選取使用者」以顯示「選取主參與者」頁面，您可以在此頁面搜尋和選取使用者。

   如果您未選取「指定執行身分」，則會使用預設行為。

   >[!NOTE]
   >
   >與xfaForm、Document Form和Form變數搭配使用的轉譯和提交服務一律使用系統使用者帳戶執行。

1. 按一下「新增主體」，指定使用者和群組對此服務擁有的許可權。
1. 「選取主參與者」畫面會顯示在「使用者管理」中設定的使用者和群組。 如果未顯示您想要的使用者或群組，請使用搜尋功能來尋找它。 按一下使用者或群組名稱。
1. 在新增許可權畫面上，選取要指派給此服務之使用者或群組的許可權：

   * **INVOKE_PERM：**&#x200B;若要叫用服務上的所有作業
   * **MODIFY_CONFIG_PERM：**&#x200B;若要修改服務的設定
   * **SUPERVISOR_PERM：**&#x200B;若要檢視從處理序建立之服務的處理序執行個體資料
   * **START_STOP_PERM：**&#x200B;若要啟動和停止服務
   * **ADD_REMOVE_ENDPOINTS_PERM：**&#x200B;若要新增、移除及修改服務的端點
   * **CREATE_VERSION_PERM：**&#x200B;若要建立服務的版本
   * **DELETE_VERSION_PERM：**&#x200B;若要刪除服務的版本
   * **MODIFY_VERSION_PERM：**&#x200B;若要修改服務的版本
   * **READ_PERM：**&#x200B;檢視服務
   * **PROCESS_OWNER_PERM：**&#x200B;用於未來版本的AEM表單。 請勿使用此許可權。
   * **SERVICE_MANAGER_PERM：**&#x200B;用於未來版本的AEM表單。 請勿使用此許可權。
   * **SERVICE_AGENT_PERM：**&#x200B;用於未來版本的AEM表單。 請勿使用此許可權。

1. 按一下「新增」。

### 從安全性設定檔移除主體 {#remove-the-principal-from-a-security-profile}

1. 在「服務管理」頁面上，選取要設定的服務。
1. 按一下&#x200B;**安全性**&#x200B;標籤，選取要移除的安全性設定檔，然後按一下&#x200B;**移除**。

## 設定服務的集區 {#configuring-pooling-for-a-service}

每項服務都可以利用集區功能來處理傳入的呼叫要求。 使用服務集區可確保單一執行緒一次叫用服務執行個體，並在叫用要求間重複使用，進而改善效能。 您也可以使用集區來指定「最大非同步服務執行個體」選項，此選項可讓服務限制並行處理的要求數目。

### 啟用集區 {#enable-pooling}

1. 在Administration Console中，按一下「服務>應用程式和服務>服務管理」。
1. 在「服務管理」頁面上，按一下要設定的服務。
1. 按一下「共用」標籤。
1. 在「請求處理策略」清單中，為所有請求選取「集區執行個體」 。
1. 在「初始服務執行處理集區大小」方塊中，輸入集區的初始大小。 部署服務時，此數字可用來決定已建立並配置給可用集區、等待呼叫要求的服務實作執行個體數目。 這可讓服務容器立即回應呼叫要求，而不需要先初始化服務執行個體。
1. 在「服務執行處理集區大小上限」方塊中，輸入指定服務之集區中的執行處理數目上限。 此設定控制可在指定時間執行指定服務的執行緒數目。 預設值為0，因此產生的集區大小不受限制。
1. 在「最大非同步服務執行個體數」方塊中，輸入可用於隨時為非同步請求提供服務的集區中的最大執行個體數。 此設定可讓服務限制可並行處理的要求數目。
1. 在「呼叫等待逾時」方塊中，輸入等候服務可供呼叫要求使用的毫秒數。 如果您未指定此設定的值，預設值為0，因此不會產生等候時間。
1. 按一下「儲存」。

### 移除集區 {#remove-pooling}

1. 在Administration Console中，按一下「服務>應用程式和服務>服務管理」。
1. 在「服務管理」頁面上，按一下要設定的服務。
1. 按一下「共用」標籤。
1. 在「請求處理策略」清單中，為每個請求選取「新執行個體」，或為所有請求選取單一執行個體。

   **所有要求的單一執行個體：**&#x200B;當第一個要求進入容器時，會建立並快取服務執行個體。 請求之後的每個請求都會使用相同的服務執行個體來處理請求。

   **每個要求的新執行個體：**&#x200B;每個收到的叫用都會建立新的服務執行個體。

1. 按一下「儲存」。
