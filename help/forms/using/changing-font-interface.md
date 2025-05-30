---
title: 變更介面的字型
description: 如何選擇性地變更使用者介面上的字型。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: e27ff9df-41d0-4eef-b04e-a3eefea3c9ab
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# 變更介面的字型{#changing-the-font-on-the-interface}

您可以變更AEM Forms工作區中顯示的字型。 在使用者介面的特定區段中使用的字型，會在樣式表的對應區段中定義。 您可以選擇性地變更使用者介面上的字型。

請依照[AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md)操作，並根據您的需求，依照自訂CSS、HTML或兩者的步驟操作。

1. 在現有樣式中變更或新增字型系列。
1. 變更或新增HTML元素的內嵌字型系列。
1. 新增樣式並將其用於HTML元素。

例如，若要將頂端導覽列錨點文字的字型變更為Courier New，請遵循下列步驟：

1. 存取`https://'[server]:[port]'/lc/crx/de/index.jsp`以登入CRXDE Lite。
1. 執行下列任一項作業：

   1. 若要變更現有樣式中的font-family，請在/apps/ws/css的newStyle.css檔案中新增下列專案。

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. 若要為HTML元素新增字型系列內嵌，請將`/libs/ws/js/runtime/templates/appnavigation.html`檔案複製到`/apps/ws/js/runtime/templates/appnavigation.html`。

      更新/apps/ws/js/runtime/templates/appnavigation.html檔案，如下所示：

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      開啟/apps/ws/js/registry.js檔案進行編輯，並將`text!/lc/libs/ws/js/runtime/templates/appnavigation.html`取代為`text!/lc/apps/ws/js/runtime/templates/appnavigation.html`。

   1. 若要新增定義font-family的樣式，請在/apps/ws/css的newStyle.css檔案中新增下列內容。

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      若要為HTML元素新增字型系列內嵌，請在/apps/ws/js/runtime/templates的appnavigation.html檔案中新增下列專案。

      ```jsp
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. 重新啟動工作區並清除瀏覽器快取，使變更可見。

![change_font_before](assets/change_font_before.png)

字型自訂前的頂端導覽列

![change_font_after](assets/change_font_after.png)

第一個索引標籤的字型自訂後的頂端導覽列
