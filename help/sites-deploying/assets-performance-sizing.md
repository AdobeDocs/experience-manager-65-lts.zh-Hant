---
title: Assets效能指南
description: 瞭解如何為新的數位資產管理(DAM)設定決定最佳硬體大小，以及如何疑難排解效能問題
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
exl-id: 49225f9f-d09e-4ab6-9e29-b47ba41e8889
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# Assets效能指南{#assets-performance-guide}

數位資產管理(DAM)通常用於效能重要的情況。 不過，典型的DAM設定包含數個可能會影響效能的軟硬體元件。 本檔案提供下列內容：

* 系統管理員如何為新的數位資產管理設定決定最佳硬體大小的資訊
* 軟體開發人員適用的資訊，旨在疑難排解DAM例項中的效能問題

## 效能問題 {#performance-issues}

數位資產管理中的效能不佳，可能會從三個方面影響使用者體驗：互動式效能、資產處理和下載速度。 若要改善效能，請務必正確測量觀察到的效能，並建立目標測量結果。

**1. 互動式搜尋和瀏覽**&#x200B;使用者正在搜尋資產或瀏覽DAM Finder，並抱怨回應時間緩慢或搜尋結果未立即顯示。 這是互動式效能問題。

互動式效能是以頁面回應時間來衡量。 這是從收到HTTP請求到關閉HTTP回應所花的時間，這可以從請求記錄檔中判斷。 一般目標效能是低於2秒的頁面回應時間。

**2. 資產處理**&#x200B;資產處理問題是使用者上傳資產時，需要幾分鐘才能將資產輕鬆轉換並擷取到Adobe Experience Manager (AEM) DAM。

資產處理效能是以平均工作流程處理完成時間來衡量。 這是叫用「資產更新」工作流程處理至完成所花的時間，時間可從工作流程報表使用者介面決定。 一般目標效能取決於處理的資產大小和型別以及轉譯數量。 目標效能的範例可能如下：

* 小於1280x1280畫素（使用標準轉譯）的影像需在10秒以下
* 對於使用標準轉譯小於100 MB的影像，時間少於1分鐘
* HD視訊剪輯不到五分鐘，長度不到一分鐘

**3。 下載速度**&#x200B;從AEM DAM下載時發生輸送量問題需花很長時間，且在瀏覽DAM Admin或DAM Finder時不會立即顯示縮圖。

傳輸量效能是以每秒千位元的速度來測量。 一般目標效能為300 Kbps，可同時下載100次。

**4。 影響資產處理效能的因素**

為了能夠估計處理資產所需的硬體，應該考慮以下方面：

* 以畫素數表示的影像解析度
* 指派給AEM流程的棧積

影像中包含的畫素數會決定處理時間，畫素越多代表處理時間越長。
影像型別、壓縮率或影像儲存所在之檔案的相關大小不會顯著影響整體效能。

棧積已被識別為最重要的限制因素。 每當資產超過可用的可用記憶體時，處理效能就會迅速下降。

DAM程式非常適合大量同時執行。 以批次及多核心處理器上傳資產，可加快每個資產的絕對逗留時間。

**5。 正在預估執行資產處理的硬體需求**

廣泛的數位資產處理需要最佳化的硬體資源，其中最相關的因素包括影像大小和已處理影像的尖峰輸送量。

配置至少16 GB的棧積，並設定[!UICONTROL DAM更新資產]工作流程以使用[Camera Raw封裝](/help/assets/camera-raw.md)來擷取原始影像。

## 瞭解系統 {#understanding-the-system}

典型的DAM設定包含透過負載平衡器存取DAM的一般使用者。 DAM執行個體可能是叢集設定的一部分，其中每個DAM執行個體都會在實體機器或虛擬機器器上的Java™虛擬機器器程式中執行。 如果有單一電腦設定，DAM儲存空間會由RAID磁碟提供；如果有叢集設定，則會由受管理的網路附加儲存空間提供。

下列圖例說明部分解決方案可能存在的效能陷阱區域（如適用）。

**與使用者的網路連線**&#x200B;網路連線速度緩慢可能會造成輸送量問題，在某些罕見情況下還會造成延遲問題。 有時使用者與ISP的連線速度很慢，尤其是在內部網路中。 這是不正確網路拓撲的標誌。

**暫存檔案系統**&#x200B;緩慢的本機檔案系統可能會導致互動式效能問題，尤其是在搜尋時，因為搜尋索引儲存在本機磁碟上。 如果使用命令列程式，也可能會導致資產處理問題。

**AEM DAM Finder**&#x200B;搜尋中經常遇到的互動式效能問題，是由相同執行個體上同時使用許多使用者或其他使用CPU的處理序所導致CPU使用率高所造成。 從虛擬機器器移至專用機器，並確定機器上未執行其他服務，有助於改善效能。 如果高CPU負載是由於資產處理和許多同時使用者所造成，Adobe建議新增其他叢集節點。

**AEM DAM工作流程**&#x200B;資產擷取期間長時間執行的工作流程會導致資產處理效能問題。 根據正在處理的資產型別，這可能表示CPU過度使用。 Adobe建議您減少系統上執行的其他處理作業數目，並藉由新增叢集節點來增加可用的CPU數目。

**NAS連線**&#x200B;與NAS的網路連線不良會導致互動式效能問題，因為在資產處理期間存取新節點的速度會因網路延遲而減慢。 此外，緩慢的網路輸送量也會對輸送量造成不良影響，也會因為載入和儲存轉譯的速度變慢而影響資產處理效能。

NAS中延遲和傳輸量不良的原因在於網路拓撲或其他服務的NAS過度使用。

**網路附加儲存裝置**&#x200B;過度使用的網路附加儲存系統可能會造成一系列問題：

* 磁碟空間不足是經常遇到的問題，可透過適當調整DAM專案的大小來避免。
* 高磁碟延遲會導致CRX存取速度緩慢，並可能導致互動式效能問題。
* 磁碟輸送量低可能會導致CQ5 DAM的效能降低。

## 效能測試 {#testing-for-performance}

對於每個DAM專案，請務必建立效能測試制度，以便快速找出並解決瓶頸。 若要這麼做，請考慮下列查核點：

1. 使用JMeter的端對端效能測試 — 模擬範例搜尋和瀏覽工作階段，以偵測互動式效能問題。
1. 使用JMeter進行輸送量和延時測試 — 在使用者端電腦上執行可確保沒有拓撲相關問題。
1. 標準化的資產處理測試 — 擷取一些資產範例並測量時間。 這應該包括外部工作流程整合。
1. 監視每個叢集節點的CPU、磁碟和記憶體使用率。
1. CRX讀取/寫入效能診斷，用於識別非處理相關問題。
1. 監視從DAM叢集到NAS的網路延遲和輸送量。
1. 如果可能的話，直接在NAS上測試、讀取和寫入效能以及磁碟延遲。

## 調整瓶頸 {#tweaking-bottlenecks}

目前為止，專案中已使用下列效能調整：

* 選擇性產生轉譯：僅透過將條件新增至資產處理工作流程，產生您所需的轉譯，因此僅針對選取的資產產生成本較高的轉譯。
* 執行個體之間共用資料存放區：當磁碟空間不足時，這可能會大幅減少所需的磁碟空間，但代價是需要付出更高的設定工作量，並失去資料存放區的自動清理。
