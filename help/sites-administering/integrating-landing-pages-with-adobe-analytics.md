---
title: 將登入頁面與Adobe Analytics整合
description: 瞭解如何將登入頁面與Adobe Analytics整合。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 24ab494d-4a11-408e-8dc0-de16508edfac
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---

# 將登入頁面與Adobe Analytics整合{#integrating-landing-pages-with-adobe-analytics}

AEM已透過使用下列召喚行動(CTA)元件，將登入頁面解決方案與[Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst)整合：

1. 點進元件
1. 圖形連結元件

這些元件會公開可透過Adobe Analytics變數（流量、轉換變數）和成功事件對應的特定屬性，以將資訊傳送至Adobe Analytics。

## 先決條件 {#prerequisites}

Adobe建議您透過[現有的AEM-Adobe Analytics整合](/help/sites-administering/adobeanalytics.md)瞭解此整合的運作方式。

## 可用於對應的元件 {#components-available-for-mapping}

在AEM中，sidekick中顯示的&#x200B;**行動號召**&#x200B;元件 — **ClickThroughLink**&#x200B;和&#x200B;**GraphicalLink** — 可以對應到Adobe Analytics變數。

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### 將登陸頁面元件對應至Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

若要將登入頁面元件對應至Adobe Analytics：

1. 建立Adobe Analytics設定和建立框架後，請從下拉式選單中選取適當的報表套裝。 這會擷取Adobe Analytics變數，並在內容尋找器中顯示它們。
1. 視需要將Call to Action (CTA)元件從Sidekick拖放至頁面中間的對應區域。

<table>
 <tbody>
  <tr>
   <td><strong>元件名稱</strong></td>
   <td><strong>屬性已公開</strong></td>
   <td><strong>屬性的含義</strong></td>
  </tr>
  <tr>
   <td><strong>CTA點進連結</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>連結上的標籤或連結的文字 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>按一下連結時所前往的目的地 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>點按事件 </td>
  </tr>
  <tr>
   <td><strong>CTA圖形連結</strong></td>
   <td><i>eventdata.clickthroughImageLabel</i> <br /> </td>
   <td>CTA影像的標題 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageTarget</i> <br /> </td>
   <td>按一下包含連結的影像時拍攝的目的地</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickgroughImageAsset</i> <br /> </td>
   <td>存放庫中影像資產的路徑 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickgroughImageClick</i> <br /> </td>
   <td>點按事件</td>
  </tr>
 </tbody>
</table>

1. 從內容尋找器將這些公開的屬性與任何Adobe Analytics變數對應。 架構現已準備就緒，可供使用。
1. 您現在可以建立登入頁面，或開啟具有現有CTA元件的現有登入頁面，然後從Sidekick按一下&#x200B;**頁面屬性**&#x200B;中的&#x200B;**雲端服務**&#x200B;索引標籤（在觸控最佳化UI中，選取&#x200B;**開啟屬性**&#x200B;並按一下&#x200B;**雲端服務**），並設定用於登入頁面的架構。 從下拉式清單中選取架構。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 使用登入頁面設定框架後，您現在可以使用儀表化的元件，對CTA的任何點按都會記錄在Adobe Analytics中。
