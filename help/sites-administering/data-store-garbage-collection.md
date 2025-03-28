---
title: 資料存放庫廢棄項目收集
description: 瞭解如何設定資料存放區記憶體回收以釋出磁碟空間。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
exl-id: 2b4214b0-1a38-4e36-b740-16fcaf9ceb54
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 0%

---

# 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

移除傳統WCM資產時，可能會從節點階層中移除對基礎資料存放區記錄的參考，但資料存放區記錄本身會保留。 然後，這個未參考的資料存放區記錄會變成不需要保留的「廢棄專案」。 在有數個垃圾資產的情況下，移除這些資產以保留空間並最佳化備份和檔案系統維護效能會很有幫助。

在大多數情況下，WCM應用程式傾向於收集資訊，但刪除資訊的頻率卻幾乎沒有。 雖然已新增新影像，但即使取代舊版本，版本控制系統仍會保留舊影像，並支援在需要時還原成舊影像。 因此，我們認為新增至系統的大部分內容實際上都會永久儲存。 那麼存放庫中，我們可能想要清理的「垃圾」的典型來源為何？

AEM使用存放庫作為數個內部和內部管理活動的儲存空間：

* 建置和下載的套件
* 為發佈復寫建立的暫存檔案
* 工作流程裝載
* DAM呈現期間暫時建立的Assets

當這些暫存物件中有任何物件夠大而需要在資料存放區中儲存時，以及當物件最終不使用時，資料存放區記錄本身會保留為「垃圾」。 在典型的WCM製作/發佈應用程式中，此型別記憶體的最大來源通常是發佈啟動程式。 當資料被復寫到Publish時，如果資料是先以稱為「Durbo」的有效資料格式收集到集合中，並儲存在`/var/replication/data`下的存放庫中，就會出現這種情況。 資料組合通常大於資料存放區的關鍵大小臨界值，因此最終會儲存為資料存放區記錄。 復寫完成時，會刪除`/var/replication/data`中的節點，但資料存放區記錄仍為「廢棄專案」。

另一個可復原的記憶體來源是封裝。 封裝資料（就像其他內容一樣）會儲存在存放庫中，因此大於4KB的封裝會儲存在資料存放區中。 在開發專案的過程中，或在維護系統的過程中，可能會多次構建和重建套件，每個組建都會產生新的資料存放區記錄，孤立以前的組建記錄。

## 資料儲存廢棄專案收集如何運作？ {#how-does-data-store-garbage-collection-work}

