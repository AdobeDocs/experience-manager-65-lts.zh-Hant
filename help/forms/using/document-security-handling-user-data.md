---
title: Document Security | 處理使用者資料
description: 瞭解AEM Forms Document Security如何讓您管理使用者資料和資料儲存，以及存取、刪除和匯出使用者資料。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
exl-id: c619a3b8-cd06-4f5d-af20-67f3a4bfcdce
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Document Security | 處理使用者資料 {#document-security-handling-user-data}

AEM Forms document security可讓您建立、儲存及套用預先定義的安全性設定至您的檔案。 可確保只有授權的使用者才能使用檔案。 您可以使用原則來保護檔案。 原則是包含安全性設定和授權使用者清單的資訊集合。 您可以將原則套用至一或多個檔案，並授權新增至AEM Forms JEE使用者管理中的使用者。

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## 使用者資料和資料存放區 {#user-data-and-data-stores}

Document Security會將與受保護檔案相關的原則和資料（包括資料庫中的使用者資料）儲存，例如My Sql、Oracle、MS® SQL Server和IBM® DB2®。 此外，原則中授權使用者的資料會儲存在使用者管理中。 如需有關儲存在使用者管理中的資料的資訊，請參閱[Forms使用者管理：處理使用者資料](/help/forms/using/user-management-handling-user-data.md)。

下表對應Document Security組織資料庫表格中資料的方式。

<table>
 <tbody>
  <tr>
   <td>資料庫表格</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>儲存使用者主要金鑰的相關資訊。 這些金鑰用於離線Document Security工作流程。</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>儲存有關稽核事件（如使用者事件、檔案事件和原則事件）的資訊。</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>儲存受保護檔案的記錄。 它會儲存每個受保護檔案的授權詳細資料。</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>儲存系統中建立的每個授權的檔名稱。</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>儲存受保護檔案撤銷與復原的相關資訊。</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>儲存使用者可建立個人原則的資訊，這些個人原則會顯示在「原則」頁面的「我的原則」標籤下。 </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>儲存原則的相關資訊。 每個原則都對應至此表格中的一列。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>儲存使用中原則的XML檔案。 原則XML<sup> </sup>包含對與該原則相關聯之使用者之主體ID的參照。 原則XML會儲存為Blob物件。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>儲存已封存原則的相關資訊。 封存的原則包含其原則XML儲存為Blob物件。</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code><br /> (Oracle和MS® SQL資料庫)</p> </td>
   <td>儲存原則集和使用者之間的對應。</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>儲存受邀使用者的相關資訊。</td>
  </tr>
 </tbody>
</table>

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以存取和匯出資料庫中使用者的Document Security資料，並在必要時永久刪除資料。

若要從資料庫匯出或刪除使用者資料，您必須使用資料庫使用者端連線到資料庫，並根據使用者的某些個人識別資訊找出主體ID。 例如，若要使用登入ID擷取使用者的主體ID，請在資料庫上執行下列`select`命令。

在`select`命令中，將`<user_login_id>`取代為您要從`EdcPrincipalUserEntity`資料庫資料表中擷取其主體識別碼之使用者的登入識別碼。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

一旦您知道主體ID，就可以匯出或刪除使用者資料。

### 匯出使用者資料 {#export-user-data}

執行下列資料庫命令，以便您從資料庫表格匯出主參與者ID的使用者資料。 在`select`命令中，將`<principal_id>`取代為您要匯出其資料之使用者的主體ID。

>[!NOTE]
>
>下列命令使用My SQL和IBM® DB2®資料庫中的資料庫表格名稱。 在Oracle和MS® SQL資料庫上執行這些命令時，請將`EdcPolicySetPrincipalEntity`取代為命令中的`EdcPolicySetPrincipalEnt`。

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>若要從`EdcAuditEntity`資料表匯出資料，請使用採用[EventSearchFilter](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html)作為引數的[EventManager.exportEvents](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API，以匯出根據`principalId`、`policyId`或`licenseId`的稽核資料。

若要取得系統中使用者的完整資料，您必須存取並匯出使用者管理資料庫中的資料。 如需詳細資訊，請參閱[Forms使用者管理：處理使用者資料](/help/forms/using/user-management-handling-user-data.md)。

### 刪除使用者資料 {#delete-user-data}

執行下列動作，從資料庫表格中刪除主體ID的Document Security資料。

1. 關閉AEM Forms伺服器。
1. 執行以下資料庫命令，以便從資料庫表格中刪除主體ID的資料，以確保Document Security。 在`Delete`命令中，將`<principal_id>`取代為您要刪除其資料之使用者的主體ID。

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >若要從`EdcAuditEntity`資料表中刪除資料，請使用以[EventSearchFilter](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html)為引數的[EventManager.deleteEvents](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API，以根據`principalId`、`policyId`或`licenseId`刪除稽核資料。

1. 使用中和封存的原則XML檔案分別儲存在`EdcPolicyXmlEntity`和`EdcPolicyArchiveEntity`資料庫資料表中。 若要從這些表格中刪除使用者的資料，請執行下列動作：

   1. 開啟`EdcPolicyXMLEntity`或`EdcPolicyArchiveEntity`資料表中每一資料列的XML Blob並擷取XML檔案。 XML檔案類似於下面所示的檔案。
   1. 編輯XML檔案，以便移除主參與者ID的blob。
   1. 對另一個檔案重複步驟1和2。

   >[!NOTE]
   >
   >移除主體ID之`Principal`標籤內的完整blob，否則原則XML可能會損毀或無法使用。

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   除了直接從`EdcPolicyXmlEntity`表格中刪除資料之外，還有另外兩種方法可以達成此目的：

   **使用管理主控台**

   1. 以管理員身分登入https://[*server*]：[*port*]/adminui的Forms JEE管理主控台。
   1. 瀏覽至&#x200B;**[!UICONTROL 服務> Document Security >原則集]**。
   1. 開啟原則集並從原則中刪除使用者。

   **使用Document Security網頁**

   有權建立個人原則的Document Security使用者可以從其原則中刪除使用者資料。 若要這麼做：

   1. 具有個人原則的使用者登入其Document Security網頁，網址為https://[*伺服器*]：[*連線埠*]/edc。
   1. 瀏覽至&#x200B;**[!UICONTROL 服務> Document Security >我的原則]**。
   1. 開啟原則並從原則中刪除使用者。

   >[!NOTE]
   >
   >管理員可以使用管理主控台，從&#x200B;**[!UICONTROL 服務>檔案安全性>我的原則]**&#x200B;中的其他使用者的個人原則搜尋、存取和刪除使用者資料。

1. 從使用者管理資料庫刪除主體ID的資料。 如需詳細步驟，請參閱[Forms使用者管理 | 正在處理使用者資料](/help/forms/using/user-management-handling-user-data.md)。
1. 啟動AEM Forms伺服器。
