---
title: 健康狀態監視概觀
description: 本檔案提供健康狀態監視器的概觀，以及存取方式的相關詳細資訊。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f187d4e4-7fe6-4f58-a2df-9d415dcff4aa
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 健康狀態監視概觀 {#overview-of-health-monitor}

健康狀態監視提供有關AEM表單系統的重要資訊，例如伺服器資訊、記憶體使用量和處理器使用量。 也可以使用Work Manager統計資料，例如佇列中的工作專案或工作數目及其狀態。 您可以使用「健康狀態監視器」執行下列工作：

* 驗證您的系統是否正確執行
* 檢視資訊以協助診斷發生的系統問題
* 對顯示問題的工作專案或工作執行作業
* 從「工作管理員」資料庫中永久刪除過時記錄

管理主控台中的「健康情況監視」頁面有三個頁簽：

* 「系統」標籤會顯示資源監檢視表和有關Forms伺服器（或叢集環境中的節點）的資訊。 （請參閱[檢視系統資訊](/help/forms/using/admin-help/view-system-information.md#view-system-information)。）
* 「工作管理員」標籤會顯示與「工作管理員」相關的資料，例如「工作管理員」佇列中的工作專案數。 您可以使用各種條件來篩選資訊，或使用作業工具來管理個別的工作專案。 （請參閱[檢視與工作管理員相關的統計資料](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)。）
* 您可以在「工作永久刪除排程器」頁簽中永久刪除「工作管理員」資料庫中的過時記錄。 （請參閱[從工作管理員資料庫](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)中清除記錄。）

健康情況監視網頁會填入透過Gemfire API收集的統計資料。 此API會自動探索叢集中的所有節點。 它也能解決從後台Proxy伺服器或負載平衡器收集統計資料時發生的安全性問題。 Java選項可用於微調健康狀態監視器，減少對AEM表單環境效能的影響。 （請參閱[微調健康狀態監視器效能](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)。）

**存取狀況監視器**

1. 在管理控制檯中，按一下頁面右上角的「健全狀態監視器」 。
