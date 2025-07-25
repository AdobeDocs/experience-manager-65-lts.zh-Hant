---
title: 使用Brand Portal設定AEM Assets
description: 瞭解如何使用Brand Portal設定AEM Assets，以將資產和集合發佈到Brand Portal。
feature: Brand Portal
role: Admin
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 22a2428d-3ebd-4368-983e-d140f99de2dd
source-git-commit: 89c9a0416f8d270f172eb42e1e308f2a986a2cb3
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 4%

---

# 使用Brand Portal設定AEM Assets {#configure-integration-65}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

Adobe Experience Manager Assets Brand Portal可讓您將核准的品牌資產從Adobe Experience Manager Assets發佈到Brand Portal，並分發給Brand Portal使用者。

AEM Assets是透過Adobe Developer Console使用Brand Portal設定的，這可取得Adobe Identity Management Services (IMS)帳戶Token以授權Brand Portal租使用者。

>[!NOTE]
>
>AEM 6.5.4.0和更新版本支援透過Adobe Developer Console使用Brand Portal設定AEM Assets。
>
<!--
>Earlier, Brand Portal was configured via legacy OAuth Gateway, which uses the JSON Web Token (JWT) exchange to obtain an IMS Access token for authorization. 
>
>Configuration via legacy OAuth Gateway is no longer supported from April 6, 2020, and is changed to Adobe Developer Console.
-->

>[!TIP]
>
>***僅供現有客戶使用***
>
>Adobe建議您繼續使用現有的舊版OAuth閘道設定。 如果您遇到舊版OAuth閘道組態的問題，請刪除現有組態，並透過Adobe Developer Console建立組態。

<!--
This help describes the following two use-cases:

