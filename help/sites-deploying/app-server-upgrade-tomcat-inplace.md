---
title: 應用程式伺服器安裝的升級步驟(Tomcat)
description: 瞭解如何升級透過Tomcat部署的AEM執行個體。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: b3c4e946a3f235fa0e3a0945f1ad692ee195e3ef
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 應用程式伺服器安裝的升級步驟（Tomcat — 就地升級） {#upgrade-steps-for-application-server-installations-tomcat-inplace}

>[!NOTE]
>
>本頁面概述從Tomcat上的AEM 6.5 LTS升級至AEM 6.5 LTS Servicepack的升級程式（就地升級）。 若要從AEM 6.5升級至6.5 LTS，[請參閱此處](/help/sites-deploying/app-server-upgrade-tomcat.md)。

## 升級前步驟 {#pre-upgrade-steps}

在執行升級之前，必須完成數個步驟。 如需詳細資訊，請參閱[升級前維護工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，請確定您的系統符合AEM 6.5 LTS Servicepack[的](/help/sites-deploying/technical-requirements.md)需求，並參閱[升級計畫考量事項](/help/sites-deploying/upgrade-planning.md)。


### 移轉先決條件 {#migration-prerequisites}

* **最低必要的Java版本**：請確定您已在Tomcat伺服器上安裝Oracle® JRE 17/21。
* **Tomcat伺服器**： AEM 6.5 LTS及其ServicePack支援的Tomcat伺服器版本為&#x200B;**10.0.x**&#x200B;和&#x200B;**10.1.x**。

### 執行升級 {#performing-the-upgrade}

此程式中的所有範例都使用Tomcat作為應用程式伺服器，並暗示您已部署AEM 6.5 LTS的有效版本。 此程式旨在記錄從AEM版本&#x200B;**6.5** LTS到&#x200B;**6.5 LTS** Servicepack所執行的升級。

1. 如果已部署AEM 6.5 LTS，請存取： *`https://<serveraddress:port>/system/console/bundles`*&#x200B;以檢查套件組合是否正常運作
1. 接下來，停止AEM 6.5 LTS。 這可以從Tomcat App Manager完成，位於： *`https://<serveraddress:port>/manager/html`*
1. 在執行任何升級活動之前，請確定您已完成[預先升級](#pre-upgrade-steps)活動，例如AEM 6.5 LTS伺服器的備份
1. 停止AEM 6.5 LTS Tomcat伺服器。 在大多數情況下，您可以透過從終端機執行此命令來執行`./catalina.sh`指令碼：

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 移除不再需要的檔案和資料夾。 您需要明確移除的專案包括：

   * **cq-quickstart-65.war**&#x200B;檔案和來自`cq-quickstart-65`資料夾的`webapps`資料夾通常位於`<path-to-aem-server>/webapps`
   * `launchpad/startup`資料夾。 假設您位於伺服器資料夾中，您可以在終端機中執行以下命令來刪除它：

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/startup
     ```

   * `base.jar`檔案。 您可以執行下列命令來達成此目的：

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt`檔案：

     ```shell
     rm -f <path-to-aem-server>/bin/crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 執行，移除`sling.options`檔案：

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * 移除`sling.bootstrap.txt`檔案：

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. 備份`sling.properties`檔案（通常出現在`<path-to-aem-server>/bin/crx-quickstart/launchpad/`中）並刪除它
1. 將AEM 6.5 LTS Servicepack war檔案複製到`<path-to-aem-server>/webapps`資料夾
1. 執行下列動作以啟動AEM 6.5 LTS Tomcat伺服器：

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 在AEM啟動時監視錯誤記錄，以檢查沒有錯誤以及AEM是否順利執行
1. AEM 6.5 LTS啟動後，請存取： *`https://<serveraddress:port>/cq/system/console/bundles`*&#x200B;以檢查套件組合是否正常運作

## 執行升級後檢查和疑難排解 {#perform-post-upgrade-checks-and-troubleshooting}

如需詳細資訊，請參閱[升級後檢查及疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
