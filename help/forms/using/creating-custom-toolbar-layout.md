---
title: 建立自訂工具列配置
description: 您可以指定表單的工具列配置。 工具列配置會定義命令和表單上工具列的配置。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
exl-id: f9ff1458-6fc9-476a-a03e-c651464105d4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# 建立自訂工具列配置{#creating-custom-toolbar-layout}

## 工具列配置 {#layout}

建立最適化表單時，您可以指定表單的工具列配置。 工具列配置會定義命令和表單上工具列的配置。

工具列版面配置的使用嚴重依賴由複雜的JavaScript和CSS程式碼驅動的使用者端處理。 組織和最佳化此程式碼的伺服可能是一個複雜的問題。 為協助處理此問題，AEM提供使用者端程式庫資料夾，可讓您將使用者端程式碼儲存在存放庫中、將其組織成類別，並定義每個類別程式碼何時及如何提供給使用者端。 然後，使用者端程式庫系統會負責在最終網頁中產生正確的連結，以載入正確的程式碼。 如需詳細資訊，請參閱[使用者端資料庫在AEM中的運作方式。](/help/sites-developing/clientlibs.md)

![工具列的範例配置](assets/default_toolbar_layout.png)

工具列的範例配置

調適型表單提供一組現成可用的版面：

![現成可用的工具列配置](assets/toolbar1.png)

現成可用的工具列配置

此外，您也可以建立自訂工具列配置。

下列程式詳細說明建立自訂工具列的步驟，此工具列在工具列中會顯示三個動作，而其他動作則會顯示在工具列的下拉式清單中。

附加的內容套件包含下述的完整程式碼。 安裝內容套件後，請開啟`/content/forms/af/CustomLayoutDemo.html`以檢視自訂工具列配置示範。

CustomToolbarLayoutDemo.zip

[取得檔案](assets/customtoolbarlayoutdemo.zip)
示範自訂工具列配置

## 若要建立自訂工具列配置 {#layout-1}

1. 建立資料夾以維護自訂工具列配置。 例如：

   `/apps/customlayout/toolbar`。

   若要建立自訂配置，您可以使用（及自訂）下列資料夾中可用的其中一個現成工具列配置：

   `/libs/fd/af/layouts/toolbar`

   例如，將`mobileFixedToolbarLayout`節點從`/libs/fd/af/layouts/toolbar`資料夾複製到`/apps/customlayout/toolbar`資料夾。

   此外，將toolbarCommon.jsp複製到`/apps/customlayout/toolbar`資料夾。

   >[!NOTE]
   >
   >您建立用來維護自訂配置圖的資料夾大多是使用`apps`資料夾建立的。

1. 將複製的節點`mobileFixedToolbarLayout`重新命名為`customToolbarLayout.`

   此外，也提供節點的相關說明。 例如，將節點的jcr：description變更為&#x200B;**工具列**&#x200B;的自訂配置。

   節點的`guideComponentType`屬性決定配置型別。 在此情況下，版面配置型別為工具列，因此會顯示在工具列版面配置選擇下拉式清單中。

   ![具有相關說明的節點](assets/toolbar3.png)

   具有相關說明的節點

   您的新自訂工具列配置會顯示在&#x200B;**最適化表單工具列**&#x200B;對話方塊設定中。

   ![可用的工具列配置清單](assets/toolbar4.png)

   可用工具列配置清單

   >[!NOTE]
   >
   >上一步驟中更新的說明會顯示在「配置」下拉式清單中。

