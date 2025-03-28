---
title: 設定Microsoft SharePoint的聯結器
description: 設定Microsoft SharePoint的聯結器，以啟用AEM表單與Microsoft SharePoint之間的通訊。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: d1575576-3a05-496c-b683-bb5badc02711
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---

# 設定Microsoft SharePoint的聯結器 {#configuring-connector-for-microsoft-sharepoint}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

Microsoft SharePoint的聯結器可啟用AEM表單與Microsoft SharePoint之間的通訊。 如需其他背景資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_63)中的「Connectors for ECM」。

1. 在管理控制檯中，按一下「服務」 > 「Microsoft SharePoint的聯結器」 。
1. 為您的SharePoint伺服器指定下列設定：

   **SharePoint伺服器主機名稱：** SharePoint伺服器上Web應用程式的主機名稱連線埠號碼，格式為`[hostname]:'port'`。

   **使用者名稱：**&#x200B;用來連線至SharePoint伺服器的使用者帳戶。

   **密碼：**&#x200B;用來連線至SharePoint伺服器的使用者帳戶密碼

   **網域名稱：** SharePoint伺服器所在的網域。

1. 按一下「儲存」。

## Microsoft SharePoint設定服務 {#microsoft-sharepoint-configuration-service}

Microsoft SharePoint設定服務`(MSSharePointConfigService)`可讓您為具有模擬許可權的AEM表單使用者指定認證。 如需模擬許可權的相關資訊，請參閱[設定Microsoft SharePoint的聯結器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。 請依照下列步驟指定`MSSharePointConfigService`的設定：

1. 在Administration Console中，按一下「服務>應用程式和服務>服務管理」。
1. 瀏覽服務清單並按一下`MSSharePointConfigService`。
1. 在「組態」頁面中指定下列設定：

   * 具有模擬許可權的使用者的使用者名稱
   * 上述使用者的密碼

1. 按一下「儲存」。
