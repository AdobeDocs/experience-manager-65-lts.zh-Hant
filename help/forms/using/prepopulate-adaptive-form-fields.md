---
title: 預填自適應表單欄位
description: 使用現有資料預先填寫最適化表單的欄位。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 69734a2b-7f9d-4661-a1e9-3bf6e362c272
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 3%

---

# 預填自適應表單欄位{#prefill-adaptive-form-fields}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

## 簡介 {#introduction}

您可以使用現有資料預先填寫最適化表單的欄位。 當使用者開啟表單時，這些欄位的值將被預填。 若要在調適型表單中預填資料，請遵循該格式以預填調適型表單的資料結構，讓使用者資料可作為預填XML/JSON使用。

## 預填資料的結構 {#the-prefill-structure}

調適型表單可以混合有已繫結和未繫結的欄位。 繫結欄位是從「內容尋找器」標籤拖曳的欄位，在欄位編輯對話方塊中包含非空白的`bindRef`屬性值。 未繫結欄位是從Sidekick的元件瀏覽器直接拖曳，並具有空的`bindRef`值。

您可以預先填寫最適化表單的繫結和未繫結欄位。 預填資料包含afBoundData和afUnBoundData區段，以預填調適型表單的繫結和未繫結欄位。 `afBoundData`區段包含繫結欄位和面板的預填資料。 此資料必須符合關聯的表單模型結構描述：

