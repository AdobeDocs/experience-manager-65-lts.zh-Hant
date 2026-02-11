---
title: 在OSGi上升級至AEM 6.5 Forms LTS
description: 您可以從AEM 6.5.22.0 Forms直接升級至AEM 6.5 Forms LTS。
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: b7aa877f9e782b0568adc7baa440dc630c690454
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 3%

---

# 在OSGi上升級至AEM 6.5 Forms LTS {#upgrade-to-aem-forms-osgi}

若要[從AEM 6.5升級至AEM 6.5 LTS](/help/sites-deploying/upgrade.md)，請升級至AEM 6.5.22.0 Forms或更新版本。 支援從AEM 6.5.22.0直接升級至AEM 6.5 Forms LTS。

如果您使用AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms、AEM 6.3 Forms、AEM 6.4 Forms或AEM 6.5 Forms，則無法直接升級至AEM 6.5 Forms LTS。 如需詳細的升級路徑，請參閱[升級路徑](/help/forms/using/upgrade.md)檔案。

升級至Service Pack AEM Forms 6.5.22.0後，請依照下列步驟升級至AEM 6.5 LTS Forms：

1. 安裝AEM Forms附加元件套件。 步驟如下：

   1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
   1. 選取標題功能表中可用的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
   1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中：
      1. 從&#x200B;**[!UICONTROL 解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
      1. 選取封裝的版本和型別。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
   1. 選取適用於您作業系統的封裝名稱，選取&#x200B;**[!UICONTROL 接受EULA條款]**，然後選取&#x200B;**[!UICONTROL 下載]**。
   1. 開啟[封裝管理員](/help/sites-administering/package-manager.md)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
   1. 選取封裝並按一下&#x200B;**[!UICONTROL 安裝]**。

      您也可以使用[AEM Forms發行版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)文章中所列的直接連結來下載套件。

      安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即停止伺服器。**&#x200B;在停止AEM Forms伺服器之前，請等候直到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在&lt;crx-repository>/error.log檔案中，而且記錄檔穩定。 另請注意，有些套件可能維持已安裝狀態。 您可以安全地忽略這些套裝程式的狀態。


      **使用下列其他JVM命令列引數重新啟動AEM執行個體**：
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      如果伺服器是透過指令碼或服務啟動，請更新以包含上述內容，這樣在後續重新啟動後也有效。

      >[!NOTE]
      >
      > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式），可能會導致AEM開發環境不一致。

