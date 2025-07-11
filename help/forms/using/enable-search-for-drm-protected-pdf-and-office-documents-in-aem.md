---
title: 啟用AEM以搜尋受Document Security保護的PDF和Microsoft Office檔案
description: 瞭解如何啟用原生AEM搜尋，以在受DRM保護的PDF檔案上執行全文搜尋。
noindex: true
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 5e9d3f3c-8fc4-4d01-9f1e-62d3c29ab9e5
source-git-commit: cd6caaf9de907488db14df2a6396fa60efa2d42c
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# 啟用AEM以搜尋受Document Security保護的PDF和Microsoft Office檔案{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供使用者介面，用於搜尋和找出AEM中儲存的各種資產。 原生搜尋可搜尋和找到AEM資產，並對各種常用的檔案格式(例如純文字檔、Microsoft Office檔案和PDF檔案)執行文字搜尋。 您也可以擴充及啟用原生搜尋，以在受DRM保護的PDF和Microsoft Office檔案上執行全文搜尋。

執行以下步驟以允許AEM搜尋受Document Security保護的PDF和Microsoft Office檔案：

## 開始之前 {#before-you-start}

* 安裝及設定AEM Forms Document Security。
* 將套件sun.util.calendar新增至&#x200B;**還原序列化防火牆設定的允許清單。**&#x200B;組態列在`https://'[server]:[port]'/system/console/configMgr`。
* 確認所有AEM套件組合皆已啟動且執行中。 這些組合列在`https://'[server]:[port]'/system/console/bundles`。 如果所有套件組合並非作用中，請稍候片刻，然後在片刻後檢查套件組合的狀態。

## 在AEM Forms工作流程中建立安全連線(JEE上的AEM Forms) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全連線可讓JEE上的AEM Forms與相同伺服器上執行的OSGi服務之間順暢地傳輸資訊。 使用下列其中一種方法來建立安全連線：

* 透過JEE管理員憑證上的AEM Forms設定AEM Forms使用者端SDK套件組合
* 使用相互驗證設定AEM Forms使用者端SDK套件組合

### 透過JEE管理員憑證上的AEM Forms設定AEM Forms使用者端SDK套件組合 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 開啟AEM設定管理員，並以管理員身分登入。 預設URL為https://&lt;serverName>：&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms使用者端SDK套件組合。 指定下列屬性的值：

   * **伺服器URL：**&#x200B;指定JEE伺服器上AEM Forms的HTTP URL。 若要啟用透過https的通訊，請使用-Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>引數，重新啟動JEE伺服器上的AEM Forms。
   * **服務名稱**：將RightsManagementService新增至指定的服務清單。
   * **使用者名稱：**&#x200B;指定JEE伺服器上AEM Forms帳戶的使用者名稱，以用來起始從JEE伺服器AEM Forms的呼叫。 指定的帳戶必須有權在JEE伺服器上的AEM Forms上叫用檔案服務。
   * **密碼**：指定使用者名稱欄位中提及的AEM Forms on JEE帳戶密碼。

   按一下「**儲存**」。AEM已啟用搜尋受Document Security保護的PDF和Microsoft Office檔案。

### 使用相互驗證設定AEM Forms使用者端SDK套件組合 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. 啟用JEE上AEM Forms的相互驗證。
1. 開啟AEM設定管理員，並以管理員身分登入。 預設URL為https://&lt;serverName>：&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms使用者端SDK套件組合。 指定下列屬性的值：

   * **伺服器URL：**&#x200B;指定JEE伺服器上AEM Forms的HTTPS URL。 若要啟用透過https的通訊，請使用-Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>引數，重新啟動JEE伺服器上的AEM Forms。
   * **啟用雙向SSL**：啟用「啟用雙向SSL」選項。
   * **KeyStore檔案URL**：指定Keystore檔案的URL。
   * **TrustStore檔案URL**：指定truststore檔案的URL。
   * **KeyStore密碼**：指定金鑰存放區檔案的密碼。
   * **TrustStorePassword**：指定truststore檔案的密碼。
   * **服務名稱**：將RightsManagementService新增至指定的服務清單。

   按一下「**儲存**」。AEM已啟用搜尋受Document Security保護的PDF和Microsoft Office檔案

   >[!NOTE]
   >
   > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式），可能會導致AEM開發環境不一致。

## 為受原則保護的PDF或Microsoft Office範例檔案建立索引 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理員身分登入AEM Assets。
1. 在AEM Digital Asset Manager中建立資料夾，並將受原則保護的PDF或Microsoft Office檔案上傳到新建立的資料夾。 現在，使用AEM搜尋來搜尋受原則保護檔案的內容。 它必須傳回包含搜尋文字的檔案。
