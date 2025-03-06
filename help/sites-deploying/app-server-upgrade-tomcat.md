---
title: 應用程式伺服器安裝的升級步驟(Tomcat)
description: 瞭解如何升級透過Tomcat部署的AEM執行個體。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 7f8de16f-9e9a-4d37-9978-d26c496b911c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 應用程式伺服器安裝的升級步驟(Tomcat) {#upgrade-steps-for-application-server-installations-tomcat}

>[!NOTE]
>
>本頁面概述Tomcat上AEM 6.5 LTS的升級程式。

## 升級前步驟 {#pre-upgrade-steps}

在執行升級之前，必須完成數個步驟。 如需詳細資訊，請參閱[升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md)和[升級前維護工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，請確定您的系統符合AEM 6.5 LTS ](/help/sites-deploying/technical-requirements.md)的[需求，並檢視[升級計畫考量事項](/help/sites-deploying/upgrade-planning.md)以及[分析器](/help/sites-deploying/pattern-detector.md)如何協助您估計複雜性。


### 移轉先決條件 {#migration-prerequisites}

* **最低必要的Java版本**：請確定您已在Tomcat伺服器上安裝Oracle® JRE 17。
* **Tomcat伺服器**： 6.5 LTS所需的Tomcat伺服器版本是&#x200B;**11.0.x**。

### 執行升級 {#performing-the-upgrade}

此程式中的所有範例都使用Tomcat作為應用程式伺服器，並暗示您已部署AEM的有效版本。 此程式旨在記錄從AEM版本&#x200B;**6.5**&#x200B;到&#x200B;**6.5 LTS**&#x200B;所執行的升級。

1. 如果已部署AEM 6.5，請存取： *`https://<serveraddress:port>/system/console/bundles`*&#x200B;以檢查套件組合是否正常運作
1. 接下來，停止AEM 6.5。這可以從Tomcat App Manager完成，位於： *`https://<serveraddress:port>/manager/html`*
1. 在執行任何升級活動之前，請確定您已完成[預先升級](#pre-upgrade-steps)活動，例如AEM 6.5伺服器的備份
1. 安裝Java 17，並透過執行以下命令來確保它正確安裝：

   ```
   java –version
   ```

1. 設定與AEM 6.5 LTS相容的Tomcat伺服器
1. 請檢閱AEM伺服器的啟動引數，並確保根據系統需求更新引數。 如需詳細資訊，請參閱[Java 17考量事項](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations)
1. 使用Java 17在Tomcat伺服器上部署新下載的6.5 LTS War，並透過執行以下指令來啟動AEM 6.5 LTS Tomcat伺服器：

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEM啟動並執行後，請存取： *`https://<serveraddress:port>/cq/system/console/bundles`*，確認所有套件組合都處於執行狀態
1. 停止AEM 6.5 LTS Tomcat伺服器。 在大多數情況下，您可以透過從終端機執行此命令來執行`./catalina.sh`指令碼：

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 現在，請依照下列步驟，將您的內容從AEM 6.5移轉至AEM 6.5 LTS： [使用AEM升級將AEM 6.5內容移轉至Oak 6.5 LTS](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md)
1. 內容移轉後，請在`sling.properties`檔案中套用任何必要的自訂變更
1. 執行下列動作以啟動AEM 6.5 LTS Tomcat伺服器：

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 在AEM啟動時監視錯誤記錄，以檢查沒有錯誤以及AEM是否順利執行
1. AEM 6.5 LTS啟動後，請存取： *`https://<serveraddress:port>/cq/system/console/bundles`*&#x200B;以檢查套件組合是否正常運作

## 部署升級的程式碼基底 {#deploy-upgraded-codebase}

升級程式完成後，應部署更新的程式碼基底。 您可以在[升級程式碼和自訂頁面](/help/sites-deploying/upgrading-code-and-customizations.md)中找到更新程式碼基底以在AEM目標版本中運作的步驟。

## 執行升級後檢查和疑難排解 {#perform-post-upgrade-checks-and-troubleshooting}

如需詳細資訊，請參閱[升級後檢查及疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
