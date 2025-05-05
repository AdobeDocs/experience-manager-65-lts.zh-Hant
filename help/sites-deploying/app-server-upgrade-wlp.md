---
title: 應用程式伺服器安裝的升級步驟(WLP)
description: 瞭解如何升級透過Webspehere Liberty部署的AEM執行個體。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 2a5d9026-49bc-4766-bcbe-38d834c14f72
source-git-commit: 82af7ee5b3665dcc33b47e05c8580e9981728888
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# 應用程式伺服器安裝的升級步驟(WLP) {#upgrade-steps-for-application-server-installations-wlp}

>[!NOTE]
>
>本頁面概述WLP (WebSphere® Liberty)上AEM 6.5 LTS的升級程式。

## 升級前步驟 {#pre-upgrade-steps}

在執行升級之前，必須完成數個步驟。 如需詳細資訊，請參閱[升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md)和[升級前維護工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，請確定您的系統符合AEM 6.5 LTS[&#128279;](/help/sites-deploying/technical-requirements.md)的需求。

檢查[規劃升級](/help/sites-deploying/upgrade-planning.md)，以及[AEM Analyzer](/help/sites-deploying/aem-analyzer.md)如何協助您評估升級AEM的複雜性。

### 移轉先決條件 {#migration-prerequisites}

* **最低必要的Java版本**：請確定您已在WLP伺服器上安裝IBM® Sumeru JRE 17。

### 執行升級 {#performing-the-upgrade}

1. 在執行任何升級活動之前，請確定您已完成[預先升級](#pre-upgrade-steps)步驟，例如備份AEM 6.5伺服器
1. 根據您的需求，選擇下列其中一個升級路徑：
   1. **就地升級**：如果目前的WLP伺服器支援Servlet 6，您可以執行就地升級並繼續步驟3。
   1. **Sidegrade**：如果您偏好全新的設定，或您的WLP伺服器不支援Servlet 6，請設定含AEM 6.5 LTS的新WLP執行個體，並按照[AEM 6.5 Content Migration Using Oak-upgrade](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md)指南中的指示，將內容移轉至AEM 6.5 LTS，然後跳至[Deploy Upgraded Codebase](#deploy-upgraded-codebase)區段

1. 停止AEM執行個體。 通常可使用此命令來完成：

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. 移除不再需要的檔案和資料夾。 您需要明確移除的專案包括：

   * 來自`dropins`資料夾的&#x200B;**cq-quickstart-65.war**&#x200B;和`expanded`資料夾通常分別位於`<path-to-aem-server>/dropins/cq-quickstart-65.war`和`<path-to-aem-server>/apps/expanded/cq-quickstart-65.war`
   * `launchpad/startup`資料夾。 假設您位於伺服器資料夾中，您可以在終端機中執行以下命令來刪除它：

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * `base.jar`檔案。 您可以執行下列命令來達成此目的：

     ```shell
     find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt`檔案：

     ```shell
     rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 執行，移除`sling.options`檔案：

     ```shell
     find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * 移除`sling.bootstrap.txt`檔案：

     ```shell
     rm -rf crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. 備份`sling.properties`檔案（通常出現在`crx-quickstart/conf/`中）並刪除它
1. 將`server.xml`檔案中的servlet版本變更為&#x200B;**6.0**
1. 安裝Java 17，並透過執行以下指令來確保正確安裝：

   ```shell
   java -version
   ```

1. 請檢閱AEM伺服器的啟動引數，並確保根據您的需求更新引數。 如需詳細資訊，請參閱[Java 17考量事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)。
1. 下載新的6.5 LTS WAR並將其複製到以下位置的資料夾： `/<path-to-aem-server>/dropins/`
1. 啟動AEM執行個體：通常可使用此命令來完成：

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. 如果您在`sling.properties`中有自訂變更，請遵循下列指示：

   1. 執行`<path-to-wlp-directory>/bin/server stop server_name`以停止AEM執行個體
   1. 將您的自訂`sling.properties`變更套用至新產生的`sling.properties`檔案（參考在步驟5建立的備份檔案）
   1. 啟動AEM執行個體。 通常可以透過執行： `<path-to-wlp-directory>/bin/server start server_name`來完成

## 部署升級的程式碼基底 {#deploy-upgraded-codebase}

升級程式完成後，應部署更新的程式碼基底。 您可以在[升級程式碼和自訂頁面](/help/sites-deploying/upgrading-code-and-customizations.md)中找到更新程式碼基底以在AEM目標版本中運作的步驟。

## 執行升級後檢查和疑難排解 {#perform-post-upgrade-checks-and-troubleshooting}

請參閱[升級後檢查及疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
