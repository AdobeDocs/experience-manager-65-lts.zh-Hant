---
title: 使用AEM Forms工作區
description: 開始使用AEM Forms工作區，並透過此程式工作流程的快速概觀。
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
exl-id: 7374797f-4154-402b-bb59-075134763c58
source-git-commit: 823923ab074bae1705cc1991e4079897e4c5cac8
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---

# 使用AEM Forms工作區{#working-with-aem-forms-workspace}

## 簡介 {#introduction}

AEM Forms工作區是AEM Forms的一部分。 除了PDF forms，Workspace還協助轉譯HTML Forms。 現在您可以從行動介面和網頁應用程式參與業務流程。

此外，AEM Forms工作區也可以使用標準HTML和JavaScript™開發方法高度自訂。 這是一種元件式軟體，可輕鬆與您的其他Web應用程式整合。

如需詳細資訊，請參閱[ AEM Forms工作區簡介](/help/forms/using/introduction-html-workspace.md)。

## 熟悉 {#getting-familiar}

若要熟悉建立表單應用程式以自動化業務流程的端對端流程，請按照以下逐步說明進行操作。 逐步說明後，您可以使用Workbench、Designer和AEM Forms工作區來建立、管理和測試應用程式。 如需實作詳細資料，請參閱[建立您的第一個AEM Forms應用程式](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html)。

## 功能概觀 {#functional-overview}

您可以使用AEM Forms工作區來執行下列工作：

**開始業務流程：** AEM Forms工作區會將您的流程分類為您的組織所設計和設定的流程。 您可以將常用的類別加到最愛，以便快速存取類別。 啟動程式時，通常會填寫表單以啟動形成工作流程控制的業務流程。 如需詳細資訊，請參閱[啟動處理序](/help/forms/using/starting-processes.md)。

**檢視工作並據以行動：**&#x200B;檢視您的待辦事項清單時，您會看到商務程式指派給您、您所屬的任何群組，或是其他使用者的共用工作。 您可以視需要開啟、處理及完成工作。 通常，完成任務需要提供資訊、核准表單或拒絕表單。 如需詳細資訊，請參閱[使用待辦事項清單](/help/forms/using/todo-lists.md)。

**追蹤任務**：若要追蹤您的任務，請使用AEM Forms工作區的[追蹤]索引標籤。 您可以搜尋您已開始或參與的使用中或已完成的程式。 您可以檢視屬於流&#39;b5&#39;7b一部分的任務、指派和表單。 您也可以使用先前啟動之流程的表單資料來啟動新流程。 如需詳細資訊，請參閱[追蹤程式](/help/forms/using/tracking-processes.md)。

## AEM Forms工作區的新功能 {#new-offering-of-aem-forms-workspace}

**支援大量核准任務**：

您可以核准相同型別的多個任務。 選取一項任務進行核准後，只有具有相同程式、相同任務名稱和相同路由選項的任務會保持啟用狀態。 如需實作詳細資料，請參閱[使用待辦事項清單](/help/forms/using/todo-lists.md)。

## 從Flex Workspace移轉至AEM Forms工作區 {#migrating-from-flex-workspace-to-aem-forms-workspace}

AEM Forms客戶不支援Flex Workspace。 所有使用Flex Workspace的客戶都應改用AEM Forms Workspace。

在AEM Forms工作區中，與XDP表單相關的預設動作設定檔中的預設轉譯和提交服務已變更，並且已引入新服務。 如需詳細資訊，請參閱[新的轉譯與提交服務](/help/forms/using/new-render-submit-service.md)。 若要移轉與XDP表單搭配使用的現有程式，若要使用這些服務，您可以遵循[這些步驟](new-render-submit-service.md)。

**將Flex Workspace自訂與AEM Forms工作區對應**

兩個工作區中各種自訂型別之間的對映如下。

