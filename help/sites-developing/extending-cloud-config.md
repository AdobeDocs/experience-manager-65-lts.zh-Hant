---
title: 雲端服務設定
description: 您可以擴充現有執行個體來建立自己的設定
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6b9b8d8c-8cd5-4c21-9b75-acd74d00354a
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# 雲端服務設定{#cloud-service-configurations}

設定旨在提供儲存服務設定的邏輯和結構。

您可以擴充現有執行個體來建立自己的設定。

## 概念 {#concepts}

開發組態時採用的原則以下列概念為基礎：

* 服務/介面卡用於擷取組態。
* 設定（例如屬性/段落）繼承自父項。
* 依路徑從Analytics節點參照。
* 可輕鬆擴充。
* 具有彈性以因應更複雜的組態，例如[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)。
* 相依性支援(例如，[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)外掛程式需要[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)設定)。

## 結構 {#structure}

設定的基本路徑為：

`/etc/cloudservices`。

對於每種設定型別，都會提供範本和元件。 如此一來，設定範本就能在客製化後滿足大部分的需求。

若要提供新服務的組態，請執行下列動作：

* 在中建立服務範圍

  `/etc/cloudservices`

* 在此底下：

   * 設定範本
   * 設定元件

範本和元件必須繼承基底範本的`sling:resourceSuperType`：

`cq/cloudserviceconfigs/templates/configpage`

或基礎元件分別使用

`cq/cloudserviceconfigs/components/configpage`

服務提供者也應該提供服務頁面：

`/etc/cloudservices/<service-name>`

### 範本 {#template}

您的範本會擴充基礎範本：

`cq/cloudserviceconfigs/templates/configpage`

並定義指向自訂元件的`resourceType`。

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### 元件 {#components}

您的元件應擴充基礎元件：

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

設定範本和元件後，您可以在下方新增子頁面以新增設定：

`/etc/cloudservices/<service-name>`

### 內容模型 {#content-model}

內容模型儲存為`cq:Page`，位於：

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

組態儲存在子節點`jcr:content`下。

* 對話方塊中定義的固定屬性應直接儲存在`jcr:node`上。
* 動態元素（使用`parsys`或`iparsys`）使用子節點來儲存元件資料。

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

如需API的參考檔案，請參閱[com.day.cq.wcm.webservicesupport](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html)。

### AEM整合 {#aem-integration}

可用的服務列在&#x200B;**頁面屬性**&#x200B;對話方塊（繼承自`foundation/components/page`或`wcm/mobile/components/page`的任何頁面）的&#x200B;**雲端服務**&#x200B;索引標籤中。

標籤也提供：

* 您可啟用服務之位置的連結
* 從路徑欄位選擇設定（服務的子節點）

#### 密碼加密 {#password-encryption}

儲存服務的使用者認證時，所有密碼都應該加密。

您可以新增隱藏的表單欄位來達成此目的。 此欄位的屬性名稱中應該有註解`@Encrypted`；也就是說，對於`password`欄位，名稱將寫成：

`password@Encrypted`

然後`EncryptionPostProcessor`會自動加密屬性（使用`CryptoSupport`服務）。

>[!NOTE]
>
>這與標準` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)`註解類似。

>[!NOTE]
>
>根據預設，`EcryptionPostProcessor`只會加密對`/etc/cloudservices`提出的`POST`個請求。

#### 服務頁面的其他屬性jcr：content節點 {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>componentreference</td>
   <td>要自動納入頁面中的元件的參照路徑。<br />這用於其他功能和JS包含。<br />這包含在包含<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br />的頁面上的元件（通常在<code>body</code>標籤之前）。<br />若是Adobe Analytics和Adobe Target，我們會使用這個包含其他功能，例如JavaScript呼叫以追蹤訪客行為。</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>服務的簡短說明。<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>服務的延伸說明。</td>
  </tr>
  <tr>
   <td>排名</td>
   <td>用於清單中的服務排名。</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>用於在頁面屬性對話方塊中顯示設定的篩選器。</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>服務網站的URL。</td>
  </tr>
  <tr>
   <td>serviceUrlLable</td>
   <td>服務URL標籤。</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>服務的縮圖路徑。</td>
  </tr>
  <tr>
   <td>可見</td>
   <td>頁面屬性對話方塊中的可見度；預設為可見（選擇性）</td>
  </tr>
 </tbody>
</table>

### 使用案例 {#use-cases}

預設會提供下列服務：

* [追蹤器代碼片段](/help/sites-administering/external-providers.md) (Google、WebTrends等)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>另請參閱[建立自訂Cloud Service](/help/sites-developing/extending-cloud-config-custom-cloud.md)。