1. 執行安裝後活動。

   * **執行移轉公用程式**

     移轉公用程式可讓舊版的最適化表單和通訊管理資產相容於AEM 6.5表單。 您可以從AEM Software Distribution下載公用程式。 如需設定及使用移轉公用程式的逐步資訊，請參閱[移轉公用程式](../../forms/using/migration-utility.md)。

     如果您使用[範例將草稿與提交元件](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)與資料庫整合，並從舊版升級，請在執行升級後執行下列SQL查詢：

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(若僅從AEM 6.2 Forms或舊版升級)重新設定Adobe Sign**

     如果您已在舊版AEM Forms中設定Adobe Sign，請從AEM雲端服務重新設定Adobe Sign 。 如需詳細資訊，請參閱[整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

   * **支援jQuery**

     在AEM 6.5 Forms中，jQuery的版本已更新至3.2.1，而jQuery UI版本已更新至1.12.1。AEM表單在&#x200B;**noConflict**&#x200B;模式下使用JQuery。 因此，如果您使用任何其他jQuery版本，則執行升級時不會顯示任何問題。 不過，當您升級至AEM 6.5 Forms時：

      * 確保您的自訂元件（如果有的話）與支援的jQuery版本相容。
      * 從自訂元件移除不支援的API。 如需已移除的API清單，請參閱[升級指南](https://jquery.com/upgrade-guide/3.0/)。 例如，會移除對load()、.unload()和.error() API的支援。 使用.on()方法取代上述的API。 例如，將$(&quot;img&quot;)。load(fn)變更為$(&quot;img&quot;)。on(&quot;load&quot;， fn)。

   * **(如果從AEM 6.2 Forms或舊版升級)重新設定分析和報表**

     在AEM 6.4 Forms中，無法使用曝光的來源和成功事件流量變數。 因此，當您從AEM 6.2 Forms或舊版升級時，AEM Forms會停止傳送資料至Adobe Analytics伺服器，且無法使用最適化表單的Analytics報表。 此外，AEM 6.4 Forms為表單分析版本引入流量變數，並為在欄位上逗留的時間量引入成功事件。 因此，請為您的AEM Forms環境重新設定分析和報表。 如需詳細步驟，請參閱[設定分析和報表](../../forms/using/configure-analytics-forms-documents.md)。

1. 請確認伺服器已順利升級，所有資料也已成功移轉，而且伺服器可正常運作。

   * **驗證套裝的狀態：**&#x200B;請確定所有套裝都處於作用中狀態。
   * **驗證復寫及反向復寫：**&#x200B;發佈、填寫及送出一些已移轉的表單。 同時驗證提交的資料。
   * **驗證對管理員和開發人員使用者介面的存取權：**&#x200B;從管理員帳戶登入AEM執行個體，並確認您擁有下列URL的存取權：

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >在AEM 6.4 Forms中，crx-repository的結構已變更。 如果從6.3 Forms升級至AEM 6.5 Forms，請使用變更的路徑進行重新建立的自訂。 如需已變更路徑的完整清單，請參閱[AEM中的Forms存放庫重組](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5)。


## 在JBoss EAP 8上部署AEM (Windows)

### 概觀

本指南逐步說明如何使用JDK 21，在Windows環境中JBoss Enterprise Application Platform (EAP) 8上部署Adobe Experience Manager (AEM)作為獨立OSGi WAR檔案。

### 系統要求

在開始部署流程之前，請確保您的環境符合以下要求：

| 元件 | 需求 |
|-----------|-------------|
| 作業系統 | Windows Server 2016或更新版本（64位元） |
| Java Development Kit | JDK 21 (Oracle或OpenJDK) |
| 應用程式伺服器 | JBoss EAP 8.x |
| AEM Distribution | AEM WAR檔案(取自Adobe) |

>[!NOTE]
>
> 驗證`JAVA_HOME`環境變數是否指向您的JDK 21安裝目錄。

### 步驟1：安裝JBoss EAP 8

#### 下載JBoss EAP

1. 導覽至Red Hat開發人員入口網站：\
   [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. 下載適用於Windows的JBoss EAP 8 ZIP散發。

#### 擷取JBoss EAP

1. 將下載的ZIP檔案解壓縮至您偏好的安裝目錄。

2. 請將此目錄路徑記為`<JBOSS_HOME>`，以便在本指南中使用。

   **範例：**\
   ```C:\jboss-eap-8.0```

### 步驟2：準備AEM WAR檔案

#### 取得AEM WAR

向AEM Software Distribution或您的Adobe代表取得Adobe WAR檔案。

#### 重新命名WAR檔案

重新命名WAR檔案，以反映您想要的URL內容路徑：

```
cq-quickstart.war
```

>[!IMPORTANT]
>
> WAR檔案名稱會決定應用程式的URL內容。 例如，`cq-quickstart.war`可在`/cq-quickstart`存取。


### 步驟3：設定AEM WAR

在&#x200B;**部署到JBoss之前，必須完成所有組態修改**。

#### 建立工作目錄

1. 建立暫存工作目錄：

   ```
   C:\aem\war-config
   ```

2. 將 `cq-quickstart.war` 複製到此目錄中。

#### 擷取WAR內容

1. 開啟&#x200B;**命令提示字元**&#x200B;並瀏覽至您的工作目錄：

   ```cmd
   cd C:\aem\war-config
   ```

2. 解壓縮WAR檔案：

   ```cmd
   jar -xvf cq-quickstart.war
   ```

   這會建立包含`WEB-INF`和其他應用程式檔案的目錄結構。

### 步驟4：設定JBoss部署Descriptor

#### 建立部署結構檔案

1. 導覽至您解壓縮的WAR中的`WEB-INF`目錄：

   ```cmd
   cd WEB-INF
   ```

2. 建立名為`jboss-deployment-structure.xml`的新檔案。

3. 新增下列XML內容：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jboss-deployment-structure xmlns="urn:jboss:deployment-structure:1.2">
       <deployment>
           <dependencies>
               <module name="jdk.unsupported" />
           </dependencies>
       </deployment>
   </jboss-deployment-structure>
   ```

4. 儲存並關閉檔案。

**用途：**&#x200B;此設定可讓您存取AEM所需的JDK內部模組。

### 步驟5：設定多部分上傳設定

>[!NOTE]
>
> 步驟5僅適用於&#x200B;**AEM Forms**。 如果您只設定&#x200B;**AEM**，則可以略過此步驟。


#### 修改web.xml

1. 在文字編輯器中開啟`WEB-INF\web.xml`。

2. 找出包含執行模式設定的`<servlet>`區段：

   ```xml
   <!-- Set the runmode per default to author -->
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

3. 將結尾的`</servlet>`標籤和前一行取代為：

   ```xml
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <multipart-config>
       <max-file-size>1048576000</max-file-size>
       <max-request-size>1048576000</max-request-size>
       <file-size-threshold>0</file-size-threshold>
   </multipart-config>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

4. 儲存並關閉`web.xml`。

**用途：**&#x200B;這些設定可為AEM Forms和數位資產管理啟用大型檔案上傳（最大1 GB）。

### 步驟6：重新封裝WAR檔案

完成所有組態變更後，重新封裝WAR檔案。

1. 導覽回包含擷取內容的工作目錄：

   ```cmd
   cd C:\aem\war-config
   ```

2. 建立新的WAR檔案：

   ```cmd
   jar -cvf cq-quickstart.war *
   ```

>[!IMPORTANT]
>
> 完成所有組態後，僅執行一次此步驟。

### 步驟7：部署並啟動AEM

#### 將WAR部署至JBoss

1. 將重新封裝的`cq-quickstart.war`複製到JBoss部署目錄：

   ```
   <JBOSS_HOME>\standalone\deployments
   ```

   **範例：**
   ```C:\jboss-eap-8.0\standalone\deployments```

#### 設定JVM設定（可選用，但建議使用）

啟動JBoss之前，請先設定JVM記憶體設定：

1. 在文字編輯器中開啟`<JBOSS_HOME>\bin\standalone.conf.bat`。

1. 修改或新增下列行以設定棧積記憶體：

   ```batch
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=512m"
   ```

>[!NOTE]
>
> 根據伺服器容量和AEM需求調整記憶體值。

1. 儲存並關閉檔案。

#### 啟動JBoss EAP

1. 以&#x200B;**系統管理員**&#x200B;的身份開啟&#x200B;**命令提示字元**。

1. 導覽至JBoss bin目錄：

   ```cmd
   cd <JBOSS_HOME>\bin
   ```

   **範例：**
   ```cmd cd C:\jboss-eap-8.0\bin```

1. 啟動JBoss伺服器：

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

   **引數：**
   * `-b 0.0.0.0` — 將伺服器繫結至所有網路介面
   * `-bmanagement 0.0.0.0` — 將管理介面繫結到所有網路介面

#### 監視部署

觀看主控台輸出中的部署訊息。 成功部署由以下指示：

```
Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
```

### 步驟8：存取AEM

部署完成且AEM已完全啟動後：

**AEM作者URL：**
```http://<server-ip>:8080/cq-quickstart```

**預設認證：**

* 使用者名稱： `admin`
* 密碼： `admin`

**重要：**&#x200B;請在第一次登入後立即變更預設密碼。

### 疑難排解

#### 常見問題

| 問題 | 解決方案 |
|-------|----------|
| 部署失敗並出現ClassNotFoundException | 確認`jboss-deployment-structure.xml`已正確設定 |
| 啟動期間發生OutOfMemoryError | 在`standalone.conf.bat`中增加棧積記憶體 |
| AEM不會在部署後啟動 | 檢查`<JBOSS_HOME>\standalone\log\server.log`中的JBoss記錄檔 |
| 無法在瀏覽器中存取AEM | 驗證防火牆設定允許連線埠8080 |

#### 記錄檔

* **JBoss伺服器記錄檔：** `<JBOSS_HOME>\standalone\log\server.log`
* **AEM錯誤記錄檔：**&#x200B;可在啟動後透過AEM Web Console取得\
  `http://<server-ip>:8080/cq-quickstart/system/console`

### 其他設定

#### 設定執行模式

若要變更AEM執行模式（製作/發佈），請在重新封裝WAR之前修改`sling.run.modes`中的`WEB-INF\web.xml`引數：

```xml
<init-param>
    <param-name>sling.run.modes</param-name>
    <param-value>publish</param-value>
</init-param>
```

#### 生產建議

針對生產環境：

* 在JBoss中設定SSL/TLS憑證
* 設定AEM復寫代理
* 設定Dispatcher以進行負載平衡
* 啟用自動備份
* 實作監控和警報

### 相關檔案

* [JBoss EAP 8檔案](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0)
* [Adobe Experience Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
* [AEM安裝與部署指南](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=zh-Hant)

### 檔案資訊

| 欄位 | 值 |
|-------|-------|
| 最近更新 | 2026年2月 |
| AEM 版本 | 6.5+ (LTS) |
| JBoss版本 | EAP 8.x |
| JDK版本 | 21 |
| Platform | Windows |


