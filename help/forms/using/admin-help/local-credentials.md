---
title: 管理本機認證
description: 瞭解如何使用信任存放區管理來管理本機認證。 AEM表單支援標準PKCS12表單中的RSA和DSA憑證。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: d297ab09-2b92-442a-8b19-ffee86e24bb9
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 管理本機認證 {#managing-local-credentials}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

本機認證是在信任存放區管理中託管的私密金鑰認證。 *本機認證*&#x200B;可識別使用者DES認證的儲存位置。 使用「信任存放區管理」，您可以匯入和管理本機認證，例如使用現有的PFX檔案，以便您可以匯入、編輯和刪除本機認證。

AEM forms支援標準PKCS12格式（.pfx和.p12檔案）中最多4096位元的RSA和DSA憑證。

您可以匯入及匯出任何數量的認證。 如果您想使用相同的別名來取代過期的認證，請刪除認證，然後以相同的別名匯入新的認證。

如需Acrobat Reader DC擴充功能的相關資訊與指示，請參閱[設定與Acrobat Reader DC擴充功能搭配使用的認證](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。

## 匯入認證 {#import-a-credential}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 按一下「匯入」。 在「信任存放區型別」下，選取下列其中一個選項：

   * **檔案簽署認證：**&#x200B;用來在檔案上發行數位簽章的認證。
   * **Acrobat Reader DC延伸模組認證：**&#x200B;特定於Acrobat Reader DC延伸模組的數位憑證，可在產生的PDF檔案中啟用Adobe Reader使用許可權。
   * **預設值：**&#x200B;指出這是搭配Acrobat Reader DC延伸模組使用的預設認證。

   如需取得認證的相關資訊，請參閱[準備安裝AEM表單](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf)。

1. 在「別名」方塊中，輸入認證的識別碼。 此識別碼會用作Acrobat Reader DC Extensions和Signature service中認證的顯示名稱。 此別名也會用來透過AEM表單SDK，以程式設計方式存取認證。

   >[!NOTE]
   >
   >別名會自動轉換為大寫以供顯示。 您在程式中參考別名時，別名名稱不區分大小寫。

1. 按一下「瀏覽」以尋找證明資料，輸入證明資料的密碼，然後按一下「確定」。

   如果出現錯誤訊息「由於檔案格式不正確或密碼不正確而無法匯入認證」，請確認密碼有效。

## 匯出認證 {#export-a-credential}

認證會匯出為PKCS#12格式的P12檔案。

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 按一下要匯出的認證的別名，然後按一下匯出。
1. 在「密碼」方塊中，輸入密碼。 此密碼是新的，用於加密匯出的認證。
1. 按一下「匯出」，依照指示匯出認證，然後按一下「確定」。

## 編輯認證的別名或信任存放區型別 {#edit-a-credential-s-alias-or-trust-store-type}

匯入認證後，您可以編輯其別名及信任存放區型別。

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 按一下您要編輯之認證的別名。
1. 按一下「更新認證」。
1. 視需要編輯別名名稱和信任存放區型別，然後按一下「確定」。

## 刪除認證 {#delete-a-credential}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 選取要刪除的認證核取方塊。
1. 按一下「刪除」，然後按一下「確定」。
