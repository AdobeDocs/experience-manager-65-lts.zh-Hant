---
title: 升級至Adobe Experience Manager 6.5
description: 瞭解將舊版Adobe Experience Manager (AEM)安裝升級至AEM 6.5的基本知識。
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f66bb283e5c2a746821839269e112be8c2714ba7
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# 升級至Adobe Experience Manager (AEM) 6.5 LTS {#upgrading-to-aem}

>[!NOTE]
>最新6個Service Pack支援升級至AEM 6.5 LTS。

本節說明如何將AEM安裝升級至AEM 6.5：

<!-- Alexandru: drafting for now 

* [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)
* [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Backward Compatibility in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  This was drafted before: * [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

<!--
* [Upgrade Procedure](/help/sites-deploying/upgrade-procedure.md)
* [Upgrading Code and Customizations](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Pre-Upgrade Maintenance Tasks](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Performing an In-Place Upgrade](/help/sites-deploying/in-place-upgrade.md)
* [Post Upgrade Checks and Troubleshooting](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Sustainable Upgrades](/help/sites-deploying/sustainable-upgrades.md)
* [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md)

-->

為了更方便參考這些程式中涉及的AEM執行個體，以下辭彙已用在這些文章中：

* *來源*&#x200B;執行個體是您正在升級的AEM執行個體。
* *target*&#x200B;執行個體是您要升級的目標執行個體。

## 變更為何？ {#what-has-changed}

### 更新 {#updates}

以下是AEM最後幾個版本的注意事項主要變更：

1. Foundation層已升級並支援Java 17 (其中包含來自Apache Sling、Apache Felix和Apache Jackrabbit Oak的套件組合開放原始碼層)

1. AEM 6.5 LTS jar封裝現在支援Jarkarta Servlet API規格5，而war封裝可部署至實施Jarta Servlet API規格5/6的servlet容器

1. AEM 6.5 LTS uber-jar的封裝已變更。 如需詳細資訊，請參閱[升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md)。

### 已移除舊版功能/成品 {#removed-legacy-features-artifacts}

下列舊版解決方案已從AEM 6.5 LTS中移除。 如需詳細資訊，請參閱TBD：發行說明連結和[升級後解除安裝的過時套件組合清單](/help/sites-deploying/obsolete-bundles.md)

1. Social
1. Commerce
1. Screens
1. We-retail
1. 整合搜尋和提升

**已移除成品**

1. CRX-explorer
1. Crx2oak
1. Google guava （因安全漏洞而移除）
1. Abdera-parser （因安全性弱點而移除）
1. jdom (`org.apache.servicemix.bundles.jdom`) （因安全性弱點而移除）
1. `com.github.jknack.handlebars` （因安全性弱點而移除）

AEM 6.5 LTS著重於功能的回溯相容性，並隨附分析器工具。 請參閱[使用AEM Analyzer評估升級複雜性](/help/sites-deploying/pattern-detector.md)，瞭解您開始規劃升級時的複雜性評估。 如需其他變更的詳細資訊，請參閱這裡的完整發行說明。 待定：AEM 6.5 LTS發行說明連結