---
title: 使用OAuth 2.0使用者端憑證流程的Salesforce與AEM Forms整合
description: 使用OAuth 2.0使用者端憑證流程整合Salesforce與AEM Forms的步驟
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
exl-id: 56b4a767-1210-47f3-b022-766b0dda9943
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 68%

---

# 使用OAuth 2.0使用者端憑證流程整合Salesforce  {#configure-salesforce-with-ouath-2.0-client-credential}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [按一下這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/aem-forms-salesforce-integration) |
| AEM 6.5 | 本文章 |

您可以使用 OAuth 2.0 用戶端認證將 AEM Forms 與 Salesforce 應用程式進行整合。OAuth 2.0 用戶端認證是一種標準且安全的直接通訊方式，無需使用者參與。

![設定AEM Forms與Salesforce應用程式之間的通訊時的工作流程](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms會交換在Salesforce連線應用程式中定義的使用者端憑證（消費者金鑰和消費者機密）以取得存取權杖。

比起授權代碼流程驗證，使用 OAuth 2.0 用戶端認證進行驗證有多種好處：

* OAuth 2.0 用戶端認證驗證允許每個使用者有五個以上的連線。
* AEM 資料來源設定可繼續進行 AEM 使用者的停用、存取變更、密碼更新。

## 先決條件 {#prerequisites}

設定 Salesforce 應用程式和 AEM 環境之間的通訊以前：

* 為貴組織建立一個[使用 OAuth 2.0 用戶端認證流程的 Salesforce 連線應用程式](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5)以及一個僅限 API 的使用者，並獲取應用程式的客戶金鑰和客戶密碼。

* 確保您的 Swagger 檔案已適當設定，和貴組織的 API 相符。或者，您可以選擇從頭開始[建立 Swagger 檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api)，專為在您的 AEM 環境中使用而量身打造。
>[!NOTE]
>
> AEM 6.5僅支援Swagger 2.0檔案規格。

+++

## 使用使用者端憑證設定Salesforce的步驟 {#steps-to-create-aem-datasource-configuration}

1. 登入您的作者執行個體。
1. 前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL 資料來源]**。
1. 選取設定檔案夾。
1. 按一下「**[!UICONTROL 建立]**」，「**[!UICONTROL 建立資料來源設定]**」會隨即顯示。
1. 指定&#x200B;**[!UICONTROL 標題]**&#x200B;並選取&#x200B;**[!UICONTROL 服務類型]**&#x200B;作為 **[!UICONTROL RESTful 服務]**。
1. 按一下「**[!UICONTROL 下一步]**」。
1. 選取 **[!UICONTROL Swagger 來源]**&#x200B;作為&#x200B;**[!UICONTROL 檔案]。**
   >[!NOTE]
   >
   > 選取swagger檔案之後，就會自動填入「配置」、「主機」名稱和「基底」路徑。

1. 按一下「**[!UICONTROL 瀏覽]**」，即可從您的本機電腦上傳已建立的 swagger 檔案。
1. 選取&#x200B;**[!UICONTROL 驗證類型]**&#x200B;作為&#x200B;**[!UICONTROL OAuth 2.0]**，**[!UICONTROL 驗證設定]**&#x200B;面板會隨即顯示。
1. 選取&#x200B;**[!UICONTROL 授權型別]**&#x200B;做為&#x200B;**[!UICONTROL 使用者端認證]**。
1. 指定&#x200B;**[!UICONTROL 用戶端 ID]**&#x200B;以及從 Salesforce 連線的應用程式獲取的&#x200B;**[!UICONTROL 用戶端密碼]**。
1. 指定&#x200B;**[!UICONTROL 存取權杖 URL]** 格式
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 每個組織都有自己特定的網域名稱。

1. 按一下「**[!UICONTROL 測試連線]**」。
1. 如果連線成功，按一下「**[!UICONTROL 建立]**」按鈕。

現在您可以[建立表單資料模型](/help/forms/using/create-form-data-model.md)，將已設定的資料來源與您的Adaptive Forms整合。
