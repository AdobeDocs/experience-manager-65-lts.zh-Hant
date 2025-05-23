---
title: 使用AEM Forms存放庫
description: 管理AEM Forms存放庫，以使用Java API和網站服務API建立資料夾、寫入、清單、讀取、更新和搜尋資源。 此外，瞭解如何建立資源關係、鎖定和刪除資源。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 4a911fe6-2939-4c8c-b486-7575c759857d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '9036'
ht-degree: 0%

---

# 使用AEM Forms存放庫 {#working-with-aem-forms-repository}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於存放庫服務**

存放庫服務提供給AEM Forms的資源儲存和管理服務。 當開發人員建立&#x200B;*AEM Forms*&#x200B;應用程式時，他們可以在存放庫中部署資產，而不是在檔案系統中。 資產可包括任何型別的附屬資料，包括XML表單、PDF forms (包括Acrobat表單)、表單片段、影像、設定檔、原則、SWF檔案、DDX檔案、XML結構描述、WSDL檔案和測試資料。

例如，請考量下列名為&#x200B;*Applications/FormsApplication*&#x200B;的Forms應用程式：

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

請注意，FormsFolder中有一個名為Loan.xdp的檔案。 若要存取此表單設計，請指定完整路徑（包括版本）： `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。

>[!NOTE]
>
>如需有關使用Workbench建立Forms應用程式的資訊，請參閱[Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63)。

AEM Forms存放庫中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

下列值顯示一些URI值的範例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>您可以使用網頁瀏覽器瀏覽AEM Forms存放庫。 若要瀏覽存放庫，請在網頁瀏覽器`https://[server name]:[server port]/repository`中輸入下列URL。 您可以使用網頁瀏覽器來驗證與「使用AEM Forms存放庫」區段關聯的快速入門結果。 例如，如果您將內容新增至AEM Forms存放庫，即可在網頁瀏覽器中檢視內容。 (請參閱[快速入門(SOAP模式)：使用Java API寫入資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)。)

存放庫API提供數個操作，可用於儲存和擷取存放庫中的資訊。 例如，當處理應用程式時需要資源時，您可以取得資源清單或擷取儲存於儲存庫中的特定資源。

>[!NOTE]
>
>存放庫API無法與內容服務互動（已棄用）。 若要與內容服務（已棄用）互動，請使用檔案管理API。

使用存放庫服務API，您可以完成下列工作：

