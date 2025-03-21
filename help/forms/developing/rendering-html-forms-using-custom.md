---
title: 使用自訂CSS檔案轉譯HTML Forms
description: 使用Forms服務來參照自訂CSS檔案，以轉譯HTML表單，以回應來自網頁瀏覽器的HTTP請求。 您可以使用Java API和網頁服務API呈現使用CSS檔案的HTML表單。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: b70404ee-21dc-4c0b-a66f-c37a6f29f98e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 0%

---

# 使用自訂CSS檔案轉譯HTML Forms {#rendering-html-forms-using-custom-css-files}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

Forms服務會根據來自網頁瀏覽器的HTTP請求轉譯HTML表單。 呈現HTML表單時，Forms服務可參考自訂CSS檔案。 您可以建立自訂CSS檔案來符合業務需求，並在使用Forms服務轉譯HTML表單時參考該CSS檔案。

Forms服務會以無訊息方式剖析自訂CSS檔案。 也就是說，Forms服務不會報告在自訂CSS檔案不符合CSS標準時可能遇到的錯誤。 在此情況下，Forms服務會忽略樣式，繼續處理CSS檔案中的其餘樣式。

下列清單指定自訂CSS檔案支援的樣式：

* **類別層級選取器樣式配對**：如果存在於自訂CSS檔案中，則會使用HTML表單中作為類別樣式使用的選取器。 未使用的類別樣式會被忽略。
* **識別項層級選擇器樣式配對**：如果所有識別項樣式都用於HTML表單，則會使用這些樣式。
* **元素層級選取器樣式配對**：所有元素樣式都會在HTML表單中使用。
* **樣式優先順序**：樣式優先順序（如重要）受到支援，並且可用於自訂CSS檔案中。
* **媒體型別**：一或多個選擇器樣式配對可以包裝在@media樣式中，以定義媒體型別。 Forms服務不會檢查指定的媒體型別是否受支援。 自訂CSS檔案中指定的媒體型別會合併為HTML表單。

您可以使用FormsIVS應用程式擷取範例CSS檔案。 上傳表單，在「測試表單設計」頁面中選取表單，然後按一下「產生CSS」。 按一下按鈕之前，您不需要設定HTML轉換型別。 接著選取「儲存」。 您可以編輯此CSS檔案以符合您的業務需求。

>[!NOTE]
>
>呈現使用自訂CSS檔案的HTML表單前，請務必充分瞭解如何呈現HTML表單。 (請參閱[將Forms轉譯為HTML](/help/forms/developing/rendering-forms-html.md)。)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

若要呈現使用CSS檔案的HTML表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms Java API物件。
1. 參考CSS檔案。
1. 呈現HTML表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms Java API物件**

您必須先建立Forms使用者端物件，才能以程式設計方式執行Forms服務支援的操作。

**參考CSS檔案**

若要呈現使用自訂CSS檔案的HTML表單，請確定您參考現有的CSS檔案。

**轉譯HTML表單**

若要呈現HTML表單，請指定在Designer中建立並儲存為XDP檔案的表單設計。 選取HTML轉換型別。 例如，您可以指定轉譯Internet Explorer 5.0或更新版本之動態HTML的HTML轉換型別。

呈現HTML表單也需要值，例如呈現其他表單型別所需的URI值。

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務轉譯HTML表單時，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流，才能讓使用者看到HTML表單。

**另請參閱**

