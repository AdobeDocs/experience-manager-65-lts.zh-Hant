---
title: 移轉至Touch UI
description: 瞭解Adobe Experience Manager移轉至Touch UI以及其如何影響。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: e9b26de3-6e14-4187-8f25-6e56ee3092a7
source-git-commit: 013c9155817811913963ca514f7a6369b338d487
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 3%

---

# 移轉至Touch UI{#migration-to-the-touch-ui}

從6.0版開始，Adobe Experience Manager (AEM)推出了稱為&#x200B;*觸控式UI*&#x200B;的新使用者介面（也簡稱為&#x200B;*觸控式UI*）。 這會與Adobe Experience Cloud及整體Adobe使用者介面指導方針一致。 這已成為AEM中的標準UI，具有稱為&#x200B;*傳統UI*&#x200B;的舊版案頭導向介面。

如果您已搭配傳統UI使用AEM，請採取行動移轉您的執行個體。 本頁旨在提供個別資源的連結，以發揮跳板的作用。

>[!NOTE]
>
>這類移轉專案可能會對您的執行個體產生重大影響。 請參閱[管理專案 — 最佳實務](/help/managing/best-practices.md)，以取得建議的准則。

## 基本資訊 {#the-basics}

移轉時，請留意Classic和觸控式UI之間的下列主要差異：

<table>
 <tbody>
  <tr>
   <td>傳統 UI</td>
   <td>觸控式UI</td>
  </tr>
  <tr>
   <td>在JCR存放庫中作為節點結構描述。 代表UI元素的每個節點稱為<em>ExtJS Widget</em>，並由<code>ExtJS</code>在使用者端轉譯。</td>
   <td>也在JCR存放庫中說明為節點結構。 但是，在這種情況下，每個節點都參考Sling資源型別（Sling元件），該資源型別負責其呈現。 因此，UI （基本）是在伺服器端呈現。</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>未使用</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>已使用</li>
     <li>例如<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>對話方塊節點：</p>
    <ul>
     <li>名稱: <code>dialog</code></li>
     <li><code>jcr:primaryType</code>： <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>對話方塊節點：</p>
    <ul>
     <li>名稱: <code>cq:dialog</code></li>
     <li><code>jcr:primaryType</code>： <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JavaScript位置：</p>
    <ul>
     <li>必要部分使用接聽程式直接內嵌或在clientlibs中管理。</li>
    </ul> </td>
   <td><p>JavaScript位置：</p>
    <ul>
     <li>命令部分不能嵌入對話方塊定義中；責任分離。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件處理：</p>
    <ul>
     <li>對話方塊Widget會直接參照JavaScript程式碼。</li>
    </ul> </td>
   <td><p>事件處理：</p>
    <ul>
     <li>JavaScript會觀察對話方塊事件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>由使用者端完成的轉譯：
    <ul>
     <li>Client會動態建立UI元件。</li>
     <li>來自伺服器的使用者端請求（提取）元件定義(JSON)。</li>
    </ul> </td>
   <td>由伺服器完成的轉譯：
    <ul>
     <li>使用者端要求頁面以及相關UI。</li>
     <li>伺服器會將UI作為HTML檔案傳送（推送）；使用Coral UI元件。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

換句話說，將UI的區段從傳統UI移轉到觸控式UI意指將&#x200B;*ExtJS Widget*&#x200B;移轉到&#x200B;*Sling元件*。 為方便起見，觸控式UI以Granite UI框架為基礎，該框架已為UI提供了一些Sling元件（稱為Granite UI元件）。

開發觸控式UI的基礎知識提供了堅實的基礎：

* [AEM觸控式UI的概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM觸控式UI的結構](/help/sites-developing/touch-ui-structure.md)

## 移轉頁面製作 {#migrating-page-authoring}

對話方塊是移轉元件時的主要因素：

* [開發AEM元件](/help/sites-developing/developing-components.md) （使用觸控式UI）
* [從傳統元件移轉](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [AEM現代化工具](/help/sites-developing/modernization-tools.md) — 協助您將傳統UI元件的對話方塊轉換為觸控式UI

   * 觸控式UI提供相容性層，可在「觸控式UI包裝函式」中開啟傳統UI對話方塊，但此功能有限，長期而言不建議使用。

* [在觸控式UI中自訂對話方塊欄位](https://helpx.adobe.com/tw/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [建立新的Granite UI欄位元件](/help/sites-developing/granite-ui-component.md)
* [自訂頁面製作](/help/sites-developing/customizing-page-authoring-touch.md) （使用觸控式UI）

## 正在移轉主控台 {#migrating-consoles}

您也可以自訂主控台：

* [自訂主控台](/help/sites-developing/customizing-consoles-touch.md) （針對觸控式UI）

## 相關考量 {#related-considerations}

雖然移轉至Touch UI並無直接關係，但建議您同時考量下列相關問題，因為這也是建議做法：

* [範本](/help/sites-developing/templates.md) - [可編輯的範本](/help/sites-developing/page-templates-editable.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hant)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=zh-Hant)

>[!NOTE]
>
>另請參閱[開發 — 最佳做法](/help/sites-developing/best-practices.md)。

## 其他資源 {#further-resources}

如需有關開發AEM的完整資訊，請參閱下列各項下的資源集合：

* [Developing使用手冊](/help/sites-developing/getting-started.md)
* [Granite UI檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 Sites教學課程與影片](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html?lang=zh-Hant)
* [開發 AEM Sites 快速入門 - WKND 教學課程](/help/sites-developing/getting-started.md)
* [AEM Gems](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=zh-Hant)
* [AEM 現代化工具](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM現代化工具是社群共同努力的結果，Adobe不提供支援或保證。