1. 選取此自訂工具列配置，然後按一下「確定」。

   在`/etc/customlayout`節點中新增clientlib （javascript和css），並在`customToolbarLayout.jsp`中包含clientlib的參考。

   ![customToolbarLayout.css檔案的路徑](assets/toolbar_3.png)

   customToolbarLayout.css檔案路徑

   範例`customToolbarLayout.jsp`：

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <cq:includeClientLib categories="customtoolbarlayout" />
   <c:if test="${isEditMode}">
           <cq:includeClientLib categories="customtoolbarlayoutauthor" />
   </c:if>
   <div class="guidetoolbar mobileToolbar mobilecustomToolbar" data-guide-position-class="guide-element-hide">
       <div data-guide-scroll-indicator="true"></div>
       <%@include file="../toolbarCommon.jsp" %>
   </div>
   ```

   >[!NOTE]
   >
   >新增配置圖的guidetoolbar類別。 工具列的現成樣式是根據guidetoolbar類別定義的。

   範例`toolBarCommon.jsp`：

   ```jsp
   <%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions"%>
   <%--------------------
   This code iterates over all the tool bar items using the guideToolbar bean.
   If the number of toolbar items are more than 3, then we create a dropdown menu using bootstrap for other actions present in the toolbar.
   In both desktop and mobile devices, the layout is different.
   ---------------------------------%>
   
   <c:forEach items="${guideToolbar.items}" var="toolbarItem" varStatus="loop">
       <c:choose>
         <c:when test="${loop.index gt 2}">
      <c:choose>
       <c:when test="${loop.index eq 3}">
                     <div class="btn-group dropdown">
                       <button type="button" class="btn btn-primary dropdown-toggle label" data-toggle="dropdown">Actions <span class="caret"></code></button>
                       <button type="button" class="btn btn-primary dropdown-toggle icon" data-toggle="dropdown"><span class="glyphicon glyphicon-th-list"></code></button>
             <ul class="dropdown-menu" role="menu">
                           <li>
                               <div id="${toolbarItem.id}_guide-item">
                                 <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                              </div>
                           </li>
                           <c:if test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                                </ul>
                                </div>
                           </c:if>
       </c:when>
       <c:when test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                          <li>
                                     <div id="${toolbarItem.id}_guide-item">
                                         <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                                     </div>
                           </li>
                       </ul>
                     </div>
   
       </c:when>
       <c:otherwise>
         <li>
          <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
          </div>
         </li>
       </c:otherwise>
      </c:choose>
         </c:when>
         <c:otherwise>
     <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
        </div>
         </c:otherwise>
    </c:choose>
   </c:forEach>
   ```

   clientlib節點內存在的CSS：

   ```css
   .mobilecustomToolbar .dropdown {
       display: inline-block;
   }
   
   .mobilecustomToolbar .dropdown {
       float: right;
   }
   
   .mobilecustomToolbar .dropdown > button {
      padding: 6px 12px;
   }
   
   .mobilecustomToolbar .dropdown .guideFieldWidget, .mobilecustomToolbar .dropdown .guideFieldWidget button {
       width: 100%;
   }
   
   .mobilecustomToolbar .dropdown .caret{
       border-bottom: 6px solid;
       border-right: 6px solid transparent;
       border-left: 6px solid transparent;
    border-top: transparent;
   }
   
   .mobilecustomToolbar .dropdown-menu{
    top: auto;
    bottom: 100%;
   }
   
   .mobilecustomToolbar .btn-group {
    vertical-align: super;
   }
   
   .mobilecustomToolbar .glyphicon {
    font-size: 24px;
   }
   
   @media (max-width: 767px){
   
    .mobilecustomToolbar .dropdown .guideButton .iconButton-icon {
      display: none;
       }
   
       .mobilecustomToolbar .dropdown .guideButton .iconButton-label {
      display: inline-block;
       }
   
       .mobilecustomToolbar .dropdown .guideButton button {
      background-color: #013853;
       }
   
    .mobilecustomToolbar .btn-group {
     vertical-align: top;
    }
   
   }
   ```

>[!NOTE]
>
>上一步驟中更新的說明會顯示在「配置」下拉式清單中。

![自訂配置工具列的案頭檢視](assets/toolbar_1.png)

自訂配置工具列的案頭檢視
