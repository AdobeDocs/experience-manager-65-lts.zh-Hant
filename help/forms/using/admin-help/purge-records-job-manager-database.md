---
title: 從「工作管理員」資料庫中清除記錄
description: 大型程式資料可能會導致AEM表單效能降低。 當不再需要記錄時，清除處理資料是很好的做法。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a5e6b09a-c4c7-41c0-8221-d563cb74b3b7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# 從「工作管理員」資料庫中清除記錄 {#purge-records-from-the-job-manager-database}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

叫用長期程式時產生的程式資料可能會變得太大，導致AEM表單效能降低，並佔用不必要的磁碟空間。 當不再需要記錄時，清除處理資料是很好的做法。

您可以使用管理主控台執行一次性永久刪除過時記錄，或排定定期的自動永久刪除。 在[清除程式資料](/help/forms/using/admin-help/purging-process-data.md#purging-process-data)中討論了其他清除過時記錄的方法。

**存取「工作清除排程器」頁面**

1. 在「管理主控台」中，按一下頁面右上角的「健全狀態監視器」 。
1. 按一下「工作清除排程器」頁簽。

有關目前排定清除的資訊會顯示在「工作清除排程器資訊」方塊中。

>[!NOTE]
>
>按一下「停止排程器」可停止未來排定的任何清除，但不會停止正在進行的清除工作。

**排程一次性清除**

1. 只選取一次。
1. 在「永久刪除完成的記錄篩選」區域中，指定將記錄視為過時並準備永久刪除的天數或周數。

   >[!NOTE]
   >
   >系統不會永久刪除與尚未完成的處理程式相關的記錄，即使這些記錄比指定的期限還舊。

1. 指定何時進行清除。 選取使用目前的日期和時間核取方塊，或清除核取方塊並按一下日曆和時鐘圖示，以指定執行清除的日期和時間。

   >[!NOTE]
   >
   >如果您指定的開始日期與時間是過去的時間，則按一下「開始排程器」時，會立即進行清除。

1. 按一下「啟動排程器」。 先前排程的排程器設定會取代為新設定。

**設定自動清除排程**

1. 選取遞回間隔，並指定清除間隔的天數或周數。
1. 在「永久刪除完成的記錄篩選」區域中，指定將記錄視為過時並準備永久刪除的天數或周數。 您不能將值設定為`0`。

   >[!NOTE]
   >
   >系統不會永久刪除與尚未完成的處理程式相關的記錄，即使這些記錄比指定的期限還舊。

1. 指定清除開始的時間。 選取使用目前的日期和時間核取方塊，或清除核取方塊並按一下日曆和時鐘圖示，以指定執行清除的日期和時間。

   >[!NOTE]
   >
   >如果您指定的開始日期和時間是過去的時間，AEM Forms會根據您指定的日期計算邏輯性的下一個開始日期。 例如，如果您將工作清除排程為從4月7日開始每週執行，現在是4月9日，則第一次清除會在4月14日執行。

1. 按一下「啟動排程器」。 先前排程的排程器設定會取代為新設定。
