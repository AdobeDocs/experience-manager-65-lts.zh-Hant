---
title: Database Credential Store安裝指南（獨立模式）
description: 在獨立模式下，尋找JBoss/Red Hat EAP上AEM Forms JEE的資料庫認證存放區設定。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: 259cb81eb9652405dc7270535cbf9deb996ad2ac
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# Database Credential Store安裝指南（獨立模式）

## 概觀

本指南涵蓋&#x200B;**獨立模式**&#x200B;下JBoss/Red Hat EAP上AEM Forms JEE的&#x200B;**資料庫認證存放區設定**。 執行手動安裝時需要此資訊。

**本指南涵蓋：**

- 正在建立資料庫認證存放區(`cred-store.p12`)
- 安全地新增資料庫密碼別名
- 設定JBoss以使用認證存放區

**嚴重：**&#x200B;這些指令碼僅在&#x200B;**離線模式中運作**。 執行這些指令碼之前，必須先停止JBoss。 指令碼使用`embed-server`模式，這要求伺服器停止。

**注意：**&#x200B;這&#x200B;**不是**&#x200B;完整的獨立安裝指南。 本檔案假設：

- 已安裝JBoss
- 獨立組態檔（`lc_oracle.xml`、`lc_mysql.xml`或`lc_mssql.xml`）已設定
- 資料庫已設定並可存取

如果您需要完整的獨立安裝指示，請參閱主要安裝指南。

## 先決條件

在執行這些指令碼之前，請確定：

1. **JBoss必須停止**
   - 這些指令碼僅能在&#x200B;**離線模式中運作**
   - 指令碼使用`embed-server`，這要求伺服器停止
   - 如果JBoss正在執行，指令碼將會失敗
   - 檢查JBoss是否正在執行：
      - Windows：檢查`java.exe`處理序的工作管理員
      - Linux： `ps aux | grep jboss`或`ps aux | grep java`
   - 停止JBoss （若正在執行）：
      - 在執行JBoss的終端機中按`Ctrl+C`
      - 或手動終止處理序

2. **您已準備好資料庫密碼**

3. **您已決定認證存放區的安全密碼**

4. **您知道要使用哪個資料庫組態檔：**
   - `lc_oracle.xml` (適用於Oracle資料庫)
   - `lc_mysql.xml` （適用於MySQL資料庫）
   - `lc_mssql.xml` (適用於Microsoft SQL Server資料庫)

## 設定步驟

### 步驟1：建立資料庫認證存放區

使用提供的指令碼建立資料庫認證存放區並新增所有必要的密碼別名。

#### 在Windows上：

**指令碼位置：** `create-elytron-cred-standalone.bat`

`batch cd path\to\script\location create-elytron-cred-standalone.bat`

**指令碼會提示您輸入：**
1. **JBOSS_HOME路徑** （例如`C:\Adobe\Adobe_Experience_Manager_Forms\jboss`）
2. **設定檔名稱** （例如，`lc_oracle.xml`、`lc_mysql.xml`或`lc_mssql.xml`）
3. **認證存放區密碼** （這可以保護金鑰存放區檔案 — 記住此密碼）
4. **資料庫密碼** （您實際的資料庫密碼）

**指令碼的作用：**

- 建立認證存放區： `JBOSS_HOME\standalone\configuration\cred-store.p12`
- 暫時修改設定檔案以啟用認證存放區建立
- 使用資料庫密碼新增下列別名：
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 將組態檔還原至其原始狀態
- 驗證所有別名是否已成功新增

#### 在Linux上：

**指令碼位置：** `create-elytron-cred-standalone.sh`

`bash cd /path/to/script/location chmod +x create-elytron-cred-standalone.sh./create-elytron-cred-standalone.sh`

**指令碼會提示您輸入：**

1. **JBOSS_HOME路徑** （例如`/opt/Adobe/Adobe_Experience_Manager_Forms/jboss`）
2. **設定檔名稱** （例如，`lc_oracle.xml`、`lc_mysql.xml`或`lc_mssql.xml`）
3. **認證存放區密碼** （這可以保護金鑰存放區檔案 — 記住此密碼）
4. **資料庫密碼** （您實際的資料庫密碼）

**指令碼的作用：**

- 建立認證存放區： `JBOSS_HOME/standalone/configuration/cred-store.p12`
- 暫時修改設定檔案以啟用認證存放區建立
- 使用資料庫密碼新增下列別名：
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 將組態檔還原至其原始狀態
- 驗證所有別名是否已成功新增

**預期輸出：**

```
=== JBoss Elytron Credential Store Setup ===
Enter JBOSS_HOME path (e.g. /opt/jboss): /opt/Adobe/Adobe_Experience_Manager_Forms/jboss
Enter configuration file name (e.g. lc_oracle.xml): lc_oracle.xml
Enter credential store password: ********
Confirm credential store password: ********
Enter database password: ********
Creating credential store using JBoss CLI...
Adding aliases to credential store...
Verifying credential store aliases...

All 4 aliases verified successfully!
- EncryptDBPassword
- EncryptDBPassword_IDP_DS
- EncryptDBPassword_EDC_DS
- EncryptDBPassword_AEM_DS

Credential store setup completed successfully!
```

