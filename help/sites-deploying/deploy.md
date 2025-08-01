---
title: 部署和維護
description: 瞭解如何開始安裝AEM。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 4a2ada26-b859-4a32-9ab0-2d4c2b695245
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 4%

---

# 部署和維護{#deploying-and-maintaining}

您可以在此頁面找到：

* [基本概念](#basic-concepts)

   * [什麼是AEM？](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [內部部署](#on-premise)
      * [使用Cloud Manager的Managed Services](#managed-services-using-cloud-manager)

* [快速入門](#getting-started)

   * [先決條件](#prerequisites)
   * [取得軟體](#getting-the-software)
   * [預設本機安裝](#default-local-install)
   * [製作和發佈安裝](#author-and-publish-installs)
   * [解壓縮的安裝目錄](#unpacked-install-directory)
   * [啟動和停止](#starting-and-stopping)

熟悉這些基本知識後，您就可以在下列子頁面中找到更進階和詳細的資訊：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [命令列啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級至AEM 6.5 LTS](/help/sites-deploying/upgrade.md)
* [設定作法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md)
* [最佳實務](/help/sites-deploying/best-practices.md)
* [AEM平台簡介](/help/sites-deploying/platform.md)

## 基本概念 {#basic-concepts}

### 什麼是AEM？ {#what-is-aem}

Adobe Experience Manager是網頁式使用者端伺服器系統，用於建立、管理和部署商業網站及相關服務。 它將數個基礎架構層級和應用程式層級的功能合併為單一整合套件。

在基礎架構層級，AEM提供下列功能：

* **Web應用程式伺服器**： AEM可部署為獨立模式（包含整合式Jetty Web伺服器），或部署為協力廠商應用程式伺服器內的Web應用程式。
* **Web應用程式架構**： AEM整合了Sling Web應用程式架構，可簡化RESTful、內容導向的Web應用程式撰寫。
* **內容存放庫**： AEM包含Java™內容存放庫(JCR)，這是專為非結構化與半結構化資料設計的階層式資料庫型別。 存放庫不僅儲存面向使用者的內容，也儲存應用程式使用的所有程式碼、範本和內部資料。

在此基礎上再接再厲，AEM也提供數種應用程式層級功能，以管理下列專案：

* **網站**
* **數位出版物**
* **Forms與檔案**
* **數位Assets**

最後，客戶可以利用這些基礎結構和應用程式層級的建置組塊，透過建置自己的應用程式來建立自訂解決方案。

AEM伺服器是&#x200B;**Java型**，並在支援該平台的大多數作業系統上執行。 所有使用者端與AEM的互動都是透過&#x200B;**網頁瀏覽器**&#x200B;完成。

>[!NOTE]
>
>AEM 6.5 LTS QuickStart提供的最適化Forms功能，僅供探索和評估之用。 若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

### 典型部署案例 {#typical-deployment-scenarios}

在AEM術語中，「例項」是指在伺服器上執行的AEM副本。 AEM安裝通常至少涉及兩個執行個體，通常在不同電腦上執行：

* **作者**：用來建立、上傳和編輯內容以及管理網站的AEM執行個體。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
* **發佈**：將發佈的內容提供給公用的AEM執行個體。

這些例項在安裝軟體方面是相同的。 它們僅能透過設定來區分。 此外，大部分安裝都使用Dispatcher：

* **Dispatcher**：靜態網頁伺服器(Apache httpd、Microsoft®IIS等)已透過AEM Dispatcher模組增強。 它快取發佈執行個體產生的網頁以提升效能。

此設定有許多進階選項和詳細說明，但製作者、發佈和Dispatcher的基本模式是大多數部署的核心。 讓我們從簡單的設定開始。 接著會討論進階部署選項。

以下各節將說明這兩種情況：

* **內部部署**： AEM已在您的公司環境中部署和管理。

* **Managed Services - Adobe Experience Manager適用的Cloud Manager**：Adobe Managed Services所部署和管理的AEM。

### 內部部署 {#on-premise}

您可以在公司環境的伺服器上安裝AEM。 典型的安裝例項包括：開發、測試和發佈環境。 請參閱[快速入門](#getting-started)，瞭解如何取得AEM軟體以在本機安裝。

<!-- To learn more about the typical on-premises deployments, see [Recommended Deployments](/help/sites-deploying/recommended-deploys.md). -->

### 使用Cloud Manager的Managed Services {#managed-services-using-cloud-manager}

<i>即將宣佈。</i>

## 快速入門 {#getting-started}

### 先決條件 {#prerequisites}

雖然生產執行個體是在執行官方支援作業系統的專用電腦上執行（請參閱[技術需求](/help/sites-deploying/technical-requirements.md)），但Experience Manager伺服器實際上會在任何支援&#x200B;[**Java™ Standard Edition 17**](https://www.oracle.com/java/technologies/downloads/#java17)的系統上執行。

為了熟悉和開發AEM，通常會使用安裝在執行Apple OS X或Microsoft® Windows或Linux®案頭版本的本機電腦上的執行個體。

在使用者端，AEM可在桌上型電腦和平板電腦作業系統上與所有現代瀏覽器(**Microsoft® Edge**、**Chrome 51+**、**Firefox 47+**、**Safari 8+**)搭配使用。 如需詳細資訊，請參閱[支援的使用者端平台](/help/sites-deploying/technical-requirements.md#supported-client-platforms)。

### 取得軟體 {#getting-the-software}

持有有效維護與支援合約的客戶應已收到內含程式碼的郵件通知，並可從&#x200B;[**Adobe授權網站**](https://licensing.adobe.com/)下載AEM。 業務夥伴可以向&#x200B;[**spphelp@adobe.com**](mailto:spphelp@adobe.com)&#x200B;要求下載存取權。

AEM軟體套件有兩種形式：

* **CQ AEM 6.5 LTS jar：**&#x200B;獨立的可執行檔&#x200B;*jar*&#x200B;檔案，包含您需要執行的所有專案。

* **CQ AEM 6.5 LTS WAR：**&#x200B;要部署在協力廠商應用程式伺服器中的&#x200B;*war*&#x200B;檔案。

在以下章節中，我們將說明&#x200B;**獨立安裝**。 如需在應用程式伺服器中安裝AEM的詳細資訊，請參閱[應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)。

### 預設本機安裝 {#default-local-install}

1. 在本機電腦上建立安裝目錄。 例如：

   UNIX®安裝位置： **/opt/aem**

   Windows安裝位置： **`C:\Program Files\aem`**

   同樣地，將範例執行個體直接安裝在案頭上的資料夾中也是很常見的做法。 無論如何，Adobe一般會將此位置稱為：

   `<aem-install>`

   *檔案目錄的路徑只能包含美國ASCII字元。*

1. 將&#x200B;**jar**&#x200B;和&#x200B;**license**&#x200B;檔案放置在此目錄中：

   ```shell
   <aem-install>/
       <aem-65-lts>.jar
       license.properties
   ```

   如果您未提供`license.properties`檔案，AEM會在啟動時將瀏覽器重新導向至&#x200B;**歡迎**&#x200B;畫面，您可以在其中輸入授權金鑰。 如果您還沒有授權金鑰，則需要向Adobe索取有效的授權金鑰。

1. 若要在GUI環境中啟動執行個體，請連按兩下&#x200B;**`<aem-65-lts>.jar`**&#x200B;檔案。

   或者，您可以從命令列啟動AEM：

   ```shell
       java -Xmx1024M -jar <aem-65-lts>.jar
   ```

AEM需要幾分鐘來解壓縮jar檔案、自行安裝並啟動。 上述程式會產生：

* **AEM作者**&#x200B;執行個體
* 正在&#x200B;**localhost**&#x200B;上執行
* 在連線埠&#x200B;**4502**&#x200B;上

若要存取執行個體，請將瀏覽器指向：

**`https://localhost:4502`**

作者執行個體中的結果將會自動設定為連線到&#x200B;**`localhost:4503`**&#x200B;上的&#x200B;**發佈執行個體**。

### 製作和發佈安裝 {#author-and-publish-installs}

預設安裝（在&#x200B;**`localhost:4502`**&#x200B;上的&#x200B;**作者**&#x200B;執行個體）只需在第一次啟動`jar`檔案之前重新命名檔案即可變更。 命名模式為：

**`cq-<instance-type>-p<port-number>.jar`**

例如，將檔案重新命名為

**`cq-author-p4502.jar`**

啟動後，會在&#x200B;**`localhost:4502`**&#x200B;上執行製作執行個體。

同樣地，重新命名和啟動檔案

**`cq-publish-p4503.jar`**

導致發佈執行個體在&#x200B;**`localhost:4503`**&#x200B;上執行。

例如，您可將這兩個例項安裝在中

`<aem-install>/author`和

**`<aem-install>/publish`**

如需自訂安裝的詳細資訊，請參閱下列內容：

* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
<!-- * [Run Modes](/help/sites-deploying/configure-runmodes.md) -->

### 解壓縮的安裝目錄 {#unpacked-install-directory}

第一次啟動快速入門jar時，它會在名為`crx-quickstart`的新子目錄下將自身解壓縮到相同的目錄中。 您應該具備下列條件：

```xml
<aem-install>/
    license.properties
    <aem-65-lts>.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

如果從UI安裝執行個體，瀏覽器視窗會自動開啟，案頭應用程式視窗也會開啟，顯示執行個體的主機和連線埠，以及開啟/關閉開關：

![啟動畫面](assets/screen_shot_.png)

### 啟動和停止 {#starting-and-stopping}

當AEM自行解壓縮並首次啟動後，在安裝目錄中連按兩下jar檔案即可啟動執行個體，但不會重新安裝。

若要從GUI停止執行個體，請按一下案頭應用程式視窗上的&#x200B;**開啟/關閉**&#x200B;開關。

您也可以從命令列停止和啟動AEM。 假設您已經第一次安裝執行個體，**命令列指令碼**&#x200B;就在這裡：

**`<aem-install>/crx-quickstart/bin/`**

此資料夾包含下列UNIX® bash shell指令碼：

* **`start`**：啟動執行個體
* `stop`：停止執行個體
* **`status`**：報告執行個體的狀態
* **`quickstart`**：用來設定啟動資訊（如有必要）。

也有等同於Windows的&#x200B;**`bat`**&#x200B;檔案。 如需詳細資訊，請參閱：

* [命令列啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM會啟動，並自動將您的網頁瀏覽器重新導向至適當的頁面，通常是登入頁面；例如：

`https://localhost:4502/`

![登入畫面](assets/screen_shot_2019-04-08at83533am.png)


登入後，您就能存取AEM。 如需詳細資訊，請參閱下列內容（視您的角色而定）：

* [製作](/help/sites-authoring/first-steps.md)
* [管理](/help/sites-administering/home.md)
* [開發](/help/sites-developing/getting-started.md)
* [管理](/help/managing/best-practices.md)

## 進階部署 {#advanced-deployment}

上節應能讓您充分瞭解AEM安裝的基本概念。 不過，安裝AEM的完整生產系統可能會相當複雜。 如需進階安裝的完整涵蓋範圍，請參閱下列子頁面：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [命令列啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [升級至AEM 6.5 LTS](/help/sites-deploying/upgrade.md)
* [設定作法文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md)
* [最佳實務](/help/sites-deploying/best-practices.md)
* [AEM平台簡介](/help/sites-deploying/platform.md)

