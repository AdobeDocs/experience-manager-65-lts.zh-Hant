---
title: 升級程式碼和自訂
description: 進一步瞭解如何在AEM中升級程式碼和自訂。
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 6b94caf1-97b7-4430-92f1-4f4d0415aef3
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# 升級程式碼和自訂{#upgrading-code-and-customizations}

規劃升級時，必須調查並處理下列實作領域。

* [升級程式碼基底](#upgrade-code-base)
* [測試程式](#testing-procedure)

## 概觀 {#overview}

1. **AEM分析器** — 依照升級規劃中的說明執行AEM分析器，並在[使用AEM分析器評估升級複雜性](/help/sites-deploying/aem-analyzer.md)頁面上詳細說明。 您會收到AEM Analyzer報表，其中除了AEM目標版本中無法使用的API/套件組合，也包含必須解決之區域的詳細資訊。 AEM Analyzer報表可指出程式碼中的任何不相容專案。 如果不存在任何專案，表示您的部署已經與6.5 LTS相容。 您仍然可以選擇使用6.5 LTS功能進行新開發，但您不只為了維護相容性而需要它。
1. **開發6.5 LTS的程式碼基底** — 為Target版本的程式碼基底建立專屬的分支或存放庫。 使用升級前相容性的資訊，規劃要更新的程式碼區域。
1. **使用6.5 LTS Uber jar編譯** — 更新程式碼基底POM以指向6.5 LTS uber jar並編譯程式碼。
1. **部署至6.5 LTS環境** - AEM 6.5 LTS的乾淨執行個體（製作+發佈）應在Dev/QA環境中站立。 應部署更新的程式碼庫和代表性內容範例（來自目前生產環境）。
1. **QA驗證和錯誤修正** - QA應在6.5 LTS的作者和發佈執行個體上驗證應用程式。 發現的任何錯誤都應修正並認可至6.5 LTS程式碼基底。 視需要重複開發週期，直到修復所有錯誤為止。

在繼續升級之前，您應該要有已針對AEM 6.5 LTS完整測試的穩定應用程式程式碼基底。

## 升級程式碼基底 {#upgrade-code-base}

### 在版本控制{#create-a-dedicated-branch-for-6.5-lts-code-in-version-control}中建立6.5 LTS程式碼的專用分支

您應使用某種形式的版本控制來管理實施AEM所需的所有程式碼和設定。 應建立版本控制中的專用分支，以管理目標版本AEM中程式碼庫所需的任何變更。 針對AEM的目標版本反複測試程式碼基底，以及後續的錯誤修正，會管理於此分支。

### 更新AEM Uber Jar版本 {#update-the-aem-uber-jar-version}

AEM Uber jar包含所有AEM API，作為您Maven專案`pom.xml`中的單一相依性。 納入Uber Jar作為單一相依性始終是最佳實務，而不是納入個別AEM API相依性。 升級程式碼基底時，請變更Uber Jar版本以指向AEM的6.5 LTS版本。 更新任何已棄用的API或方法，使其與AEM的目標版本相容。 針對新版本的Uber Jar重新編譯程式碼基底。

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>AEM 6.5和AEM 6.5 LTS Uber Jar的封裝方式略有不同。 請參閱以下章節：

適用於AEM 6.5的&#x200B;**Uber Jar**

1. `uber-jar-6.5.x.jar` — 包含AEM 6.5的所有公用API。
1. `uber-jar-6.5.x-apis-with-deprecations.jar` — 包含AEM 6.5的公用API和已過時的API。

適用於AEM 6.5 LTS的&#x200B;**Uber Jar**

對於AEM 6.5 LTS，再次存在兩種型別的Uber Jar：

1. `uber-jar-6.6.x-apis.jar` — 包含AEM 6.5 LTS的所有公用API。
1. `uber-jar-6.6.x-deprecated-apis.jar` — 僅包含來自AEM 6.5 LTS的已棄用API。

**主要差異： AEM 6.5與AEM 6.5 LTS Uber Jars**

* 在AEM 6.5中，如果同時需要公用和過時的API，您可以在`pom.xml`檔案中使用包含單一jar `uber-jar-6.5.x-apis-with-deprecations.jar`。
* 在AEM 6.5 LTS中，如果您同時需要公用和過時的API，您必須包含兩個個別的jar，即公用API的`uber-jar-6.6.x-apis.jar`和過時的API的`uber-jar-6.6.x-deprecated-apis.jar`。

已棄用的API Jar的&#x200B;**Maven座標**

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 開發人員注意事項 {#developer-notes}

* AEM 6.5 LTS不含現成的Google Guava程式庫，可視需求安裝所需版本。
* Sling XSS組合現在使用Java HTML Sanitizer程式庫，應該使用`XSSAPI#filterHTML()`方法的使用來安全地呈現HTML內容，而不是將資料傳遞至其他API。

## 測試程式 {#testing-procedure}

應準備完整的測試計畫以進行測試升級。 測試升級的程式碼基底和應用程式必須先在較低的環境中完成。 找到的任何錯誤都應透過反複的方式進行修正，直到程式碼庫穩定為止，只有那時才應該升級較高層級的環境。

### 測試升級程式 {#testing-upgrade-procedure}

這裡概述的升級程式應在開發和QA環境中進行測試，如您的自訂執行手冊中所述（請參閱[規劃升級](/help/sites-deploying/upgrade-planning.md)）。 升級程式應重複執行，直到所有步驟都記錄在升級執行手冊中且升級過程順利進行。

### 實作測試區域  {#implementation-test-areas-}

以下是任何AEM實作的重要區域，在環境升級且部署升級後的程式碼庫後，這些區域應包含在測試計畫中。

<table>
 <tbody>
  <tr>
   <td><strong>功能測試區域</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>已發佈的網站</td>
   <td>透過Dispatcher在發佈階層<br />上測試AEM實作和相關聯的程式碼。 應該包含頁面更新和<br />快取失效的條件。</td>
  </tr>
  <tr>
   <td>製作</td>
   <td>在製作層級上測試AEM實作和相關程式碼。 應包括頁面、元件製作和對話方塊。</td>
  </tr>
  <tr>
   <td>與Experience Cloud解決方案整合</td>
   <td>驗證與Analytics等產品的整合。</td>
  </tr>
  <tr>
   <td>與協力廠商系統整合</td>
   <td>驗證「作者」和「發佈」階層上的任何協力廠商整合。</td>
  </tr>
  <tr>
   <td>驗證、安全性和許可權</td>
   <td>任何驗證機制（如LDAP/SAML）都應經過驗證。<br />許可權和群組應在Author和Publish<br />層級上進行測試。</td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>自訂索引和查詢應該與查詢效能一起測試。</td>
  </tr>
  <tr>
   <td>UI自訂</td>
   <td>在製作環境中AEM UI的任何擴充功能或自訂專案。</td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td>自訂和/或現成的工作流程及功能。</td>
  </tr>
  <tr>
   <td>效能測試</td>
   <td>載入測試應在模擬真實世界情境的製作和發佈層級上執行。</td>
  </tr>
 </tbody>
</table>

### 記錄測試計畫和結果 {#document-test-plan-and-results}

應建立涵蓋上述實作測試區域的測試計畫。 通常，依作者和發佈工作清單來區隔測試計畫是可行的做法。 此測試計畫應在升級生產環境之前於開發、QA和中繼環境上執行。 測試結果和效能量度應在較低層級環境中擷取，以便在升級中繼和生產環境時提供比較。
