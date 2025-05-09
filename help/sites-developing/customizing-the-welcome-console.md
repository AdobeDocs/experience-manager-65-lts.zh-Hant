---
title: 自訂歡迎主控台（傳統UI）
description: 「歡迎」主控台提供AEM中各種主控台和功能的連結清單
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: a3595673-8d43-4ef2-a00e-ec8aa8d9cb55
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 6%

---

# 自訂歡迎主控台（傳統UI）{#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>本頁面說明傳統UI。
>
>如需有關標準觸控式UI的詳細資訊，請參閱[自訂主控台](/help/sites-developing/customizing-consoles-touch.md)。

「歡迎」主控台提供AEM中各種主控台和功能的連結清單。

![cq_welcomescreen](assets/cq_welcomescreen.png)

您可以設定可見的連結。 這可為特定使用者和/或群組定義。 要採取的動作取決於目標型別（這與其所在的主控台區段相關）：

* [主主控台](#links-in-main-console-left-pane) — 主主控台中的連結（左窗格）
* [資源、檔案和參考、功能](#links-in-sidebar-right-pane) — 側邊欄中的連結（右側窗格）

## 主主控台中的連結（左窗格） {#links-in-main-console-left-pane}

以下列出AEM的主要主控台。

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### 設定是否顯示主要主控台連結 {#configuring-whether-main-console-links-are-visible}

節點層級的許可權會決定是否顯示連結。 有問題的節點包括：

* **網站：** `/libs/wcm/core/content/siteadmin`

* **數位Assets：** `/libs/wcm/core/content/damadmin`

* **社群：** `/libs/collab/core/content/admin`

* **行銷活動：** `/libs/mcm/content/admin`

* **收件匣：** `/libs/cq/workflow/content/inbox`

* **使用者：** `/libs/cq/security/content/admin`

* **工具：** `/libs/wcm/core/content/misc`

* **標籤：** `/libs/cq/tagging/content/tagadmin`

例如：

* 若要限制對&#x200B;**工具**&#x200B;的存取權，請從移除讀取存取權

  `/libs/wcm/core/content/misc`

如需如何設定所需許可權的詳細資訊，請參閱[安全性區段](/help/sites-administering/security.md)。

### 側邊欄中的連結（右窗格） {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

這些連結是以下列路徑下存在&#x200B;*和*&#x200B;節點的讀取存取權為基礎：

`/libs/cq/core/content/welcome`

預設提供三個區段（稍微相隔）：

<table>
 <tbody>
  <tr>
   <td><strong>資源</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> 雲端服務</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> 工作流程</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> 任務管理</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> 複製</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> 報告</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> 出版物</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> 手稿</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>檔案與參考資料</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> 文件</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> 開發人員資源</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>功能</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> 套件</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> 套件共用</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> 叢集</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> 備份</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> Web 主控台<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Web主控台狀態傾印<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### 設定是否顯示側欄連結 {#configuring-whether-sidebar-links-are-visible}

您可以移除代表連結之節點的讀取存取權，以隱藏連結，不讓特定使用者或群組存取。

* 資源 — 移除對下列專案的存取權：

  `/libs/cq/core/content/welcome/resources/<link-target>`

* 檔案 — 移除對下列專案的存取權：

  `/libs/cq/core/content/welcome/docs/<link-target>`

* 功能 — 移除對下列專案的存取權：

  `/libs/cq/core/content/welcome/features/<link-target>`

例如：

* 若要移除指向&#x200B;**報表**&#x200B;的連結，請從移除讀取許可權

  `/libs/cq/core/content/welcome/resources/reports`

* 若要移除指向&#x200B;**封裝**&#x200B;的連結，請從移除讀取許可權

  `/libs/cq/core/content/welcome/features/packages`

如需如何設定所需許可權的詳細資訊，請參閱[安全性區段](/help/sites-administering/security.md)。

### 連結選擇機制 {#link-selection-mechanism}

在`/libs/cq/core/components/welcome/welcome.jsp`中，由[ConsoleUtil](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/ConsoleUtil.html)使用，這會在具有屬性的節點上執行查詢：

* 值為`cq:Console`的`jcr:mixinTypes`

>[!NOTE]
>
>執行以下查詢以檢視現有清單：
>
>* `select * from cq:Console`
>

當使用者或群組沒有具有mixin `cq:Console`之節點的讀取許可權時，`ConsoleUtil`搜尋不會擷取該節點，因此它不會列在主控台上。

### 新增自訂專案 {#adding-a-custom-item}

[連結選擇機制](#link-selection-mechanism)可用來將您自己的自訂專案加入連結清單。

將`cq:Console` mixin新增至您的Widget或資源，以將您的自訂專案新增至清單。 可透過定義屬性來完成：

* 值為`cq:Console`的`jcr:mixinTypes`
