---
title: 正在設定AEM DS設定
description: 瞭解在提交表單前如何指定處理伺服器URL。
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 8ad3afd6-e1c6-4f21-bb0f-4d97ef50710e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 正在設定AEM DS設定{#configuring-aem-ds-settings}

本文說明如何設定&#x200B;**AEM DS設定服務**。 此設定可用於多個情境，例如：

* 在通訊管理中

   * 設定AEM Forms工作流程
   * 使用Forms入口網站從遠端儲存草稿/提交內容時

* 在調適型表單中，適用於從發佈執行個體提交調適型表單的情況

以下是設定&#x200B;**[!UICONTROL AEM DS設定]**&#x200B;的步驟：

1. 使用URL在發佈執行個體上開啟Configuration Manager：\
   *https://localhost:port/system/console/configMgr*。

   ![AEM Web主控台組態](assets/web_configuration_console_new.png)

1. 在&#x200B;**[!UICONTROL Adobe Experience Manager Web主控台組態]**&#x200B;視窗中，找到並按一下&#x200B;**[!UICONTROL AEM DS設定]**&#x200B;選項。

   ![DS設定](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS設定服務]**&#x200B;視窗會顯示AEM DS元件的通用組態設定。

   ![DS設定服務](assets/ds_settings_service_new.png)

1. 在個別欄位中新增下列資訊：

   **[!UICONTROL 處理伺服器URL]**：處理伺服器是必須觸發Forms或AEM工作流程的伺服器。 這可以與AEM編寫執行個體的URL或其他伺服器URL (即https://localhost:port/)相同。

   **[!UICONTROL 正在處理伺服器使用者名稱]**：工作流程使用者的使用者名稱[，根據正在使用的伺服器URL]

   **[!UICONTROL 處理伺服器密碼]**：工作流程使用者的密碼

   >[!NOTE]
   >
   >
   >    
   >    
   >    * 使用Forms或AEM工作流程時，您必須先設定DS設定服務，才能從發佈伺服器提交任何內容。 否則，表單提交將會失敗。
   >    
   >
