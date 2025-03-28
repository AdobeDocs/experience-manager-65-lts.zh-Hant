---
title: 匯入和匯出資料
description: 使用表單資料整合服務將資料匯入PDF表單，並使用Java API和網站服務API從PDF表單匯出資料。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 2e8b73eb-7070-4b7b-b14b-bfcca6175afb
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2754'
ht-degree: 0%

---

# 匯入和匯出資料 {#importing-and-exporting-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於表單資料整合服務 {#about-the-form-data-integration-service}

表單資料整合服務可將資料匯入PDF表單，並從PDF表單匯出資料。 匯入和匯出作業支援兩種型別的PDF forms：

* Acrobat表單(在Acrobat中建立)是包含表單欄位的PDF檔案。
* Adobe XML表單(在Designer中建立)是符合XML Adobe XML Forms架構(XFA)的PDF檔案。

根據PDF表單的型別，表單資料可以下列格式之一存在：

* XFDF檔案，這是Acrobat表單資料格式的XML版本。
* XDP檔案，此檔案是包含表單欄位定義的XML檔案。 其中也可能包含表單欄位資料和內嵌的PDF檔案。 Designer產生的XDP檔案必須攜帶內嵌Base-64編碼的PDF檔案，才能使用。

您可以使用表單資料整合服務完成這些工作：