[呈現使用CSS檔案的HTML表單（使用Java API）](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將Forms轉譯為HTML](/help/forms/developing/rendering-forms-html.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 呈現使用CSS檔案的HTML表單（使用Java API） {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

使用Forms API (Java)呈現使用自訂CSS檔案的HTML表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms Java API物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormsServiceClient`物件。

1. 參考CSS檔案

   * 使用物件的建構函式建立`HTMLRenderSpec`物件。
   * 若要呈現使用自訂CSS檔案的HTML表單，請叫用`HTMLRenderSpec`物件的`setCustomCSSURI`方法，並傳遞指定CSS檔案位置和名稱的字串值。

1. 呈現HTML表單

   叫用`FormsServiceClient`物件的`(Deprecated) (Deprecated) renderHTMLForm`方法，並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML喜好設定型別的`TransformTo`列舉值。 例如，若要呈現與適用於Internet Explorer 5.0或更新版本的動態HTML相容的HTML表單，請指定`TransformTo.MSDHTML`。
   * 包含要與表單合併之資料的`com.adobe.idp.Document`物件。 如果您不想合併資料，請傳遞空的`com.adobe.idp.Document`物件。
   * 儲存HTML執行階段選項的`HTMLRenderSpec`物件。
   * 字串值，指定`HTTP_USER_AGENT`標頭值，例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * `URLSpec`物件儲存轉譯HTML表單所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。

   `(Deprecated) renderHTMLForm`方法傳回`FormsResult`物件，其中包含必須寫入使用者端網頁瀏覽器的表單資料流。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件。
   * 透過叫用物件的`getContentType`方法，取得`com.adobe.idp.Document`物件的內容型別。
   * 透過叫用其`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容型別來設定`javax.servlet.http.HttpServletResponse`物件的內容型別。
   * 呼叫`javax.servlet.h\ttp.HttpServletResponse`物件的`getOutputStream`方法，建立用來將表單資料流寫入使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 呼叫`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 呼叫`InputStream`物件的`read`方法，並將位元組陣列作為引數傳遞，以建立位元組陣列並以表單資料串流填入。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[使用自訂CSS檔案轉譯HTML Forms](#rendering-html-forms-using-custom-css-files)

[快速入門(SOAP模式)：透過Java API呈現使用CSS檔案的HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API呈現使用CSS檔案的HTML表單 {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

使用HTML API （網頁服務）呈現使用自訂CSS檔案的Forms表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 在類別路徑中包含Java Proxy類別。

1. 建立Forms Java API物件

   建立`FormsService`物件並設定驗證值。

1. 參考CSS檔案

   * 使用物件的建構函式建立`HTMLRenderSpec`物件。
   * 若要呈現使用自訂CSS檔案的HTML表單，請叫用`HTMLRenderSpec`物件的`setCustomCSSURI`方法，並傳遞指定CSS檔案位置和名稱的字串值。

1. 呈現HTML表單

   叫用`FormsService`物件的`(Deprecated) renderHTMLForm`方法，並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML喜好設定型別的`TransformTo`列舉值。 例如，若要呈現與適用於Internet Explorer 5.0或更新版本的動態HTML相容的HTML表單，請指定`TransformTo.MSDHTML`。
   * 包含要與表單合併之資料的`BLOB`物件。 如果您不想合併資料，請傳遞`null`。 (請參閱[使用可流動配置預先填入Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
   * 儲存HTML執行階段選項的`HTMLRenderSpec`物件。
   * 字串值，指定`HTTP_USER_AGENT`標頭值，例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果您不想設定此值，可以傳遞空字串。
   * `URLSpec`物件儲存轉譯HTML表單所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。
   * 由`(Deprecated) renderHTMLForm`方法填入的空白`com.adobe.idp.services.holders.BLOBHolder`物件。 此引數值會儲存演算後的表單。
   * 由`(Deprecated) renderHTMLForm`方法填入的空白`com.adobe.idp.services.holders.BLOBHolder`物件。 此引數會儲存輸出XML資料。
   * 由`(Deprecated) renderHTMLForm`方法填入的空白`javax.xml.rpc.holders.LongHolder`物件。 此引數會儲存表單中的頁數。
   * 由`(Deprecated) renderHTMLForm`方法填入的空白`javax.xml.rpc.holders.StringHolder`物件。 此引數會儲存地區設定值。
   * 由`(Deprecated) renderHTMLForm`方法填入的空白`javax.xml.rpc.holders.StringHolder`物件。 此引數會儲存所使用的HTML演算值。
   * 包含此作業結果的空白`com.adobe.idp.services.holders.FormsResultHolder`物件。

   `(Deprecated) renderHTMLForm`方法會將必須寫入使用者端網頁瀏覽器的表單資料流，填入作為最後一個引數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 取得`com.adobe.idp.services.holders.FormsResultHolder`物件之`value`資料成員的值，以建立`FormResult`物件。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 透過叫用物件的`getContentType`方法，取得`BLOB`物件的內容型別。
   * 透過叫用其`setContentType`方法並傳遞`BLOB`物件的內容型別來設定`javax.servlet.http.HttpServletResponse`物件的內容型別。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立用來將表單資料流寫入使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 建立位元組陣列，並透過叫用`BLOB`物件的`getBinaryData`方法來填入該陣列。 此工作會將`FormsResult`物件的內容指派給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[使用自訂CSS檔案轉譯HTML Forms](#rendering-html-forms-using-custom-css-files)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
