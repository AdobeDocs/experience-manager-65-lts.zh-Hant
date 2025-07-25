---
title: 復原AEM表單資料
description: 本檔案說明復原AEM表單資料所需的步驟。
contentOwner: admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 6345edda-cdc6-4e13-ade6-2dd6de9d9616
source-git-commit: f7adcbe7700d0ea9cbd18eb0b59bcd76f56e8cc5
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---

# 復原AEM表單資料 {#recovering-the-aem-forms-data}

本節說明復原AEM表單資料所需的步驟。 另請參閱[備份與復原的特殊考量](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery)。

>[!NOTE]
>
>資料庫、GDS、AEM存放庫和內容儲存根目錄必須還原至與原始資料庫具有相同DNS名稱的電腦。

AEM forms應該可以從以下故障中可靠地復原：

**磁碟失敗：**&#x200B;需要最新的備份媒體才能復原資料庫內容。

**資料損毀：**&#x200B;檔案系統沒有記錄過去的交易記錄，系統可能會意外覆寫必要的程式資料。

**使用者錯誤：**&#x200B;復原僅限於資料庫所提供的資料。 如果資料已儲存且可供使用，復原程式就會簡化。

**電源中斷，系統當機：**&#x200B;檔案系統API的設計或使用方式通常不夠穩健，無法防止意外的系統故障。 如果發生電源中斷或系統當機，儲存在資料庫中的檔案內容比儲存在檔案系統中的內容更可能是最新的。

如果您使用捲動備份模式，復原後仍會處於備份模式。 如果您使用快照備份模式，則在復原後不會處於備份模式。

從備份還原至新系統時，下列設定可能會不同。 此差異不應影響AEM表單應用程式的成功復原：

* IP 位址
* 實體系統組態（CPU、磁碟、記憶體）
* GDS位置

>[!NOTE]
>
>內容儲存根目錄的備份必須還原到該目錄的位置，如同在Content Services設定期間所設定的一樣。

如果多節點叢集的單一節點失敗，且叢集的其餘節點正常運作，請執行叢集單一節點復原程式。

## 復原AEM表單資料 {#recover-the-aem-forms-data}

1. 停止AEM Forms服務和應用程式伺服器（如果執行）。
1. 如有必要，請從系統映像重新建立實體系統。 例如，如果復原的原因是錯誤的資料庫伺服器，則可能不需要執行此步驟。
1. 套用修補程式或更新至AEM表單，這些修補程式或更新在製作影像後即已套用。 此資訊會記錄在備份程式中。 AEM表單必須修補至與系統備份時相同的修補層級。
1. (WebSphere® Application Server)如果要復原到WebSphere® Application Server的新執行個體，請執行restoreConfig.bat/sh命令。
1. 請先使用資料庫備份檔案執行資料庫還原作業，然後將交易重做日誌套用至復原的資料庫，以復原AEM表單資料庫。 (請參閱[AEM表單資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。)如需詳細資訊，請參閱下列知識庫文章之一：

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [適用於AEM表單的Oracle備份與復原](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [適用於AEM表單的MySQL備份與復原](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. 請先刪除AEM表單現有安裝上的GDS目錄內容，然後從備份的GDS複製GDS目錄內容，以復原GDS目錄。 如果您變更了GDS目錄位置，請參閱[在復原期間變更GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。
1. 重新命名要還原的GDS備份目錄，如下列範例所示：

   >[!NOTE]
   >
   >如果/restore目錄已經存在，請先備份該目錄，然後再刪除它，然後再重新命名包含最新資料的/backup目錄。

   * (JBoss®)將`[appserver root]/server/'server'/svcnative/DocumentStorage/backup`重新命名為：

     `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`。

   * (WebLogic)將`[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup`重新命名為：

     `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`。

   * (WebSphere®)將`[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup`重新命名為：

     `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`。

1. 請先刪除現有AEM Forms安裝上的「內容儲存根目錄」內容，然後針對獨立或叢集環境執行以下工作來復原內容，以復原「內容儲存根目錄」：

   >[!NOTE]
   >
   >內容儲存根目錄的備份，必須還原至內容儲存根目錄的位置，如同在內容服務（已棄用）設定期間所設定。

   **獨立：**&#x200B;在復原程式中，還原所有已備份的目錄。 還原這些目錄時，如果存在/backup-lucene-indexes目錄，請將其重新命名為/lucene-indexes。 否則，lucene-indexes目錄應該已經存在，並且不需要採取任何動作。

   **叢集：**&#x200B;在復原程式中，還原所有已備份的目錄。 若要還原索引根目錄，請在叢集的每個節點上執行下列步驟：

   * 刪除索引根目錄中的所有內容。
   * 如果/backup-lucene-indexes目錄存在，請將&#x200B;*內容儲存根目錄*/backup-lucene-indexes目錄的內容複製到索引根目錄，並刪除&#x200B;*內容儲存根目錄*/backup-lucene-indexes目錄。
   * 如果/lucene-indexes目錄存在，請將&#x200B;*內容儲存根目錄*/lucene-indexes目錄的內容複製到索引根目錄。

1. 還原/復原CRX-repository。

   * **獨立**

     *還原作者和發佈執行個體*：如果發生災難，您可以執行[備份與還原](/help/sites-administering/backup-and-restore.md)中所述的步驟，將存放庫還原到上次備份的狀態。

     「作者」節點完全還原後，Forms Manager和AEM Forms Workspace資料也會完全還原。

   * **叢集**

     若要在叢集環境中進行還原，請參閱[在叢集環境中進行備份與還原的策略](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment)。

1. 刪除在java.io.temp目錄或AEM臨時目錄中建立的任何Adobe表單暫存檔。
1. 啟動AEM表單（請參閱[啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)）<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->。

## 在復原期間變更GDS位置 {#changing-the-gds-location-during-recovery}

如果您的GDS還原到原始位置以外的位置，請執行LCSetGDS指令碼以將GDS設定到新位置。 指令碼在`[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline`資料夾中。 指令碼需要兩個引數： `defaultGDS`和`newGDS`。 如需如何執行指令碼的指示，請參閱相同資料夾中的`ReadMe.txt`檔案。

>[!NOTE]
>
>如果您已在資料庫中啟用檔案儲存，則不需要變更GDS位置。

>[!NOTE]
>
>只有在這種情況下，您才應該使用此指令碼來變更GDS位置。 若要在AEM表單執行時變更GDS位置，請使用管理主控台。 (請參閱[設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。)

>[!NOTE]
>
>如果GDS目錄位於磁碟機根目錄(例如，D:\)，則在Windows上部署元件將會失敗。 對於GDS，您必須確定目錄不是位於磁碟機的根目錄，而是位於子目錄中。 例如，目錄應該是D:\GDS，而不應該只是D:\。

## 將GDS復原至叢集環境 {#recovering-the-gds-to-a-clustered-environment}

若要變更叢集環境中的GDS位置，請關閉整個叢集，並在叢集的單一節點上執行LCSetGDS指令碼。 （請參閱[在復原期間變更GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。）僅啟動該節點。 當該節點完全啟動時，叢集中的其他節點可以安全地啟動，並正確地指向新的GDS。

>[!NOTE]
>
>如果您無法確保在啟動其他節點之前完全啟動一個節點，則必須在啟動叢集之前，在叢集中的每個節點上執行LCSetGDS指令碼。
