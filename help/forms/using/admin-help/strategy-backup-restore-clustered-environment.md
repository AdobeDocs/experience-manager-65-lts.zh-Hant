---
title: 在叢集環境中進行備份與還原的策略
description: 如果您的AEM表單實作將其他自訂資料儲存在其他資料庫中，您必須實作策略來備份此資料，以確保其與AEM表單資料保持同步。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 0fe9b02a-96b4-462f-a940-a2d6084ed0a4
source-git-commit: 1b7e0c532ab46346059de01cee4a1adecf3a0a13
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# 在叢集環境中進行備份與還原的策略 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>如果您的AEM表單實作將其他自訂資料儲存在其他資料庫中，您必須實作策略來備份此資料，以確保其與AEM表單資料保持同步。 此外，應用程式的設計必須足夠健全，能夠處理其他資料庫不同步的情況。 強烈建議您在交易內容中執行任何資料庫作業，以協助維持一致狀態。

您需要備份AEM表單系統的下列部分，才能從任何錯誤中復原：

* AEM表單使用的資料庫
* 有長期資料和其他永續性檔案的GDS
* AEM資料庫(crx-repository)

>[!NOTE]
>
>您需要備份AEM表單設定所使用的任何其他資料，例如客戶字型、聯結器資料等。

## 備份叢集環境 {#back-up-a-clustered-environment}

本主題說明備份任何AEM表單叢集環境的下列策略：

* 離線備份與停機時間
* 離線備份，不需停機（備份已關閉的次要節點）
* 線上備份沒有停機時間，但回應延遲
* 備份Bootstrap屬性檔案

### 離線備份與停機時間 {#offline-backup-with-downtime}

1. 關閉整個叢集及相關服務。 （請參閱[啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)）
1. 在任何節點上，備份資料庫、GDS和聯結器。 （請參閱[要備份和復原的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)）
1. 若要離線備份AEM存放庫，請執行以下步驟：

   1. 針對每個叢集節點，備份包含叢集節點ID的檔案。
   1. 備份任何次要叢集節點的所有檔案，包括子目錄。
   1. 分別備份每個叢集節點的儲存庫/系統ID。

   如需詳細步驟，請參閱[備份與還原](/help/sites-administering/backup-and-restore.md)。

1. 備份任何其他資料，例如客戶字型。
1. 再次啟動叢集。

### 離線備份，無停機時間 {#offline-backup-with-no-downtime}

1. 進入滾動備份模式。 （請參閱[進入備份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)）

   復原後，請離開滾動備份模式。

1. 關閉任何與AEM相關的叢集次要節點。 （請參閱[啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)）
1. 在任何節點上，備份資料庫、GDS和聯結器。 （請參閱[要備份和復原的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)）
1. 若要離線備份AEM存放庫，請執行以下步驟：

   1. 針對每個叢集節點，備份包含叢集節點ID的檔案。
   1. 備份任何次要叢集節點的所有檔案，包括子目錄。
   1. 分別備份每個叢集節點的repository/system.id 。

   如需詳細步驟，請參閱[備份與還原](/help/sites-administering/backup-and-restore.md)。

1. 備份任何其他資料，例如客戶字型。
1. 再次啟動叢集。

### 線上備份沒有停機時間，但回應延遲 {#online-backup-with-no-downtime-but-delay-in-response}

1. 進入滾動備份模式。 （請參閱[進入備份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)）

   復原後，請離開滾動備份模式。

1. 關閉任何與AEM相關的叢集次要節點。 （請參閱[啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)）
1. 在任何節點上，備份資料庫、GDS和聯結器。 （請參閱[要備份和復原的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)）
1. 若要線上備份AEM存放庫，請執行以下步驟：

   1. 針對每個叢集節點，備份包含cluster_node.id的檔案。
   1. 分別備份每個叢集節點的repository/system.id 。
   1. 在任何次要節點上，對存放庫進行線上備份，以取得詳細步驟，請參閱線上備份。

1. 備份任何其他資料，例如客戶字型。
1. 再次啟動叢集。

### 備份Bootstrap屬性檔案 {#back-up-the-bootstrap-properties-file}

建立AEM叢集時，會在應用程式伺服器中為所有次要節點建立屬性檔案。 建議備份Bootstrap屬性檔案。 您可以在應用程式伺服器的下列位置找到檔案：

* JBoss®：在BIN目錄中
* WebLogic：在網域目錄中
* WebSphere®：在設定檔目錄中

備份檔案以用於AEM次要節點的災難復原情況，並在應用程式伺服器上的指定位置取代該檔案（如果還原）。

## 在叢集環境中進行復原 {#recovery-in-a-clustered-environment}

如果整個叢集或單一節點發生任何失敗，請使用備份來還原。

若要進行單一節點復原，請關閉單一節點並執行單一節點復原程式。

