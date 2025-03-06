---
title: 安裝最新6.5.15.0個Service Pack後，CRX/套件組合和開始頁面服務即發生無法使用的錯誤
description: 安裝最新6.5.15.0個Service Pack後，CRX/套件組合和開始頁面服務即發生無法使用的錯誤
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
exl-id: f62d526b-9510-4db8-9351-02fd7f192109
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# 安裝AEM (6.5.15.0) Service Pack後發生服務無法使用錯誤 {#steps-to-resolve-error-after-installing-service-pack}

## 問題 {#issue}

安裝[AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)後，錯誤發生如下：
* 錯誤[FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent錯誤(org.osgi.framework.BundleException：無法解析org.apache.sling.scripting.console

安裝AEM 6.5.15.0 Service Pack後，CRX/套件組合和起始頁面顯示服務無法使用錯誤。

## 套用至 {#applies-to}

此解決方案適用於：
* 所有JEE伺服器（在JBoss EAP 7.4.0上執行的除外）上的AEM Forms

## 解決方案 {#solution}

>[!NOTE]
>
>疑難排解步驟適用於除JBoss EAP 7.4以外的所有應用程式伺服器。

安裝[AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)後，如果CRX/套件組合和起始頁面顯示服務無法使用錯誤，請執行下列步驟：

1. 停止應用程式伺服器。
1. 導覽至 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`。
1. 找到`bundle.info`檔案。
1. 在Ant文字編輯器中開啟`bundle.info`檔案，並以`org.apache.felix.http.bridge`搜尋套件組合名稱。

   >[!NOTE]
   >
   >如果`bundle52`底下的`bundle.info`不包含`org.apache.felix.http.bridge`組合，請檢查`org.apache.felix.http.bridge`旁方括弧中的組合編號。 然後導覽至[aem-forms根目錄]\crx-repository\launchpad\felix\bundle[x]，並在此位置執行後續步驟。

1. 導覽至URL： `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`。
1. 搜尋`bundle.jar`並將`bundle.jar`重新命名為`bundle.jar.bak`。
1. 從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar)複製此位置的`Bundle for AEM 6.5 Forms on JEE Service Pack 15`。
1. 啟動應用程式伺服器，等待記錄檔穩定並檢查套件組合狀態。
1. 當所有套件組合都處於作用中狀態時，請從`system/console/bundles`在JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)上安裝AEM 6.5 Forms的[片段，並等待應用程式伺服器穩定下來。
1. 停止應用程式伺服器。
1. 導覽至`[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1`並刪除`bundle.jar`。
1. 將`bundle.jar.bak`重新命名為`bundle.jar`。
1. 啟動應用程式伺服器。