<table>
 <tbody>
  <tr>
   <td><strong>自訂型別 </strong></td>
   <td><strong>涵蓋自訂內容 </strong></td>
   <td><strong>對應的AEM Forms工作區自訂案例</strong></td>
  </tr>
  <tr>
   <td>本地化自訂</td>
   <td>
    <ol>
     <li>變更Workspace的地區設定</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">變更AEM Forms工作區地區設定</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>佈景主題自訂</td>
   <td>
    <ol>
     <li>取代影像</li>
     <li>修改顏色</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">變更組織標誌</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">變更色彩配置</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>版面配置自訂</td>
   <td>
    <ol>
     <li>簡化Workspace使用者介面<br /> </li>
     <li>建立新的登入畫面</li>
     <li>建立自訂核准容器</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">使用可重複使用的元件</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">建立登入畫面</a></li>
     <li>核准容器已棄用。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Flex WorkspaceAEM Forms工作區中未提供的部分功能包括：訊息和通知、歡迎頁面、核准容器，以及管理欄標題的選項。 如需完整清單，請參閱[AEM Forms工作區中不提供的Flex Workspace功能](/help/forms/using/features-flex-workspace-available-html.md)。

## 使用AEM Forms工作區進行開發 {#developing-with-aem-forms-workspace}

### 架構 {#architecture}

AEM Forms工作區是以HTML和JavaScript™為基礎的網頁應用程式，託管於CRX™。 在瀏覽器中開啟Workspace URL時，系統會存取CRX™資源，並將應用程式呈現為瀏覽器中的HTML頁面。 JavaScript程式庫和自訂JavaScript程式碼可管理應用程式的內部和外部行為，例如使用者介面、使用者互動以及與AEM Forms伺服器的通訊。 如需詳細資訊，請參閱AEM Forms工作區[架構](/help/forms/using/html-workspace-architecture.md)。

### AEM Forms工作區自訂 {#aem-forms-workspace-customization}

AEM Forms工作區支援各種自訂，以更新使用者介面的版面、外觀、功能等。 自訂涉及更新下列一或多個專案：

* 使用者介面的外觀
* 使用語意自訂的功能
* 在其他網頁應用程式中重複使用HTML元件

[自訂](introduction-customizing-html-workspace.md#types-of-customizations)文章說明此類自訂的型別。

### 設定開發人員環境 {#set-up-the-developer-environment}

AEM Forms工作區交付專案包括部署在CRX上的CRX套件、包含完整原始程式碼的SDK封存、第三方JavaScript程式庫，以及AEM Forms工作區的建置指令碼。 使用這些專案來設定開發人員環境，以執行上述自訂。 如需詳細資訊，請參閱[建立AEM Forms工作區程式碼](introduction-customizing-html-workspace.md#building-html-workspace-code)。

您可以自訂介面和核心功能的主要部分，例如，字型、色彩配置、標誌、登入畫面、錯誤對話方塊、與協力廠商應用程式的整合，以及協力廠商應用程式中元件的重複使用。 您也可以增強「工作摘要」頁面上顯示的內容、顯示工作路由動作的影像，甚至修改建立AEM Forms工作區應用程式的低階骨幹模型與檢視。

### XDP Forms的HTML轉譯 {#html-rendering-of-xdp-forms}

根據預設，針對新程式，XDP表單會在桌上型電腦上以PDF格式呈現，並在平板電腦上以HTML格式呈現。 您可以一律以HTML格式呈現XDP表單。 如需詳細資訊，請參閱[新的轉譯與提交服務](/help/forms/using/new-render-submit-service.md)。

[行動Forms](/help/forms/using/introduction.md)功能可搭配[設定檔](/help/forms/using/custom-profile.md)使用，以啟用HTML的XDP表單轉譯。 依預設，「轉譯新HTML表單」會使用您可變更的`default.html`設定檔。 您也可以新增在HTML格式轉譯XDP表單之前發生的自訂變更。