如果存放庫已設定為使用外部資料存放區，[資料存放區記憶體回收將在每週維護期間自動執行](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection)。 系統管理員也可以視需要[手動](#running-data-store-garbage-collection)執行資料存放區記憶體回收。 一般而言，建議定期執行資料存放區廢棄專案收集，但在規劃資料存放區廢棄專案收集時，應考量下列因素：

* 資料存放區記憶體回收需要時間，且可能影響效能，因此應據此規劃。
* 移除資料存放區記憶體記錄不會影響正常效能，因此這並非效能最佳化。
* 如果不必擔心儲存空間使用率及相關因素（如備份時間），資料存放區記憶體回收可能會安全地延遲。

資料存放區記憶體回收行程會在處理序開始時，先記下目前的時間戳記。 然後使用多通道標籤/掃描圖樣演演算法來執行收集。

在第一階段，資料存放區記憶體回收行程會執行所有存放庫內容的完整周遊作業。 對於每個具有資料存放區記錄參照的內容物件，它會在檔案系統中定位檔案，執行中繼資料更新 — 修改「上次修改」或MTIME屬性。 此時，此階段存取的檔案會比初始基準時間戳記更新。

在第二階段，資料存放區記憶體回收行程會周游資料存放區的實體目錄結構，其方式與「尋找」類似。 它檢查檔案的「上次修改」或MTIME屬性，並作出以下判斷：

* 如果MTIME比初始基準時間戳記新，則可能是在第一階段找到檔案，或是收集程式進行期間新增到存放庫的全新檔案。 在這兩種情況下，記錄都會被視為作用中，且檔案不可刪除。
* 如果MTIME在初始基準時間戳記之前，則檔案不是主動參照的檔案，且會視為可移除的記憶體。

此方法適用於具有私人資料存放區的單一節點。 不過，資料存放區可能會共用，如果這表示系統不會檢查來自其他存放庫之資料存放區記錄的可能作用中即時參照，且可能會誤移除作用中參照的檔案。 系統管理員在計畫任何記憶體回收之前，必須先瞭解資料存放區的共用性質，並在已知資料存放區未共用時，僅使用簡單的內建資料存放區記憶體回收流程。

>[!NOTE]
>
>在叢集或共用資料存放區設定（使用Mongo或Segment Tar）中執行記憶體回收時，記錄可能會顯示無法刪除某些blob ID的警告。 發生此情況是因為其他叢集或共用節點再次錯誤地參考了先前記憶體回收中所刪除的blob ID，而其他叢集或共用節點沒有ID刪除的相關資訊。 因此，執行記憶體回收時，會在嘗試刪除上次執行中已刪除的ID時記錄警告。 此行為不會影響效能或功能。

## 正在執行資料存放區記憶體回收 {#running-data-store-garbage-collection}

根據AEM執行所在的資料存放區設定，有三種方式可執行資料存放區記憶體回收：

1. 透過[修訂清理](/help/sites-deploying/revision-cleanup.md) — 一種通常用於節點存放區清理的記憶體收集機制。

1. 透過[資料存放區記憶體回收](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) — 作業儀表板中提供的外部資料存放區專屬記憶體回收機制。
1. 透過[JMX主控台](/help/sites-administering/jmx-console.md)。

如果TarMK同時作為節點存放區和資料存放區使用，則修訂清除可用於節點存放區和資料存放區的記憶體回收。 不過，如果外部資料存放區已設定（例如檔案系統資料存放區），則資料存放區記憶體回收必須明確觸發，且獨立於修訂清除。 資料存放區記憶體回收可以透過Operations Dashboard或JMX主控台觸發。

下表顯示AEM 6中所有支援的資料存放區部署所需使用的資料存放區廢棄專案收集型別：

<table>
 <tbody>
  <tr>
   <td><strong>節點存放區</strong><br /> </td>
   <td><strong>資料存放區</strong></td>
   <td><strong>記憶體回收機制</strong><br /> </td>
  </tr>
  <tr>
   <td>tarmk</td>
   <td>tarmk</td>
   <td>修訂清理（二進位檔案與區段存放區內聯）</td>
  </tr>
  <tr>
   <td>tarmk</td>
   <td>外部檔案系統</td>
   <td><p>透過操作控制面板的資料存放區廢棄專案收集任務</p> <p>JMX主控台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>透過操作控制面板的資料存放區廢棄專案收集任務</p> <p>JMX主控台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>外部檔案系統</td>
   <td><p>透過操作控制面板的資料存放區廢棄專案收集任務</p> <p>JMX主控台</p> </td>
  </tr>
 </tbody>
</table>

### 透過操作儀表板執行資料存放區記憶體回收 {#running-data-store-garbage-collection-via-the-operations-dashboard}

內建的每週維護視窗可透過[Operations Dashboard](/help/sites-administering/operations-dashboard.md)使用，其中包含要在星期日凌晨1:00觸發資料存放區垃圾收集的內建工作。

如果您需要在此時間以外執行資料存放區垃圾收集，可以透過操作儀表板手動觸發。

在執行資料存放區記憶體回收之前，您應該檢查當時是否沒有執行任何備份。

1. 透過&#x200B;**導覽** > **工具** > **操作** > **維護**&#x200B;開啟操作儀表板。
1. 按一下&#x200B;**每週維護期間**。

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 選取&#x200B;**資料存放區記憶體回收**&#x200B;工作，然後按一下&#x200B;**執行**&#x200B;圖示。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 資料存放區記憶體回收會執行，其狀態會顯示在儀表板中。

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>只有在您已設定外部檔案資料存放區時，資料存放區廢棄專案收集工作才會顯示。 如需有關如何設定檔案資料存放區的資訊，請參閱[在AEM 6](/help/sites-deploying/data-store-config.md#file-data-store)中設定節點存放區和資料存放區。

### 透過JMX主控台執行資料存放區記憶體回收 {#running-data-store-garbage-collection-via-the-jmx-console}

本節說明如何透過JMX主控台手動執行資料存放區記憶體回收。 如果您的安裝是在沒有外部資料存放區的情況下設定的，則這不適用於您的安裝。 請改為參閱[維護存放庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)下有關如何執行修訂清除的說明。

>[!NOTE]
>
>如果您使用外部資料存放區執行TarMK，必須先執行修訂清除，才能讓記憶體回收有效。

若要執行記憶體回收：

1. 在Apache Felix OSGi Management Console中，反白顯示&#x200B;**主要**&#x200B;索引標籤，然後從下列功能表中選取&#x200B;**JMX**。
1. 接著，搜尋並按一下&#x200B;**存放庫管理員** MBean （或移至`https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`）。
1. 按一下&#x200B;**startDataStoreGC（布林值markOnly）**。
1. 如有必要，請為`markOnly`引數輸入&quot;`true`&quot;：

   | **選項** | **說明** |
   |---|---|
   | 布林值markOnly | 設定為true以僅標籤參照，而不在標籤和掃描操作中進行掃描。 當基礎BlobStore在多個不同存放庫之間共用時，將使用此模式。 對於所有其他情況，請將其設為false以執行完整的記憶體回收。 |

1. 按一下&#x200B;**叫用**。 CRX會執行記憶體回收，並指出其完成時間。

>[!NOTE]
>
>資料存放區廢棄專案收集不會收集過去24小時內已刪除的檔案。

>[!NOTE]
>
>只有在您已設定外部檔案資料存放區時，資料存放區廢棄專案收集工作才會啟動。 如果尚未設定外部檔案資料存放區，則工作將在叫用後傳回訊息`Cannot perform operation: no service of type BlobGCMBean found`。 如需有關如何設定檔案資料存放區的資訊，請參閱[在AEM 6](/help/sites-deploying/data-store-config.md#file-data-store)中設定節點存放區和資料存放區。

## 自動化資料存放區廢棄專案收集 {#automating-data-store-garbage-collection}

如果可能的話，資料存放區垃圾收集應在系統負載很少時執行，例如，在早上。

內建的每週維護視窗可透過[Operations Dashboard](/help/sites-administering/operations-dashboard.md)使用，其中包含要在星期日凌晨1:00觸發資料存放區垃圾收集的內建工作。 您也應該檢查目前沒有執行任何備份。 必要時，可透過控制面板自訂維護時段的開始。

>[!NOTE]
>
>不同時執行的原因是，舊的（和未使用的）資料存放區檔案也會進行備份，因此如果需要復原為舊的修訂版本，二進位檔案仍會保留在備份中。

如果您不想要使用作業儀表板中的每週維護視窗來執行資料存放區廢棄專案收集，也可以使用wget或curl HTTP使用者端將其自動化。 以下是如何藉由使用curl來自動化記憶體回收的範例：

>[!CAUTION]
>
>在下列範例中，`curl`命令可能需要為您的執行個體設定各種引數；例如，主機名稱( `localhost`)、連線埠( `4502`)、管理員密碼( `xyz`)以及實際資料存放區垃圾收集的各種引數。

以下是透過命令列叫用資料存放區記憶體回收的curl命令範例：

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl命令會立即傳回。

## 檢查資料存放區一致性 {#checking-data-store-consistency}

資料存放區一致性檢查會報告任何遺失但仍被參考的資料存放區二進位檔。 若要開始一致性檢查，請遵循下列步驟：

1. 前往JMX主控台。 如需有關如何使用JMX主控台的資訊，請參閱[使用JMX主控台監視伺服器資源](/help/sites-administering/jmx-console.md#using-the-jmx-console)。
1. 搜尋&#x200B;**BlobGarbageCollection** Mbean並按一下它。
1. 按一下`checkConsistency()`連結。

一致性檢查完成後，訊息會顯示回報為遺失的二進位檔數目。 如果數字大於0，請檢查`error.log`以取得有關遺失二進位檔的詳細資料。

在底下，您會找到如何在記錄中報告遺失的二進位檔範例：

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