* [New configuration](#configure-new-integration-65): If you are a new Brand Portal user and want to configure your AEM Assets Author instance with Brand Portal, you can create a configuration by way of the Adobe Developer Console. 
* [Upgrade configuration](#upgrade-integration-65): If you are an existing Brand Portal user having configuration on legacy OAuth Gateway, delete the existing configuration and create a configuration by way of Adobe Developer Console.
-->
所提供的資訊是基於任何閱讀本「說明」的人員都熟悉以下技術的假設：

* 安裝、設定和管理Adobe Experience Manager和AEM套件。

* 使用Linux®和Microsoft® Windows作業系統。

## 先決條件 {#prerequisites}

您需要下列項目才能使用 Brand Portal 設定 AEM Assets：

* 具最新Service Pack且正在執行中的AEM Assets作者執行個體
* Brand Portal租使用者URL
* 在Brand Portal租使用者的IMS組織具有系統管理員許可權的使用者

[下載並安裝AEM 6.5](#aemquickstart)

[下載並安裝最新的AEM Service Pack](#servicepack)

### 下載並安裝AEM 6.5 LTS {#aemquickstart}

建議您使用AEM 6.5 LTS來設定AEM Author例項。 如果您尚未啟動並執行AEM，請從下列位置下載：

* 如果您是AEM現有客戶，請從[AEM授權網站](https://licensing.adobe.com)下載Adobe 6.5 LTS。

* 如果您是Adobe合作夥伴，請使用[Adobe合作夥伴訓練計畫](https://solutionpartners.adobe.com/)要求AEM 6.5。

下載AEM之後，如需設定AEM Author執行個體的指示，請參閱[部署和維護](/help/sites-deploying/deploy.md#default-local-install)。

### 下載並安裝AEM最新Service Pack {#servicepack}

如需詳細指示，請參閱目前的[AEM 6.5 LTS Service Pack發行說明](/help/release-notes/release-notes.md)。

如果找不到最新的Adobe套件或Service Pack，請&#x200B;**連絡AEM客戶支援**。

## 建立設定 {#configure-new-integration-65}

>[!NOTE]
>
>從2024年6月起，您無法建立新的JWT憑證。 此後，只會建立OAuth認證。 請參閱建立OAuth設定的詳細資訊。

使用Brand Portal設定AEM Assets需要在AEM Assets Author例項和Adobe Developer Console中進行設定。

1. 在Adobe Developer Console中，為您的Brand Portal租使用者（組織）建立專案。
1. 在Experience Manager Assets中，使用IMS帳戶和Brand Portal端點（組織URL）設定Brand Portal雲端服務。
1. 從Experience Manager Assets發佈資產到Brand Portal以測試設定。

<!--
1. In AEM Assets, create an IMS account and generate a public certificate (public key).
1. In Adobe Developer Console, create a project for your Brand Portal tenant (organization).
1. Under the project, configure an API using the public key to create a service account (JWT) connection.
1. Get the service account credentials and JWT payload information.
1. In AEM Assets, configure the IMS account using the service account credentials and JWT payload.
1. In AEM Assets, configure the Brand Portal cloud service using the IMS account and Brand Portal endpoint (organization URL).
1. Test your configuration by publishing an asset from AEM Assets to Brand Portal.
-->

>[!NOTE]
>
>AEM Assets作者例項只能設定為一個Brand Portal租使用者。

如果您是第一次使用Brand Portal設定AEM Assets，請依照列出的順序執行下列步驟：

### 建立新設定 {#create-new-configuration}

以指定順序執行下列步驟，使用Brand Portal設定Experience Manager Assets。

1. [在Adobe Developer Console中設定OAuth認證](#config-oauth)
1. [使用OAuth建立新的Adobe IMS整合](#create-ims-account-configuration)
1. [設定雲端服務](#configure-cloud-service)

#### 在Adobe Developer Console中設定OAuth認證 {#config-oauth}

[在Adobe Developer Console中設定OAuth認證](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/security/setting-up-ims-integrations-for-aem#credentials-in-the-developer-console)，並選取Brand Portal API。

#### 使用OAuth建立新的Adobe IMS整合 {#create-ims-account-configuration}

[使用OAuth建立新的Adobe IMS整合](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/security/setting-up-ims-integrations-for-aem#creating-oauth-configuration)，並從下拉式清單中選取Brand Portal。

#### 設定雲端服務 {#configure-cloud-service}

<!--
1. [Obtain a public certificate](#public-certificate)
1. [Create service account (JWT) connection](#createnewintegration) 
1. [Configure an IMS account](#create-ims-account-configuration)
1. [Configure cloud service](#configure-cloud-service)
1. [Test configuration](#test-integration)
-->
<!--
### Create IMS configuration {#create-ims-configuration}

The IMS configuration authenticates your AEM Assets Author instance with the Brand Portal tenant. 

IMS configuration includes two steps:

* [Obtain a public certificate](#public-certificate) 
* [Configure an IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your profile on Adobe Developer Console.

1. Log in to your AEM Assets Author instance. The default URL is `http://localhost:4502/aem/start.html`.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In the Adobe IMS Configurations page, click **[!UICONTROL Create]**. It redirects to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.

1. Select **[!UICONTROL Adobe Brand Portal]** in the **[!UICONTROL Cloud Solution]** dropdown list.  

1. Select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as the name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

   ![Create Certificate](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. 

   The public key is used later to configure the API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   ![Download Certificate](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**. 

   In the **Account** tab, an Adobe IMS account is created which requires the service account credentials that are generated in Adobe Developer Console. Keep this page open for now.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration) so you can get the credentials and JWT payload for configuring the IMS account. 

### Create the service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at the Brand Portal tenant (organization) level. Configuring an API creates a service account (JWT) connection. There are two methods to configure the API, by generating a key pair (private and public keys) or by uploading a public key. To configure AEM Assets with Brand Portal, you must generate a public key (certificate) in AEM Assets and create credentials in Adobe Developer Console by uploading the public key. These credentials are required to configure the IMS account in AEM Assets. Once the IMS account is configured, you can configure the Brand Portal cloud service in AEM Assets.

To create the service account credentials and JWT payload, do the following:

1. Log in to Adobe Developer Console with system administrator privileges on the IMS organization (Brand Portal tenant). The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Ensure that you have selected the correct IMS organization (Brand Portal tenant) from the drop-down (organization) list in the upper-right corner.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]** so you can update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**. 

   Ensure that you have access to the AEM Brand Portal service.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. 

   Click **[!UICONTROL Next]**.

   ![Upload Public Key](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Assets Brand Portal]** as the default product profile and click **[!UICONTROL Save configured API]**. 
-->
<!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->
<!--
   ![Select Product Profile](assets/service-account4.png)

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE]
   >
   >You can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Service Account Credentials](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in AEM Assets.

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe Developer Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information that is used to create IMS account configuration.
-->
<!--
### Configure the IMS account {#create-ims-account-configuration}

Ensure that you have already performed the following steps:

* [Obtain a public certificate](#public-certificate)
* [Create service account (JWT) connection](#createnewintegration)

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   Click **[!UICONTROL Create]**.

   The IMS account is configured. 

   ![IMS Account configuration](assets/create-new-integration6.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![Healthy Configuration confirmation dialog](assets/create-new-integration5.png)

>[!CAUTION]
>
>You must have only one IMS configuration.
>
>Ensure that the IMS configuration passes the health check. If the configuration does not pass the health check, it is invalid. Delete it and create another valid configuration.
-->

1. 登入您的AEM Assets Author例項。

1. 從&#x200B;**工具** ![工具](assets/do-not-localize/tools.png)面板，瀏覽至&#x200B;**[!UICONTROL 雲端服務]** > **[!UICONTROL AEM Brand Portal]**。

1. 在Brand Portal設定頁面中，按一下&#x200B;**[!UICONTROL 建立]**。

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選取您在[設定IMS帳戶](#create-ims-account-configuration)時所建立的IMS設定。

   在&#x200B;**[!UICONTROL 服務URL]**&#x200B;欄位中，指定您的Brand Portal租使用者（組織） URL。

   ![Brand Portal設定視窗](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。 雲端設定已建立。

   您的AEM Assets Author例項現在已透過Brand Portal租使用者完成設定。

<!--

### Test and validate the configuration {#test-integration}

1. Log in to your AEM Assets cloud instance.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![The Tools panel](assets/test-integration1.png)

1. In the Replication page, click **[!UICONTROL Agents on Author]**.

   ![Replication page](assets/test-integration2.png)

   You can see the four replication agents created for your Brand Portal tenant. 

   Locate the replication agents of your Brand Portal tenant and click the replication agent URL. 

   ![Assets replication configuration](assets/test-integration3.png)

   >[!NOTE]
   >
   >The replication agents work in parallel and share the job distribution equally, so that it increases the publishing speed by four times the original speed. After the cloud service is configured, additional configuration is not required to enable the replication agents that are activated by default to enable parallel publishing of multiple assets.

1. To verify the connection between AEM Assets and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![Verifying the assets replication settings](assets/test-integration4.png)

   A message appears that your *test package is successfully delivered*.

   ![Test confirmation output](assets/test-integration5.png)

1. Verify the test results on all four replication agents.


   >[!NOTE]
   >
   >Avoid disabling any of the replication agents, as it can cause the replication of the assets (running-in-queue) to fail.
   >
   >Ensure that all the four replication agents are configured to avoid timeout error. See [troubleshoot issues in parallel publishing to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html?lang=zh-Hant#connection-timeout).
   >
   >Do not modify any autogenerated settings.

You can now:

* [Publish assets from AEM Assets to Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=zh-Hant) - Asset Sourcing in Brand Portal 
* [Publish folders from AEM Assets to Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publish collections from AEM Assets to Brand Portal](../assets/brand-portal-publish-collection.md) 
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=zh-Hant)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=zh-Hant)

See the [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=zh-Hant) for more information.

-->
<!--
## Upgrade configuration {#upgrade-integration-65}

To upgrade your existing configurations to Adobe Developer Console, do the following steps, in the listed sequence : 

1. [Verify running jobs](#verify-jobs)
1. [Delete existing configurations](#delete-existing-configuration)
1. [Create configuration](#configure-new-integration-65)

### Verify running jobs {#verify-jobs}

Ensure that no publishing job is running on your AEM Assets Author instance before you make any edits. For that, you can verify the status of active jobs on all the four replication agents and ensure that the queues are idle.  

1. Log in to your AEM Assets Author instance.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Deployment Replication]**.

1. In the Replication page, click **[!UICONTROL Agents on Author]**.

   ![Replication agents for assets](assets/test-integration2.png)

1. Locate the replication agents of your Brand Portal tenant. 
   
   Ensure that the **Queue is Idle** for all the replication agents, and no publishing job is active. 

   ![Replication queue settings](assets/test-integration3.png)

### Delete existing configurations {#delete-existing-configuration}

Run the following checklist while deleting the existing configurations:

* Delete all four replication agents
* Delete Brand Portal cloud service
* Delete Mac user 

1. Log in to your AEM Assets Author instance and open CRX Lite as an administrator. The default URL is `http://localhost:4502/crx/de/index.jsp`.

1. Navigate to `/etc/replications/agents.author` and delete all the four replication agents of your Brand Portal tenant.

   ![Replication agent in CRXDE](assets/delete-replication-agent.png)

1. Navigate to `/etc/cloudservices/mediaportal` and delete the Brand Portal cloud service configuration.

   ![Detail of replication agent in CRXDE](assets/delete-cloud-service.png)

1. Navigate to `/home/users/mac` and delete the **Mac user** of your Brand Portal tenant.

   ![More detail of replication agent in CRXDE](assets/delete-mac-user.png)


You can now [create a configuration](#configure-new-integration-65) by way of the Adobe Developer Console on your AEM 6.5 Author instance. 
-->
