---
title: 與Adobe Target整合的先決條件
description: 瞭解與Adobe Target整合的先決條件。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: e1771229-b2ce-406a-95a5-99b11fafbe34
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# 與Adobe Target整合的先決條件{#prerequisites-for-integrating-with-adobe-target}

作為AEM與Adobe Target[整合的](/help/sites-administering/target.md)一部分，您需要向Adobe Target註冊、設定復寫代理程式，以及在發佈節點上安全活動設定。

## 向Adobe Target註冊 {#registering-with-adobe-target}

若要將AEM與Adobe Target整合，您必須具備有效的Adobe Target帳戶。 此帳戶必須至少具有&#x200B;**核准者**&#x200B;層級許可權。 註冊Adobe Target時，您會收到使用者端代碼。 您需要使用者端代碼以及Adobe Target登入名稱和密碼，才能將AEM連線至Adobe Target。

使用者端代碼會在呼叫Adobe Target伺服器時識別Adobe Target客戶帳戶。

>[!NOTE]
>
>Target團隊必須啟用您的帳戶才能使用整合。
>
>如果不是這種情況，請聯絡[Adobe客戶服務](https://experienceleague.adobe.com/en/docs/target/using/cmp-resources-and-contact-information)。

## 啟用Target復寫代理 {#enabling-the-target-replication-agent}

必須在編寫執行個體上啟用測試和目標[復寫代理程式](/help/sites-deploying/replication.md)。 請注意，如果您使用[nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent)執行模式來安裝AEM，預設不會啟用此復寫代理程式。 如需保護生產環境的詳細資訊，請參閱[安全性檢查清單](/help/sites-administering/security-checklist.md)。

1. 在AEM首頁上，按一下&#x200B;**工具** > **部署** > **復寫**。
1. 按一下作者上的&#x200B;**代理程式**。
1. 按一下&#x200B;**Test and Target (test and target)**&#x200B;復寫代理程式，然後按一下&#x200B;**編輯**。
1. 選取[啟用]選項，然後按一下[確定]。**&#x200B;**

   >[!NOTE]
   >
   >當您設定Test and Target復寫代理程式時，在&#x200B;**傳輸**&#x200B;索引標籤中，URI預設會設為`tnt:///`。 請勿以`https://admin.testandtarget.omniture.com`取代此URI。
   >
   >如果您嘗試使用`tnt:///`測試連線，它會顯示錯誤，這是預期行為。 原因在於URI僅供內部使用。 請勿搭配&#x200B;**測試連線**&#x200B;使用。

## 保護活動設定節點 {#securing-the-activity-settings-node}

保護發佈執行個體上的活動設定節點&#x200B;**cq:ActivitySettings**，使其無法正常使用者存取。 活動設定節點應該只能由處理與Adobe Target的活動同步的服務存取。

在CRXDE Lite中，活動&#x200B;**節點下的:ActivitySettings*** *下有`/content/campaigns/*nameofbrand*`cq`jcr:content`節點可供使用。 例如 `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`。此節點只有在您鎖定元件目標之後才會建立。

活動的&#x200B;**下的:ActivitySettings** cq`jcr:content`節點受下列ACL保護：

* 拒絕所有人的所有。
* 允許`jcr:read,rep:write`的`target-activity-authors` （作者是此開箱即用群組的成員）。
* 允許`jcr:read,rep:write`的`targetservice`。

這些設定可確保一般使用者無權存取節點屬性。 在製作和發佈上使用相同的ACL。 如需詳細資訊，請參閱[使用者管理與安全性](/help/sites-administering/security.md)。

## 設定AEM連結外部器 {#configuring-the-aem-link-externalizer}

在Adobe Target中編輯活動時，除非您變更AEM作者節點上的URL，否則URL會指向&#x200B;**localhost**。 如果您希望匯出的內容指向特定的&#x200B;*發佈*&#x200B;網域，可以設定AEM Link Externalizer。

>[!NOTE]
>
>另請參閱[新增雲端設定](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)。

若要設定AEM Externalizer：

>[!NOTE]
>
>如需詳細資訊，請參閱[外部化URL](/help/sites-developing/externalizer.md)。

1. 導覽至&#x200B;**https://&lt;server>：&lt;port>/system/console/configMgr的OSGi Web主控台。**
1. 尋找&#x200B;**Day CQ Link Externalizer**&#x200B;並輸入作者節點的網域。

   ![天CQ連結外部器](assets/aem-externalizer-01.png)
