---
title: 以生產就緒模式執行AEM
description: 瞭解如何在生產就緒模式下執行AEM。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 99724bd6-41b4-4491-9958-1f5d9e1f5050
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 3%

---

# 以生產就緒模式執行AEM{#running-aem-in-production-ready-mode}

透過AEM 6.1，Adobe推出了新的`"nosamplecontent"`執行模式，旨在將準備AEM執行個體以部署在生產環境中所需的步驟自動化。

新的執行模式不僅會自動設定執行個體以遵循安全性檢查清單中說明的安全性最佳實務，而且還會移除流程中的所有範例Geometrixx應用程式和設定。

>[!NOTE]
>
>由於實際原因，AEM生產就緒模式將僅涵蓋保護執行個體所需的大部分任務，強烈建議您先參閱[安全性檢查清單](/help/sites-administering/security-checklist.md)，然後再開始使用您的生產環境。
>
>另外也請注意，以生產就緒模式執行AEM將有效停用CRXDE Lite的存取權。 如果您需要此工具以進行偵錯，請參閱[在AEM中啟用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md)。

![chlimage_1-83](assets/chlimage_1-83a.png)

若要以生產就緒模式執行AEM，您必須透過`-r`執行模式切換將`nosamplecontent`新增到您現有的啟動引數：

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例如，您可以使用生產準備啟動具有MongoDB持續性的作者執行個體，如下所示：

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 變更部分生產就緒模式 {#changes-part-of-the-production-ready-mode}

更具體來說，AEM以生產就緒模式執行時，會執行下列設定變更：

1. **CRXDE支援組合** ( `com.adobe.granite.crxde-support`)預設為在生產就緒模式中停用。 您可以隨時從Adobe公共Maven存放庫進行安裝。 AEM 6.1需要版本3.0.0。

1. **Apache Sling對存放庫** ( `org.apache.sling.jcr.webdav`)套件組合的「簡單WebDAV存取」只能在&#x200B;**作者**&#x200B;執行個體上使用。

1. 新建立的使用者必須在第一次登入時變更密碼。 這不適用於管理員使用者。
1. 已針對&#x200B;**Apache Sling JavaScript處理常式**&#x200B;停用&#x200B;**產生偵錯資訊**。

1. 已針對&#x200B;**Apache Sling JSP指令碼處理常式**&#x200B;停用&#x200B;**對應內容**&#x200B;和&#x200B;**產生偵錯資訊**。

1. **Day CQ WCM篩選器**&#x200B;在&#x200B;**作者**&#x200B;上設定為`edit`，在&#x200B;**發佈**&#x200B;執行個體上設定為`disabled`。

1. **Adobe Granite HTML資料庫管理員**&#x200B;已設定下列設定：

   1. **最小化：** `enabled`
   1. **偵錯：** `disabled`
   1. **Gzip：** `enabled`
   1. **時間：** `disabled`

1. 根據預設，**Apache Sling GET Servlet**&#x200B;設定為支援安全設定，如下所示：

| **組態** | **作者** | **發佈** |
|---|---|---|
| TXT轉譯 | 已停用 | 已停用 |
| HTML轉譯 | 已停用 | 已停用 |
| JSON轉譯 | 已啟用 | 已啟用 |
| XML轉譯 | 已停用 | 已停用 |
| json.maximumresults | 1000 | 100 |
| 自動索引 | 已停用 | 已停用 |