* 將資料匯入PDF forms。 如需詳細資訊，請參閱[匯入表單資料](importing-exporting-data.md#importing-form-data)。
* 從PDF forms匯出資料。 如需詳細資訊，請參閱[匯出表單資料](importing-exporting-data.md#exporting-form-data)。

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 匯入表單資料 {#importing-form-data}

您可以使用表單資料整合服務，將表單資料匯入互動式PDF forms。 互動式PDF表單是一份PDF檔案，其中包含一或多個欄位，用來向使用者收集資訊或顯示自訂資訊。 表單資料整合服務不支援表單計算、驗證或指令碼。

若要將資料匯入到Designer中建立的表單，您必須參考有效的XDP XML資料來源。 請考量下列範例抵押貸款申請表單。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

若要將資料值匯入此表單，您必須擁有與表單對應的有效XDP XML資料來源。 您無法使用任意XML資料來源，將資料匯入使用「表單資料整合」服務的表單。 任意XML資料來源和XDP XML資料來源之間的差異在於XDP資料來源符合XML Forms架構(XFA)。 下列XML代表與範例抵押應用程式表單相對應的XDP XML資料來源。

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將表單資料匯入PDF表單，請執行下列步驟：

1. 包含專案檔案。
1. 建立表單資料整合服務使用者端。
1. 參考PDF表單。
1. 參考XML資料來源。
1. 將資料匯入PDF表單。
1. 將PDF表單儲存為PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如需關於這些JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立表單資料整合服務使用者端**

您必須先建立資料整合服務使用者端，才能以程式設計方式將資料匯入PDF表單使用者端API。 建立服務使用者端時，您可以定義呼叫服務所需的連線設定。 如需詳細資訊，請參閱[設定連線內容](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**參考PDF表單**

若要將資料匯入PDF表單，您必須參考在Designer中建立的XML表單或在Acrobat中建立的Acrobat表單。

**參考XML資料來源**

若要匯入表單資料，您必須參考有效的資料來源。 若要將資料匯入在Designer中建立的XFA XML表單，您必須使用XDP XML資料來源。 如果您參照Acrobat表單，則必須使用XFDF資料來源。 對於您想要匯入資料的每個欄位，必須指定值。 如果XML資料來源中的元素未對應至表單中的欄位，則會忽略該元素。

**將資料匯入PDF表單**

參考PDF表單和有效的XML資料來源後，您可以將資料匯入PDF表單。

**將PDF表單儲存為PDF檔案**

將資料匯入表單後，可將表單儲存為PDF檔案。 儲存為PDF檔案後，使用者就可以在Adobe Reader或Acrobat中開啟表單，並檢視包含匯入資料的表單。

**另請參閱**

[使用Java API匯入表單資料](importing-exporting-data.md#import-form-data-using-the-java-api)

[使用網站服務API匯入表單資料](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速入門](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[匯出表單資料](importing-exporting-data.md#exporting-form-data)

### 使用Java API匯入表單資料 {#import-form-data-using-the-java-api}

使用表單資料整合API (Java)匯入表單資料：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormDataIntegrationClient`物件。

1. 參考PDF表單。

   * 使用物件的建構函式建立`java.io.FileInputStream`物件。 傳遞字串值，該值會指定PDF表單的位置。
   * 使用`com.adobe.idp.Document`建構函式建立儲存PDF表單的`com.adobe.idp.Document`物件。 將包含PDF表單的`java.io.FileInputStream`物件傳遞給建構函式。

1. 參考XML資料來源。

   * 使用物件的建構函式建立`java.io.FileInputStream`物件，並傳遞字串值，指定包含要匯入表單之資料的XML檔案位置。
   * 使用`com.adobe.idp.Document`建構函式建立儲存表單資料的`com.adobe.idp.Document`物件。 將包含表單資料的`java.io.FileInputStream`物件傳遞給建構函式。

1. 將資料匯入PDF表單。

   透過叫用`FormDataIntegrationClient`物件的`importData`方法並傳遞下列值，將資料匯入PDF表單：

   * 儲存PDF表單的`com.adobe.idp.Document`物件。
   * 儲存表單資料的`com.adobe.idp.Document`物件。

   `importData`方法傳回`com.adobe.idp.Document`物件，該物件儲存的PDF表單包含XML資料來源中的資料。

1. 將PDF表單儲存為PDF檔案。

   * 建立`java.io.File`物件，並確認副檔名為「。PDF」。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案（請確定您使用的是`importData`方法傳回的`Document`物件）。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API匯入表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API匯入表單資料 {#import-form-data-using-the-web-service-api}

使用表單資料整合API （網站服務）匯入表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立表單資料整合服務使用者端。

   * 使用預設建構函式建立`FormDataIntegrationClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`FormDataIntegrationClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`FormDataIntegrationClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF表單。

   * 使用物件的建構函式建立`BLOB`物件。 此`BLOB`物件是用來儲存PDF表單。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞字串值，該值會指定PDF表單的位置以及開啟檔案的模式。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 參考XML資料來源。

   * 使用物件的建構函式建立`BLOB`物件。 此`BLOB`物件是用來儲存匯入表單的資料。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞字串值，指定包含要匯入之資料的XML檔案位置，以及開啟檔案的模式。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 將資料匯入PDF表單。

   透過叫用`FormDataIntegrationClient`物件的`importData`方法並傳遞下列值，將資料匯入PDF表單：

   * 儲存PDF表單的`BLOB`物件。
   * 儲存表單資料的`BLOB`物件。

   `importData`方法傳回`BLOB`物件，該物件儲存的PDF表單包含XML資料來源中的資料。

1. 將PDF表單儲存為PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案位置的字串值。
   * 建立位元組陣列，儲存`importData`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 匯出表單資料 {#exporting-form-data}

您可以使用表單資料整合服務，從互動式PDF表單匯出表單資料。 匯出的資料格式取決於表單型別。 如果表單型別是在Acrobat中建立的Acrobat表單，則匯出的資料為XFDF。 如果表單型別是在Designer中建立的XML表單，則匯出的資料為XDP。

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要從PDF表單匯出表單資料，請執行以下步驟：

1. 包含專案檔案
1. 建立表單資料整合服務使用者端。
1. 參考PDF表單。
1. 從PDF表單匯出資料。
1. 將匯出的資料儲存為XML檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立表單資料整合服務使用者端**

您必須先建立資料整合服務使用者端，才能以程式設計方式將資料匯入PDF formClient API。 建立服務使用者端時，您可以定義呼叫服務所需的連線設定。 如需詳細資訊，[正在設定連線內容](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**參考PDF表單**

若要從PDF表單匯出資料，您必須參考在Designer或Acrobat中建立且包含表單資料的PDF表單。 如果您嘗試從空白的PDF表單匯出資料，您將會取得空白的XML結構描述。

**從PDF表單匯出資料**

參考包含表單資料的PDF表單後，您可以從表單匯出資料。 資料會匯出至以表單為基礎的XML結構描述中。

**將表單資料儲存為XML檔案**

匯出表單資料後，可將資料儲存為XML檔案。 儲存為XML檔案後，您可以在XML檢視器中開啟XML檔案，以檢視表單資料。

**另請參閱**

[使用Java API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-java-api)

[使用網站服務API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速入門](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[匯入表單資料](importing-exporting-data.md#importing-form-data)

### 使用Java API匯出表單資料 {#export-form-data-using-the-java-api}

使用表單資料整合API (Java)匯出表單資料：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormDataIntegrationClient`物件。

1. 參考PDF表單。

   * 使用物件的建構函式建立`java.io.FileInputStream`物件，並傳遞字串值，指定包含要匯出之資料的PDF表單位置。
   * 使用`com.adobe.idp.Document`建構函式建立儲存PDF表單的`com.adobe.idp.Document`物件。 將包含PDF表單的`java.io.FileInputStream`物件傳遞給建構函式。

1. 從PDF表單匯出資料。

   叫用`FormDataIntegrationClient`物件的`exportData`方法匯出表單資料，並傳遞儲存PDF表單的`com.adobe.idp.Document`物件。 此方法會傳回將表單資料儲存為XML結構描述的`com.adobe.idp.Document`物件。

1. 將PDF表單儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為XML。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案（請確定您使用的是`exportData`方法傳回的`Document`物件）。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API匯出表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API匯出表單資料 {#export-form-data-using-the-web-service-api}

使用表單資料整合API （網站服務）匯出表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   * 將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立表單資料整合服務使用者端。

   * 使用預設建構函式建立`FormDataIntegrationClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`FormDataIntegrationClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`FormDataIntegrationClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF表單。

   * 使用物件的建構函式建立`BLOB`物件。 此`BLOB`物件是用來儲存資料匯出的PDF表單。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞字串值，該值會指定PDF表單的位置以及開啟檔案的模式。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 從PDF表單匯出資料。

   叫用`FormDataIntegrationClient`物件的`exportData`方法，並傳遞儲存PDF表單的`BLOB`物件，將資料匯入PDF表單。 此方法會傳回將表單資料儲存為XML結構描述的`BLOB`物件。

1. 將PDF表單儲存為PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表XML檔案位置的字串值。
   * 建立位元組陣列，儲存`exportData`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