### 步驟2：更新獨立組態檔

執行指令碼後，您需要設定JBoss在啟動時讀取認證存放區密碼。

#### 在Windows上：

**檔案位置：** `<JBOSS_HOME>\bin\standalone.conf.bat`

範例：`C:\Adobe\Adobe_Experience_Manager_Forms\jboss\bin\standalone.conf.bat`

新增或更新下列行：

```batch
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourActualPassword123"
```

以您在步驟1中使用的`YourActualPassword123`認證存放區密碼&#x200B;**取代**。

#### 在Linux上：

**檔案位置：** `<JBOSS_HOME>/bin/standalone.conf`

範例：`/opt/Adobe/Adobe_Experience_Manager_Forms/jboss/bin/standalone.conf`

新增或更新下列行：

```bash
JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourActualPassword123"
```

以您在步驟1中使用的`YourActualPassword123`認證存放區密碼&#x200B;**取代**。

### 步驟3：啟動JBoss

完成認證存放區設定後，請使用適當的設定檔案啟動JBoss。

**注意：**&#x200B;如需以獨立模式啟動JBoss的確切啟動命令和程式，請參閱&#x200B;**主要安裝指南**。 啟動命令可能會依您的特定組態和資料庫型別（`lc_oracle.xml`、`lc_mysql.xml`或`lc_mssql.xml`）而有所不同。

## 驗證

### 檢查伺服器記錄檔

**記錄檔位置：**

- Windows： `<JBOSS_HOME>\standalone\log\server.log`
- Linux： `<JBOSS_HOME>/standalone/log/server.log`

**尋找成功的啟動訊息：**

```
INFO  [org.jboss.as.server] WFLYSRV0025: JBoss EAP started
INFO  [org.jboss.as.connector.deployers.jdbc] Bound data source [java:/AdobeDataSource]
```

**沒有與**&#x200B;相關的錯誤

- 正在載入認證存放區
- 資料庫連線
- 缺少別名

## 疑難排解

### 問題1：找不到認證存放區

**錯誤訊息：**

```
ERROR Unable to load credential store
```

**解決方案：**

1. 確認認證存放區檔案存在：
   - Windows： `dir <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux： `ls -l <JBOSS_HOME>/standalone/configuration/cred-store.p12`
2. 如果遺失，請重新執行認證存放區建立指令碼（步驟1）

### 問題2：錯誤的認證存放區密碼

**錯誤訊息：**

```
ERROR Unable to load credential store - Invalid password
```

**解決方案：**
驗證`standalone.conf.bat` / `standalone.conf` （步驟2）中的密碼是否與建立認證存放區（步驟1）時使用的密碼相符。

要修正的&#x200B;**：**
編輯`standalone.conf.bat` / `standalone.conf`並更新密碼：

```
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=CorrectPassword"
```

### 問題3：資料庫連線失敗

**錯誤訊息：**

```
ERROR Failed to obtain connection
```

**解決方案：**

1. 驗證認證存放區中使用的資料庫密碼是否正確
2. 檢查資料來源設定是否參考正確的別名
3. 驗證資料庫伺服器的網路連線

**若要重新建立認證存放區：**

1. 停止JBos
2. 刪除現有的認證存放區：
   - Windows： `del <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux： `rm <JBOSS_HOME>/standalone/configuration/cred-store.p12`
3. 使用正確的資料庫密碼重新執行認證存放區建立指令碼

### 問題4：執行期間指令碼失敗

**錯誤訊息：**

```
ERROR: jboss-cli.bat is not found
```

**解決方案：**
請確認JBOSS_HOME路徑是否正確，並指向JBoss安裝目錄。

**錯誤訊息：**

```
ERROR: Configuration file not found
```

**解決方案：**

1. 確認組態檔名稱是否正確
2. 檢查檔案是否存在於`JBOSS_HOME\standalone\configuration\`目錄中
3. 確定您使用正確的資料庫特定組態檔

## 快速參考

### 資料庫認證存放區（獨立模式）

**用途：**&#x200B;安全地儲存資料庫密碼

**指令碼：**

- Windows： `create-elytron-cred-standalone.bat`
- Linux： `create-elytron-cred-standalone.sh`

**建立：**

- 檔案： `standalone/configuration/cred-store.p12`
- 別名： `EncryptDBPassword`， `EncryptDBPassword_IDP_DS`， `EncryptDBPassword_EDC_DS`， `EncryptDBPassword_AEM_DS`

**設定：**

- 變數： `-DCS_PASS=password`
- 檔案： `standalone.conf.bat` (Windows)或`standalone.conf` (Linux)

