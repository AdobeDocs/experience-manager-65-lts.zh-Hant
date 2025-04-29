---
title: 疑難排解復寫
description: 本文提供如何疑難排解復寫問題的相關資訊。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 015def31-c7de-42b3-8218-1284afcb6921
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 疑難排解復寫{#troubleshooting-replication}

此頁面提供如何疑難排解復寫問題的資訊。

## 問題 {#problem}

復寫（非反向復寫）由於某些原因而失敗。

## 解決方法 {#resolution}

復寫失敗的原因有很多。 本文會說明分析這些問題時可能會採取的方法。

**按一下[啟動]按鈕時，是否會觸發復寫？ 如果NOT，則執行下列動作：**

1. 前往/crx/de/index.jsp並以管理員身分登入。
1. 檢視節點/bin/replicate或/bin/replicate.json是否存在。 如果節點存在，則刪除它並儲存。

**復寫是否在復寫代理程式佇列中排入佇列？**

請前往/etc/replication/agents.author.html檢查此專案，然後按一下復寫代理程式以進行檢查。

**如果一個代理程式佇列或幾個代理程式佇列卡住：**

1. 佇列是否顯示&#x200B;**已封鎖**&#x200B;狀態？ 如果存在，則發佈執行個體是否未執行或無回應？ 檢查發佈執行個體看看它有什麼問題。 也就是說，檢查記錄檔，並檢視是否發生OutOfMemory錯誤或某些其他問題。 如果速度很慢，則進行對話串傾印並加以分析。
1. 佇列狀態是否顯示&#x200B;**佇列為作用中 — # pending**？ 基本上，復寫工作可能會卡在等待發佈執行個體或Dispatcher回應的通訊端讀取中。 這可能表示發佈執行個體或Dispatcher處於高負載或卡在鎖定中。 在此情況下，從作者進行對話串傾印並發佈。

   * 在執行緒傾印分析器中開啟來自作者的執行緒傾印，檢查它是否顯示復寫代理程式的sling事件工作卡在socketRead中。
   * 在執行緒傾印分析器中從發佈開啟執行緒傾印，分析可能導致發佈執行個體未回應的原因。 您應該會看到名稱中包含POST /bin/receive的執行緒，這是從作者接收復寫的執行緒。

**如果所有代理程式佇列都卡住**

1. 由於存放庫損毀或某些其他問題，可能無法在/var/replication/data下序列化特定內容片段。 如需相關錯誤，請檢視logs/error.log 。 若要清除錯誤的復寫專案，請執行下列動作：

   1. 前往https://&lt;host>：&lt;port>/crx/de並以管理員使用者身分登入。
   1. 按一下頂端功能表中的「工具」。
   1. 按一下放大鏡按鈕。
   1. 選取「XPath」作為「型別」。
   1. 在「查詢」方塊中，輸入此查詢/jcr：root/var/eventing/jobs//element(&#42;，slingevent：Job) order by @slingevent：created
   1. 按一下「搜尋」。
   1. 在結果中，排名最前的專案是最新的Sling事件工作。 按一下每個復寫，然後尋找符合佇列頂端所顯示內容的停滯復寫。

**建立replication.log**

有時候，在DEBUG層級將所有的復寫記錄檔設定為新增到個別的記錄檔中會很有幫助。 若要這麼做：

1. 前往https://host:port/system/console/configMgr並以管理員身分登入。
1. 尋找Apache Sling記錄記錄器設定，並按一下工廠設定右側的&#x200B;**+**&#x200B;按鈕以建立執行個體。 這會建立新的記錄日誌程式。
1. 設定設定如下：

   * 記錄層級： DEBUG
   * 記錄檔：logs/replication.log
   * 記錄器： com.day.cq.replication

1. 如果您懷疑問題與任何方式的Sling事件/工作有關，您也可以在categories：org.apache.sling.event底下新增此Java™套件

## 暫停復寫代理程式佇列  {#pausing-replication-agent-queue}

有時候，暫停復寫佇列以減輕作者系統的負載，而不停用它可能是合適的。 目前，這只能透過暫時設定無效連線埠的駭客攻擊來完成。 從5.4版開始，復寫代理程式佇列中可能會顯示暫停按鈕，但有一些限制

1. 狀態不會持續存在，這表示如果您重新啟動伺服器或復寫套件組合回收，它會回復到執行狀態。
1. 暫停會閒置較短的時間（沒有其他執行緒使用復寫的活動後出現1小時），而不會再閒置較長時間。 因為Sling中有避免閒置執行緒的功能。 基本上會檢查工作佇列執行緒是否閒置了較長時間，如果是，它會啟動清除週期。 由於清除循環，它會停止執行緒，因此會遺失暫停的設定。 由於作業持續存在，因此會起始新的執行緒來處理沒有暫停組態詳細資訊的佇列。 因為此佇列會變成執行中狀態。

## 使用者啟動時不會復寫頁面許可權 {#page-permissions-are-not-replicated-on-user-activation}

不會復寫頁面許可權，因為這些許可權儲存在授予存取權的節點下，而不是儲存在使用者中。

一般而言，頁面許可權不應從作者復寫至發佈，預設情況下也不應如此。 這是因為在這兩個環境中，存取許可權應該不同。 因此，Adobe建議您在publish上設定ACL （與編寫分開）。

## 將名稱空間資訊從作者復寫到發佈時封鎖復寫佇列 {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

嘗試將名稱空間資訊從製作執行個體復寫到發佈執行個體時，有時復寫佇列會被封鎖。 發生此狀況是因為復寫使用者沒有`jcr:namespaceManagement`許可權。 若要避免此問題，請確定：

* 復寫使用者（在[Transport](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) tab>User下設定）也存在於發佈執行個體上。
* 使用者在安裝內容的路徑具有讀取和寫入許可權。
* 使用者在存放庫層級具有`jcr:namespaceManagement`許可權。 您可以授與許可權，如下所示：

1. 以管理員身分登入CRX/DE ( `https://localhost:4502/crx/de/index.jsp`)。
1. 按一下「**存取控制**」標籤。
1. 選取&#x200B;**存放庫**。
1. 按一下&#x200B;**新增專案** （加號圖示）。
1. 輸入使用者的名稱。
1. 從許可權清單中選取`jcr:namespaceManagement`。
1. 按一下&#x200B;**「確定」**。
