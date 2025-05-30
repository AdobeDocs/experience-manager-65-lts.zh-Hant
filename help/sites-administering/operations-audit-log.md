---
title: AEM 6中的稽核記錄維護
description: 瞭解Adobe Experience Manager (AEM)中的稽核記錄維護。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
feature: Operations
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: dd0f90f7-5e92-49d3-a5b4-17d99ed927b9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---

# AEM 6中的稽核記錄維護{#audit-log-maintenance-in-aem}

符合稽核記錄資格的AEM事件會產生大量封存資料。 由於複製、資產上傳和其他系統活動，這些資料會隨著時間快速成長。

「稽核記錄維護」包含了數項功能，可讓您根據特定原則自動進行稽核記錄維護。

這是作為可設定的每週維護任務實作，並可透過操作儀表板監視控制檯存取。

如需詳細資訊，請參閱[操作儀表板檔案](/help/sites-administering/operations-dashboard.md)。

「稽核日誌永久刪除」選項有三種型別：

1. [頁面稽核記錄清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM稽核記錄清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [復寫稽核記錄檔期間](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每種都可透過在AEM Web Console中建立規則來設定。 設定之後，您可以移至&#x200B;**工具 — 作業 — 維護 — 每週維護期間**&#x200B;並執行&#x200B;**稽核記錄檔維護工作**&#x200B;來觸發這些工作。

## 設定頁面稽核記錄清除 {#configure-page-audit-log-purging}

請依照下列步驟設定「稽核記錄清除」：

1. 將您的瀏覽器指向`http://localhost:4502/system/console/configMgr/`，移至Web主控台管理員

1. 搜尋名為&#x200B;**頁面稽核記錄清除規則**&#x200B;的專案，然後按一下該專案。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 接下來，根據您的需求設定清除排程器。 可使用的選項包括：

   * **規則名稱：**&#x200B;稽核原則規則的名稱；
   * **內容路徑：**&#x200B;將套用規則之內容的路徑；
   * **最小年齡：**&#x200B;需要保留稽核記錄的時間（以天為單位）；
   * **稽核記錄型別：**&#x200B;應清除的稽核記錄型別。

   >[!NOTE]
   >
   >內容路徑僅適用於存放庫中`/var/audit/com.day.cq.wcm.core.page`節點的子系。

1. 儲存規則。
1. 您建立的規則必須顯示在「操作控制面板」中，才能執行。 若要這麼做，請從AEM歡迎畫面前往&#x200B;**工具 — 作業 — 維護**。

1. 按下&#x200B;**每週維護期間**&#x200B;卡片。

1. 您會發現&#x200B;**AuditLog維護任務**&#x200B;卡片下已經有維護任務。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以檢查下一次執行的日期、進行設定，或按播放按鈕手動執行。

在AEM 6.3中，如果排定的維護視窗在稽核記錄整個清除工作完成之前關閉，工作會自動停止。 當下一個維護視窗開啟時，它會繼續。

**使用AEM 6.5**，您可以按一下&#x200B;**停止**&#x200B;圖示來手動停止執行中的稽核記錄清除工作。 在下次執行時，工作將安全地繼續。

>[!NOTE]
>
>若要停止維護任務，表示要暫停其執行，而不會失去已進行中工作的追蹤。

## 設定DAM稽核記錄清除 {#configure-dam-audit-log-purging}

1. 瀏覽至&#x200B;*https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*&#x200B;的系統主控台
1. 搜尋&#x200B;**DAM稽核記錄清除**&#x200B;規則，然後按一下結果。
1. 在下一個視窗中，適當地設定您的規則。 選項包括：

   * **規則名稱：**&#x200B;稽核原則規則的名稱；
   * **內容路徑：**&#x200B;將套用規則的內容路徑
   * **最小年齡：**&#x200B;需要保留稽核記錄的時間（以天為單位）
   * **稽核記錄DAM事件型別：**&#x200B;應清除的DAM稽核事件型別。

1. 按一下&#x200B;**儲存**&#x200B;以儲存您的設定

## 設定復寫稽核記錄清除  {#configure-replication-audit-log-purging}

1. 瀏覽至&#x200B;*https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*&#x200B;的系統主控台
1. 搜尋&#x200B;**復寫稽核記錄清除排程器**&#x200B;並按一下結果
1. 在下一個視窗中，適當地設定您的規則。 選項包括：

   * **規則名稱：**&#x200B;稽核原則規則的名稱
   * **內容路徑：**&#x200B;將套用規則的內容路徑
   * **最小年齡：**&#x200B;需要保留稽核記錄的時間（以天為單位）
   * **稽核記錄復寫事件型別：**&#x200B;應清除的復寫稽核事件型別

1. 按一下[儲存]儲存您的設定。**&#x200B;**