如果整個叢集因資料庫當機等失敗而失敗，請執行下列步驟。 還原取決於使用的備份方法。

### 還原單一節點 {#restoring-a-single-node}

1. 停止損壞的節點。

   >[!NOTE]
   >
   >如果損壞的節點是AEM主要節點，請關閉整個叢集節點。

1. 從系統映像重新建立實體系統。
1. 套用修補程式或更新至AEM表單，這些修補程式或更新在製作影像後即已套用。 備份程式期間會記錄此資訊。 AEM表單必須復原到與系統備份時相同的修補程式層級。
1. （*選擇性*）如果所有其他節點都正常運作，AEM存放庫也有可能已損毀。 在此情況下，您會在AEM存放庫的error.log檔案中看到一個存放庫取消同步訊息。

   若要還原存放庫，請執行下列步驟。

   >[!NOTE]
   >
   >如果已壓縮的crx存放庫備份連線，請在任何位置將其解壓縮，然後進行離線還原程式。

   1. 刪除節點之clusterNode目錄中的儲存庫、共用、版本和工作區目錄。
   1. 將叢集節點（包括子目錄）的備份還原至節點。
   1. 刪除節點上的檔案clusterNode/revision.log 。
   1. 刪除節點上的.lock （如果存在）。
   1. 刪除節點上的repository/system.id （如果存在）。
   1. 刪除節點上的檔案&amp;amp；&amp;amp；&amp;ast；/listener.properties （如果存在）。
   1. 還原個別叢集節點的repository/cluster_node.id。

>[!NOTE]
>
>請考量下列幾點：

* 如果失敗的節點是AEM主要節點，請將次要存放庫資料夾（crx-repository\crx.0000，其中0000可以是任何數字）中的所有內容複製到crx-repository\存放庫資料夾，並刪除次要存放庫資料夾。
* 在重新啟動任何叢集節點之前，請確定您已從主要節點刪除存放庫/clustered.txt 。
* 確定主要節點先啟動，並在啟動後啟動其他節點。

### 還原整個叢集 {#restoring-the-entire-cluster}

1. 停止所有叢集節點。
1. 從系統映像重新建立實體系統。
1. 套用修補程式或更新至AEM formsAEM表單，這些修補程式或更新在製作影像後已套用。 此資訊會記錄在備份程式的步驟1中。 AEM表單必須復原到與系統備份時相同的修補程式層級。
1. 還原資料庫、GDS和聯結器。
1. 執行下列動作以離線復原AEM存放庫：

   >[!NOTE]
   >
   >如果已壓縮的crx存放庫備份連線，請在任何位置將其解壓縮，然後進行離線還原程式。

   1. 在所有叢集節點上，刪除clusterNode目錄中的存放庫、共用目錄、版本目錄和工作區目錄。
   1. 刪除共用目錄中的所有檔案和目錄。
   1. 將叢集節點（包括子目錄）的備份還原至一個叢集節點。
   1. 將已還原叢集節點的所有檔案複製到所有其他叢集節點。 完成後，每個叢集節點都會包含相同的資料。
   1. 刪除所有叢集節點上的檔案clusterNode/revision.log 。
   1. 刪除所有叢集節點上的.lock （如果存在）。
   1. 刪除repository/system.id所有叢集節點（如果存在）。
   1. 刪除所有叢集節點上的檔案&amp;amp；&amp;amp；&amp;ast；/listener.properties （如果存在）。
   1. 還原個別叢集節點的repository/cluster_node.id。

>[!NOTE]
>
>請考量下列幾點：

* 如果失敗的節點是AEM主要節點，請將次要存放庫資料夾中的所有內容（類似於crx-repository\crx.000，其中0000可以是任何數字）複製到crx-repository\存放庫資料夾。
* 在重新啟動任何叢集節點之前，請確定您已從主要節點刪除存放庫/clustered.txt 。
* 確定主要節點先啟動，並在啟動後啟動其他節點。

## 備份和還原Correspondence Management Solution發佈節點 {#back-up-and-restore-correspondence-management-solution-publish-node}

發行者節點在叢集環境中沒有任何主要 — 次要關係。 您可以執行[備份與還原](/help/sites-administering/backup-and-restore.md)，以備份任何發行者節點。

### 復原單一發行者節點 {#recover-a-single-publisher-node}

1. 關閉必須復原的節點，在節點再次啟動之前不要進行任何發佈活動。
1. 使用[還原備份](/help/sites-administering/backup-and-restore.md)來還原發佈節點。

### 復原叢集 {#recover-a-cluster}

1. 關閉叢集。
1. 使用[還原備份](/help/sites-administering/backup-and-restore.md)來還原發佈節點。
1. 啟動主要節點，接著啟動製作叢集的次要節點。
