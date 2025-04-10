---
title: 為草稿和提交設定儲存服務
description: 瞭解如何設定草稿和提交的儲存空間
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
exl-id: 33769e4f-2213-442b-bd1c-1728cd917460
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 為草稿和提交設定儲存服務 {#configuring-storage-services-for-drafts-and-submissions}

## 概觀 {#overview}

透過AEM Forms，您可以儲存：

* **草稿**：一般使用者填寫並儲存以供稍後使用，以及之後提交的工作中表單。

* **提交專案**：提交的表單包含使用者提供的資料。

AEM Forms入口網站資料和中繼資料服務提供草稿和提交方式的支援。 依預設，資料會儲存在發佈執行個體中，然後反向復寫至已設定的製作執行個體，以供滲透至其他發佈執行個體。

現有的現成可用方法問題是將所有資料儲存在發佈執行個體上，包括可能是個人識別資訊(PII)的資料。

除了上述預設方法之外，也有替代實施方法可用來直接推送表單資料進行處理，而非儲存於本機。 擔心在發佈執行個體上儲存潛在敏感資料的客戶，可選擇將資料傳送至處理伺服器的替代實作。 由於處理作業會在製作執行個體上進行，因此通常會保留在安全區域中。

>[!NOTE]
>
>當您使用Forms入口網站提交動作或啟用最適化表單中的將資料儲存在表單入口網站選項時，表單資料會儲存在AEM存放庫中。 在生產環境中，建議不要將草稿或提交的表單資料儲存在AEM存放庫中。 相反地，您必須將草稿和提交元件與安全的儲存裝置（例如企業資料庫）整合，以儲存草稿和提交的表單資料。
>
>如需詳細資訊，請參閱[將草稿與提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)。

## 設定Forms Portal草稿和提交服務 {#configuring-forms-portal-drafts-and-submissions-services}

在AEM Web主控台設定( `https://[host]:'port'/system/console/configMgr`)中，按一下以在編輯模式中開啟&#x200B;**Forms入口網站草稿和提交設定**。

根據您的需求指定屬性的值，如下所述：

### 開箱即用的服務，用於儲存發佈執行個體上的資料 {#out-of-the-box-services-to-store-data-on-publish-instance}

將資料反向復寫至設定的製作執行個體。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms入口網站草稿資料服務(草稿資料服務的識別碼(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms入口網站草稿中繼資料服務(草稿中繼資料服務的識別碼(<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms入口網站提交資料服務(提交資料服務的識別碼(<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms入口網站提交中繼資料服務(提交中繼資料服務的識別碼(<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### 開箱即用的服務，用於儲存遠端處理執行個體上的資料 {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

資料會直接推送至已設定的遠端執行個體

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms入口網站草稿資料服務(草稿資料服務的識別碼(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms入口網站草稿中繼資料服務(草稿中繼資料服務的識別碼(<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms入口網站提交資料服務(提交資料服務的識別碼(<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms入口網站提交中繼資料服務(提交中繼資料服務的識別碼(<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

除了上述指定的設定之外，請提供已設定遠端處理執行個體的相關資訊。

在AEM Web主控台設定( `https://[host]:'port'/system/console/configMgr`)中，按一下以在編輯模式中開啟&#x200B;**AEM DS設定服務**。 在AEM DS設定服務對話方塊中，提供有關處理伺服器URL、處理伺服器使用者名稱和密碼的資訊。

>[!NOTE]
>
>也提供將使用者資料儲存在資料庫中的範例實作。 若要瞭解如何設定資料和中繼資料服務，以將使用者資料儲存在外部資料庫中，請參閱[將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)。
