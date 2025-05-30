---
title: 建立已關閉的使用者群組
description: 瞭解如何建立「已關閉的使用者群組」。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: c44ecbb4-a883-4468-bddc-55964485529b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# 建立已關閉的使用者群組{#creating-a-closed-user-group}

封閉式使用者群組(CUG)可用來限制對已發佈網際網路網站中特定頁面的存取。 這類頁面需要指派的成員登入並提供安全性認證。

若要在網站中設定這類區域，請：

* [建立實際的已關閉使用者群組並指派成員](#creating-the-user-group-to-be-used)。

* [將此群組套用至必要的頁面](#applying-your-closed-user-group-to-content-pages)，然後選取（或建立）登入頁面以供CUG的成員使用；也會在套用CUG至內容頁面時指定。

* [在受保護區域](#linking-to-the-cug-pages)內，建立至少一個頁面的連結（某種形式），否則不會顯示。

* [設定Dispatcher](#configure-dispatcher-for-cugs) （若使用中）。

>[!CAUTION]
>
>建立封閉式使用者群組(CUG)時，一律應考量效能。
>
>雖然CUG中的使用者和群組數量並沒有限制，但單一頁面上大量的CUG可能會降低轉譯效能。
>
>進行效能測試時，應一律考慮CUG的影響。

## 建立要使用的使用者群組 {#creating-the-user-group-to-be-used}

若要建立已關閉的使用者群組：

1. 從AEM主畫面移至&#x200B;**工具 — 安全性**。

   >[!NOTE]
   >
   >如需建立和設定使用者與群組的完整資訊，請參閱[管理使用者與群組](/help/sites-administering/security.md#managing-users-and-groups)。

1. 從下一個畫面中選取&#x200B;**群組**&#x200B;卡片。

   ![熒幕擷圖_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按右上角的&#x200B;**建立**&#x200B;按鈕以建立群組。
1. 命名您的新群組；例如，`cug_access`。

   ![熒幕擷圖_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 移至&#x200B;**成員**&#x200B;標籤，並將必要的使用者指派給此群組。

   ![熒幕擷圖_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 啟用您已指派給您的CUG的任何使用者；在此情況下，則是`cug_access`的所有成員。
1. 啟動已關閉的使用者群組，使其可在發佈環境中使用；在此範例中，`cug_access`。

## 將封閉使用者群組套用至內容頁面 {#applying-your-closed-user-group-to-content-pages}

若要將CUG套用至一或多個頁面：

1. 導覽至您要指派給CUG之受限制區段的根頁面。
1. 按一下頁面的縮圖，然後在頂端工具列選取&#x200B;**屬性**&#x200B;以選取頁面。

   ![熒幕擷圖_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在下列視窗中，開啟&#x200B;**進階**&#x200B;標籤。

1. 向下捲動至&#x200B;**驗證需求**&#x200B;區段。

   1. 啟動&#x200B;**啟用**&#x200B;核取方塊。

   1. 新增路徑至您的&#x200B;**登入頁面**。
這是選用專案，如果保留為空白，系統會使用標準登入頁面。

   ![CUG已新增](assets/cug-authentication-requirement.png)

1. 接著，移至&#x200B;**許可權**&#x200B;標籤，並選取&#x200B;**編輯已關閉的使用者群組**。

   ![熒幕擷圖_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >許可權索引標籤中的CUG無法從Blueprint轉出至即時副本。 設定即時副本時，請對此進行規劃。
   >
   >如需詳細資訊，請參閱[AEM中的已關閉使用者群組 — Livecopy](closed-user-groups.md#aem-livecopy)。

1. **編輯已關閉的使用者群組**&#x200B;對話方塊開啟。 您可以在這裡搜尋並選取您的CUG，然後使用&#x200B;**儲存**&#x200B;確認群組選擇。

   群組將新增至清單；例如，群組&#x200B;**cug_access**。

   ![CUG已新增](assets/cug-added.png)

1. 透過&#x200B;**儲存並關閉**&#x200B;確認變更。

>[!NOTE]
>
>請參閱[Identity Management](/help/sites-administering/identity-management.md)，以取得有關發佈環境中設定檔及提供登入和登出表單的資訊。

## 連結至CUG頁面 {#linking-to-the-cug-pages}

由於匿名使用者看不到任何CUG頁面連結的目標，因此連結檢查器會移除這類連結。

若要避免此問題，建議您建立指向CUG區域中頁面的非受保護重新導向頁面。 然後轉譯導覽專案，而不會導致連結檢查器發生任何問題。 只有在實際存取重新導向頁面時，才會在CUG區域將使用者重新導向 — 在成功提供其登入憑證後。

## 為CUG設定Dispatcher {#configure-dispatcher-for-cugs}

如果您使用Dispatcher，則需要使用下列屬性定義Dispatcher陣列：

* [virtualhosts](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant#identifying-virtual-hosts-virtualhosts)：符合CUG套用之頁面的路徑。
* \sessionmanagement：請參閱下文。
* [快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant#configuring-the-dispatcher-cache-cache)：專屬於CUG套用之檔案的快取目錄。

### 為CUG設定Dispatcher工作階段管理 {#configuring-dispatcher-session-management-for-cugs}

在dispatcher.any檔案[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant#enabling-secure-sessions-sessionmanagement)中設定CUG的工作階段管理。 要求CUG頁面的存取權時所使用的驗證處理常式，會決定您設定工作階段管理的方式。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>當Dispatcher陣列啟用工作階段管理時，不會快取陣列處理的所有頁面。 若要快取CUG以外的頁面，請在dispatcher.any中建立第二個陣列
>處理非CUG頁面的即時通訊協定。

1. 定義`/directory`以設定[/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant#enabling-secure-sessions-sessionmanagement)；例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 將[/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant#caching-when-authentication-is-used)設為`0`。
