---
title: 使用PDF公用程式
description: 使用PDF公用程式服務在PDF和XDP檔案格式之間轉換，設定和擷取PDF檔案屬性，以及操控XMP中繼資料。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Services, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 06869949-4a71-4d8a-9431-b94df13985e9
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 1%

---

# 使用PDF公用程式 {#working-with-pdf-utilities}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於PDF公用程式服務**

PDF公用程式服務可以在PDF和XDP檔案格式之間轉換、設定和擷取PDF檔案屬性，以及操控XMP中繼資料。 例如，在將PDF檔案轉換為另一種格式之前，檢查其屬性以判斷要為轉換叫用的服務作業會很有用。

您可以使用PDF公用程式服務完成這些工作：

* 將PDF檔案轉換為XDP檔案。
* 將XDP檔案轉換為PDF檔案。 (請參閱[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)。)
* 擷取PDF檔案屬性。 (請參閱[擷取PDF檔案屬性](pdf-utilities.md#retrieving-pdf-document-properties)。)
* 儲存PDF檔案並將其最佳化，以快速進行網頁檢視。 (請參閱[設定PDF檔案儲存模式](pdf-utilities.md#setting-pdf-document-save-modes)。)

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PDF檔案轉換為XDP檔案 {#converting-pdf-documents-into-xdp-documents}

您可以使用PDF公用程式Java和Web服務API，以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將PDF檔案轉換為XDP檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService使用者端
1. 叫用PDF到XDP轉換操作。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService使用者端**

您必須先建立PDFUtilityService使用者端，才能以程式設計方式執行「PDF公用程式」作業。 使用Java API時，可藉由建立`PDFUtilityServiceClient`物件來完成。 使用Web服務API時，可使用`PDFUtilityServiceService`物件來完成。

**叫用PDF到XDP轉換作業**

建立服務使用者端後，您可以叫用PDF到XDP的轉換操作。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用網站服務API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將PDF檔案轉換為XDP檔案 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

使用PDF公用程式API (Java)將PDF檔案轉換為XDP檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`PDFUtilityServiceClient`物件。

1. 叫用PDF到XDP轉換操作

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`convertPDFtoXDP`方法，並傳入代表PDF檔案的`com.adobe.idp.Document`物件。 此方法會傳回代表新建立之XDP檔案的`com.adobe.idp.Document`物件。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將PDF檔案轉換為XDP檔案 {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

使用PDF公用程式API （Web服務）將PDF檔案轉換為XDP檔案：

1. 包含專案檔案

   * 建立使用Microsoft公用程式服務WSDL檔案的PDF .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立PDFUtilityService客戶端

   使用您的Proxy類別建構函式建立`PDFUtilityServiceService`物件。

1. 叫用PDF到XDP轉換操作

   叫用`PDFUtilityServiceService`物件的`convertPDFtoXDP`方法，並傳入代表PDF檔案的`BLOB`物件。 此方法會傳回代表新建立之XDP檔案的`BLOB`物件。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 將XDP檔案轉換為PDF檔案 {#converting-xdp-documents-into-pdf-documents}

您可以使用PDF公用程式Java和Web服務API，以程式設計方式將XDP檔案轉換為PDF檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要將XDP檔案轉換為PDF檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService使用者端
1. 叫用XDP到PDF的轉換操作。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService使用者端**

您必須先建立PDFUtilityService使用者端，才能以程式設計方式執行「PDF公用程式」作業。 使用Java API時，可藉由建立`PDFUtilityServiceClient`物件來完成。 使用Web服務API時，可使用`PDFUtilityServiceService`物件來完成。

**叫用XDP到PDF的轉換作業**

建立服務使用者端後，您可以叫用XDP到PDF的轉換操作。

**另請參閱**

[使用Java API將XDP檔案轉換為PDF檔案](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[使用網站服務API將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將XDP檔案轉換為PDF檔案 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

使用PDF Utilities API (Java)將XDP檔案轉換為PDF檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`PDFUtilityServiceClient`物件。

1. 叫用XDP至PDF轉換操作

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`convertXDPtoPDF`方法，並傳入代表XDP檔案的`com.adobe.idp.Document`物件。 此方法會傳回代表新建立PDF檔案的`com.adobe.idp.Document`物件。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將XDP檔案轉換為PDF檔案 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

使用PDF公用程式API （Web服務API）將XDP檔案轉換為PDF檔案：

1. 包含專案檔案

   * 建立使用Microsoft公用程式服務WSDL檔案的PDF .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立PDFUtilityService客戶端

   使用您的Proxy類別建構函式建立`PDFUtilityServiceService`物件。

1. 叫用XDP至PDF轉換操作

   若要執行轉換，請叫用`PDFUtilityServiceService`物件的`convertXDPtoPDF`方法，並傳入代表XDP檔案的`BLOB`物件。 此方法會傳回代表新建立PDF檔案的`BLOB`物件。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 擷取PDF檔案屬性 {#retrieving-pdf-document-properties}

您可以使用PDF公用程式Java和Web服務API以程式設計方式擷取PDF檔案屬性，例如檔案是可填寫的表單還是讀取檔案所需的最低Acrobat版本。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟摘要 {#summary_of_steps-2}

若要擷取PDF檔案屬性，請執行下列步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService使用者端
1. 叫用屬性擷取作業。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService使用者端**

您必須先建立PDFUtilityService使用者端，才能以程式設計方式執行「PDF公用程式」作業。 使用Java API時，可藉由建立`PDFUtilityServiceClient`物件來完成。 使用Web服務API時，可使用`PDFUtilityServiceService`物件來完成。

**叫用屬性擷取作業**

建立服務使用者端之後，您可以叫用屬性擷取作業。

**另請參閱**

[使用Java API擷取PDF檔案屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[使用Web服務API擷取PDF檔案屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API擷取PDF檔案屬性 {#retrieve-pdf-document-properties-using-the-java-api}

使用PDF公用程式API (Java)擷取PDF檔案屬性：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`PDFUtilityServiceClient`物件。

1. 叫用屬性擷取作業

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`getPDFProperties`方法，並傳入下列專案：

   * 代表PDF檔案的`com.adobe.idp.Document`物件。
   * 包含要評估之屬性的`PDFPropertiesOptionSpec`物件。

   方法傳回包含查詢結果的`PDFPropertiesResult`物件。

**另請參閱**

[擷取PDF檔案屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API擷取PDF檔案屬性 {#retrieve-pdf-document-properties-using-the-web-service-api}

使用PDF公用程式Web服務API擷取PDF檔案屬性：

1. 包含專案檔案

   * 建立使用Microsoft公用程式服務WSDL檔案的PDF .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立PDFUtilityService客戶端

   使用您的Proxy類別建構函式建立`PDFUtilityServiceService`物件。

1. 叫用屬性擷取作業

   若要執行轉換，請叫用`PDFUtilityServiceService`物件的`getPDFProperties`方法，並傳入下列專案：

   * 代表PDF檔案的`BLOB`物件。
   * 包含要評估之屬性的`PDFPropertiesOptionSpec`物件。

   方法傳回包含查詢結果的`PDFPropertiesResult`物件。

**另請參閱**

[擷取PDF檔案屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 設定PDF檔案儲存模式 {#setting-pdf-document-save-modes}

您可以使用PDF公用程式服務Java和Web服務API，以程式設計方式設定PDF檔案的儲存模式。 使用PDF公用程式服務設定儲存模式時，PDF公用程式服務只會設定儲存模式，實際上並不儲存PDF檔案。 PDF檔案在傳遞至其他服務作業時便會儲存。 例如，您可以使用PDF公用程式服務來設定特定的儲存模式，並將其傳遞至加密服務，以實際儲存和加密PDF檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

若要設定PDF檔案的儲存選項，請執行下列步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService使用者端
1. 設定儲存模式。
1. 叫用儲存作業。
1. 將PDF檔案傳遞至另一個作業。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService使用者端**

您必須先建立PDFUtilityService使用者端，才能以程式設計方式執行「PDF公用程式」作業。 使用Java API時，可藉由建立`PDFUtilityServiceClient`物件來完成。 使用Web服務API時，可使用`PDFUtilityServiceService`物件來完成。

**設定儲存模式**

您可以選擇下列其中一個儲存選項：

* `INCREMENTAL`：若要遞增儲存，以減少儲存所需的時間
* `FAST_WEB_VIEW`：儲存以供快速網頁檢視
* `FULL`：若要使用完整儲存進行儲存（沒有最佳化）

**叫用儲存樣式作業**

建立服務使用者端之後，您可以叫用屬性擷取作業。

**將PDF檔案傳遞給另一個AEM Forms作業**

PDF公用程式服務設定指定的儲存模式後，請將PDF檔案傳遞至另一個AEM Forms作業。 從操作返回後，PDF檔案會以指定模式儲存。 例如，如果您使用PDF Utilities服務設定`FAST_WEB_VIEW`模式，然後將PDF檔案傳遞給加密服務的`encryptUsingPassword`作業，則傳回的PDF檔案會以密碼加密，並儲存為`FAST_WEB_VIEW`模式。

>[!NOTE]
>
>與此區段關聯的快速入門會設定`FAST_WEB_VIEW`模式，然後將PDF檔案傳遞給加密服務的`encryptUsingPassword`作業。

**另請參閱**

[使用Java API設定PDF檔案儲存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[使用Web服務API設定PDF檔案儲存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API設定PDF檔案儲存選項 {#set-pdf-document-save-options-using-the-java-api}

使用PDF公用程式API (Java)設定PDF檔案儲存選項：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`PDFUtilityServiceClient`物件。

1. 設定儲存模式

   * 使用物件的建構函式建立`PDFUtilitySaveMode`物件。
   * 透過叫用`PDFUtilitySaveMode`物件的`setSaveStyle`方法並傳遞指定儲存模式的字串值來設定儲存模式。 例如，若要儲存以快速檢視網頁，請傳遞`FAST_WEB_VIEW`。

1. 叫用儲存樣式作業

   叫用`PDFUtilityServiceClient`物件的`setSaveMode`方法，並傳遞下列值：

   * 代表PDF檔案的`com.adobe.idp.Document`物件。
   * 包含要使用的儲存樣式的`PDFUtilitySaveMode`物件。
   * Boolean值，用來決定是否覆寫先前的設定。

   此方法會傳回使用指定儲存樣式格式化的`com.adobe.idp.Document`物件。

1. 將PDF檔案傳遞至另一個AEM Forms作業

   * 將傳回的`com.adobe.idp.Document`物件傳遞給另一個AEM Forms作業。

**另請參閱**

[設定PDF檔案儲存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API設定PDF檔案儲存選項 {#set-pdf-document-save-options-using-the-web-service-api}

使用PDF公用程式AP （Web服務）設定PDF檔案儲存選項：

1. 包含專案檔案

   * 建立使用Microsoft公用程式服務WSDL檔案的PDF .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立PDFUtilityService客戶端

   使用您的Proxy類別建構函式建立`PDFUtilityServiceService`物件。

1. 設定儲存模式

   * 使用物件的建構函式建立`PDFUtilitySaveMode`物件。
   * 將字串值指派給`PDFUtilitySaveMode`物件指定儲存模式的`saveStyle`方法，以設定儲存模式。 例如，若要儲存以快速檢視網頁，請指定`FAST_WEB_VIEW`。

1. 叫用儲存樣式作業

   叫用`PDFUtilityServiceService`物件的`setSaveMode`方法，並傳遞下列值：

   * 代表PDF檔案的`BLOB`物件。
   * 包含要使用的儲存樣式的`PDFUtilitySaveMode`物件。
   * Boolean值，用來決定是否覆寫先前的設定。

   此方法會傳回使用指定儲存樣式格式化的`BLOB`物件。 然後您可以將該物件儲存為PDF檔案。

1. 將PDF檔案傳遞至另一個Forms作業

   * 將傳回的`BLOB`物件傳遞給另一個AEM Forms作業。

**另請參閱**

[設定PDF檔案儲存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 淨化PDF檔案 {#sanitizing-pdf-documents}

您可以使用PDF公用程式Java API以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

若要處理PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService使用者端
1. 叫用清理作業。

**包含專案檔**

將必要的檔案納入您的開發專案中。 若要使用Java建立使用者端應用程式，請包含必要的JAR檔案。

**建立PDFUtilityService使用者端**

您必須先建立PDFUtilityService使用者端，才能以程式設計方式執行清理作業。 使用Java API時，可藉由建立`PDFUtilityServiceClient`物件來完成。

**叫用PDF到XDP轉換作業**

建立服務使用者端後，您可以叫用清理作業。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用網站服務API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API處理PDF檔案 {#sanitize-pdf-documents-using-the-java-api}

使用PDF公用程式API (Java)整理檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`PDFUtilityServiceClient`物件。

1. 叫用PDF到XDP轉換操作

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`convertPDFtoXDP`方法，並傳入代表PDF檔案的`com.adobe.idp.Document`物件。 此方法會傳回代表新建立之XDP檔案的`com.adobe.idp.Document`物件。

**另請參閱**

[淨化PDF檔案](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
