---
title: 整合 Adobe Analytics
description: 瞭解如何將Adobe Experience Manager (AEM)與Adobe Analytics整合。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 4f7e1794-af5a-45a2-8dc6-80029c47caeb
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 24%

---

# 整合 Adobe Analytics{#integrating-with-adobe-analytics}

整合Adobe Analytics和AEM可讓您追蹤您的網頁活動：

* Adobe Analytics設定可讓AEM使用Adobe Analytics進行驗證。
* 框架可識別傳送至Adobe Analytics報表套裝的資料。

資料包括頁面和使用者資料；例如：

* AEM元件收集的資料
* 連結點按次數
* 視訊使用資訊
* 來自Adobe Analytics的頁面瀏覽數

下列頁面可協助您設定整合：

* [連線到Adobe Analytics並建立框架](/help/sites-administering/adobeanalytics-connect.md)
* [設定Adobe Analytics的連結追蹤](/help/sites-administering/adobeanalytics-link.md)
* [使用Adobe Analytics屬性對應元件資料](/help/sites-administering/adobeanalytics-mapping.md)
* [設定Adobe Analytics的視訊追蹤](/help/sites-administering/adobeanalytics-video.md)
* [Adobe分類](/help/sites-administering/adobeanalytics-classifications.md)

您也可以使用[選擇加入精靈](/help/sites-administering/opt-in.md)輕鬆執行整合。

>[!NOTE]
>
>另請參閱作法文章： [使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

## 更多資訊 {#further-information}

請參閱：

* [延伸Adobe Analytics整合](/help/sites-developing/extending-analytics.md)，以取得有關開發收集使用者資料的元件以及自訂Adobe Analytics架構的資訊。

>[!NOTE]
>
>如果您使用Adobe Analytics搭配自訂的代理設定，則需要 [設定](/help/sites-deploying/configuring-osgi.md) Apache HTTP Client **&#x200B;**&#x200B;Proxy設定所需的兩個OSGi組合 (例如，搭配Web主控台)。由於AEM的某些功能使用3.x API，而其他功能則使用4.x API，因此這兩者皆為必要。設定：
>
>* **Day Commons HTTP Client 3.1**&#x200B;以設定3.x API；
>  &#x200B;>  例如，[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP元件Proxy設定**&#x200B;以設定4.x API；
>  &#x200B;>  例如，[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
