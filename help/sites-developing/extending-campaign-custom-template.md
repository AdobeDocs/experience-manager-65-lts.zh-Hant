---
title: 使用Adobe Campaign表單元件建立自訂AEM頁面範本
description: 建立使用Adobe Campaign表單元件的自訂頁面範本
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 59a79455-c108-4f4b-93c1-d8c6f23aec88
index: false
source-git-commit: 2edf37c2d6bb04b418618f2780f773ab37559114
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 2%

---


# 使用Adobe Campaign表單元件建立自訂AEM頁面範本{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

此頁面說明如何透過檢查Geometrixx-outdoors範本([)的實作方式，建置使用](/help/sites-authoring/adobe-campaign-components.md)Adobe Campaign Form`/apps/geometrixx-outdoors/components/page_campaign_profile`元件的自訂頁面範本，並指出建立您自己的自訂範本時可能需要的重要資訊。

>[!CAUTION]
>
>AEM電子郵件元件已淘汰。 由於電子郵件結合了內容和樣式，因此由AEM提供的現成可用電子郵件元件對於客戶的重複使用有限，因為需要將自訂樣式實作到專案所需的任何元件中。
>
>電子郵件元件可在專案層級實作，而過時的AEM電子郵件元件會說明如何實作。 不過，請勿在專案上使用這些已棄用的元件。


若要使用AEM表單元件建立自訂Adobe Campaign頁面範本，請確定您具備下列條件：

1. **正確的resourceSuperType**

   確定頁面元件繼承自`mcm/campaign/components/profile`。

   此servlet需要此項才能取得和儲存資訊

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext設定**

   當您檢視clientcontext設定( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`)時，您會看到下列設定：

   * ClientContext指向`/etc/clientcontext/campaign`
   * 還有一個額外的&#x200B;*設定*&#x200B;節點。

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   在&#x200B;**head.jsp**&#x200B;中，您會看到下列使用&#x200B;**clientcontext-config**&#x200B;和&#x200B;**cloudservice-hook**&#x200B;的行：

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   在&#x200B;**body.jsp**&#x200B;中，雲端服務載入頁面底部：

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **行銷活動頁面屬性**

   為了能夠選取Adobe Campaign範本，頁面屬性會以&#x200B;**行銷活動**&#x200B;索引標籤擴充：

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **範本設定**。

   在範本( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`)中，您會看到下列預設值：

   | **acMapping** | mapRecipient (適用於Adobe Campaign 6.1)、設定檔(適用於Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | 郵件 |

   ![chlimage_1-204](assets/chlimage_1-204.png)
