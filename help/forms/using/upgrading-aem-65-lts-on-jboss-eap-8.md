---
title: 在JBoss EAP 8 (Windows)上升級AEM 6.5 LTS
description: 本指南逐步說明如何使用JDK 21，將現有Adobe Experience Manager (AEM) 6.5 LTS安裝從Windows上的JBoss EAP 7.4升級為JBoss EAP 8。
source-git-commit: 835530039678bc16a6de87b8d580be91a2026f94
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 3%

---

# 在JBoss EAP 8 (Windows)上升級AEM 6.5 LTS

## 概觀

本指南逐步說明如何使用JDK 21，將現有Adobe Experience Manager (AEM) 6.5 LTS安裝從Windows上的JBoss EAP 7.4升級為JBoss EAP 8。

**升級路徑：** JBoss EAP 7.4 (JDK 11) → JBoss EAP 8 (JDK 21)

## 重要通知

>[!NOTE]
>
>這是關鍵的升級程式。 請一律先在非生產環境中執行此升級，並維護完整的備份。
>
> **先決條件：**在繼續之前，必須先完成系統備份及記錄的復原計畫。

## 升級前需求

### 系統要求

| 元件 | 需求 |
|-----------|-------------|
| 作業系統 | Windows Server 2016或更新版本（64位元） |
| Source環境 | JBoss EAP 7.4搭配AEM 6.5 LTS |
| 目標環境 | JBoss EAP 8.x |
| Java Development Kit | JDK 21 （Oracle或OpenJDK） |
| AEM 版本 | AEM 6.5 Service Pack （最新建議版本） |
| 磁碟空間 | 升級程式的最少50 GB可用空間 |

### 必要的下載

開始升級前，請先取得下列資料：

