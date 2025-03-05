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
source-git-commit: d4f89be13039e53564cd3a3148a4b845bcc183a7
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 升級至Adobe Experience Manager (AEM) 6.5 LTS {#upgrading-to-aem}

>[!NOTE]
>最新6個Service Pack支援升級至AEM 6.5 LTS。

本節說明如何將AEM安裝升級至AEM 6.5 LTS：

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

基礎層現在支援Java 17，並結合Apache Sling、Felix和Jackrabbit Oak的最新開放原始碼套件組合。 此外，AEM 6.5 LTS uber-jar的封裝已變更。 此外，AEM 6.5 LTS中也移除了一些舊版功能。 如需詳細資訊，請參閱[發行說明](/help/release-notes/release-notes.md#whats-new-what-s-new)和[升級後解除安裝的過時套件組合清單](/help/sites-deploying/obsolete-bundles.md)

AEM 6.5 LTS著重於功能的回溯相容性，並隨附分析器工具。 請參閱[使用AEM Analyzer評估升級複雜性](/help/sites-deploying/aem-analyzer.md)，以瞭解當您開始[規劃升級](/help/sites-deploying/upgrade-planning.md)時的複雜性評估。
