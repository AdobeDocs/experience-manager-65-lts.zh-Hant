---
title: AEM表單的備份與復原策略
description: 瞭解如何實作策略以備份資料，並確保其與AEM表單資料保持同步。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2f34b48a-0b95-4994-ac4f-616620a5b211
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 0%

---

# AEM表單的備份與復原策略{#backup-and-recovery-strategy-for-aem-forms}

如果您的AEM表單實作將其他自訂資料儲存在其他資料庫中，您應負責實作策略來備份此資料，並確保其與AEM表單資料保持同步。 此外，應用程式的設計必須足夠健全，能夠處理其他資料庫不同步的情況。 強烈建議您在交易內容中執行任何資料庫作業，以協助維持一致狀態。

識別使用AEM表單的方式後，請決定必須備份哪些檔案、備份頻率以及備份視窗的可用性。

>[!NOTE]
>
>和AEM表單實作的任何其他方面一樣，您的備份與復原策略必須在開發或中繼環境中開發及測試，之後才用於生產環境，以確保整個解決方案如預期般運作且不會遺失資料。

Adobe Experience Manager (AEM)是AEM表單不可或缺的一部分。 因此，您需要備份AEM以及與AEM表單同步備份，因為通訊管理解決方案和服務（例如表單管理員）都是以AEM表單的AEM部分中所儲存的資料為基礎。為了防止任何資料遺失，AEM表單特定資料必須以確保GDS和AEM （儲存庫）與資料庫參考相互關聯的方式進行備份。資料庫、GDS、AEM和內容儲存根目錄必須還原到與原始檔案具有相同DNS名稱的電腦。

## 備份型別 {#types-of-backups}

AEM Forms備份策略包含兩種型別的備份：

**系統映像：**&#x200B;完整的系統備份，可在硬碟或整部電腦停止運作時，用來還原電腦的內容。 系統影像備份只有在AEM表單的生產部署之前才有必要。 然後，內部公司政策會規定系統影像備份的頻率。

**AEM表單特定資料：**&#x200B;應用程式資料存在於資料庫、全域檔案儲存(GDS)和AEM存放庫中，且必須即時備份。 GDS是用來儲存處理程式中所使用之長期檔案的目錄。 這些檔案可能包含PDF、原則或表單範本。

>[!NOTE]
>
>如果已安裝Content Services （已棄用），請一併備份內容儲存根目錄。 請參閱[內容儲存根目錄（僅限Content Services）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only)。

資料庫可用來儲存表單成品、服務組態、處理狀態，以及GDS檔案的資料庫參考。 如果您在資料庫中啟用了檔案儲存，則GDS中的永久資料和檔案也會儲存在資料庫中。 您可以使用下列方法來備份及復原資料庫：

* **快照集備份**&#x200B;模式表示AEM表單系統處於無限期備份模式，或持續指定的分鐘數，之後不再啟用備份模式。 若要進入或離開快照備份模式，您可以使用下列其中一個選項。 在復原案例之後，不應啟用快照備份模式。

   * 使用「管理主控台」中的「備份設定值」頁面。 若要進入快照模式，請選取「在安全備份模式下操作」核取方塊。 取消選取核取方塊以結束快照模式。
   * 使用LCBackupMode指令碼（請參閱[備份資料庫、GDS和內容儲存根目錄](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)）。 若要結束快照集備份模式，請在指令碼引數中，將`continuousCoverage`引數設定為`false`或使用`leaveContinuousCoverage`選項。
   * 使用提供的備份/復原API。<!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **正在捲動備份**&#x200B;模式表示系統一律處於備份模式，前一工作階段一經釋出就會啟動新的備份模式工作階段。 沒有與滾動備份模式相關的逾時。 呼叫LCBackupMode指令碼或API以離開滾動備份模式時，就會開始新的滾動備份模式工作階段。 此模式在支援連續備份時非常有用，但仍允許從GDS目錄中清除舊的和不需要的檔案。 不支援透過「備份與復原」頁面來捲動備份模式。 復原情況後，仍會啟用捲動備份模式。 您可以使用包含`leaveContinuousCoverage`選項的LCBackupMode指令碼，離開連續備份模式（滾動備份模式）。

>[!NOTE]
>
>離開捲動備份模式會立即開始新的備份模式工作階段。 若要完全停用滾動備份模式，請使用指令碼中的`leaveContinuousCoverage`選項，這會覆寫現有的滾動備份工作階段。 當處於快照備份模式時，您可以像往常一樣離開備份模式。

