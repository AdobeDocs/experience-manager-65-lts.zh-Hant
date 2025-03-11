---
title: 應用程式伺服器安裝
description: 瞭解如何使用應用程式伺服器安裝Adobe Experience Manager。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 09d54b52-485a-453c-a2d0-535adead9e6c
source-git-commit: 5f968f5dc0696a683cc063d330c8edfba05f11ab
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# 應用程式伺服器安裝{#application-server-install}

>[!NOTE]
>
>`JAR`和`WAR`是Adobe Experience Manager (AEM)發行所在的檔案型別。 這些格式正在進行品質保證，以符合Adobe所承諾的支援等級。
>

本節將說明如何使用應用程式伺服器安裝Adobe Experience Manager (AEM)。 請參閱[支援平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers)區段，瞭解個別應用程式伺服器提供的特定支援等級。

以下應用程式伺服器的安裝步驟已說明：

* [WebSphere](#websphere)
* [Tomcat 11.0.x](#tomcat)

請參閱適當的應用程式伺服器檔案，以取得有關安裝Web應用程式、伺服器設定以及如何啟動和停止伺服器的詳細資訊。

<!-- >[!NOTE]
>
>If you are using Dynamic Media in a WAR deployment, see [Dynamic Media documentation](/help/assets/config-dynamic.md#enabling-dynamic-media). -->

## 一般說明 {#general-description}

### 在應用程式伺服器中安裝AEM時的預設行為 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM會以單一war檔案的形式進行部署。

如果部署，預設將會發生下列情況：

* 執行模式為`author`
* 執行個體（存放庫、Felix OSGI環境、套件組合等）的安裝位置為`${user.dir}/crx-quickstart`，其中`${user.dir}`為目前的工作目錄。 此crx-quickstart路徑稱為`sling.home`

* 內容根目錄是WAR檔案名稱。 例如，`aem-65-lts`。

#### 設定 {#configuration}

您可以透過下列方式變更預設行為：

* 執行模式：部署前在AEM war檔案的`WEB-INF/web.xml`檔案中設定`sling.run.modes`引數

* sling.home：在部署之前設定AEM war檔案`WEB-INF/web.xml`檔案中的`sling.home`引數

* 內容根目錄：重新命名AEM war檔案

#### 發佈安裝 {#publish-installation}

若要部署發佈執行個體，您必須將執行模式設定為發佈：

* 從AEM war檔案中解壓縮`WEB-INF/web.xml`
* 變更`sling.run.modes`引數以發佈
* 將`web.xml`檔案重新封裝到AEM war檔案中
* 部署AEM war檔案

#### 安裝檢查 {#installation-check}

若要檢查是否已安裝所有專案，您可以：

* 追蹤`error.log`檔案以檢視是否已安裝所有內容
* 檢視`/system/console`所有套件組合均已安裝

#### 同一應用程式伺服器上的兩個執行個體 {#two-instances-on-the-same-application-server}

為了示範，將製作和發佈執行個體同時安裝在同一部應用程式伺服器上可能是適當的。 若要達成此目的，您需要：

1. 變更發佈執行個體的`sling.home`變數和`sling.run.modes`變數
1. 從AEM war檔案中解壓縮`WEB-INF/web.xml`檔案
1. 將`sling.home`引數變更為不同的路徑（可以使用絕對和相對路徑）
1. 將發佈執行個體的`sling.run.modes`變更為`publish`
1. 重新封裝`web.xml`檔案
1. 重新命名war檔案，使其名稱不同。 例如，將其中一個重新命名為`aemauthor.war`，將另一個重新命名為`aempublish.war`
1. 使用較高的記憶體設定。 例如，預設AEM執行個體使用`-Xmx3072m`
1. 部署兩個網頁應用程式
1. 部署後，停止兩個Web應用程式
1. 在製作和發佈執行個體中，請確定在`sling.properties`檔案中，屬性`felix.service.urlhandlers`設定為`false`。 （預設值是設為`true`）。
1. 再次啟動兩個網頁應用程式。

## 應用程式伺服器的安裝程式 {#application-servers-installation-procedures}

### WebSphere® 24.0.0.7 {#websphere}

在部署之前，請閱讀上述[一般說明](#general-description)。

**伺服器準備**

* 讓基本驗證標題通過：

   * 讓AEM驗證使用者的一種方式是停用WebSphere®伺服器的全域管理安全性。 若要這麼做，請移至&#x200B;**安全性>全域安全性**&#x200B;並取消勾選&#x200B;**啟用系統管理安全性核取方塊**，儲存並重新啟動伺服器。

* 設定 `"JAVA_OPTS= -Xmx2048m"`
* 如果您想使用內容根目錄= /安裝AEM，請變更現有預設Web應用程式的內容根目錄。

**部署AEM Web應用程式**

* 下載AEM war檔案
* 如有需要，請在`web.xml`檔案中進行設定。 如需詳細資訊，請參閱上述[一般說明](#general-description)。

   * 解壓縮`WEB-INF/web.xml`檔案
   * 將`sling.run.modes`引數變更為`publish`
   * 取消註解初始`sling.home`引數，並視需要設定此路徑
   * 重新封裝`web.xml`檔案。

* 部署AEM war檔案

   * 選擇內容根目錄。 如果要設定sling執行模式，您需要選取部署精靈的詳細步驟，然後在精靈的步驟6中指定。

* 啟動AEM網路應用程式

#### Tomcat 11.0.x {#tomcat}

在部署之前，請閱讀上述[一般說明](#general-description)。

* **準備Tomcat伺服器**

   * 增加VM記憶體設定：

      * 在`bin/catalina.bat` (UNIX®上代表`catalina.sh`)中新增下列設定：

        ```
        set "JAVA_OPTS= -Xmx2048m`
        ```

   * Tomcat在安裝時不會啟用管理員或管理員存取權。 因此，您必須手動編輯`tomcat-users.xml`以允許這些帳戶的存取權：

      * 編輯`tomcat-users.xml`以包含管理員和管理員的存取權。 設定看起來應該類似下列範例：

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
        <role rolename="admin"/>
        <role rolename="role1"/>
        <role rolename="manager-gui"/>
        <user username="both" password="tomcat" roles="tomcat,role1"/>
        <user username="tomcat" password="tomcat" roles="tomcat"/>
        <user username="admin" password="admin" roles="admin,manager-gui"/>
        <user username="role1" password="tomcat" roles="role1"/>
        </tomcat-users>
        ```

   * 如果您想要使用內容根目錄「/」部署AEM，則必須變更現有ROOT Web應用程式的內容根目錄：

      * 停止並取消部署ROOT Web應用程式
      * 重新命名Tomcat的Webapps資料夾中的`ROOT.war`資料夾
      * 再次啟動Webapp

   * 如果您使用管理員gui安裝AEM Web應用程式，則需要增加已上傳檔案的最大大小，因為預設僅允許50MB上傳大小。 為了達成開啟管理員Web應用程式的`web.xml`的目的：

     `webapps/manager/WEB-INF/web.xml`

     並將`max-file-size`和`max-request-size`增加到至少500MB。 在下列範例`web.xml`檔案中檢視下列`multipart-config`：

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **部署AEM Web應用程式**

   * 下載AEM war檔案。
   * 如有需要，請在`web.xml`檔案中進行設定。

      * 解壓縮`WEB-INF/web.xml`檔案
      * 將`sling.run.modes`引數變更為`publish`
      * 取消註解初始`sling.home`引數，並視需要設定此路徑
      * 重新封裝`web.xml`檔案。

   * 如果您要將AEM war檔案部署為根Webapp，請將它重新命名為`ROOT.war`。 如果要將`aemauthor`重新命名為內容根目錄，請將其重新命名為`aemauthor.war`。
   * 將其複製到Tomcat的webapps資料夾
   * 等到安裝AEM為止。
