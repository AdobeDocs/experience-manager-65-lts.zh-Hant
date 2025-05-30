---
title: 自訂處理序執行個體清單
description: 如何自訂AEM Forms工作區中流程例項顯示的屬性。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 7ffde604-2f56-4b53-88ab-5fac321e4753
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---

# 自訂處理序執行個體清單 {#customizing-the-listing-of-process-instances}

流程例項清單會顯示在AEM Forms工作區的「追蹤」標籤中。

在流程例項清單中，AEM Forms工作區會針對每個流程例項顯示該例項的一些屬性。 下列屬性適用於每個程式執行個體。 這些屬性作為屬性儲存在流程例項元件模型中，並可用於其檢視和範本。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td>說明</td>
   <td>程式執行個體的描述。</td>
  </tr>
  <tr>
   <td>發起人</td>
   <td>程式執行個體的啟動器名稱。</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>程式執行個體啟動器的ID。</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>程式完成時的時間戳記。</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>程式執行個體的ID。</td>
  </tr>
  <tr>
   <td>processinstancestatus</td>
   <td>0 =已起始<br /> 1 =正在執行<br /> 2 =完成<br /> 3 =正在完成<br /> 4 =已終止<br /> 5 =正在終止<br /> 6 =已暫停<br /> 7 =正在暫停<br /> 8 =正在取消暫停</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>處理序的名稱。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>處理序啟動時的時間戳記。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>程式變數的物件陣列。 每個處理序變數物件都包含<strong>name</strong> （處理序變數的名稱）、<strong>value</strong> （處理序變數的值）和<strong>型別</strong> （處理序變數的型別）。</td>
  </tr>
 </tbody>
</table>

**範例：**

若要在程式執行個體卡片中顯示程式執行個體的`description`屬性，請執行下列步驟。

1. 執行[AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 請執行下列動作：

   1. 將/libs/ws/js/runtime/templates/processinstance.html複製到/apps/ws/js/runtime/templates/ （如果它不存在）。 按一下&#x200B;**「儲存全部」**。
   1. 以class = &#39;processDescription&#39; inprocessinstance.html新增處理序描述div。

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 請執行下列動作：

   1. 開啟/apps/ws/js/registry.js進行編輯。
   1. 搜尋並以&#x200B;`text!/lc/`**應用程式**/ws/js/runtime/templates/processinstance.html取代`text!/lc/libs/ws/js/runtime/templates/processinstance.html`。

1. 若要進行上述變更，請以下列方式在樣式表/apps/ws/css/newStyle.css中新增專案，以更新CSS檔案：

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement and user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
