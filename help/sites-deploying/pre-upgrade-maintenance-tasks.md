---
title: 升級前維護任務
description: 瞭解為AEM建議的升級前工作。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 108e1b3d840287e3d694242d934d0fbe4606801c
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# 升級前維護任務{#pre-upgrade-maintenance-tasks}

在開始升級之前，請務必遵循這些維護任務，以確保系統準備就緒，並可在發生問題時回覆：

* [索引定義](#index-definitions)
* [確保有足夠的磁碟空間](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [完整備份AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [產生quickstart.properties檔案](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [設定工作流程和稽核記錄清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [安裝、設定及執行升級前工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [停用自訂登入模組](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [從/install目錄移除更新](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [停止任何冷待命執行個體](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [停用自訂排程工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [執行離線修訂清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [執行資料存放區記憶體回收](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [視需要升級資料庫綱要](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [刪除可能阻礙升級的使用者](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [旋轉記錄檔](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 索引定義 {#index-definitions}

請確定您至少已安裝隨AEM Service Pack 22提供的AEM 6.5 Service Pack發行的必要索引定義(如需詳細資訊，請參閱[AEM 6.5 servicepack發行說明](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/release-notes/release-notes))。

## 確保有足夠的磁碟空間 {#ensure-sufficient-disk-space}

執行升級時，除了內容和程式碼升級活動外，還必須執行存放庫移轉。 移轉作業會以新的Segment Tar格式建立存放庫復本。 因此，您需要足夠的磁碟空間，以保留儲存庫的第二個（可能更大）版本。

## 完整備份AEM {#fully-back-up-aem}

在開始升級之前，應該先完整備份AEM。 請務必備份存放庫、應用程式安裝、資料存放區和Mongo執行個體（如適用）。 如需有關備份和還原AEM執行個體的詳細資訊，請參閱[備份和還原](/help/sites-administering/backup-and-restore.md)。

## 產生quickstart.properties檔案 {#generate-quickstart-properties}

從jar檔案啟動AEM時，會在`crx-quickstart/conf`下產生`quickstart.properties`檔案。 如果AEM過去僅以啟動指令碼啟動，則此檔案不存在，且升級失敗。 請確定檢查此檔案是否存在，如果不存在，請從jar檔案重新啟動AEM。

## 設定工作流程和稽核記錄清除 {#configure-wf-audit-purging}

`WorkflowPurgeTask`和`com.day.cq.audit.impl.AuditLogMaintenanceTask`任務需要單獨的OSGi設定，沒有它們就無法運作。 如果它們在升級前工作執行期間失敗，遺失設定是最可能的原因。 因此，如果您不想執行OSGi設定，請務必為這些工作新增OSGi設定，或將其從升級前最佳化工作清單中完全移除。 您可以在[管理工作流程執行個體](/help/sites-administering/workflows-administering.md)找到設定工作流程清除工作的檔案，也可以在AEM 6](/help/sites-administering/operations-audit-log.md)中的[稽核記錄維護找到稽核記錄維護工作設定。

如需CQ 5.6的工作流程與稽核記錄清除，以及AEM 6.0的稽核記錄清除，請參閱[清除工作流程與稽核節點](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html)。

## 安裝、設定及執行升級前工作 {#install-configure-run-pre-upgrade-tasks}

升級前必須手動執行的維護工作已最佳化並自動化。 升級前維護最佳化可讓您以統一方式觸發這些任務，並可依需求檢查結果。

### 使用方式 {#how-to-use-it}

`PreUpgradeTasksMBean` OSGI元件已預先設定可一次執行所有升級前維護工作的清單。 您可以依照以下程式來設定這些工作：

1. 瀏覽至&#x200B;*https://serveraddress:serverport/system/console/configMgr*&#x200B;以移至Web主控台

1. 搜尋「**preupgradetasks**」，然後按一下第一個相符的元件。 元件的完整名稱是`com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. 修改必須執行的維護工作清單，如下所示：

   ![1487758925984](assets/1487758925984.png)

以下說明每個維護任務所針對的執行模式。

| 任務 | 備註 |
|---|---|
| WorkflowPurgeTask | 必須先設定Adobe Granite工作流程清除設定OSGi，才能執行。 |
| GenerateBundlesListFileTask |   |
| RevisionCleanupTask |   |
| com.day.cq.audit.impl.AuditLogMaintenanceTask | 必須先設定稽核記錄清除排程器OSGi設定，才能執行。 |

### 升級前健康狀態檢查的預設設定 {#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI元件已預先設定在呼叫`runAllPreUpgradeHealthChecks`方法時要執行的升級前健康情況檢查標籤清單：

* **system** - granite維護狀況檢查所使用的標籤

* **升級前** — 可新增到升級前可設定執行之所有健康狀態檢查的自訂標籤

**MBean方法**

可以使用[JMX主控台](/help/sites-administering/jmx-console.md)存取受管理Bean功能。

存取MBean的方法有：

1. 前往位於&#x200B;*https://serveraddress:serverport/system/console/jmx*&#x200B;的JMX主控台
1. 搜尋&#x200B;**PreUpgradeTasks**&#x200B;並按一下結果

1. 從&#x200B;**作業**&#x200B;區段中選取任何方法，並在下列視窗中選取&#x200B;**叫用**。

以下為`PreUpgradeTasksMBeanImpl`公開的所有可用方法清單：

| 方法名稱 | 類型 | 說明 |
|---|---|---|
| runAllPreUpgradeTasks() | 動作 | 執行清單中的所有升級前維護任務。 |
| runPreUpgradeTask(preUpgradeTaskName) | 動作 | 執行升級前維護任務，並將名稱指定為引數。 |
| getPreUpgradeTaskLastRunTime(preUpgradeTaskName) | 動作 | 顯示升級前維護工作的確切執行時間，其名稱會指定為引數。 |
| getPreUpgradeTaskLastRunState(preUpgradeTaskName) | 動作 | 顯示升級前維護任務的最後一次執行狀態，其名稱會指定為引數。 |
| runAllPreUpgradeHealthChecks(shutDownOnSuccess) | 動作 | 執行所有升級前健康情況檢查並將其狀態儲存在sling本位目錄路徑中名為preUpgradeHCStatus.properties的檔案中。 如果shutDownOnSuccess設為true，AEM執行個體會關閉，但前提是所有升級前健康狀態檢查的狀態都是「正常」。 屬性檔案是作為任何未來升級的先決條件，如果升級前健康情況檢查執行失敗，則會停止升級程式。 如果您要忽略升級前健康情況檢查的結果並仍要啟動升級，您可以刪除檔案。 |
| detectUsageOfUnavailableAPI(aemVersion) | 動作 | 列出升級到指定的AEM版本時不再滿足的所有匯入套件。 目標AEM版本必須提供為引數。 |

>[!NOTE]
>
>MBean方法可透過以下方式叫用：
>
>* JMX主控台
>* 連線到JMX的任何外部應用程式
>* cURL
>

## 從/install目錄移除更新 {#remove-updates-install-directory}

>[!NOTE]
>
>僅在關閉AEM執行個體後，從crx-quickstart/install目錄移除套件。 此步驟是開始就地升級程式之前的最後一個步驟之一。

移除任何透過本機檔案系統上的`crx-quickstart/install`目錄部署的Service Pack、Feature Pack或Hotfix。 這麼做可避免在更新完成後，在新AEM版本之上意外安裝舊版Hotfix和Service Pack。

## 停止任何冷待命執行個體 {#stop-tarmk-coldstandby-instance}

如果使用TarMK冷待命，請停止任何冷待命執行個體。 這麼做可確保在升級過程中發生問題時，能以有效率的方式重新上線。 成功完成升級後，必須從升級的主要執行個體重建冷待命執行個體。

## 停用自訂排程工作 {#disable-custom-scheduled-jobs}

停用應用程式程式碼中包含的任何OSGi排程工作。

## 執行離線修訂清除 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>只有TarMK安裝才需要此步驟

如果使用TarMK，您應在升級前執行離線修訂清除。 如此一來，存放庫移轉步驟和後續升級工作執行速度會大幅加快，有助於確保在升級完成後，線上修訂清除可以成功執行。 如需有關執行離線修訂清除的資訊，請參閱[執行離線修訂清除](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup)。

## 旋轉記錄檔 {#rotate-log-files}

Adobe建議在開始升級之前，先封存目前的記錄檔。 如此一來，在升級期間和升級之後，您就可以更輕鬆地監視和掃描記錄檔，以識別並解決任何可能發生的問題。
