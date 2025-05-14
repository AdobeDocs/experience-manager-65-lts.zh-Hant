---
title: 執行就地升級
description: 瞭解如何針對AEM 6.5 LTS執行就地升級。
topic-tags: upgrading
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: c7351625-b29e-45a7-b966-e7c0f56d4f22
source-git-commit: 9e58e4c993929f792bd71bf70b3e64719e761b7f
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 執行就地升級 {#performing-an-in-place-upgrade}

>[!NOTE]
>
>本頁面概述AEM 6.5 LTS的就地升級程式。 如果安裝已部署到應用程式伺服器，請參閱[應用程式伺服器安裝的升級步驟](/help/sites-deploying/app-server-upgrade.md)。

## 升級前步驟 {#pre-upgrade-steps}

在執行升級之前，必須完成數個步驟。 如需詳細資訊，請參閱[升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md)和[升級前維護工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，請確定您的系統符合AEM 6.5 LTS ](/help/sites-deploying/technical-requirements.md)的[需求，並檢視[升級計畫考量事項](/help/sites-deploying/upgrade-planning.md)以及[分析器](/help/sites-deploying/pattern-detector.md)如何協助您估計複雜性。

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 移轉先決條件 {#migration-prerequisites}

* **最低必要的Java版本：**&#x200B;請確定您的系統上已安裝Oracle的Java™ 17/21。

## 準備AEM Quickstart jar檔案 {#prep-quickstart-file}

1. 下載新的AEM 6.5 LTS jar檔案

1. [判斷正確的升級啟動命令](#determining-the-correct-upgrade-start-command)

1. 如果執行個體正在執行，請停止執行個體

1. 使用新的AEM 6.5 LTS jar取代`crx-quickstart`資料夾之外的舊的

1. 備份`sling.properties`檔案（通常出現在`crx-quickstart/conf/`中），然後刪除它

1. 透過執行以下動作將新的quickstart jar解壓縮：

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

1. 如果需要套用自訂sling.properties，請建立新的本機AEM執行個體，並從其crx-quickstart/conf目錄中擷取sling.properties檔案。 套用必要的自訂變更至此檔案，然後將其複製到要升級之AEM執行個體的crx-quickstart/conf目錄。 如果沒有自訂屬性，可以跳過此步驟。

<!-- Alexandru: drafting temporarily

## Content Repository Migration {#content-repository-migration}

This migration is not required if you are upgrading from AEM 6.3. For versions older than 6.3, Adobe provides a tool that can be used to migrate the repository to the new version of the Oak Segment Tar present in AEM 6.3. It is provided as part of the quickstart package and is mandatory for any upgrades that will be using TarMK. Upgrades for environments that are using MongoMK do not require repository migration. For more information on what the benefits of the new Segment Tar format are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

The actual migration is performed using the standard AEM quickstart jar file, executed with a new `-x crx2oak` option which executes the crx2oak tool to simplify the upgrade and make it more robust.

>[!NOTE]
>
>If you are performing TarMK repository content migration using the CRX2Oak Quickstart extension, you might remove the **samplecontent** runmode by adding the following to the migration command line:
>
>* `--promote-runmode nosamplecontent`
>

To determine the command that you should run, use the following command:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Where `<<YOUR_PROFILE>>` and `<<ADDITIONAL_FLAGS>>` are replaced with the profile and flags listed in the following table:

<table>
 <tbody>
  <tr>
   <td><strong>Source Repository</strong></td>
   <td><strong>Target Repository</strong></td>
   <td><strong>Profile</strong></td>
   <td><strong>Additional Flags</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 or TarMK with <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK or crx2 with <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>TarMK with no datastore</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>No migration is needed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Where:**

* `mongo-host` is the MongoDB server IP (for example, 127.0.0.1)

* `mongo-port` is the MongoDB server port (for example: 27017)

* `mongo-database-name` represents the name of the database (for example: aem-author)

**You may also require additional switches for the following scenarios:**

* If you are performing the upgrade on a Windows system where Java memory mapping is not handled correctly, add the `--disable-mmap` parameter to the command.

For additional instructions on using the crx2oak tool, see Using the [CRX2Oak Migration Tool](/help/sites-deploying/using-crx2oak.md). The crx2oak helper JAR can be manually upgraded if needed, by manually replacing it with newer versions after unpacking the quickstart. Its location in the AEM installation folder is: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. The newest version of the CRX2Oak migration tool is available for download from the Adobe Repository at: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

If the migration has completed successfully, the tool will exit with an exit code of zero. Additionally, check for WARN and ERROR messages in the `upgrade.log` file, located under `crx-quickstart/logs` in the AEM installation directory, as these could indicate non-fatal errors that occurred during the migration.

Check the configuration files beneath `crx-quickstart/install` folder. If a migration was necessary these will be updated to reflect the target repository.

**A note on datastores:**

While `FileDataStore` is the new default for AEM 6.3 installations, using an external datastore is not required. While using an external datastore is recommended as a best practice for production deployments, it is not a prerequisite to upgrade. Due to the complexity already present in upgrading AEM, Adobe recommends performing the upgrade without doing a datastore migration. If desired, a datastore migration can be executed afterwards as a separate effort.

## Troubleshooting Migration Issues {#troubleshooting-migration-issues}

Skip this section if you are upgrading from 6.3. While the provided crx2oak profiles should meet the needs of most customers, there are times when additional parameters will be necessary. If you run into an error during your migration, it is possible that there are aspects of your environment that require additional configuration options to be provided. If so, you will likely encounter the following error:

**Checkpoints are not copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info.**

For some reason, the migration process needs access to binaries in the datastore and is unable to find it. To specify your datastore configuration, include the following flags in the `<<ADDITIONAL_FLAGS>>` portion of your migration command:

**For S3 datastores:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Where `/path/to/SharedS3DataStore.config` represents the path to your S3 datastore config file and `/path/to/datastore` represents the path to your S3 datastore.

**For File datastores:**

```shell
--src-datastore=/path/to/datastore
```

Where `/path/to/datastore` represents the path to your File Datastore.

-->

## 執行升級 {#performing-the-upgrade}

**如果使用S3：**

1. 移除`crx-quickstart/install`底下與舊版S3聯結器關聯的所有jar。

1. 從[https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) <!-- Alexandru: this is a stub link for now -->下載1.60.2 S3聯結器的最新版本

1. 解壓縮S3聯結器（1.60.2版）並複製`crx-quickstart/install`下下列資料夾的內容，如下所示：

   1. 複製`crx-quickstart/install/1`下的`com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/1`
   1. 複製`crx-quickstart/install/15`下的`com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/15`

現在，使用[決定正確的升級啟動命令](#determining-the-correct-upgrade-start-command)區段下的資訊，使用新命令來啟動AEM執行個體。

### 正在判斷正確的升級開始命令 {#determining-the-correct-upgrade-start-command}

>[!NOTE]
>
>Java 17/21中已移除對部分Java 8/11引數的支援，請參閱[Oracle Java™ 17檔案](https://docs.oracle.com/en/java/javase/17/docs/specs/man/java.html)、[Oracle Java™ 21檔案](https://docs.oracle.com/en/java/javase/21/docs/specs/man/java.html)以及AEM 6.5 LTS的[Java&amp;trade引數考量事項](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations)。

若要執行升級，重要的是使用jar檔案啟動AEM以啟動執行個體。

請注意，從啟動指令碼啟動AEM將不會開始升級。 大部分客戶都是使用啟動指令碼啟動AEM，並已自訂此啟動指令碼，以納入環境設定（例如記憶體設定、安全性憑證等）的開關。 因此，Adobe建議依照此程式來決定正確的升級命令：

1. 在執行中的AEM執行個體上，從命令列執行以下命令：

   ```shell
   ps -ef | grep java
   ```

1. 尋找AEM程式。 它看起來會像這樣：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 將現有jar的路徑（在此案例中為`crx-quickstart/app/aem-quickstart*.jar`）取代為`crx-quickstart`資料夾同層級的新AEM 6.5 LTS jar，以修改命令。 以我們先前的指令為例，我們的指令會是：

   ```shell
   /usr/bin/java -server -Xmx4096m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar <AEM-6.5-LTS.jar> -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   這將確保所有適當的記憶體設定、自訂執行模式和其他環境引數都套用於升級。 升級完成後，執行個體可在未來啟動時從啟動指令碼啟動。

## 部署升級的程式碼基底 {#deploy-upgraded-codebase}

就地升級程式完成後，應部署更新的程式碼基底。 您可以在[升級程式碼和自訂頁面](/help/sites-deploying/upgrading-code-and-customizations.md)中找到更新程式碼基底以在AEM目標版本中運作的步驟。

## 執行升級後檢查和疑難排解 {#perform-post-upgrade-check-troubleshooting}

請參閱[升級後檢查及疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