* 針對使用[XFA表單範本](../../forms/using/prepopulate-adaptive-form-fields.md)的最適化表單，請使用與XFA範本的資料結構描述相容的預填XML。
* 針對使用[XML結構描述](#xml-schema-af)的適用性表單，請使用符合XML結構描述結構的預填XML。
* 針對使用[JSON結構描述](#json-schema-based-adaptive-forms)的最適化表單，請使用符合JSON結構描述的預先填入JSON。
* 針對使用FDM架構的適用性表單，請使用符合FDM架構的預填JSON。
* 對於具有[無表單模型](#adaptive-form-with-no-form-model)的最適化表單，沒有繫結資料。 每個欄位都是未繫結的欄位，並使用未繫結的XML預先填入。

### 預填XML結構範例 {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### 預填JSON結構範例 {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

對於具有相同bindref的繫結欄位或具有相同名稱的未繫結欄位，所有欄位都會填入XML標籤或JSON物件中指定的資料。 例如，表單中的兩個欄位對應到預填資料中的名稱`textbox`。 在執行階段，如果第一個文字方塊欄位包含「A」，則第二個文字方塊會自動填入「A」。 此連結稱為自適應表單欄位的即時連結。

### 使用XFA表單範本的最適化表單 {#xfa-based-af}

針對XFA型調適型表單預先填入XML與提交的XML的結構如下：

* **預填XML結構**：XFA型最適化表單的預填XML必須符合XFA表單範本的資料結構描述。 若要預填未繫結欄位，請將預填XML結構包裝成`/afData/afBoundData`標籤。

* **已提交的XML結構**：當未使用預填XML時，已提交的XML包含`afData`包裝函式標籤中繫結和未繫結欄位的資料。 如果使用預填XML，則提交的XML具有與預填XML相同的結構。 如果預填XML以`afData`根標籤開頭，則輸出XML也具有相同的格式。 如果預填XML沒有`afData/afBoundData`包裝函式，而是直接從結構描述根標籤（如`employeeData`）開始，則提交的XML也會從`employeeData`標籤開始。

Prefill-Submit-Data-ContentPackage.zip

[取得檔案](assets/prefill-submit-data-contentpackage.zip)
包含預填資料和已提交資料的範例

### XML結構描述型調適型表單  {#xml-schema-af}

根據XML結構描述的最適化表單的預填XML和已提交的XML結構如下：

* **預填XML結構**：預填XML必須符合關聯的XML結構描述。 若要預填未繫結欄位，請將預填XML結構包裝在/afData/afBoundData標籤中。
* **已送出的XML結構**：如果未使用預填XML，則送出的XML會包含`afData`包裝函式標籤中繫結和未繫結欄位的資料。 如果使用預填XML，則提交的XML具有與預填XML相同的結構。 如果預填XML以`afData`根標籤開頭，則輸出XML的格式會相同。 如果預填XML沒有`afData/afBoundData`包裝函式，而是直接從結構描述根標籤（如`employeeData`）開始，則提交的XML也會以`employeeData`標籤開始。

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

對於模型為XML結構描述的欄位，資料會預先填入`afBoundData`標籤，如下面的範例XML所示。 它可用來以一或多個未繫結文字欄位預先填寫調適型表單。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>建議不要在繫結面板(具有非空白`bindRef`且已透過從Sidekick或「資料來源」索引標籤拖曳元件而建立的面板)中使用未繫結欄位。 這可能會導致這些未繫結欄位的資料遺失。 此外，建議整個表單中的欄位名稱必須是唯一的，尤其是未繫結的欄位。

#### 不含afData和afBoundData包裝函式的範例 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### JSON結構描述型調適型表單 {#json-schema-based-adaptive-forms}

針對以JSON結構為基礎的適用性表單，底下說明預填JSON和已提交JSON的結構。 如需詳細資訊，請參閱[使用JSON結構描述建立最適化表單](../../forms/using/adaptive-form-json-schema-form-model.md)。

* **預填JSON結構**：預填JSON必須符合關聯的JSON結構描述。 如果您也想要預先填入未繫結欄位，可以選擇將其包裝到/afData/afBoundData物件中。
* **已提交的JSON結構**：如果未使用預填JSON，則已提交的JSON會包含afData包裝函式標籤中繫結和未繫結欄位的資料。 如果使用預填JSON，則提交的JSON將與預填JSON具有相同的結構。 如果預填JSON以afData根物件開頭，則輸出JSON會具有相同的格式。 如果預填JSON沒有afData/afBoundData包裝函式，而是直接從結構描述根物件（例如使用者）開始，則提交的JSON也會從使用者物件開始。

```json
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

對於使用JSON結構描述模型的欄位，資料會預先填入afBoundData物件，如下面的範例JSON所示。 它可用來以一或多個未繫結文字欄位預先填寫調適型表單。 以下是具有`afData/afBoundData`包裝函式的資料範例：

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

以下是沒有`afData/afBoundData`包裝函式的範例：

```json
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>不建議在繫結面板(具有非空白bindRef的面板，這些面板是從Sidekick或「資料來源」索引標籤拖曳元件而建立的)中使用未繫結欄位，因為這可能會造成未繫結欄位的資料遺失。**&#x200B;** 建議在表單中設定唯一的欄位名稱，尤其是未繫結欄位。

### 無表單模型的最適化表單 {#adaptive-form-with-no-form-model}

針對沒有表單模型的最適化表單，所有欄位的資料都在`<afUnboundData> tag`的`<data>`標籤下。

此外，請注意下列事項：

針對針對各種欄位提交的使用者資料所產生的XML標籤，是使用欄位名稱產生的。 因此，欄位名稱必須是唯一的。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## 使用Configuration Manager設定預填服務 {#configuring-prefill-service-using-configuration-manager}

若要啟用預填服務，請在「AEM Web主控台設定」中指定「預設預填服務設定」 。 使用下列步驟來設定預填服務：

>[!NOTE]
>
>預填服務設定適用於最適化表單、HTML5表單及HTML5表單集。

1. 使用URL開啟&#x200B;**[!UICONTROL Adobe Experience Manager Web主控台組態]**：\
   https://&lt;server>：&lt;port>/system/console/configMgr
1. 搜尋並開啟&#x200B;**[!UICONTROL 預設預填服務組態]**。

   ![預填設定](assets/prefill_config_new.png)

1. 輸入&#x200B;**資料檔位置**&#x200B;的資料位置或規則運算式（規則運算式）。 有效資料檔案位置的範例為：

   * file:///C:/Users/public/Document/Prefill/.&#42;
   * https://localhost:8000/somesamplexmlfile.xml

   >[!NOTE]
   >
   >預設情況下，所有型別的調適型Forms （XSD、XDP、JSON、FDM以及無表單模型型）都允許透過crx檔案進行預填。 只有JSON和XML檔案才允許預填。

1. 您的表單現已設定預填服務。

   >[!NOTE]
   >
   >crx通訊協定會負責預先填入的資料安全性，因此預設允許。 透過其他通訊協定使用通用regex預先填寫可能會造成漏洞。 在設定中，指定用於保護資料的安全URL設定。

## 可重複面板的奇怪情況 {#the-curious-case-of-repeatable-panels}

通常，繫結（表單結構描述）和未繫結欄位會以相同的調適型表單編寫，但如果繫結是可重複的，則有下列幾個例外：

* 使用XFA表單範本、XSD、JSON結構描述或FDM結構描述的適用性表單不支援未繫結的可重複面板。
* 請勿在已繫結的可重複面板中使用未繫結欄位。

>[!NOTE]
>
>根據經驗，如果繫結和未繫結欄位在終端使用者填寫的資料中相交，請勿將其混合在一起。 如果可能的話，您應該修改結構描述或XFA表單範本，並為未繫結欄位新增專案，這樣它也會變成繫結，而且其資料可以像提交資料中的其他欄位一樣使用。

## 預填使用者資料的支援通訊協定 {#supported-protocols-for-prefilling-user-data}

使用有效的規則運算式設定時，可透過下列通訊協定，以預填資料格式預填適用性表單的使用者資料：

### crx://通訊協定 {#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

指定的節點必須具有名為`jcr:data`的屬性並儲存資料。

### file://通訊協定  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

參照的檔案必須在相同的伺服器上。

### https://通訊協定 {#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### service://通訊協定 {#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME是指OSGI預填服務的名稱。 請參考[建立並執行預填服務](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)。
* 識別碼會參照OSGI預填服務擷取預填資料所需的任何中繼資料。 登入使用者的識別碼是可使用的中繼資料範例。

>[!NOTE]
>
>不支援傳遞驗證引數。

### 在slingRequest中設定資料屬性 {#setting-data-attribute-in-slingrequest}

您也可以在`slingRequest`中設定`data`屬性，其中`data`屬性是包含XML或JSON的字串，如下列範常式式碼所示（範例為XML）：

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

您可以撰寫包含所有資料的簡單XML或JSON字串，並在slingRequest中進行設定。 您可以在轉譯器JSP中針對任何元件輕鬆完成這項操作，您想要將元件加入可設定slingRequest資料屬性的頁面中。

例如，您想要為具有特定標題型別的頁面使用特定設計的位置。 若要達成此目的，您可以撰寫自己的`header.jsp`，將其包含在頁面元件中並設定`data`屬性。

另一個很好的範例是使用案例，您想要在透過Facebook、Twitter或LinkedIn等社交帳戶登入時預先填入資料。 在此情況下，您可以在`header.jsp`中加入簡單的JSP，它會從使用者帳戶擷取資料並設定資料引數。

預填頁面component.zip

[取得檔案](assets/prefill-page-component.zip)
頁面元件中的prefill.jsp範例

## AEM Forms自訂預填服務 {#aem-forms-custom-prefill-service}

您可以針對持續從預先定義的來源讀取資料的情況，使用自訂預填服務。 預填服務會從已定義的資料來源讀取資料，並使用預填資料檔案的內容預填調適型表單的欄位。 它還有助於您將預填的資料與最適化表單永久建立關聯。

### 建立並執行預填服務 {#create-and-run-a-prefill-service}

預填服務是一項OSGi服務，會透過OSGi套件組合封裝。 您可以建立OSGi套件組合、上傳並安裝至AEM Forms套件組合。 開始建立套件組合之前：

* [下載AEM Forms使用者端SDK](https://helpx.adobe.com/tw/aem-forms/kb/aem-forms-releases.html)
* 下載範本套件

* 將資料（預填資料）檔案放入crx存放庫中。 您可以將檔案放置在crx-repository的\contents資料夾中的任何位置。

[取得檔案](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 建立預填服務 {#create-a-prefill-service}

樣板套件（範例預填服務套件）包含AEM Forms預填服務的範例實作。 在程式碼編輯器中開啟樣板套件。 例如，在Eclipse中開啟範本專案進行編輯。 在程式碼編輯器中開啟樣板套件後，請執行以下步驟來建立服務。

1. 開啟src\main\java\com\adobe\test\Prefill.java檔案進行編輯。
1. 在程式碼中，設定值：

   * `nodePath:`指向crx存放庫位置的節點路徑變數包含資料（預填）檔案的路徑。 例如， /content/prefilldata.xml
   * `label:` label引數指定服務的顯示名稱。 例如，預設預填服務

1. 儲存並關閉`Prefill.java`檔案。
1. 將`AEM Forms Client SDK`套件新增至樣版專案的建置路徑。
1. 編譯專案並為該套件組合建立.jar。

#### 啟動並使用預填服務 {#start-and-use-the-prefill-service}

若要啟動預填服務，請上傳JAR檔案至AEM Forms Web主控台，然後啟動服務。 現在，該服務開始出現在最適化表單編輯器中。 若要將預填服務關聯至調適型表單：

1. 在Forms編輯器中開啟最適化表單，然後開啟表單容器的「屬性」面板。
1. 在「屬性」主控台中，導覽至「AEM Forms容器>基本>預填服務」 。
1. 選取預設預填服務，然後按一下&#x200B;**[!UICONTROL 儲存]**。 此服務與表單相關聯。

## 在使用者端預先填入資料 {#prefill-at-client}

預先填寫最適化表單時，AEM Forms伺服器會將資料與最適化表單合併，並將填寫的表單傳送給您。 依預設，資料合併動作會在伺服器上進行。

您可以設定AEM Forms伺服器，在使用者端而非伺服器上執行資料合併動作。 它大幅減少預填和轉譯調適型表單所需的時間。 預設會停用該功能。 您可以從Configuration Manager或命令列啟用它。

* 若要從組態管理員啟用或停用：
   1. 開啟AEM Configuration Manager。
   1. 找到並開啟最適化表單和互動式通訊Web Channel設定
   1. 啟用Configuration.af.clientside.datamerge.enabled.name選項
* 若要從命令列啟用或停用：
   * 若要啟用，請執行下列cURL命令：

     `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * 若要停用，請執行下列cURL命令：

     `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  若要充分利用使用者端上的預先填入資料選項，請更新預填服務以傳回[FileAttachmentMap](https://helpx.adobe.com/tw/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)和[CustomContext](https://helpx.adobe.com/tw/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)