為避免資料遺失，AEM表單特定資料必須以確保GDS和內容儲存根目錄檔案與資料庫參考相互關聯的方式進行備份。

>[!NOTE]
>
>當GDS儲存在檔案系統而非資料庫中時，請在GDS備份之前執行資料庫備份。

## 備份與復原的特殊考量 {#special-considerations-for-backup-and-recovery}

如果您因為下列變更而必須將AEM表單復原到其他環境，請使用下列准則：

* 變更AEM Forms伺服器的IP位址、主機名稱或連線埠
* 變更磁碟機代號或目錄路徑
* 變更為其他資料庫主機、連線埠或名稱

一般而言，這類復原情況是由裝載應用程式伺服器、資料庫伺服器或Forms伺服器的伺服器硬體故障所造成。 除了本節所述的AEM表單專屬設定外，如果AEM伺服器的主機名稱或IP位址變更，您也應該對AEM Forms表單部署的其他部分（例如負載平衡器和防火牆）進行必要的變更。

### 無法變更的專案 {#what-cannot-be-changed}

即使您可以變更資料庫伺服器和許多其他引數，當您從備份復原AEM表單時，也無法變更應用程式伺服器型別或資料庫型別。 例如，如果您正在復原AEM表單備份，則無法將應用程式伺服器從JBoss變更為WebLogic，或將資料庫從Oracle變更為DB2。 此外，復原的AEM表單必須使用相同的檔案系統路徑，例如字型目錄。

### 復原後重新啟動 {#restarting-after-a-recovery}

復原後，重新啟動Forms伺服器之前，請先執行下列動作：

1. 以維護模式啟動系統。
1. 請務必在維護模式下將表單管理員與AEM表單同步：

   1. 移至https://&lt;*伺服器*>：&lt;*連線埠*>/lc/fm並使用管理員/密碼認證登入。
   1. 按一下右上角的使用者名稱（此案例中為「超級管理員」）。
   1. 按一下&#x200B;**管理選項**。
   1. 按一下&#x200B;**開始**，從存放庫同步資產。

1. 在叢集環境中，主要節點(就AEM而言)應在次要節點之前。
1. 在驗證系統的正常作業之前，請確定沒有從內部或外部來源(例如Web、SOAP或EJB程式啟動器)啟動任何程式。

如果主要AEM表單資料庫已移動或變更，請檢閱與您的應用程式伺服器相關的安裝指南，以取得更新AEM表單資料來源IDP_DS和EDC_DS的資料庫連線資訊的相關資訊。

>[!NOTE]
> 
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式），可能會導致AEM開發環境不一致。

### 變更AEM表單主機名稱或IP位址 {#changing-the-aem-forms-hostname-or-ip-address}

在叢集中，如果您使用TCP快取而非UDP，則必須更新快取定位器組態。 請參閱與應用程式伺服器相關的設定指南中的「設定快取定位器（僅使用TCP快取）」。

### 變更AEM表單節點檔案系統路徑 {#changing-the-aem-forms-node-file-system-paths}

如果您變更獨立節點的檔案系統路徑，則必須在偏好設定、其他系統組態、自訂應用程式和已部署的AEM表單應用程式中更新適當的參照。 另一方面，對於叢集，所有節點都必須使用相同的檔案系統路徑設定。 設定Global Document Storage (GDS)根目錄，並確保它指向復原的GDS復本，該復本與復原的資料庫同步。 設定GDS路徑很重要，因為GDS可以包含要在應用程式伺服器重新啟動時持續存在的資料。

在叢集環境中，所有叢集節點在備份前和復原後的儲存庫檔案系統路徑設定應該相同。

變更檔案系統路徑後，請使用`[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline`資料夾中的`LCSetGDS`指令碼來設定GDS路徑。 如需詳細資訊，請參閱相同資料夾中的`ReadMe.txt`檔案。 如果無法使用舊的GDS目錄路徑，則必須使用`LCSetGDS`指令碼來設定GDS的新路徑，然後再啟動AEM表單。

>[!NOTE]
>
>只有在這種情況下，您才應該使用此指令碼來變更GDS位置。 若要在AEM表單執行時變更GDS位置，請使用管理主控台。 (請參閱[設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*。) *

設定GDS路徑後，請以維護模式啟動Forms伺服器，然後使用管理主控台更新新節點的剩餘檔案系統路徑。 確認所有必要的設定均已更新後，請重新啟動並測試AEM表單。
