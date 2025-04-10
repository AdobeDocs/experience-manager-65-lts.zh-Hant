---
title: 最佳化Forms服務的效能
description: 在呈現表單時設定執行階段選項，並將XDP檔案儲存在存放庫中，以最佳化Forms服務的效能。
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
exl-id: 63ddfd09-17b5-48b4-b7ee-961f2bdd2ae2
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# 最佳化Forms服務的效能 {#optimizing-the-performance-of-theforms-service}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 最佳化Forms服務的效能 {#optimizing-the-performance-of-the-forms-service}

轉譯表單時，您可以設定執行階段選項，以最佳化Forms服務的效能。 另一個您可以執行以改善Forms服務效能的工作是將XDP檔案儲存在存放庫中。 不過，本節並未說明如何執行此工作。 （請參閱[使用Java使用者端程式庫叫用服務](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)。）

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要最佳化Forms服務在呈現表單時的效能，請執行以下工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 設定效能執行階段選項。
1. 演算表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API作業。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms Web服務API，請建立`FormsService`物件。

**設定效能執行階段選項**

您可以設定下列效能執行階段選項，以改善Forms服務的效能：

* **表單快取**：您可以在伺服器快取中快取轉譯為PDF的表單。 每個表單在首次產生後都會進行快取。 在後續轉譯時，如果快取表單比表單設計的時間戳記新，則會從快取中擷取表單。 透過快取表單，您可以改善Forms服務的效能，因為它不需要從存放庫擷取表單設計。
* 表單參考線（已棄用）的轉譯時間可能比其他轉換型別長。 建議您快取表單參考線（已棄用）以提高效能。
* **獨立選項**：如果您不需要Forms服務來執行伺服器端計算，您可以將「獨立」選項設為`true`，這會產生沒有狀態資訊的表單轉譯。 如果您想要將互動式表單轉譯給一般使用者，然後這些使用者在表單中輸入資訊，並將表單提交回Forms服務，則需要狀態資訊。 Forms服務接著會執行計算操作，並將表單轉譯回使用者，結果會顯示在表單中。 如果將沒有狀態資訊的表單提交回Forms服務，則只有XML資料可用，並且不會執行伺服器端計算。
* **線性化PDF**：已組織線性化PDF檔案，以在網路環境中啟用有效的增量存取。 PDF檔案在所有方面都是有效的PDF，且與所有現有檢視器和其他PDF應用程式相容。 也就是說，線性PDF可在下載時進行檢視。
* 此選項無法改善使用者端上轉譯PDF表單時的效能。
* **GuideRSL選項**：啟用使用執行階段共用程式庫產生表單指南（已棄用）。 這表示第一個要求會下載較小的SWF檔案，以及儲存在瀏覽器快取中的較大共用程式庫。 如需詳細資訊，請參閱Flex檔案中的RSL 。
* 您也可以在使用者端上呈現表單，以改善Forms服務的效能。 (請參閱[在使用者端轉譯Forms](/help/forms/developing/rendering-forms-client.md)。)

**轉譯表單**

若要在設定效能選項後轉譯表單，您可以使用與轉譯沒有效能選項的表單相同的應用程式邏輯。

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務轉譯表單後，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流。 寫入使用者端網頁瀏覽器時，使用者可看見表單。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將Forms轉譯為HTML](/help/forms/developing/rendering-forms-html.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API最佳化效能 {#optimize-the-performance-using-the-java-api}

使用Forms API (Java)呈現具有最佳化效能的表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormsServiceClient`物件。

1. 設定效能執行階段選項

   * 使用物件的建構函式建立`PDFFormRenderSpec`物件。
   * 透過叫用`PDFFormRenderSpec`物件的`setCacheEnabled`方法並傳遞`true`來設定表單快取選項。
   * 透過叫用`PDFFormRenderSpec`物件的`setLinearizedPDF`方法並傳遞`true.`來設定線性化選項

1. 演算表單

   叫用`FormsServiceClient`物件的`renderPDFForm`方法，並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。
   * 包含要與表單合併之資料的`com.adobe.idp.Document`物件。 如果您不想合併資料，請傳遞空的`com.adobe.idp.Document`物件。
   * 儲存執行階段選項以改善效能的`PDFFormRenderSpec`物件。
   * 包含Forms服務所需URI值的`URLSpec`物件。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。

   `renderPDFForm`方法傳回`FormsResult`物件，其中包含必須寫入使用者端網頁瀏覽器的表單資料流。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立用來傳送表單資料流至使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件。
   * 呼叫`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 呼叫`InputStream`物件的`read`方法，並將位元組陣列作為引數傳遞，以建立位元組陣列並以表單資料串流填入。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[快速入門(SOAP模式)：使用Java API最佳化效能](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API最佳化效能 {#optimize-the-performance-using-the-web-service-api}

使用Forms API （Web服務）呈現具有最佳化效能的表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立`FormsService`物件並設定驗證值。

1. 設定效能執行階段選項

   * 使用物件的建構函式建立`PDFFormRenderSpec`物件。
   * 呼叫`PDFFormRenderSpec`物件的`setCacheEnabled`方法並傳遞true，以設定表單快取選項。
   * 透過叫用`PDFFormRenderSpec`物件的`setStandAlone`方法並傳遞true來設定獨立選項。
   * 呼叫`PDFFormRenderSpec`物件的`setLinearizedPDF`方法並傳遞true，以設定線性化的選項。

1. 演算表單

   叫用`FormsService`物件的`renderPDFForm`方法，並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。
   * 包含要與表單合併之資料的`BLOB`物件。 如果您不想合併資料，請傳遞`null`。
   * 儲存執行階段選項的`PDFFormRenderSpecc`物件。
   * 包含Forms服務所需URI值的`URLSpec`物件。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。
   * 方法填入的空白`com.adobe.idp.services.holders.BLOBHolder`物件。 這是用來儲存轉譯的PDF表單。
   * 方法填入的空白`javax.xml.rpc.holders.LongHolder`物件。 （此引數會儲存表單中的頁數）。
   * 方法填入的空白`javax.xml.rpc.holders.StringHolder`物件。 （此引數將會儲存地區設定值）。
   * 包含此作業結果的空白`com.adobe.idp.services.holders.FormsResultHolder`物件。

   `renderPDFForm`方法會將必須寫入使用者端網頁瀏覽器的表單資料流，填入作為最後一個引數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 取得`com.adobe.idp.services.holders.FormsResultHolder`物件之`value`資料成員的值，以建立`FormResult`物件。
   * 建立用來傳送表單資料流至使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 建立位元組陣列，並透過叫用`BLOB`物件的`getBinaryData`方法來填入該陣列。 此工作會將`FormsResult`物件的內容指派給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
