---
title: 使用SubmittedXML資料建立PDF檔案
description: 使用Forms服務來擷取使用者在互動式表單中輸入的表單資料。 將表單資料傳遞至另一個AEM Forms服務作業，並使用資料建立PDF檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Services, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 66736a58-b2ef-404e-b94c-9bc407828359
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---

# 使用已提交的XML資料建立PDF檔案 {#creating-pdf-documents-with-submittedxml-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 使用已提交的XML資料建立PDF檔案 {#creating-pdf-documents-with-submitted-xml-data}

讓使用者填寫互動式表單的網頁式應用程式，需要將資料提交回伺服器。 使用Forms服務，您可以擷取使用者在互動式表單中輸入的表單資料。 然後，您可以將表單資料傳遞至另一個AEM Forms服務操作，並使用資料建立PDF檔案。

>[!NOTE]
>
>在閱讀本內容之前，建議您務必瞭解如何處理已提交的表單。 處理提交的Forms中會說明一些概念，例如表單設計與提交的XML資料之間的關係。

請考量下列涉及三個AEM Forms服務的工作流程：

* 使用者從網頁型應用程式將XML資料提交至Forms服務。
* Forms服務用於處理提交的表單並擷取表單欄位。 可以處理表單資料。 例如，資料可以提交至企業資料庫。
* 表單資料會傳送至輸出服務，以建立非互動式PDF檔案。
* 非互動式PDF檔案會儲存在Content Services中（已棄用）。

下圖提供此工作流程的視覺化表示法。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

使用者從使用者端Web瀏覽器提交表單後，非互動式PDF檔案會儲存在內容服務中（已棄用）。 下圖顯示儲存在Content Services （已棄用）中的PDF檔案。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 步驟摘要 {#summary-of-steps}

若要使用提交的XML資料建立非互動式PDF檔案，並將其儲存在內容服務（已棄用）的PDF檔案中，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms、輸出和檔案管理物件。
1. 使用Forms服務擷取表單資料。
1. 使用輸出服務建立非互動式PDF檔案。
1. 使用檔案管理服務將PDF表單儲存在內容服務（已棄用）中。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms、輸出和檔案管理物件**

在您以程式設計方式執行Forms服務API作業之前，請先建立Forms使用者端API物件。 同樣地，由於此工作流程會叫用「輸出」和「檔案管理」服務，因此請建立「輸出使用者端API」物件和「檔案管理使用者端API」物件。

**使用Forms服務擷取表單資料**

擷取提交至Forms服務的表單資料。 您可以處理提交的資料，以符合您的業務需求。 例如，您可以將表單資料儲存在企業資料庫中。 不過，若要建立非互動式PDF檔案，表單資料會傳遞至Output服務。

**使用輸出服務建立非互動式PDF檔案。**

使用輸出服務來建立以表單設計和XML表單資料為基礎的非互動式PDF檔案。 在工作流程中，會從Forms服務擷取表單資料。

**使用Document Management服務，將PDF表單儲存在Content Services （已棄用）**

使用檔案管理服務API將PDF檔案儲存在內容服務中（已棄用）。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### 使用Java API建立包含已提交XML資料的PDF檔案 {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

使用Forms、輸出和檔案管理API (Java)，建立包含已提交XML資料的PDF檔案：

1. 包含專案檔案

   在您的Java專案類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar、adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立Forms、輸出和檔案管理物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormsServiceClient`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentManagementServiceClientImpl`物件。

1. 使用Forms服務擷取表單資料

   * 叫用`FormsServiceClient`物件的`processFormSubmission`方法，並傳遞下列值：

      * 包含表單資料的`com.adobe.idp.Document`物件。
      * 字串值，指定環境變數，包括所有相關的HTTP標題。 為`CONTENT_TYPE`環境變數指定一或多個值，以指定要處理的內容型別。 例如，若要處理XML資料，請為此引數指定下列字串值： `CONTENT_TYPE=text/xml`。
      * 字串值，指定`HTTP_USER_AGENT`標頭值，例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存執行階段選項的`RenderOptionsSpec`物件。

     `processFormSubmission`方法傳回包含表單提交結果的`FormsResult`物件。

   * 判斷Forms服務是否已透過叫用`FormsResult`物件的`getAction`方法來完成表單資料的處理。 如果此方法傳回值`0`，資料即可處理。
   * 透過呼叫`FormsResult`物件的`getOutputContent`方法建立`com.adobe.idp.Document`物件來擷取表單資料。 （此物件包含可傳送至Output服務的表單資料。）
   * 呼叫`java.io.DataInputStream`建構函式並傳遞`com.adobe.idp.Document`物件以建立`java.io.InputStream`物件。
   * 呼叫靜態`org.w3c.dom.DocumentBuilderFactory`物件的`newInstance`方法，以建立`org.w3c.dom.DocumentBuilderFactory`物件。
   * 呼叫`org.w3c.dom.DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立`org.w3c.dom.DocumentBuilder`物件。
   * 呼叫`org.w3c.dom.DocumentBuilder`物件的`parse`方法並傳遞`java.io.InputStream`物件，以建立`org.w3c.dom.Document`物件。
   * 擷取XML檔案中每個節點的值。 完成此工作的一種方式是建立接受兩個引數的自訂方法： `org.w3c.dom.Document`物件以及您要擷取其值的節點名稱。 此方法會傳回代表節點值的字串值。 在此程式之後的程式碼範例中，此自訂方法稱為`getNodeText`。 會顯示此方法的內文。

1. 使用輸出服務建立非互動式PDF檔案。

   叫用`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定表單設計的名稱。 確認表單設計與從Forms服務擷取的表單資料相容。
   * 字串值，指定表單設計所在的內容根。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`com.adobe.idp.Document`物件。 請確定`FormsResult`物件的`getOutputContent`方法已傳回此物件。
   * `generatePDFOutput`方法傳回包含作業結果的`OutputResult`物件。
   * 叫用`OutputResult`物件的`getGeneratedDoc`方法，擷取非互動式PDF檔案。 此方法會傳回代表非互動式PDF檔案的`com.adobe.idp.Document`執行個體。

1. 使用檔案管理服務將PDF表單儲存在內容服務（已棄用）中

   叫用`DocumentManagementServiceClientImpl`物件的`storeContent`方法並傳遞下列值以新增內容：

   * 字串值，指定新增內容的存放區。 預設存放區為`SpacesStore`。 此值為必要引數。
   * 字串值，指定新增內容的空間完整路徑（例如`/Company Home/Test Directory`）。 此值為必要引數。
   * 代表新內容的節點名稱（例如，`MortgageForm.pdf`）。 此值為必要引數。
   * 字串值，指定節點型別。 若要新增內容(例如PDF檔案)，請指定`{https://www.alfresco.org/model/content/1.0}content`。 此值為必要引數。
   * 代表內容的`com.adobe.idp.Document`物件。 此值為必要引數。
   * 字串值，指定編碼值（例如，`UTF-8`）。 此值為必要引數。
   * 指定如何處理版本資訊的`UpdateVersionType`列舉值(例如，`UpdateVersionType.INCREMENT_MAJOR_VERSION`以遞增內容版本。 )此值是必要引數。
   * 指定內容相關方面的`java.util.List`執行個體。 此值是選用引數，您可以指定`null`。
   * 儲存內容屬性的`java.util.Map`物件。

   `storeContent`方法傳回描述內容的`CRCResult`物件。 例如，您可以使用`CRCResult`物件來取得內容的唯一識別碼值。 若要執行此工作，請叫用`CRCResult`物件的`getNodeUuid`方法。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