* 建立資料夾。 請參閱[建立資料夾](aem-forms-repository.md#creating-folders)。
* 寫入資源及其屬性。 請參閱[寫入資源](aem-forms-repository.md#writing-resources)。
* 列出指定集合中或其他資源相關的資源。 請參閱[列出資源](aem-forms-repository.md#listing-resources)。
* 讀取資源及其屬性。 請參閱[讀取資源](aem-forms-repository.md#reading-resources)。
* 更新資源及其屬性。 請參閱[更新資源](aem-forms-repository.md#updating-resources)。
* 搜尋資源，包括其歷史記錄、相關資源和屬性。 請參閱[搜尋資源](aem-forms-repository.md#searching-for-resources)。
* 指定資源之間的關係。 請參閱[建立資源關係](aem-forms-repository.md#creating-resource-relationships)。
* 管理資源存取控制，包括鎖定和解鎖資源，以及讀取和寫入存取控制清單(ACL)。 請參閱[鎖定資源](aem-forms-repository.md#locking-resources)。
* 刪除資源及其屬性。 請參閱[刪除資源](aem-forms-repository.md#deleting-resources)。

>[!NOTE]
>
>使用存放庫API時，您無法使用ECM存放庫來管理資源存取控制、搜尋資源或指定資源關係。

>[!NOTE]
>
>將加密的PDF寫入存放庫時，無法使用自動關係擷取功能。 否則，加密的PDF可以儲存在存放庫中，並於稍後擷取。 擷取器可選擇在從存放庫中擷取PDF後將其解密。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立資料夾 {#creating-folders}

資料夾（資源集合）可用來將物件（檔案或資源）儲存在有組織的群組中。 資料夾可以包含資源和其他資料夾，也稱為子資料夾。 資源一次只能儲存在一個資料夾中。

檔案從資料夾繼承存取控制清單(ACL)，子資料夾從其父資料夾繼承ACL。 因此，您必須先存在父資料夾，才能建立子資料夾。 IDE僅允許您逐個資料夾進行互動，而不是逐個檔案進行互動。 您無法設定資料夾的版本，因此不需要設定版本；資料夾本身並不包含資料。 相反地，它只是包含資料之資源的容器。 預設ACL是系統層級的許可權，這表示使用者必須具有系統層級的許可權（讀取、寫入、周遊、管理ACL），直到有人授予他們特定檔案夾的許可權為止。 ACL只能在IDE中運作。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要建立資料夾，請執行下列步驟：

1. 包含專案檔案。
1. 建立服務使用者端。
1. 建立資料夾。
1. 將資料夾寫入存放庫。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式建立資源集合。 這是透過建立服務使用者端來完成。

**建立資料夾**

叫用存放庫服務方法建立資源集合，並以識別資訊（包括其UUID、資料夾名稱和說明）填入資源集合。

**將資料夾寫入存放庫**

叫用存放庫服務方法來寫入資源集合，指定目標資料夾的URI。

**另請參閱**

[使用Java API建立資料夾](aem-forms-repository.md#create-folders-using-the-java-api)

[使用Web服務API建立資料夾](aem-forms-repository.md#create-folders-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API建立資料夾 {#create-folders-using-the-java-api}

使用存放庫服務API (Java)建立資料夾：

1. 包含專案檔案

   將專案檔案包含在Java專案的類別路徑中。

1. 建立服務使用者端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。

1. 建立資料夾

   若要建立資源集合，您必須先建立`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`物件。

   叫用`repositoryInfomodelFactoryBean`物件的`newResourceCollection`方法，並傳入下列引數：

   * 要指派給資源的`com.adobe.repository.infomodel.Id` UUID識別碼。
   * 要指派給資源的`com.adobe.repository.infomodel.Lid` UUID識別碼。
   * 包含資源集合名稱的`java.lang.String`。 例如，`FormsFolder`。

   此方法會傳回代表新資料夾的`com.adobe.repository.infomodel.bean.ResourceCollection`物件。

   使用`setDescription`方法設定資料夾的說明，並傳入下列引數：

   * 說明資源集合的`String`。 在此範例中，`"test Folder"`已使用`.`

1. 將資料夾寫入存放庫

   叫用`ResourceRepositoryClient`物件的`writeResource`方法，並傳入資料夾和`ResourceCollection`物件的URI。 例如，資料夾的URI可以是下列值`/Applications/FormsApplication/1.0/`。

   此方法會傳回新建立的`com.adobe.repository.infomodel.bean.Resource`物件的執行個體。 例如，您可以叫用`com.adobe.repository.infomodel.bean.Resource`物件的`getId`方法來擷取新資源的識別碼值。

**另請參閱**

[建立資料夾](aem-forms-repository.md#creating-folders)

[快速入門(SOAP模式)：使用Java API建立資料夾](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立資料夾 {#create-folders-using-the-web-service-api}

使用存放庫服務API （Web服務）建立資料夾：

1. 包含專案檔案

   * 使用base64建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`RepositoryServiceService`物件。 使用包含使用者名稱和密碼的`System.Net.NetworkCredential`物件設定其`Credentials`屬性。

1. 建立資料夾

   使用`ResourceCollection`類別的預設建構函式建立資料夾，並傳入下列引數：

   * `Id`物件，這是透過叫用`Id`類別的預設建構函式所建立，並指派給`Resource`物件的`id`欄位。
   * `Lid`物件，這是透過叫用`Lid`類別的預設建構函式所建立，並指派給`Resource`物件的`lid`欄位。
   * 包含指派給`Resource`物件之`name`欄位之資源集合名稱的字串。 此範例中使用的名稱為`"testfolder"`。
   * 包含已指派給`Resource`物件之`description`欄位之資源集合說明的字串。 此範例中使用的說明是`"test folder"`。

1. 將資料夾寫入存放庫

   叫用`RepositoryServiceService`物件的`writeResource`方法，並傳入下列引數：

   * 要建立資料夾的路徑。
   * 代表資料夾的`ResourceCollection`物件。
   * 為其他兩個引數傳遞`null`。

**另請參閱**

[建立資料夾](aem-forms-repository.md#creating-folders)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 寫入資源 {#writing-resources}

您可以在存放庫中的指定位置中建立資源。 自然檔案大小受資料庫限制和工作階段逾時的影響。 對於預設設定，檔案限製為25 MB。 若要提高或降低檔案大小上限，您必須變更資料庫組態。

寫入資源等同於將資料儲存在存放庫中。 將資源寫入存放庫後，存放庫生態系統中的所有使用者端都可以存取該資源。 將資源（例如XML結構描述、XDP檔案和XSD檔案）寫入存放庫時，會根據MIME型別來剖析內容。 如果支援MIME型別，剖析器會判斷是否與其他內容有隱含的關係。 例如，如果階層式樣式表(CSS)具有參照一般CSS的相對URL，您應該也會將一般CSS提交至存放庫。 兩個資源之間的關係會儲存為未決關係，為期30天的不可調整期間。 當您在30天內將通用CSS提交至存放庫時，就會建立關係。

當您建立資源時，存取控制清單(ACL)繼承自父資料夾。 在建立初始資源或資料夾之前，根資料夾具有系統層級的許可權，此時資源或資料夾會獲得預設ACL許可權。

您可以使用存放庫服務Java API或Web服務API，以程式設計方式編寫資源。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要寫入資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定要讀取的資源的URI。
1. 讀取資源。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定資源目標資料夾的URI**

建立包含要讀取之資源的URI的字串。 語法包含正斜線，如同此範例： &quot;/*path*/*folder*&quot;。

**建立資源**

叫用存放庫服務方法來建立資源，並將識別資訊（包括其UUID、資源名稱和說明）填入資源。

**指定資源內容**

叫用存放庫服務方法來建立資源內容，並將該內容儲存在資源中。

**將資源寫入目標資料夾**

叫用存放庫服務方法來寫入資源，指定目標資料夾的URI。

**另請參閱**

[使用Java API寫入資源](aem-forms-repository.md#write-resources-using-the-java-api)

[使用網站服務API寫入資源](aem-forms-repository.md#write-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API寫入資源 {#write-resources-using-the-java-api}

使用存放庫服務API (Java)編寫資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。

1. 指定資源目標資料夾的URI

   指定資源之目標資料夾的URI。 在此案例中，因為名為`testResource`的資源將儲存在名為`testFolder`的資料夾中，所以資料夾的URI為`"/testFolder"`。 URI會儲存為`java.lang.String`物件。

1. 建立資源

   若要建立資源，您必須先建立`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`物件。

   叫用`RepositoryInfomodelFactoryBean`物件的`newResource`方法，這會建立`com.adobe.repository.infomodel.bean.Resource`物件。 此範例中提供下列引數：

   * `com.adobe.repository.infomodel.Id`物件，這是透過叫用`Id`類別的預設建構函式所建立。
   * `com.adobe.repository.infomodel.Lid`物件，這是透過叫用`Lid`類別的預設建構函式所建立。
   * 包含資源檔案名稱的`java.lang.String`。

   若要指定資源的描述，請叫用`Resource`物件的`setDescription`方法，並傳遞包含描述的字串。 在此範例中，描述為`"test resource"`。

1. 指定資源內容

   若要建立資源的內容，請叫用`RepositoryInfomodelFactoryBean`物件的`newResourceContent`方法，此方法會傳回`com.adobe.repository.infomodel.bean.ResourceContent`物件。 將內容新增至`ResourceContent`物件。 在此範例中，這是透過執行下列工作來完成：

   * 正在叫用`ResourceContent`物件的`setDataDocument`方法並傳入`com.adobe.idp.Document`物件
   * 正在叫用`ResourceContent`物件的`setSize`方法，並傳入`Document`物件的大小（位元組）

   叫用`Resource`物件的`setContent`方法並傳入`ResourceContent`物件，以新增內容至資源。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 將資源寫入目標資料夾

   叫用`ResourceRepositoryClient`物件的`writeResource`方法，並傳入資料夾的URI和`Resource`物件。

**另請參閱**

[寫入資源](aem-forms-repository.md#writing-resources)

[快速入門(SOAP模式)：使用Java API撰寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API寫入資源 {#write-resources-using-the-web-service-api}

使用存放庫服務API （Web服務）寫入資源：

1. 包含專案檔案

   * 使用base64建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`RepositoryServiceService`物件。 使用包含使用者名稱和密碼的`System.Net.NetworkCredential`物件設定其`Credentials`屬性。

1. 指定資源目標資料夾的URI

   指定資源之目標資料夾的URI。 在此案例中，因為名為`testResource`的資源將儲存在名為`testFolder`的資料夾中，所以資料夾的URI為`"/testFolder"`。 使用與Microsoft .NET Framework相容的語言時（例如C#），請將URI儲存在`System.String`物件中。

1. 建立資源

   若要建立資源，請叫用`Resource`類別的預設建構函式。 在此範例中，下列資訊儲存在`Resource`物件中：

   * `com.adobe.repository.infomodel.Id`物件，這是透過叫用`Id`類別的預設建構函式所建立，並指派給`Resource`物件的`id`欄位。
   * `com.adobe.repository.infomodel.Lid`物件，這是透過叫用`Lid`類別的預設建構函式所建立，並指派給`Resource`物件的`lid`欄位。
   * 包含指派給`Resource`物件之`name`欄位之資源的檔案名稱的字串。 此範例中使用的名稱為`"testResource"`。
   * 包含指派給`Resource`物件之`description`欄位之資源描述的字串。 此範例中使用的說明是`"test resource"`。

1. 指定資源內容

   若要建立資源的內容，請叫用`ResourceContent`類別的預設建構函式。 然後將內容新增至`ResourceContent`物件。 在此範例中，這是透過執行下列工作來完成：

   * 正在指派包含檔案的`BLOB`物件至`ResourceContent`物件的`dataDocument`欄位。
   * 正在將`BLOB`物件的大小指派給`ResourceContent`物件的`size`欄位（位元組）。

   將`ResourceContent`物件指派至`Resource`物件的`content`欄位，以新增內容至資源。

1. 將資源寫入目標資料夾

   叫用`RepositoryServiceService`物件的`writeResource`方法，並傳入資料夾的URI和`Resource`物件。 為其他兩個引數傳遞`null`。

**另請參閱**

[寫入資源](aem-forms-repository.md#writing-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 列出資源 {#listing-resources}

您可以透過列出資源來探索資源。 對存放庫執行查詢，以尋找與指定資源集合相關的所有資源。

組織資源後，您可以透過檢視結構的特定分支來檢查您建立的結構，就像在作業系統中一樣。

列出資源會依關係操作：資源是資料夾的成員。 成員資格由「成員」型別的關係表示。 當您在指定的資料夾中列出資源時，會透過關係「成員」查詢與指定資料夾相關的資源。 關係具有方向性：關係的成員具有作為目標成員的來源。 來源是資源；目標是父資料夾。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

若要列出資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立服務使用者端。
1. 指定資料夾路徑。
1. 擷取資源清單。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式建立資源集合。 這是透過建立服務使用者端來完成。

**指定資料夾路徑**

建立包含資源之資料夾路徑的字串。 語法包含正斜線，如同此範例： &quot;/*path*/*folder*&quot;。

**擷取資源清單**

叫用存放庫服務方法來擷取資源清單，指定目標資料夾的路徑。

**另請參閱**

[使用Java API列出資源](aem-forms-repository.md#list-resources-using-the-java-api)

[使用網站服務API列出資源](aem-forms-repository.md#list-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API列出資源 {#list-resources-using-the-java-api}

使用存放庫服務API (Java)列出資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。

1. 指定資料夾路徑

   指定要查詢之資源集合的URI。 在此案例中，其URI為`"/testFolder"`。 URI會儲存為`java.lang.String`物件。

1. 擷取資源清單

   叫用`ResourceRepositoryClient`物件的`listMembers`方法，並傳入資料夾的URI。

   此方法傳回`java.util.List`個`com.adobe.repository.infomodel.bean.Resource`物件，這些物件是型別`Relation.TYPE_MEMBER_OF`之`com.adobe.repository.infomodel.bean.Relation`的來源，且以資源集合URI為目標。 您可以逐一檢視此`List`，以擷取每個資源。 在此範例中，會顯示每個資源的名稱和說明。

**另請參閱**

[列出資源](aem-forms-repository.md#listing-resources)。

[快速入門(SOAP模式)：使用Java API列出資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API列出資源 {#list-resources-using-the-web-service-api}

使用存放庫服務API （Web服務）列出資源：

1. 包含專案檔案

   * 建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`RepositoryServiceService`物件。 使用包含使用者名稱和密碼的`System.Net.NetworkCredential`物件設定其`Credentials`屬性。

1. 指定資料夾路徑

   指定包含要查詢之資料夾URI的字串。 在此案例中，其URI為`"/testFolder"`。 使用與Microsoft .NET Framework相容的語言時（例如C#），請將URI儲存在`System.String`物件中。

1. 擷取資源清單

   叫用`RepositoryServiceService`物件的`listMembers`方法，並將資料夾的URI傳入做為第一個引數。 為其他兩個引數傳遞`null`。

   方法傳回可轉換為`Resource`物件的物件陣列。 您可以逐一檢視物件陣列，以擷取每個相關資源。 在此範例中，會顯示每個資源的名稱和說明。

**另請參閱**

[列出資源](aem-forms-repository.md#listing-resources)。

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 正在讀取資源 {#reading-resources}

您可以從儲存庫中的指定位置擷取資源，以讀取其內容和中繼資料。 工作流程會以初始化表單作為前端。 此程式具有讀取表單所需的所有許可權。 系統會擷取資料表單，並從存放庫讀取內容。 存放庫會授予內容和中繼資料的存取權（甚至知道資源存在的能力）。

存放庫有以下四種許可權型別：

* **周遊**：可讓您列出資源；也就是說，可讀取資源中繼資料，但不讀取資源內容
* **讀取**：可讓您讀取資源內容
* **寫入**：可讓您寫入資源內容
* **管理存取控制清單(ACL)**：可讓您操控資源上的ACL

使用者只有在其擁有執行流程的許可權時，才能執行流程。 IDE使用者需要周遊和讀取許可權，才能與存放庫同步。 ACL只會在設計時套用，因為執行階段發生在系統內容中。

您可以使用存放庫服務Java API或Web服務API，以程式設計方式讀取資源。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

若要讀取資源，請執行下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定要讀取的資源的URI。
1. 讀取資源。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定要讀取的資源URI**

建立包含要讀取之資源的URI的字串。 語法包含正斜線，如同此範例： &quot;/*path*/*resource*&quot;。

**讀取資源**

叫用存放庫服務方法來讀取資源，指定URI。

**另請參閱**

[使用Java API讀取資源](aem-forms-repository.md#read-resources-using-the-java-api)

[使用網站服務API讀取資源](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API讀取資源 {#read-resources-using-the-java-api}

使用存放庫服務API (Java)讀取資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。

1. 指定要讀取的資源的URI

   指定代表要擷取之資源URI的字串值。 例如，假設資源名為&#x200B;*testResource*，而該資源位於名為&#x200B;*testFolder*&#x200B;的資料夾中，請指定`/testFolder/testResource`。

1. 讀取資源

   叫用`ResourceRepositoryClient`物件的`readResource`方法，並將資源的URI作為引數傳遞。 此方法會傳回代表資源的`Resource`執行個體。

**另請參閱**

[正在讀取資源](aem-forms-repository.md#reading-resources)

[快速入門(SOAP模式)：使用Java API讀取資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API讀取資源 {#reading-resources-using-the-web-service-api}

使用存放庫服務API （Web服務）讀取資源：

1. 包含專案檔案

   * 建立使用存放庫WSDL的Microsoft .NET使用者端元件。 （請參閱[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。）
   * 參考Microsoft .NET使用者端元件。 （請參閱[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。）

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`RepositoryServiceService`物件。 使用包含使用者名稱和密碼的`System.Net.NetworkCredential`物件設定其`Credentials`屬性。

1. 指定要讀取的資源的URI

   指定包含要擷取之資源URI的字串。 在此案例中，由於名為`testResource`的資源位於名為`testFolder`的資料夾中，其URI為`"/testFolder/testResource"`。 使用與Microsoft .NET Framework相容的語言時（例如C#），請將URI儲存在`System.String`物件中。

1. 讀取資源

   叫用`RepositoryServiceService`物件的`readResource`方法，並將資源的URI傳遞為第一個引數。 為其他兩個引數傳遞`null`。

**另請參閱**

[正在讀取資源](aem-forms-repository.md#reading-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 更新資源 {#updating-resources}

您可以擷取並更新存放庫中的資源內容。 更新資源時，這些資源的存取控制在各版本之間保持不變。 執行更新時，您可以選擇增加主要版本。 如果您不選擇遞增主要版本，則會自動更新次要版本。

更新資源時，會根據指定的資源屬性建立新版本。 更新資源時，請指定兩個重要引數：目標URI和包含所有已更新中繼資料的資源執行個體。 請務必注意，如果您未變更特定屬性（例如名稱），則在您傳入的執行個體中仍需要該屬性。 剖析內容時建立的關係會新增至特定版本，除非另有指定，否則不會轉寄。

例如，如果您更新XDP檔案並且它包含對其他資源的參照，則也會記錄這些額外的參照。 假設form.xdp 1.0版有兩個外部參照：一個標誌和一個樣式表，而您之後更新了form.xdp，使其現在有三個參照：一個標誌、一個樣式表和一個結構描述檔案。 在更新期間，存放庫會將第三個關係（到結構描述檔案）新增到其暫止關係表中。 一旦結構描述檔案出現在存放庫中，關係就會自動形成。 不過，如果form.xdp 2.0版不再使用標誌，form.xdp 2.0版將不會與標誌有關係。

所有更新操作都是原子式且交易式。 例如，如果兩個使用者讀取相同的資源，並且都決定將1.0版更新為2.0版，則其中一個將成功，而其中一個將失敗，將維護存放庫的完整性，並且兩個使用者都將收到確認成功或失敗的訊息。 如果交易未認可，則會在資料庫失敗時回覆，並會逾時或回覆，視應用程式伺服器而定。

您可以使用存放庫服務Java API或網站服務API，以程式設計方式更新資源。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

若要更新資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 擷取要更新的資源。
1. 更新資源。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**擷取要更新的資源**

讀取資源。 如需詳細資訊，請參閱[讀取資源](aem-forms-repository.md#reading-resources)。

**更新資源**

在資源中設定新資訊，並叫用存放庫服務方法來更新資源，指定URI、更新的資源以及應該如何更新版本資訊。

**另請參閱**

[使用Java API更新資源](aem-forms-repository.md#update-resources-using-the-java-api)

[使用網站服務API更新資源](aem-forms-repository.md#update-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API更新資源 {#update-resources-using-the-java-api}

使用存放庫服務API (Java)更新資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。

1. 擷取要更新的資源

   指定要擷取及讀取資源的資源URI。 在此範例中，資源的URI為`"/testFolder/testResource"`。

1. 更新資源

   更新`Resource`物件的資訊。 在此範例中，若要更新描述，請叫用`Resource`物件的`setDescription`方法，並將新的描述字串作為引數傳遞。

   然後叫用`ServiceClientFactory`物件的`updateResource`方法，並傳入下列引數：

   * 包含資源URI的`java.lang.String`物件。
   * 包含已更新資源資訊的`Resource`物件。
   * 一個`boolean`值，指示要更新主要版本還是次要版本。 在此範例中，傳入`true`的值表示主要版本將遞增。

**另請參閱**

[更新資源](aem-forms-repository.md#updating-resources)

[快速入門(SOAP模式)：使用Java API更新資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API更新資源 {#update-resources-using-the-web-service-api}

使用存放庫API （Web服務）更新資源：

1. 包含專案檔案

   * 建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`RepositoryServiceService`物件。 使用包含使用者名稱和密碼的`System.Net.NetworkCredential`物件設定其`Credentials`屬性。

1. 擷取要更新的資源

   指定要擷取的資源URI並讀取資源。 在此範例中，資源的URI為`"/testFolder/testResource"`。 如需詳細資訊，請參閱[讀取資源](aem-forms-repository.md#reading-resources)。

1. 更新資源

   更新`Resource`物件的資訊。 在此範例中，若要更新說明，請將新值指派給`Resource`物件的`description`欄位。

1. 叫用`RepositoryServiceService`物件的`updateResource`方法，並傳入下列引數：

   * 包含資源URI的`System.String`物件。
   * 包含已更新資源資訊的`Resource`物件。
   * 一個`boolean`值，指示要更新主要版本還是次要版本。 在此範例中，傳入`true`的值表示主要版本將遞增。
   * 傳入`null`以取得其餘兩個引數。

**另請參閱**

[更新資源](aem-forms-repository.md#updating-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 搜尋資源 {#searching-for-resources}

您可以建構用來搜尋存放庫中資源（包括歷史記錄、相關資源和屬性）的查詢。

您可以擷取相關資源，以判斷表單與其片段之間的相依性。 例如，如果您有表單，您可以決定要使用哪些片段或外部資源。 如果您有影像，也可以找出使用影像的表單。 您也可以使用根據屬性的篩選功能來搜尋相關資源。 例如，您可以搜尋使用具有指定名稱之影像的所有表單，或尋找由具有指定名稱之表單使用的任何影像。 您也可以使用資源屬性來搜尋。 例如，您可以執行查詢來尋找其名稱以指定字串開頭的所有表單或資源，該字串可能包含&#39;%&#39;和&#39;_&#39;萬用字元。 請記住，根據屬性的搜尋不是根據關係；這類搜尋是根據您對特定資源具有特定知識的假設。

**查詢陳述式**

*查詢*&#x200B;包含一或多個邏輯上以條件聯結的陳述式。 *陳述式*&#x200B;包含左運算元、運算元和右運算元。 此外，您可以指定要用於搜尋結果的排序順序。 *排序順序*&#x200B;包含等同於SQL `ORDER BY`子句的資訊，由包含搜尋所依據之屬性的元素以及指示是否要使用遞增或遞減順序的值所組成。

您可以使用存放庫服務Java API，以程式設計方式搜尋資源。 目前無法使用網站服務API來搜尋資源。

**排序行為**

叫用`ResourceRepositoryClient`物件的`searchProperties`方法並指定排序順序時，未遵循排序順序。 例如，假設您建立具有三個自訂屬性的資源，其中屬性名稱為`name`、`secondName`和`asecondName`。 接下來，您在屬性名稱上建立排序順序專案，並將`ascending`值設定為`true`。

接著您叫用`ResourceRepositoryClient`物件的`searchProperties`方法，並傳入排序順序。 搜尋會傳回正確的資源，包含三個屬性。 不過，屬性並未依屬性名稱排序。 它們會以新增的順序傳回： `name`、`secondName`和`asecondName`。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

若要搜尋資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定搜尋的目標資料夾。
1. 指定搜尋中使用的屬性。
1. 建立用於搜尋的查詢。
1. 建立搜尋結果的排序順序。
1. 搜尋資源。
1. 從搜尋結果擷取資源。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定搜尋的目標資料夾**

建立字串，其中包含進行搜尋的基本路徑。 語法包含正斜線，如同此範例： &quot;/*path*/*folder*&quot;。

**指定搜尋中使用的屬性**

您可以根據資源中所包含的屬性進行搜尋。 指定要執行搜尋的屬性值。

**建立用於搜尋的查詢**

使用陳述式和條件來建構查詢。 每個陳述式都會指定搜尋所依據的屬性、要使用的條件，以及要在搜尋中使用的屬性值。

**建立搜尋結果的排序順序**

排序順序由元素組成，每個元素都包含搜尋中使用的其中一個屬性，以及一個指示要使用升序或降序的值。

**搜尋資源**

使用資料夾、查詢和排序順序來搜尋資源。 此外，指出搜尋的深度，以及要傳回的結果數目上限。

**從搜尋結果擷取資源**

逐一檢視傳回的資源清單，並擷取資訊以供進一步處理。

**另請參閱**

[使用Java API搜尋資源](aem-forms-repository.md#search-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API搜尋資源 {#search-for-resources-using-the-java-api}

使用存放庫服務API (Java)搜尋資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。

1. 指定搜尋的目標資料夾

   指定要執行搜尋之基礎路徑的URI。 在此範例中，資源的URI為`/testFolder`。

1. 指定搜尋中使用的屬性

   指定要執行搜尋的屬性值。 屬性存在於`com.adobe.repository.infomodel.bean.Resource`物件中。 在此範例中，將會在name屬性上進行搜尋；因此，會使用包含`Resource`物件名稱的`java.lang.String`，在此例中為`testResource`。

1. 建立用於搜尋的查詢

   若要建立查詢，請叫用`Query`類別的預設建構函式來建立`com.adobe.repository.query.Query`物件，並將陳述式新增至查詢。

   若要建立陳述式，請叫用`com.adobe.repository.query.Query.Statement`類別的建構函式，並傳入下列引數：

   * 包含資源屬性常數的左運算元。 在此範例中，因為使用資源的名稱做為搜尋的基礎，所以使用靜態值`Resource.ATTRIBUTE_NAME`。
   * 包含用於搜尋屬性的條件的運運算元。 運運算元必須是`Query.Statement`類別中的靜態常數之一。 在此範例中，使用靜態值`Query.Statement.OPERATOR_BEGINS_WITH`。
   * 包含進行搜尋之屬性值的右運算元。 在此範例中，使用name屬性（包含值`"testResource"`的`String`）。

   呼叫`Query.Statement`物件的`setNamespace`方法，並傳入`com.adobe.repository.infomodel.bean.ResourceProperty`類別中包含的其中一個靜態值，以指定左運算元的名稱空間。 這個例子使用 `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`。

   呼叫`Query`物件的`addStatement`方法並傳入`Query.Statement`物件，以將每個陳述式新增至查詢。

1. 建立搜尋結果的排序順序

   若要指定搜尋結果中使用的排序順序，請叫用`SortOrder`類別的預設建構函式來建立`com.adobe.repository.query.sort.SortOrder`物件，然後將元素加入排序順序。

   若要建立排序順序的元素，請叫用`com.adobe.repository.query.sort.SortOrder.Element`類別的其中一個建構函式。 在此範例中，因為資源的名稱是做為搜尋的基礎，所以使用靜態值`Resource.ATTRIBUTE_NAME`做為第一個引數，而遞增順序（`true`的`boolean`值）則指定為第二個引數。

   呼叫`SortOrder`物件的`addSortElement`方法並傳入`SortOrder.Element`物件，以將每個專案加入排序順序。

1. 搜尋資源

   若要根據屬性屬性來搜尋`resources`，請叫用`ResourceRepositoryClient`物件的`searchProperties`方法，並傳入下列引數：

   * 包含要執行搜尋之基礎路徑的`String`。 在此案例中，使用`"/testFolder"`。
   * 搜尋中使用的查詢。
   * 搜尋的深度。 在此案例中，`com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE`用於表示要使用基底路徑及其所有資料夾。
   * `int`值，表示要選取未分頁結果集的第一個資料列。 在此範例中，指定了`0`。
   * 表示傳回結果最大數量的`int`值。 在此範例中，指定了`10`。
   * 搜尋中使用的排序順序。

   此方法會以指定的排序順序傳回`java.util.List`個物件（共`Resource`個）。

1. 從搜尋結果擷取資源

   若要擷取搜尋結果中包含的資源，請逐一檢視`List`，並將每個物件轉換為`Resource`以擷取其資訊。 在此範例中，會顯示每個資源的名稱。

**另請參閱**

[搜尋資源](aem-forms-repository.md#searching-for-resources)

[快速入門(SOAP模式)：使用Java API搜尋資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 建立資源關係 {#creating-resource-relationships}

您可以指定存放庫中資源之間的關係。 有三種關係：

* **相依性**：資源相依於其他資源的關係，表示存放庫需要所有相關資源。
* **成員資格（檔案系統）**：資源位於指定資料夾中的關聯性。
* **自訂**：您在資源之間指定的關聯性。 例如，如果某個資源已棄用，而另一個資源已引入存放庫，則您可以指定自己的替代關係。

您可以建立自己的自訂關係。 例如，如果您將HTML檔案儲存在存放庫中，而且該檔案使用影像，則可以指定自訂關係，將HTML檔案與影像相關聯（因為通常只有XML檔案會使用存放庫定義的相依關係與影像相關聯）。 另一個自訂關係的範例是，如果您想使用循環圖表結構而不是樹狀結構來建置存放庫的不同檢視。 您可以連同檢視器一起定義圓形圖形，以周遊這些關係。 最後，您可以指出一個資源會取代另一個資源，即使這兩個資源完全不同。 在這種情況下，您可以在預留範圍之外定義關係型別，並在這兩個資源之間建立關係。 您的應用程式將是唯一可偵測及處理該關係的使用者端，並且可用於搜尋該關係。

您可以使用存放庫服務Java API或Web服務API，以程式設計方式指定資源之間的關係。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

若要指定兩個資源之間的關係，請執行下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定相關資源的URI。
1. 建立關係。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定相關資源的URI**

建立包含相關資源URI的字串。 語法包含正斜線，如同此範例： &quot;/*path*/*resource*&quot;。

**建立關聯性**

叫用存放庫服務方法以建立並指定關係型別。

**另請參閱**

[使用Java API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[使用網站服務API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API建立關係資源 {#create-relationship-resources-using-the-java-api}

使用存放庫服務Java API建立關係資源，執行以下工作：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。

1. 指定要關聯之資源的URI

   指定相關資源的URI。 在此案例中，因為資源名為`testResource1`和`testResource2`，且位於名為`testFolder`的資料夾中，所以其URI為`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 URI會儲存為`java.lang.String`物件。 在此範例中，資源會先寫入存放庫，並擷取其URI。 如需有關寫入資源的詳細資訊，請參閱[寫入資源](aem-forms-repository.md#writing-resources)。

1. 建立關係

   叫用`ResourceRepositoryClient`物件的`createRelationship`方法，並傳入下列引數：

   * 來源資源的URI。
   * 目標資源的URI。
   * 關聯性型別，是`com.adobe.repository.infomodel.bean.Relation`類別中的靜態常數之一。 在此範例中，相依關係是透過指定值`Relation.TYPE_DEPENDANT_OF`建立的。
   * 一個`boolean`值，指出目標資源是否自動更新為新標頭資源的`com.adobe.repository.infomodel.Id`型識別碼。 在此範例中，因為相依關係，所以指定了值`true`。

   您也可以叫用`ResourceRepositoryClient`物件的`getRelated`方法，並傳入下列引數，以擷取指定資源的相關資源清單：

   * 要擷取相關資源的資源URI。 在此範例中，指定來源資源( `"/testFolder/testResource1"`)。
   * 表示指定的資源是否為關聯性中的來源資源的`boolean`值。 在此範例中，指定值`true`，因為情況如此。
   * 關聯性型別，是`Relation`類別中的靜態常數之一。 在此範例中，使用先前使用的相同值來指定相依關係： `Relation.TYPE_DEPENDANT_OF`。

   `getRelated`方法傳回`Resource`個物件中的`java.util.List`個，您可以透過它重複擷取每一個相關資源，將`List`中包含的物件轉型為`Resource`。 在此範例中，`testResource2`應該位於傳回的資源清單中。

**另請參閱**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[快速入門(SOAP模式)：使用Java API建立資源之間的關係](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API建立關係資源 {#create-relationship-resources-using-the-web-service-api}

使用存放庫API （Web服務）建立關係資源：

1. 包含專案檔案

   * 建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`RepositoryServiceService`物件。 使用包含使用者名稱和密碼的`System.Net.NetworkCredential`物件設定其`Credentials`屬性。

1. 指定要關聯之資源的URI

   指定相關資源的URI。 在此案例中，因為資源名為`testResource1`和`testResource2`，且位於名為`testFolder`的資料夾中，所以其URI為`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 使用與Microsoft .NET Framework相容的語言時（例如C#），URI會儲存為`System.String`物件。 在此範例中，資源會先寫入存放庫，並擷取其URI。 如需有關寫入資源的詳細資訊，請參閱[寫入資源](aem-forms-repository.md#writing-resources)。

1. 建立關係

   叫用`RepositoryServiceService`物件的`createRelationship`方法，並傳入下列引數：

   * 來源資源的URI。
   * 目標資源的URI。
   * 關係的型別。 在此範例中，相依關係是透過指定值`3`建立的。
   * 表示是否已指定關聯性型別的`boolean`值。 在此範例中，指定值`true`。
   * 一個`boolean`值，指出目標資源是否自動更新為新標頭資源的`Id`型識別碼。 在此範例中，因為相依關係，所以指定了值`true`。
   * 表示是否已指定目標標頭的`boolean`值。 在此範例中，指定值`true`。
   * 為最後一個引數傳遞`null`。

   您也可以叫用`RepositoryServiceService`物件的`getRelated`方法，並傳入下列引數，以擷取指定資源的相關資源清單：

   * 要擷取相關資源的資源URI。 在此範例中，指定來源資源( `"/testFolder/testResource1"`)。
   * 表示指定的資源是否為關聯性中的來源資源的`boolean`值。 在此範例中，指定值`true`，因為情況如此。
   * 表示是否已指定來源資源的`boolean`值。 在此範例中，提供了值`true`。
   * 包含關聯性型別的整數陣列。 在此範例中，相依關係是使用先前使用的陣列中的相同值來指定： `3`。
   * 傳入`null`以取得其餘兩個引數。

   `getRelated`方法傳回可以轉換為`Resource`物件的物件陣列，您可以透過該陣列反複擷取每個相關資源。 在此範例中，`testResource2`應該位於傳回的資源清單中。

**另請參閱**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 鎖定資源 {#locking-resources}

您可以鎖定資源或資源集，以供特定使用者獨佔使用，或供多個使用者共用。 共用鎖定表示資源會發生狀況，但不會防止其他人員對該資源採取動作。 共用鎖定應視為訊號機制。 專屬鎖定表示鎖定資源的使用者將會變更資源，而鎖定可確保除非使用者不再需要存取資源且已解除鎖定，否則其他人都無法變更。 如果存放庫管理員解除鎖定資源，該資源的所有專屬和共用鎖定都會自動移除。 這類動作適用於使用者不再可用且尚未解除鎖定資源的情況。

鎖定資源時，當您在Workbench中檢視「資源」標籤時，會出現鎖定圖示，如下圖所示。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

您可以使用存放庫服務Java API或Web服務API，以程式設計方式控制對資源的存取。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

若要鎖定和解鎖資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定要鎖定的資源的URI。
1. 鎖定資源。
1. 擷取資源的鎖定。
1. 解除鎖定資源

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定要鎖定的資源的URI**

建立包含要鎖定之資源的URI的字串。 語法包含正斜線，如同此範例： &quot;/*path*/*resource*&quot;。

**鎖定資源**

叫用存放庫服務方法來鎖定資源，指定URI、鎖定型別和鎖定深度。

**擷取資源的鎖定**

叫用儲存庫服務方法以擷取資源的鎖定，並指定URI。

**解除鎖定資源**

叫用存放庫服務方法來解除鎖定資源，指定URI。

**另請參閱**

[使用Java API鎖定資源](aem-forms-repository.md#lock-resources-using-the-java-api)

[使用Web服務API鎖定資源](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API鎖定資源 {#lock-resources-using-the-java-api}

使用存放庫服務API (Java)鎖定資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。

1. 指定要鎖定的資源的URI

   指定要鎖定的資源的URI。 在此案例中，由於名為`testResource`的資源位於名為`testFolder`的資料夾中，其URI為`"/testFolder/testResource"`。 URI會儲存為`java.lang.String`物件。

1. 鎖定資源

   叫用`ResourceRepositoryClient`物件的`lockResource`方法，並傳入下列引數：

   * 資源的URI。
   * 鎖定範圍。 在此範例中，由於資源將被鎖定以供獨佔使用，因此鎖定範圍指定為`com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`。
   * 鎖定深度。 在此範例中，由於鎖定只會套用至特定資源，不會套用至其任何成員或子系，因此鎖定深度會指定為`Lock.DEPTH_ZERO`。

   >[!NOTE]
   >
   >需要四個引數的`lockResource`方法多載版本擲回例外狀況。 請確保使用需要三個引數的`lockResource`方法，如本逐步說明中所示。

1. 擷取資源的鎖定

   叫用`ResourceRepositoryClient`物件的`getLocks`方法，並將資源的URI作為引數傳遞。 此方法會傳回Lock物件清單，您可以透過該清單進行反複運算。 在此範例中，透過分別叫用每個鎖定物件的`getOwnerUserId`、`getDepth`和`getType`方法，為每個物件列印鎖定擁有者、深度和範圍。

1. 解除鎖定資源

   叫用`ResourceRepositoryClient`物件的`unlockResource`方法，並將資源的URI作為引數傳遞。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**另請參閱**

[鎖定資源](aem-forms-repository.md#locking-resources)

[快速入門(SOAP模式)：使用Java API鎖定資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API鎖定資源 {#lock-resources-using-the-web-service-api}

使用存放庫服務API （Web服務）鎖定資源：

1. 包含專案檔案

   * 使用Base64建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`RepositoryServiceService`物件。 使用包含使用者名稱和密碼的`System.Net.NetworkCredential`物件設定其`Credentials`屬性。

1. 指定要鎖定的資源的URI

   指定包含要鎖定之資源URI的字串。 在此案例中，由於名為`testResource`的資源位於資料夾`testFolder`中，其URI為`"/testFolder/testResource"`。 使用與Microsoft .NET Framework相容的語言時（例如C#），請將URI儲存在`System.String`物件中。

1. 鎖定資源

   叫用`RepositoryServiceService`物件的`lockResource`方法，並傳入下列引數：

   * 資源的URI。
   * 鎖定範圍。 在此範例中，由於資源將被鎖定以供獨佔使用，因此鎖定範圍指定為`11`。
   * 鎖定深度。 在此範例中，由於鎖定只會套用至特定資源，不會套用至其任何成員或子系，因此鎖定深度會指定為`2`。
   * 表示鎖定到期前的秒數的`int`值。 在此範例中，使用`1000`的值。
   * 為最後一個引數傳遞`null`。

1. 擷取資源的鎖定

   叫用`RepositoryServiceService`物件的`getLocks`方法，並傳遞資源的URI做為第一個引數，並為第二個引數傳遞`null`。 此方法傳回包含`Lock`物件的`object`陣列，您可以透過該陣列進行反複運算。 在此範例中，透過分別存取每個`Lock`物件的`ownerUserId`、`depth`和`type`欄位，為每個物件列印鎖定擁有者、深度和範圍。

1. 解除鎖定資源

   叫用`RepositoryServiceService`物件的`unlockResource`方法，並傳遞資源的URI做為第一個引數，並為第二個引數傳遞`null`。

**另請參閱**

[鎖定資源](aem-forms-repository.md#locking-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 刪除資源 {#deleting-resources}

您可以使用存放庫服務Java API(SOAP)，以程式設計方式從存放庫中的指定位置刪除資源。

當您刪除資源時，刪除通常是永久性的，但在某些情況下，ECM存放庫可能會根據其歷史記錄機制來儲存資源的版本。 因此，在刪除資源時，請務必確保您永遠不需要該資源。 刪除資源的常見原因包括需要增加資料庫中的可用空間。 您可以刪除資源的版本，但如果您這樣做，您必須指定資源識別碼，而不是其邏輯識別碼(LID)或路徑。 如果您刪除資料夾，則該資料夾中的所有專案（包括子資料夾和資源）都會自動刪除。

不會刪除相關資源。 例如，如果您有一個使用logo.gif檔案的表單，當您刪除logo.gif時，關係將會儲存在擱置關係表中。 另外，對於版本淘汰，請將最新版本的物件狀態設定為「淘汰」。

在ECM系統中，刪除操作不是交易安全的。 例如，如果您嘗試刪除100個資源，而第50個資源的作業失敗，則會刪除前49個執行個體，但其餘的執行個體不會刪除。 否則，預設行為是回覆（非承諾）。

>[!NOTE]
>
>在搭配ECM存放庫(EMC Documentum Content Server和IBM FileNet P8 Content Manager)使用`com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()`方法時，如果刪除其中一個指定資源失敗，則不會復原交易，這表示無法刪除已刪除的檔案。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

若要刪除資源，請執行下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定要刪除之資源的URI。
1. 刪除資源。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定要刪除之資源的URI**

建立包含要刪除之資源URI的字串。 語法包含正斜線，如同此範例： &quot;/*path*/*resource*&quot;。 如果要刪除的資源是資料夾，則會遞回刪除。

**刪除資源**

叫用存放庫服務方法以刪除資源，指定URI。

**另請參閱**

[使用Java API刪除資源](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[使用網站服務API刪除資源](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API(SOAP)刪除資源 {#delete-resources-using-the-java-api-soap}

使用存放庫API (Java)刪除資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。

1. 指定要刪除的資源的URI

   指定要擷取的資源URI。 在此案例中，由於名為testResourceToBeDeleted的資源位於名為testFolder的資料夾中，其URI為`/testFolder/testResourceToBeDeleted`。 URI會儲存為`java.lang.String`物件。 在此範例中，資源會先寫入存放庫，並擷取其URI。 如需有關寫入資源的詳細資訊，請參閱[寫入資源](aem-forms-repository.md#writing-resources)。

1. 刪除資源

   叫用`ResourceRepositoryClient`物件的`deleteResource`方法，並將資源的URI作為引數傳遞。

**另請參閱**

[刪除資源](aem-forms-repository.md#deleting-resources)

[快速入門(SOAP模式)：使用Java API搜尋資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API刪除資源 {#delete-resources-using-the-web-service-api}

使用存放庫API （Web服務）刪除資源：

1. 包含專案檔案

   * 使用Base64建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`RepositoryServiceService`物件。 使用包含使用者名稱和密碼的`System.Net.NetworkCredential`物件設定其`Credentials`屬性。

1. 指定要刪除的資源的URI

   指定要擷取的資源URI。 在此案例中，由於名為`testResourceToBeDeleted`的資源位於名為`testFolder`的資料夾中，其URI為`"/testFolder/testResourceToBeDeleted"`。 在此範例中，資源會先寫入存放庫，並擷取其URI。 如需有關寫入資源的詳細資訊，請參閱[寫入資源](aem-forms-repository.md#writing-resources)。

1. 刪除資源

   叫用`RepositoryServiceService`物件的`deleteResources`方法，並傳遞包含資源URI的`System.String`陣列做為第一個引數。 為第二個引數傳遞`null`。

**另請參閱**

[刪除資源](aem-forms-repository.md#deleting-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
