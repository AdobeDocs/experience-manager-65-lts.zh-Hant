---
title: 組合PDF產品組合
description: 組合PDF產品組合以組合多種型別的檔案，包括word檔案、影像檔案和PDF檔案。 您可以使用Java API和Web服務API組合PDF產品組合。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Services
hide: true
hidefromtoc: true
exl-id: 43460ac1-a152-4a0d-943f-1b3ed007f089
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---

# 組合PDF產品組合 {#assembling-pdf-portfolios}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以使用組合器Java和Web服務API組合PDF Portfolio。 產品組合可以組合多種型別的檔案，包括Word檔案、影像檔案（例如jpeg檔案）和PDF檔案。 投資組合的版面可設定為不同的樣式，例如&#x200B;*具有預覽的格線*、*在影像上*&#x200B;的版面，甚至&#x200B;*旋轉*。

下圖是影像&#x200B;*樣式配置上具有*&#x200B;的產品組合熒幕擷圖。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

建立PDF Portfolio可作為傳送一組檔案的無紙化替代方案。 使用AEM Forms，您可以透過叫用包含結構化DDX檔案的組合器服務來建立投資組合。 下列DDX檔案是建立PDF Portfolio的DDX檔案範例。

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

DXX檔案必須包含具有巢狀`Navigator`標籤的`Portfolio`標籤。 請注意，只有在將`myNavigator`指派為onImage配置導覽器時，才需要標籤`<Resource name="navigator/image.xxx" source="myImage.png"/>`： `AdobeOnImage.nav`。 此標籤可讓組合器服務選取要做為產品組合背景的影像。 包含`PackageFiles`和`File`標籤以定義封裝檔案的檔案名稱和MIME型別。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱[組合器服務與DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

若要建立PDF Portfolio，請執行以下工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考必要的檔案。
1. 設定執行階段選項。
1. 組合投資組合。
1. 儲存組合的產品組合。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立PDF組合器使用者端**

在您以程式設計方式執行組合器作業之前，請先建立組合器服務使用者端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDF Portfolio。 此DDX檔案必須包含`Portfolio`、`Navigator`和`PackageFiles`元素。

**參考必要的檔案**

若要組裝PDF Portfolio，請參照代表要組裝的檔案的所有檔案。 例如，將DDX檔案中指定的所有影像檔案傳遞至組合器服務。 請注意，這些檔案參考於本節所指定的DDX檔案： *myImage.png*&#x200B;和&#x200B;*saint_bernard.jpg*。

組裝PDF Portfolio時，請將NAV檔案（導覽器檔案）傳遞至Assembler服務。 您傳遞至組合器服務的NAV檔案取決於要建立的PDF Portfolio型別。 例如，若要在影像&#x200B;*配置上建立*，請傳遞AdobeOnImage.nav檔案。 您可以在下列資料夾中找到NAV檔案：

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

從Acrobat 9 （或更新版本）安裝目錄複製NAV檔案。 將NAV檔案放置在使用者端應用程式可存取的位置。 所有檔案都會傳遞到Map集合物件中的Assembler服務。

>[!NOTE]
>
>與組合PDF產品組合相關的快速入門使用AdobeOnImage.nav。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。

**組合投資組合**

若要組裝PDF Portfolio，請呼叫`invokeDDX`操作。 組合器服務會傳回集合物件中的PDF Portfolio 。

**儲存組合的產品組合**

PDF Portfolio會在集合物件中傳回。 逐一檢視集合物件，並將PDF Portfolio儲存為PDF檔案。

**另請參閱**

[使用Java API組合PDF Portfolio](#assemble-a-pdf-portfolio-using-the-java-api)

[使用網站服務API組合PDF Portfolio](#assemble-a-pdf-portfolio-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API組合PDF Portfolio {#assemble-a-pdf-portfolio-using-the-java-api}

使用組合器服務API (Java)組合PDF Portfolio：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`AssemblerServiceClient`物件。

1. 參考現有的DDX檔案。

   * 使用它的建構函式並傳遞指定DDX檔案位置的字串值，建立代表DDX檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 參考必要的檔案。

   * 使用`HashMap`建構函式建立用來儲存輸入PDF檔案的`java.util.Map`物件。
   * 使用物件的建構函式建立`java.io.FileInputStream`物件。 傳遞所需NAV檔案的位置（針對建立投資組合所需的每個檔案重複此工作）。
   * 建立`com.adobe.idp.Document`物件並傳遞包含NAV檔案的`java.io.FileInputStream`物件（針對建立投資組合所需的每個檔案重複此工作）。
   * 透過叫用物件的`put`方法並傳遞下列引數，將專案新增至`java.util.Map`物件：

      * 代表索引鍵名稱的字串值。 此值必須符合DDX檔案中指定的來源元素值。 （針對建立投資組合所需的每個檔案重複此工作）。
      * 包含PDF檔案的`com.adobe.idp.Document`物件。 （針對建立投資組合所需的每個檔案重複此工作）。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 透過叫用屬於`AssemblerOptionSpec`物件的方法，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法，然後傳遞`false`。

1. 組合投資組合。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列必要值：

   * 代表要使用的DDX檔案的`com.adobe.idp.Document`物件
   * 包含建置PDF Portfolio所需檔案的`java.util.Map`物件。
   * 指定執行階段選項（包括預設字型和作業記錄層級）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件

   `invokeDDX`方法傳回`com.adobe.livecycle.assembler.client.AssemblerResult`物件，其中包含已組裝的PDF Portfolio以及發生的任何例外狀況。

1. 儲存組合的產品組合。

   若要取得PDF Portfolio，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 此方法會傳回`java.util.Map`物件。
   * 逐一檢視`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件為止。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF Portfolio。

**另請參閱**

[快速入門(SOAP模式)：使用Java API組合PDF產品組合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API組合PDF Portfolio {#assemble-a-pdf-portfolio-using-the-web-service-api}

使用組合器服務API （Web服務）組合PDF Portfolio：

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
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表DDX檔案檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。

1. 參考必要的檔案。

   * 對於每個輸入檔案，使用其建構函式來建立`BLOB`物件。 `BLOB`物件是用來儲存輸入檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表輸入檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此集合物件用於儲存建立PDF Portfolio所需的輸入檔案。
   * 針對每個輸入檔案，建立`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 將代表索引鍵名稱的字串值指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`key`欄位。 此值必須符合DDX檔案中指定的元素值。 （針對每個輸入檔案執行此工作。）
   * 將儲存輸入檔案的`BLOB`物件指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`欄位。 (針對每個輸入PDF檔案執行此工作。)
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 叫用`MyMapOf_xsd_string_To_xsd_anyType`物件的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`物件。 (針對每個輸入PDF檔案執行此工作。)

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 將值指派給屬於`AssemblerOptionSpec`物件的資料成員，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請將`false`指派給`AssemblerOptionSpec`物件的`failOnError`資料成員。

1. 組合投資組合。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列值：

   * 代表DDX檔案的`BLOB`物件
   * 包含必要檔案的`MyMapOf_xsd_string_To_xsd_anyType`物件
   * 指定執行階段選項的`AssemblerOptionSpec`物件

   `invokeDDX`方法傳回`AssemblerResult`物件，其中包含工作的結果和發生的任何例外狀況。

1. 儲存組合的產品組合。

   若要取得新建立的PDF Portfolio，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，這是包含結果PDF檔案的`Map`物件。
   * 逐一檢視`Map`物件以取得每個結果檔案。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 存取其`BLOB`物件的`MTOM`屬性，以擷取代表PDF檔案的二進位資料。 這會傳回您可以寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
