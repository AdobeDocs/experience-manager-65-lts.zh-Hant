---
title: 升級後檢查及疑難排解
description: 瞭解如何疑難排解升級後可能出現的問題。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 09b297721b08ef428f1ac8a26fec38d5a8bd34fd
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# 升級後檢查及疑難排解{#post-upgrade-checks-and-troubleshooting}

## 升級後檢查 {#post-upgrade-checks}

在[就地升級](/help/sites-deploying/in-place-upgrade.md)之後，應執行下列活動以完成升級。 我們假設AEM已使用AEM 6.5 LTS jar啟動，且已部署升級後的程式碼基底。

* [驗證升級成功的記錄檔](#verify-logs-for-upgrade-success)

* [驗證OSGi組合](#verify-osgi-bundles)

* [驗證Oak版本](#verify-oak-version)

* [頁面初始驗證](#initial-validation-of-pages)

* [驗證排程的維護設定](#verify-scheduled-maintenance-configurations)

* [啟用復寫代理](#enable-replication-agents)

* [啟用自訂排程工作](#enable-custom-scheduled-jobs)

* [執行測試計畫](#execute-test-plan)


### 驗證升級成功的記錄檔 {#verify-logs-for-upgrade-success}

**upgrade.log**

在過去，檢查執行個體的升級後狀態需要仔細檢查各種記錄檔、存放庫部分和啟動板。 產生升級後報告，有助於在上線前偵測有瑕疵的升級。

此功能的主要目的，是為了減少需要手動解譯，或是跨越多個端點的複雜剖析邏輯，以確認升級成功。 此解決方案旨在為外部自動化系統提供明確資訊，以在更新成功或識別為失敗時做出反應。

更具體來說，這可確保：

* 升級架構偵測到的升級故障會集中到單一升級報告中。
* 升級報告包含有關必要手動介入的指標。

為了因應這種情況，已在`upgrade.log`檔案中產生記錄的方式上做了變更。

**error.log**

在使用目標版本jar啟動AEM期間和之後，應該仔細檢閱error.log。 應檢閱任何警告或錯誤。 一般來說，最好在記錄的開頭尋找問題。 稍後在記錄中發生的錯誤，實際上可能是檔案中較早呼叫的根原因的副作用。 如果發生重複錯誤和警告，請參閱下面的[分析升級問題](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade)。

### 驗證OSGi組合 {#verify-osgi-bundles}

導覽至OSGi主控台`/system/console/bundles`，並檢視是否有任何套件組合未啟動。 如果有任何套件組合處於安裝狀態，請參閱`error.log`以判斷根問題。

### 驗證Oak版本 {#verify-oak-version}

升級後，您應該會看到Oak版本已更新為&#x200B;**1.68.1-B002**。 若要驗證Oak版本，請導覽至OSGi主控台，並檢視與Oak套件組合相關聯的版本：Oak Core、Oak Commons、Oak Segment Tar。

### 頁面初始驗證 {#initial-validation-of-pages}

對AEM中的數個頁面執行初始驗證。 如果升級作者環境，請開啟開始頁面和歡迎頁面( `/aem/start.html`， `/libs/cq/core/content/welcome.html`)。 在製作和發佈環境中，請開啟一些應用程式頁面，並進行冒煙測試，以正確轉譯。 如果發生任何問題，請參閱`error.log`以進行疑難排解。

### 驗證排程的維護設定 {#verify-scheduled-maintenance-configurations}

#### 啟用資料存放區記憶體回收 {#enable-data-store-garbage-collection}

如果使用檔案資料存放區，請確定資料存放區記憶體回收工作已啟用，並已新增到每週維護清單中。 說明概述在[修訂清理](/help/sites-administering/data-store-garbage-collection.md)下。

>[!NOTE]
>
>S3自訂資料存放區安裝或使用共用資料存放區時，不建議採用此做法。

#### 啟用線上修訂清除 {#enable-online-revision-cleanup}

如果使用MongoMK或新的TarMK區段格式，請確保已啟用「修訂清除」任務並將其新增到「每日維護」清單中。 說明概述在[修訂清理](/help/sites-deploying/revision-cleanup.md)下。

### 啟用復寫代理 {#enable-replication-agents}

發佈環境完全升級和驗證後，在製作環境中啟用復寫代理程式。 驗證代理程式是否能夠連線至個別的發佈執行個體。 如需事件順序的詳細資訊，請參閱[升級程式](/help/sites-deploying/upgrade-procedure.md)。

### 啟用自訂排程工作 {#enable-custom-scheduled-jobs}

此時可以啟用任何已排程的工作，做為程式碼庫的一部分。

### 執行測試計畫 {#execute-test-plan}

執行[升級&#x200B;**測試程式**&#x200B;區段](/help/sites-deploying/upgrading-code-and-customizations.md#testing-procedure-testing-procedure)下的程式碼和自訂專案中所定義的詳細測試計畫。

## 分析升級相關問題 {#analyzing-issues-with-the-upgrade}

本節包含升級到AEM 6.5 LTS的程式中可能會遇到的一些問題案例。

### 套件和套件組合無法更新  {#packages-and-bundles-fail-to-update}

如果升級期間無法安裝套件，則其中包含的套件組合也不會更新。 這類問題是由資料存放區設定錯誤所造成。 它們也會在error.log中顯示為&#x200B;**ERROR**&#x200B;和&#x200B;**WARN**&#x200B;訊息。 由於在大部分的情況下，預設登入可能會無法運作，因此您可以直接使用CRXDE來檢查並尋找設定問題。

### 升級未執行 {#the-upgrade-did-not-run}

在開始準備步驟之前，請確定您先使用`java -jar aem-quickstart.jar`命令執行&#x200B;**來源**&#x200B;執行個體。 這是確定已正確產生quickstart.properties檔案所必需的。 如果遺失，升級將無法運作。 或者，您可以透過檢視來源執行個體的安裝資料夾中的`crx-quickstart/conf`來檢查檔案是否存在。 此外，啟動AEM以開始升級時，必須使用`java -jar <aem-quickstart-6.5-LTS.jar>`命令執行。 從啟動指令碼啟動時，在升級模式下不會啟動AEM。

### 有些AEM套件組合沒有切換至作用中狀態 {#some-aem-bundles-are-not-switching-to-the-active-state}

如果有未啟動的組合，請檢查是否有任何未滿足的相依性。

如果出現此問題，但此問題的基礎是套件安裝失敗，導致套件組合無法升級，則會將其視為與新版本不相容。 如需如何疑難排解此問題的詳細資訊，請參閱上面的&#x200B;**無法更新的套件和套件組合**。

此外也建議您將全新AEM 6.5 LTS執行個體的套件組合清單與升級後的套件組合清單進行比較，以偵測未升級的套件組合。 這將提供更密切的`error.log`搜尋範圍。

### 自訂組合未切換至作用中狀態 {#custom-bundles-not-switching-to-the-active-state}

如果您的自訂套件組合未切換至使用中狀態，很可能是因為有程式碼未匯入已變更的API。 這通常會導致不滿意的相依性。

最好檢查造成問題的變更是否必要，如果不是，則回覆。 此外，在嚴格的語意版本設定後，檢查套件匯出的版本增加是否超過必要。

### 正在分析error.log和upgrade.log {#analyzing-the-error.log-and-upgrade.log}

在大多數情況下，需要查閱記錄檔中的錯誤，以找出問題的原因。 不過，在升級時，也需要監視相依性問題，因為舊的套件組合可能無法正確升級。

最好的方法是移除error.log，移除所有預期與您面臨的問題無關的訊息。 您可以透過grep等工具使用以下工具完成此操作：

```shell
grep -v UnrelatedErrorString
```

有些錯誤訊息可能不會立即說明錯誤。 在此情況下，檢視發生錯誤的內容也有助於瞭解錯誤是在何處建立的。 您可以使用以下方式分隔錯誤：

* `grep -B`以在錯誤之前新增行；

或

* `grep -A`在之後新增行。

在少數情況下也會發現錯誤「警告」訊息，因為有些有效案例會導致此狀態，而應用程式並不總是能夠判斷這是否為實際錯誤。 也請務必參閱這些訊息。

### 連絡 Adobe 支援人員 {#contacting-adobe-support}

如果您詳閱過本頁面的建議，但仍遇到問題，請聯絡Adobe支援。 若要向處理您案例的支援工程師提供儘可能多的資訊，請務必加入升級中的`error.log`和`upgrade.log`檔案。
