---
title: Adobe Experience Manager中的服務使用者
description: 瞭解Adobe Experience Manager中的服務使用者。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 893d04cb-3a71-4400-9ca4-62ad46aacfdd
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 0%

---

# Adobe Experience Manager (AEM)中的服務使用者 {#service-users-in-aem}

## 概觀 {#overview}

在AEM中取得管理工作階段或資源解析程式的主要方式是使用Sling提供的`SlingRepository.loginAdministrative()`和`ResourceResolverFactory.getAdministrativeResourceResolver()`方法。

但是，這兩種方法都不是依照最低許可權的[原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)設計的。 如此一來，開發人員就很容易無法及早針對內容規劃適當的結構和對應的存取控制層級(ACL)。 如果此類服務中存在漏洞，即使程式碼本身不需要系統管理許可權即可運作，也經常會導致許可權升級至`admin`使用者。

## 如何逐步淘汰管理員工作階段 {#how-to-phase-out-admin-sessions}

### 優先順序0：功能是否啟用/需要/已棄用？ {#priority-is-the-feature-active-needed-derelict}

某些情況下可能未使用管理員工作階段，或功能完全停用。 若您的實作是如此，請確定您完全移除該功能，或使用[NOP程式碼](https://en.wikipedia.org/wiki/NOP)來配合。

### 優先順序1：使用請求工作階段 {#priority-use-the-request-session}

只要可能就會重構您的功能，以便使用已驗證的指定請求工作階段來讀取或寫入內容。 如果無法這麼做，通常可依照下列優先順序套用優先順序來達成。

### 優先順序2：重新建構內容 {#priority-restructure-content}

許多問題都可透過重新建構內容來解決。 進行重新建構時，請謹記下列簡單規則：

* **變更存取控制**

   * 確定真正需要存取許可權的使用者或群組確實擁有存取權；

* **調整內容結構**

   * 將其移至其他位置，例如，存取控制與可用的請求工作階段相符的位置；
   * 變更內容粒度；

* **將您的程式碼重構為適當的服務**

   * 將商業邏輯從JSP程式碼移至服務。 這允許不同的內容模式。

此外，請確定您開發的任何新功能都遵守以下原則：

* **安全性需求應該驅動內容結構**

   * 管理存取控制應該感覺很自然
   * 存取控制必須由存放庫執行，而非應用程式

* **使用節點型別**

   * 限制可設定的屬性集

* **尊重隱私權設定**

   * 如果有私人設定檔，其中一個範例就是不要公開在私人`/profile`節點上找到的設定檔圖片、電子郵件或全名。

## 嚴格存取控制 {#strict-access-control}

無論您在重新建構內容時套用存取控制，還是為新的服務使用者執行此動作時，都必須儘可能套用最嚴格的ACL。 使用所有可能的存取控制工具：

* 例如，不要在`/apps`上套用`jcr:read`，而只將其套用至`/apps/*/components/*/analytics`

* 使用[限制](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 為節點型別套用ACL
* 限制權限

   * 例如，當只需要寫入內容時，不要授予`jcr:write`許可權；請改用`jcr:modifyProperties`

## 服務使用者與對應 {#service-users-and-mappings}

如果上述操作失敗，Sling 7提供服務使用者對應服務，可讓您設定套件組合對使用者對應和兩個對應的API方法：

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

這些方法會傳回僅具有已設定使用者之許可權的工作階段/資源解析程式。 這些方法具有下列特性：

* 它們允許對應服務到使用者
* 它們可讓您定義子服務使用者
* 中央組態點為： `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [&quot;：&quot;subservice-name]

* `service-id`對應到資源解析程式和/或JCR存放庫使用者ID以進行驗證
* `service-name`是提供服務的套件組合之符號名稱

## 其他建議 {#other-recommendations}

### 將管理員工作階段取代為服務使用者 {#replacing-the-admin-session-with-a-service-user}

服務使用者是不設定密碼的JCR使用者，以及執行特定工作所需的最低許可權集。 未設定密碼表示無法以服務使用者登入。

取代管理工作階段的方法是使用服務使用者工作階段來取代它。 如有需要，也可由多位子服務使用者取代。

若要以服務使用者取代管理工作階段，您應該執行下列步驟：

1. 識別您服務的必要許可權，牢記最小許可權原則。
1. 檢查是否有使用者可以使用您所需的確切許可權設定。 如果沒有任何現有使用者符合您的需求，請建立系統服務使用者。 需要RTC才能建立服務使用者。 有時候，建立多個子服務使用者（例如，一個用於寫入，一個用於讀取）以進一步劃分存取權是有意義的。
1. 為您的使用者設定及測試ACE。
1. 為您的服務和`user/sub-users`新增`service-user`對應

1. 讓您的套件組合可以使用服務使用者sling功能：更新至`org.apache.sling.api`的最新版本。

1. 以`loginService`或`getServiceResourceResolver` API取代程式碼中的`admin-session`。

## 建立服務使用者 {#creating-a-new-service-user}

在您確認AEM服務使用者清單中的任何使用者都不適用於您的使用案例，且對應的RTC問題已核准後，請將新使用者新增至預設內容。

建議的方法是建立服務使用者，以使用位於&#x200B;*https://&lt;server>：&lt;port>/crx/explorer/index.jsp*&#x200B;的存放庫總管

目標是取得有效的`jcr:uuid`屬性，這是透過內容套件安裝建立使用者的必要屬性。

您可以透過下列方式建立服務使用者：

1. 前往位於&#x200B;*https://&lt;server>：&lt;port>/crx/explorer/index.jsp*&#x200B;的存放庫總管
1. 按一下畫面左上角的&#x200B;**登入**&#x200B;連結，以管理員身分登入。
1. 接下來，建立您的系統使用者並為其命名。 若要將使用者建立為系統使用者，請將中繼路徑設為`system`並根據您的需求新增可選的子資料夾：

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 確認您的系統使用者節點如下所示：

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >沒有與服務使用者相關聯的mixin型別。 這表示系統使用者沒有存取控制原則。

將對應的.content.xml新增至套件組合的內容時，請確定您已設定`rep:authorizableId`，且主要型別為`rep:SystemUser`。 它應如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## 正在新增組態修正至ServiceUserMapper組態 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

若要將對應從您的服務新增至對應的系統使用者，請建立[`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)服務的工廠組態。 若要保持此模組化，可以使用[Sling修正機制](https://issues.apache.org/jira/browse/SLING-3578)提供此組態。 建議您使用[Sling初始內容載入](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html)，將此組態與您的套件一起安裝：

1. 在套件的src/main/resources資料夾下方建立子資料夾SLING-INF/content
1. 在此資料夾中，建立名為org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;您工廠設定的某些唯一名稱>.xml的檔案，其中包含您工廠設定的內容（包括所有子服務使用者對應）。 範例：

1. 在您的套件組合的`src/main/resources`資料夾底下建立`SLING-INF/content`資料夾；
1. 在此資料夾中，建立包含您工廠組態內容的檔案`named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml`，包含所有子服務使用者對應。

   為了方便說明，請取得名為`org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`的檔案：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. 參考您套件組合`pom.xml`中`maven-bundle-plugin`的組態中的Sling初始內容。 範例：

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 安裝您的套件組合，並確定已安裝工廠組態。 您可以透過以下方式進行：

   * 前往位於&#x200B;*https://serverhost:serveraddress/system/console/configMgr*&#x200B;的Web主控台
   * 搜尋&#x200B;**Apache Sling Service使用者對應程式服務修正**
   * 按一下連結，您就能檢視是否有正確的設定。

## 在服務中處理共用工作階段 {#dealing-with-shared-sessions-in-services}

對`loginAdministrative()`的呼叫通常與共用工作階段一起出現。 這些工作階段會在服務啟動時取得，並只會在服務停止後登出。 雖然這是常見做法，但會導致兩個問題：

* **安全性：**&#x200B;此類管理工作階段用於快取及傳回繫結至共用工作階段的資源或其他物件。 稍後在呼叫棧疊中，這些物件可以適應具有更高許可權的工作階段或資源解析器。 呼叫者通常無法得知這是他們運作的管理員工作階段。
* **效能：**&#x200B;在Oak中，共用工作階段可能會導致效能問題，不建議您使用它們。

針對安全性風險，最顯而易見的解決方案是將`loginAdministrative()`呼叫取代為`loginService()`呼叫，以提供給具有受限制許可權的使用者。 但是，這不會對任何潛在的效能降級造成任何影響。 降低這種問題的可能方式是，將所有要求的資訊包裝在與工作階段無關聯的物件中。 然後，隨選建立（或銷毀）工作階段。

建議的方法是重構服務的API，讓呼叫者能夠控制工作階段的建立/破壞。

## JSP中的管理階段作業 {#administrative-sessions-in-jsps}

JSP無法使用`loginService()`，因為沒有關聯的服務。 不過，JSP中的管理階段作業通常是違反MVC範例的標誌。

此問題可透過兩種方式修正：

1. 以可讓您透過使用者工作階段操控內容的方式重新建構內容；
1. 將邏輯擷取至提供API （可供JSP使用）的服務。

首選方法是第一個方法。

## 處理事件、複製前置處理器和作業 {#processing-events-replication-preprocessors-and-jobs}

處理事件或工作（有時是工作流程）時，觸發事件的對應工作階段會遺失。 這會導致事件處理常式和工作處理常式使用管理工作階段來執行其工作。 有不同可行的方法可解決此問題，各有其優缺點：

1. 傳遞事件裝載中的`user-id`並使用模擬。

   **優點：**&#x200B;使用簡單。

   **缺點：**&#x200B;仍使用`loginAdministrative()`。 它會重新驗證已驗證的請求。

1. 建立或重複使用可存取資料的服務使用者。

   **優點：**&#x200B;與目前的設計一致。 只需要最少的變更。

   **缺點：**&#x200B;需要強大的服務使用者彈性化，這很容易導致許可權提升。 規避安全性模式。

1. 傳遞事件裝載中`Subject`的序列化，並根據該主題建立`ResourceResolver`。 其中一個範例是在`ResourceResolverFactory`中使用JAAS `doAsPrivileged`。

   **優點：**&#x200B;從安全性觀點來清除實作。 它可避免重新驗證，並以原始許可權操作。 安全性相關程式碼對事件的取用者而言是透明的。

   **缺點：**&#x200B;需要重構。 安全性相關程式碼對事件的取用者而言是透明的，這也可能造成問題。

第三種方法是慣用的處理技術。

## 工作流程處理 {#workflow-processes}

在工作流程實作中，觸發工作流程的對應使用者工作階段會遺失。 這會導致工作流程處理經常使用管理階段來執行其工作。

若要修正這些問題，建議使用[處理事件、復寫前置處理器和工作](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs)中提到的相同方法。

## Sling POST處理器與已刪除頁面 {#sling-post-processors-and-deleted-pages}

Sling POST處理器實施中會使用幾個管理工作階段。 通常，管理工作階段會用來存取處理之POST內擱置刪除的節點。 因此，無法再透過要求工作階段使用這些功能。 可能會存取擱置刪除的節點，以揭露原本不應存取的中繼資料。