1. **JBoss EAP 8.0發佈**\
   下載來源： [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. **JDK 21安裝程式**\
   下載Windows版（64位元）Oracle JDK 21或OpenJDK 21

3. **AEM 6.5 LTS WAR檔案**\
   從AEM Software Distribution取得最新的Adobe 6.5 Service Pack WAR

## 步驟1：建立完整備份

>[!IMPORTANT]
>
> 繼續之前，請先執行完整的備份。

### 備份檢查清單

- [ ]現有JBoss EAP 7.4安裝目錄的完整備份
- [ ]資料夾的`crx-repository`備份
- [ ]資料夾的`crx-quickstart`備份
- [ ]匯出所有自訂設定
- [ ]資料庫備份（如果使用外部資料庫）
- [ ]記錄目前的系統狀態和設定

### 建立備份

```cmd
# Example backup location
C:\AEM-Backups\Pre-Upgrade-<date>

# Copy entire JBoss 7.4 directory
xcopy "C:\jboss-eap-7.4" "C:\AEM-Backups\Pre-Upgrade-<date>\jboss-eap-7.4" /E /I /H
```

**建議：**&#x200B;將備份存放於不同的磁碟機或網路位置。

## 步驟2：安裝JBoss EAP 8

### 擷取JBoss EAP 8

1. 將JBoss EAP 8 ZIP散發解壓縮至您的目標安裝目錄：

   ```
   C:\jboss-eap-8.0
   ```

2. 請將此目錄路徑記為`<JBOSS_HOME>`，以便在本指南中使用。

### 復寫目錄結構

請確認新的JBoss EAP 8安裝與先前的JBoss EAP 7.4安裝具有相同的自訂目錄結構，特別是：

- 自訂部署目錄
- 外部設定資料夾
- 記錄檔位置
- 任何自訂模組或程式庫

## 步驟3：移轉存放庫資料

### 複製CRX存放庫

1. 導覽至現有的JBoss EAP 7.4安裝：

   ```
   <OLD_JBOSS_HOME>\bin\crx-repository
   ```

2. 將整個`crx-repository`資料夾複製到新的JBoss EAP 8安裝：

   ```cmd
   xcopy "C:\jboss-eap-7.4\bin\crx-repository" "C:\jboss-eap-8.0\bin\crx-repository" /E /I /H
   ```

**重要：**&#x200B;此資料夾包含您的內容存放庫，必須完全傳輸。

### 驗證存放庫副本

複製後，請驗證存放庫大小和結構是否符合來源：

```cmd
dir "C:\jboss-eap-8.0\bin\crx-repository" /s
```

## 步驟4：停止AEM例項

在進行任何變更之前，請確保AEM已完全停止。

### 透過Windows服務停止

1. 開啟&#x200B;**服務** （執行： `services.msc`）
2. 找到您的AEM/JBoss服務
3. 按一下滑鼠右鍵並選取&#x200B;**停止**
4. 等待服務完全停止

### 透過命令列停止

如果AEM是手動啟動：

1. 前往JBoss主控台視窗
2. 按`Ctrl+C`
3. 等待正常關機完成

### 驗證關機

確認Java程式已不再執行：

```cmd
tasklist | findstr java
```

## 步驟5：清理舊版AEM檔案

從`crx-quickstart`目錄移除過時的檔案，以確保升級完全正常。

>[!CAUTION]
>
> 僅刪除下列的特定檔案和資料夾。 請勿移除任何其他組態檔、自訂程式碼或存放庫資料。

### 5.1移除Launchpad啟動資料夾

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\startup
```

**動作：**

```cmd
rd /s /q "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\startup"
```

**用途：**&#x200B;此資料夾包含升級期間將重新產生的舊OSGi組合。

### 5.2移除基底JAR檔案

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar
```

**動作：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar"
```

**用途：**&#x200B;此JAR將由新WAR檔案中的版本取代。

### 5.3移除Bootstrap命令檔案

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt
```

**動作：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt"
```

**用途：**&#x200B;將針對新環境重新產生Bootstrap命令。

### 5.4移除sling.options檔案

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file
```

**動作：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file"
```

### 5.5移除sling_bootstrap.txt檔案

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt
```

**動作：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt"
```

### 5.6備份並移除sling.properties檔案

此檔案包含環境特定的設定，這些設定稍後可能需要合併。

**位置：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
```

**動作：**

1. **建立備份：**

   ```cmd
   copy "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties" "C:\AEM-Backups\sling.properties.backup"
   ```

2. **刪除原始檔案：**

   ```cmd
   del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties"
   ```

**用途：**&#x200B;將產生新的`sling.properties`。 請檢閱您的備份，以在升級後還原任何自訂設定。

## 步驟6：安裝和設定JDK 21

### 安裝JDK 21

1. 執行Windows適用的JDK 21安裝程式
2. 安裝到標準位置（例如，`C:\Program Files\Java\jdk-21`）
3. 完成安裝精靈

### 設定環境變數

#### 設定JAVA_HOME

1. 開啟&#x200B;**系統屬性** → **進階** → **環境變數**
2. 在&#x200B;**系統變數**&#x200B;下，按一下&#x200B;**新增**
3. 設定：
   - 變數名稱： `JAVA_HOME`
   - 變數值： `C:\Program Files\Java\jdk-21`
4. 按一下&#x200B;**確定**

#### 更新路徑變數

1. 在&#x200B;**系統變數**&#x200B;中，選取`Path`並按一下&#x200B;**編輯**
2. 新增專案：

   ```
   %JAVA_HOME%\bin
   ```

3. 將此專案移至清單頂端，以確保JDK 21優先
4. 在所有對話方塊上按一下&#x200B;**確定**

### 驗證Java安裝

1. 開啟&#x200B;**新**&#x200B;命令提示字元（以載入更新的環境變數）
2. 驗證Java版本：

   ```cmd
   java -version
   ```

   預期輸出：

   ```
   java version "21.0.x"
   Java(TM) SE Runtime Environment (build 21.0.x+...)
   Java HotSpot(TM) 64-Bit Server VM (build 21.0.x+..., mixed mode, sharing)
   ```

3. 驗證JAVA_HOME：

   ```cmd
   echo %JAVA_HOME%
   ```

## 步驟7：設定JVM設定

部署AEM之前，請先設定適當的JVM記憶體設定以供生產使用。

### 編輯standalone.conf.bat

1. 瀏覽到:

   ```
   <JBOSS_HOME>\bin
   ```

2. 在文字編輯器中開啟`standalone.conf.bat` （以系統管理員身分）

3. 尋找或新增`JAVA_OPTS`組態：

   ```batch
   rem # AEM Production JVM Settings
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=768m"
   set "JAVA_OPTS=%JAVA_OPTS% -Djava.net.preferIPv4Stack=true"
   set "JAVA_OPTS=%JAVA_OPTS% -Dfile.encoding=UTF-8"
   set "JAVA_OPTS=%JAVA_OPTS% -server"
   ```

4. 儲存並關閉檔案

**建議的設定：**

| 參數 | 建議值 | 說明 |
|-----------|-------------------|-------------|
| `-Xms` | 4096m - 8192m | 初始棧積大小 |
| `-Xmx` | 4096m - 8192m | 棧積大小上限 |
| `-XX:MaxMetaspaceSize` | 768m - 1024m | Metaspace限制 |

**注意：**&#x200B;根據伺服器的可用記憶體和工作負載需求調整值。

## 步驟8：部署AEM 6.5 LTS WAR

### 準備WAR

確保您的AEM WAR檔案已依照部署指南正確設定：

- `jboss-deployment-structure.xml`已存在
- `web.xml`包含多部分組態設定
- 若進行任何修改，WAR會重新封裝

### 部署至JBoss

1. 將AEM 6.5 LTS WAR檔案複製到部署目錄：

   ```cmd
   copy "C:\AEM-Downloads\cq-quickstart-6.5.xx.war" "C:\jboss-eap-8.0\standalone\deployments\cq-quickstart.war"
   ```

**重要：**&#x200B;請確定WAR檔案名稱符合您想要的URL內容路徑。

## 步驟9：使用AEM啟動JBoss EAP 8

### 啟動伺服器

1. 以&#x200B;**管理員**&#x200B;身分開啟&#x200B;**命令提示字元**

2. 導覽至JBoss bin目錄：

   ```cmd
   cd C:\jboss-eap-8.0\bin
   ```

3. 啟動JBoss EAP 8：

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

### 監視初始啟動

觀看主控台輸出：

1. **WAR部署：**

   ```
   Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
   ```

2. **AEM初始化訊息：**

   ```
   Apache Sling Application Launcher
   Sling Home: crx-repository/crx-quickstart
   ```

3. **存放庫升級（如果適用）：**

   ```
   Performing repository migration...
   ```

**預期啟動時間：** 5-15分鐘，視存放庫大小和系統資源而定。

## 步驟10：確認升級成功

### 檢查AEM啟動

監視JBoss主控台以取得最終的啟動訊息：

```
**** AEM started successfully ****
```

### 存取AEM介面

1. 開啟網頁瀏覽器
2. 瀏覽到:

   ```
   http://localhost:8080/cq-quickstart
   ```

3. 使用管理員憑證登入：
   - 使用者名稱： `admin`
   - 密碼： `admin` （或您的自訂密碼）

### 驗證系統資訊

1. 瀏覽至&#x200B;**工具** → **作業** → **網頁主控台**

   ```
   http://localhost:8080/cq-quickstart/system/console
   ```

2. 按一下&#x200B;**系統資訊**

3. 驗證：

   - **JVM版本：**&#x200B;應該會顯示Java 21
   - **JBoss版本：**&#x200B;應顯示EAP 8.x
   - **AEM版本：**&#x200B;應顯示6.5.xx

### 檢查系統健康狀況

瀏覽至&#x200B;**工具** → **作業** → **診斷**&#x200B;以執行健康狀態檢查：

- 套件組合狀態：所有套件組合都應該是「作用中」
- 資源解析：應顯示健康狀態
- 查詢效能：檢閱是否有任何效能降低

## 升級後工作

### 還原自訂設定

1. 檢閱備份的`sling.properties`檔案
2. 將任何自訂執行模式或設定還原到新檔案：

   ```
   <JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
   ```

3. 如果設定已變更，請重新啟動AEM

### 更新復寫代理

1. 瀏覽至&#x200B;**工具** → **部署** → **復寫** → **作者代理程式**
2. 檢閱及測試所有復寫代理
3. 更新任何對舊伺服器路徑的硬式編碼參照

### 測試關鍵功能

- [ ]內容製作與發佈
- [ ]資產上傳與處理
- [ ]工作流程執行
- [ ]使用者驗證
- [ ]整合端點
- [ ]個自訂元件和範本

### 效能最佳化

1. 檢閱及清除任何臨時快取
2. 監視初始使用期間的系統效能
3. 視需要根據實際使用模式調整JVM設定

## 疑難排解

### 常見問題

| 問題 | 可能的原因 | 解決方案 |
|-------|---------------|----------|
| AEM無法啟動 | 不正確的Java版本 | 驗證`JAVA_HOME`點是否指向JDK 21 |
| 存放庫損毀錯誤 | 不完整的存放庫副本 | 從備份還原並重新複製存放庫 |
| OutOfMemoryError | 棧積記憶體不足 | 在`-Xmx`中增加`standalone.conf.bat` |
| 「已安裝」狀態的套件組合 | 缺少相依性 | 在Web主控台中檢查套件組合相依性 |
| 連線埠8080已在使用中 | 使用連線埠的其他服務 | 停止衝突的服務或變更JBoss連線埠 |

### 記錄檔位置

- **JBoss伺服器記錄檔：**\
  `<JBOSS_HOME>\standalone\log\server.log`

- **AEM錯誤記錄檔：**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\error.log`

- **AEM存取記錄檔：**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\access.log`

### 反轉程式

如果升級失敗且無法解析：

1. 停止JBoss EAP 8
2. 還原JBoss EAP 7.4的完整備份
3. 還原`crx-repository`資料夾
4. 驗證`JAVA_HOME`點至JDK 11 （如果回覆）
5. 啟動上一個環境

## 最佳做法

### 生產部署之前

- [ ]在開發環境中測試完整的升級程式
- [ ]在具備生產資料的中繼環境中測試
- [ ]記錄所有自訂設定和整合
- [ ]建立詳細的復原計畫
- [ ]在維護期間排程升級
- [ ]通知所有利害關係人計畫停機時間

### 成功升級後

- [ ]監視系統記錄檔48至72小時
- [ ]執行負載測試以識別效能問題
- [ ]更新系統檔案
- [ ]訓練團隊瞭解任何JBoss EAP 8差異
- [ ]封存所有升級檔案與備份

## 相關檔案

- [JBoss EAP 8移轉指南](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0/html/migration_guide/)
- [Adobe Experience Manager 6.5升級指南](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html)
- [AEM正在安裝Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

## 檔案資訊

| 欄位 | 值 |
|-------|-------|
| 檔案版本 | 1.0 |
| 最近更新 | 2026年2月 |
| AEM 版本 | 6.5 LTS |
| Source平台 | JBoss EAP 7.4 / JDK 11 |
| Target平台 | JBoss EAP 8.x / JDK 21 |
| 作業系統 | Windows Server |

**法律注意事項：** Adobe、Adobe Experience Manager和AEM是Adobe Inc.的註冊商標。JBoss和Red Hat是Red Hat， Inc.的註冊商標。
