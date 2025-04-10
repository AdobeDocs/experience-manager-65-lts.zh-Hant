---
title: 自訂錯誤處理常式顯示的頁面
description: Adobe Experience Manager隨附處理HTTP錯誤的標準錯誤處理常式。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4f98853d-306f-4d11-a3d8-83122b372b2d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# 自訂錯誤處理常式顯示的頁面{#customizing-pages-shown-by-the-error-handler}

Adobe Experience Manager (AEM)隨附處理HTTP錯誤的標準錯誤處理常式，例如，顯示：

![chlimage_1-67](assets/chlimage_1-67a.png)

系統提供的指令碼存在（在`/libs/sling/servlet/errorhandler`下）以回應錯誤碼，依預設，標準CQ執行個體可使用下列專案：

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM是以Apache Sling為基礎。 因此，請參閱[錯誤處理](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)以取得Sling錯誤處理的詳細資訊。

>[!NOTE]
>
>在作者執行個體上，預設會啟用[CQ WCM偵錯篩選器](/help/sites-deploying/osgi-configuration-settings.md)。 這會一律產生回應代碼200。 預設錯誤處理常式會透過將完整棧疊追蹤寫入回應來回應。
>
>在發佈執行個體上，CQ WCM偵錯篩選器是&#x200B;*一律*&#x200B;停用（即使設定為已啟用）。

## 如何自訂錯誤處理常式顯示的頁面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以開發自己的指令碼，以在發生錯誤時自訂錯誤處理常式顯示的頁面。 您的自訂頁面是在`/apps`下建立並覆蓋預設頁面（在`/libs`下）。

>[!NOTE]
>
>如需詳細資訊，請參閱[使用覆蓋](/help/sites-developing/overlays.md)。

1. 在存放庫中，複製預設指令碼：

   * 從 `/libs/sling/servlet/errorhandler/`
   * 至`/apps/sling/servlet/errorhandler/`

   由於預設不存在目的地路徑，因此您必須在第一次執行此動作時建立該路徑。

1. 導覽至`/apps/sling/servlet/errorhandler`並執行下列任一項作業：

   * 編輯適當的現有指令碼，以便提供所需的資訊。
   * 建立和編輯所需程式碼的新指令碼。

1. 儲存變更並測試。

>[!CAUTION]
>
>404.jsp和403.jsp處理常式已設計為符合CQ5驗證；特別是，在發生這些錯誤時允許系統登入。
>
>因此，取代這兩個處理常式時應格外小心。

### 自訂HTTP 500錯誤的回應 {#customizing-the-response-to-http-errors}

HTTP 500錯誤是由伺服器端例外狀況所造成。

* **[500內部伺服器錯誤](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
伺服器發生非預期的情況，導致它無法完成要求。

當請求處理導致例外狀況時，Apache Sling架構(AEM的建置基礎)：

* 記錄例外狀況
* 傳回：

   * HTTP回應代碼500
   * 例外狀況棧疊追蹤

  在回應內文中。

透過[自訂錯誤處理常式所顯示的頁面](#how-to-customize-pages-shown-by-the-error-handler)，即可建立`500.jsp`指令碼。 但是，只有在`HttpServletResponse.sendError(500)`明確執行時才使用它；也就是說，從例外狀況收集器執行。

否則，回應程式碼會設為500，但不會執行`500.jsp`指令碼。

若要處理500個錯誤，錯誤處理常式指令碼的檔案名稱必須與exception類別（或超級類別）相同。 若要處理所有此類例外，您可以建立指令碼`/apps/sling/servlet/errorhandler/Throwable.js`p或`/apps/sling/servlet/errorhandler/Exception.jsp`。

>[!CAUTION]
>
>在作者執行個體上，預設會啟用[CQ WCM偵錯篩選器](/help/sites-deploying/osgi-configuration-settings.md)。 這會一律產生回應代碼200。 預設錯誤處理常式會透過將完整棧疊追蹤寫入回應來回應。
>
>自訂錯誤處理常式需要程式碼為500的回應，因此必須停用[CQ WCM偵錯篩選器](/help/sites-deploying/osgi-configuration-settings.md)。 這可確保傳回回應代碼500，這隨之會觸發正確的Sling錯誤處理常式。
>
>在發佈執行個體上，CQ WCM偵錯篩選器是&#x200B;*一律*&#x200B;停用（即使設定為已啟用）。
