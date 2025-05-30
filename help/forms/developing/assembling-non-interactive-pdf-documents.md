---
title: 組合非互動式PDF檔案
description: 使用非互動式PDF表單作為輸入，透過Java API和Web服務API彙編非互動式PDF檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
hide: true
hidefromtoc: true
exl-id: fc5ea2a6-79b4-436e-b5bc-c4beaf3619ee
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# 組合非互動式PDF檔案 {#assembling-non-interactive-pdf-documents}

使用互動式PDF表單作為輸入時，您可以組合非互動式PDF檔案。 也就是說，假設您有一個表單，使用者可使用該表單在欄位中輸入資料。 您可以將該表單傳遞至Assembler服務，導致Assembler服務傳回PDF檔案，以防止使用者在其欄位中輸入資料。 本檔案為非互動式PDF表單。 例如，下圖顯示代表互動式表單的貸款應用程式。

為了進行此討論，假設使用下列DDX檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

在此DDX檔案中，請注意來源屬性已指派值`inDoc`。 如果只有一個輸入PDF檔案傳遞至Assembler服務並傳回一個PDF檔案，而您叫用`invokeOneDocument`作業，請將值`inDoc`指派給PDF來源屬性。 叫用`invokeOneDocument`作業時，`inDoc`值是必須在DDX檔案中指定的預先定義金鑰。

相反地，將兩個或多個輸入PDF檔案傳遞至組合器服務時，您可以叫用`invokeDDX`作業。 在此情況下，請將輸入PDF檔案的檔案名稱指派給`source`屬性。

此DDX檔案包含`NoXFA`元素，它會指示Assembler服務傳回非互動式PDF檔案。

如果輸入PDF檔案是以Acrobat表單或靜態XFA表單為基礎，則組合器服務可組合非互動式PDF檔案，而輸出服務不會成為AEM表單安裝的一部分。 不過，如果輸入PDF檔案是動態XFA表單，則輸出服務必須是AEM表單安裝的一部分。 組裝動態XFA表單時，如果輸出服務不是AEM表單安裝的一部分，則會擲回例外狀況。 請參閱[建立檔案輸出資料流](/help/forms/developing/creating-document-output-streams.md)。

>[!NOTE]
>
>閱讀本節之前，建議您先熟悉使用Assembler服務組合PDF檔案。 本節不討論概念，例如建立包含輸入檔案的集合物件，或學習如何從傳回的集合物件中擷取結果。 (請參閱[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱[組合器服務與DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

若要組合非互動式PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考互動式PDF檔案。
1. 設定執行階段選項。
1. 組合PDF檔案。
1. 儲存非互動式PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在J2EE應用程式伺服器的JAR檔案。

**建立組合器使用者端**

您必須先建立組合器服務使用者端，才能以程式設計方式執行組合器作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDF檔案。 此DDX檔案必須包含`NoXFA`元素，這會指示Assembler服務傳回非互動式PDF檔案。

**參考互動式PDF檔案**

必須參考互動式PDF檔案並傳遞至Assembler服務，才能取回非互動式PDF檔案。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。

**組裝PDF檔案**

建立Assembler服務使用者端、參考DDX檔案、參考互動式PDF檔案，以及設定執行階段選項之後，您可以叫用`invokeOneDocument`作業。 因為只有一個輸入PDF檔案傳遞至組合器服務且傳回單一檔案，所以您可以使用`invokeOneDocument`作業（而非`invokeDDX`作業）。

**儲存非互動式PDF檔案**

如果只有單一PDF檔案傳遞至Assembler服務，Assembler服務會傳回單一檔案，而非集合物件。 也就是說，叫用`invokeOneDocument`作業時，會傳回單一檔案。 因為本節中參考的DDX檔案包含建立非互動式PDF檔案的指示，組合器服務會傳回可儲存為PDF檔案的非互動式PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API組合非互動式PDF檔案 {#assemble-a-non-interactive-pdf-document-using-the-java-api}

使用組合器服務API (Java)組合非互動式PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立組合器使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`AssemblerServiceClient`物件。

1. 參考現有的DDX檔案。

   * 使用它的建構函式並傳遞指定DDX檔案位置的字串值，建立代表DDX檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 參考互動式PDF檔案。

   * 使用物件的建構函式並傳遞互動式PDF檔案的位置，以建立`java.io.FileInputStream`物件。
   * 建立`com.adobe.idp.Document`物件並傳遞包含PDF檔案的`java.io.FileInputStream`物件。 此`com.adobe.idp.Document`物件已傳遞至`invokeOneDocument`方法。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 透過叫用屬於`AssemblerOptionSpec`物件的方法，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法，然後傳遞`false`。

1. 組合PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeOneDocument`方法，並傳遞下列值：

   * 代表DDX檔案的`com.adobe.idp.Document`物件。 確定此DDX檔案包含PDF來源專案的值`inDoc`。
   * 包含互動式PDF檔案的`com.adobe.idp.Document`物件。
   * 指定執行階段選項（包括預設字型和作業記錄層級）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件。

   `invokeOneDocument`方法傳回包含非互動式PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存非互動式PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案。 請確定您使用的是`invokeOneDocument`方法傳回的`Document`物件。

* 「快速入門(SOAP模式)：使用Java API彙編非互動式PDF檔案」

## 使用網站服務API組合非互動式PDF檔案 {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

使用組合器服務API （Web服務）組合非互動式PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立組合器使用者端。

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
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表DDX檔案檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 參考互動式PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存輸入PDF檔案。 此`BLOB`物件會以引數的形式傳遞至`invokeOneDocument`。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 將值指派給屬於`AssemblerOptionSpec`物件的資料成員，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請將`false`指派給`AssemblerOptionSpec`物件的`failOnError`資料成員。

1. 組合PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeOneDocument`方法，並傳遞下列值：

   * 代表DDX檔案的`BLOB`物件
   * 代表互動式PDF檔案的`BLOB`物件
   * 指定執行階段選項的`AssemblerOptionSpec`物件

   `invokeOneDocument`方法傳回包含非互動式PDF檔案的`BLOB`物件。

1. 儲存非互動式PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表非互動式PDF檔案檔案位置的字串值，以及用來開啟檔案的模式。
   * 建立位元組陣列，儲存`invokeOneDocument`方法傳回的`BLOB`物件內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

* 「快速入門(MTOM)：使用網站服務API彙編非互動式PDF檔案」。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
