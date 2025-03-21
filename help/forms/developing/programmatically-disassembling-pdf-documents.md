---
title: 以程式設計方式分解PDF檔案
description: 使用Assembler服務，透過Java API和Web服務API將單一PDF檔案分解為多個PDF檔案。
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
hide: true
hidefromtoc: true
exl-id: 04700c18-c5fe-45c3-b9ad-16d4b427d65e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 0%

---

# 以程式設計方式分解PDF檔案 {#programmatically-disassembling-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以將PDF檔案傳遞給Assembler服務來分解。 一般來說，這項工作在PDF檔案原本由許多個別檔案建立時相當實用，例如一組陳述式。 在下圖中，DocA會分成多個結果檔案，其中頁面上的第一個第1層書籤會識別新結果檔案的開頭。

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

若要拆解PDF檔案，請確定`PDFsFromBookmarks`元素位於DDX檔案中。 `PDFsFromBookmarks`專案是結果專案，而且只能是`DDX`專案的子專案。 它沒有`result`屬性，因為它可能導致產生多個檔案。

`PDFsFromBookmarks`元素會針對來原始檔中的每個層級1書籤產生單一檔案。

為了進行此討論，假設使用下列DDX檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>閱讀本節之前，建議您先熟悉使用Assembler服務組合PDF檔案。 (請參閱[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>將單一PDF檔案傳遞至組合器服務並取回單一檔案時，您可以叫用`invokeOneDocument`作業。 不過，若要拆解PDF檔案，請使用`invokeDDX`作業，因為雖然已將一個輸入PDF檔案傳遞至組合器服務，組合器服務仍會傳回包含一或多個檔案的集合物件。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱[組合器服務與DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

若要拆分PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考PDF檔案以分解。
1. 設定執行階段選項。
1. 拆分PDF檔案。
1. 儲存已拆解的PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在受支援的J2EE應用程式伺服器（不是JBoss）上，則必須將adobe-utilities.jar和jbossall-client.jar取代為特定於已部署AEM Forms之J2EE應用程式伺服器的JAR檔案。

**建立PDF組合器使用者端**

您必須先建立組合器服務使用者端，才能以程式設計方式執行組合器作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能分解PDF檔案。 此DDX檔案必須包含`PDFsFromBookmarks`專案。

**參考PDF檔案以分解**

若要拆解PDF檔案，請參考代表要拆解PDF檔案的PDF檔案。 當傳遞至Assembler服務時，會針對檔案中的每個1級書籤傳回個別的PDF檔案。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。

**拆解PDF檔案**

在您建立Assembler服務使用者端、參考DDX檔案、參考PDF檔案以拆解並設定執行階段選項後，您可以透過叫用`invokeDDX`方法來拆解PDF檔案。 只要DDX檔案包含分解PDF檔案的指示，組合器服務就會傳回集合物件中已分解的PDF檔案。

**儲存已解壓縮的PDF檔案**

所有已拆解的PDF檔案都會在集合物件中傳回。 逐一檢視系列物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API分解PDF檔案 {#disassemble-a-pdf-document-using-the-java-api}

使用組合器服務API (Java)分解PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`AssemblerServiceClient`物件。

1. 參考現有的DDX檔案。

   * 使用它的建構函式並傳遞指定DDX檔案位置的字串值，建立代表DDX檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 參考PDF檔案以分解。

   * 使用`HashMap`建構函式建立用來儲存輸入PDF檔案的`java.util.Map`物件。
   * 使用物件的建構函式並傳遞PDF檔案的位置來建立`java.io.FileInputStream`物件以進行拆解。
   * 建立`com.adobe.idp.Document`物件並傳遞包含PDF檔案的`java.io.FileInputStream`物件以拆解。
   * 透過叫用物件的`put`方法並傳遞下列引數，將專案新增至`java.util.Map`物件：

      * 代表索引鍵名稱的字串值。 此值必須符合DDX檔案中指定的PDF來源元素的值。
      * 包含要分解之PDF檔案的`com.adobe.idp.Document`物件。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 透過叫用屬於`AssemblerOptionSpec`物件的方法，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法，然後傳遞`false`。

1. 拆分PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列必要值：

   * 代表要使用的DDX檔案的`com.adobe.idp.Document`物件
   * 包含要分解之PDF檔案的`java.util.Map`物件
   * 指定執行階段選項（包括預設字型和作業記錄層級）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件

   `invokeDDX`方法傳回`com.adobe.livecycle.assembler.client.AssemblerResult`物件，其中包含已解除組裝的PDF檔案以及發生的任何例外狀況。

1. 儲存已拆解的PDF檔案。

   若要取得已拆解的PDF檔案，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 逐一檢視`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件為止。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

**另請參閱**

[以程式設計方式分解PDF檔案](#programmatically-disassembling-pdf-documents)

[快速入門(SOAP模式)：使用Java API分解PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API分解PDF檔案 {#disassemble-a-pdf-document-using-the-web-service-api}

使用組合器服務API （Web服務）分解PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您在設定服務參考時使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立PDF組合器使用者端。

   * 使用預設建構函式建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。
   * 取得`AssemblerServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存DDX檔案。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表DDX檔案檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。

1. 參考PDF檔案以分解。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存輸入PDF檔案。 此`BLOB`物件會以引數的形式傳遞至`invokeOneDocument`。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將位元組陣列的內容指派給其`MTOM`欄位，以填入`BLOB`物件。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此集合物件是用來儲存PDF以進行拆解。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 將代表索引鍵名稱的字串值指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`key`欄位。 此值必須符合DDX檔案中指定的PDF來源元素的值。
   * 將儲存PDF檔案的`BLOB`物件指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`欄位。
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 叫用`MyMapOf_xsd_string_To_xsd_anyType`物件&#39; `Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`物件。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 將值指派給屬於`AssemblerOptionSpec`物件的資料成員，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請將`false`指派給`AssemblerOptionSpec`物件的`failOnError`欄位。

1. 拆分PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列值：

   * `BLOB`物件，代表拆解PDF檔案的DDX檔案
   * 包含PDF檔案的`MyMapOf_xsd_string_To_xsd_anyType`物件進行拆解
   * 指定執行階段選項的`AssemblerOptionSpec`物件

   `invokeDDX`方法傳回`AssemblerResult`物件，其中包含工作結果和發生的任何例外狀況。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是包含已解壓縮PDF檔案的`Map`物件。
   * 逐一檢視`Map`物件以取得每個結果檔案。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 存取其`BLOB`物件的`MTOM`屬性，以擷取代表PDF檔案的二進位資料。 這會傳回您可以寫出至PDF檔案的位元組陣列。

**另請參閱**

[以程式設計方式分解PDF檔案](#programmatically-disassembling-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
