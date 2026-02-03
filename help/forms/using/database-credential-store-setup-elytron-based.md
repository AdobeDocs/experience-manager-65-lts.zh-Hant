---
title: 資料庫認證存放區設定（Elytron型）
description: JBoss EAP 8支援Elytron認證存放區，以便在AEM Forms中安全地管理資料庫密碼，以進行網域模式設定。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: 259cb81eb9652405dc7270535cbf9deb996ad2ac
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 2%

---


# 資料庫認證存放區設定（Elytron型）

## 使用Elytron設定資料庫認證存放區

JBoss EAP 8使用&#x200B;**Elytron認證存放區**&#x200B;來安全地管理AEM Forms部署的資料庫密碼。 Adobe提供&#x200B;**自動化指令碼**，以簡化網域模式中Elytron認證存放區的建立和設定。

在啟動JBoss網域控制站&#x200B;**之前，必須先完成此設定**。

### 先決條件

* 在執行認證存放區建立指令碼之前，必須完全停止&#x200B;**JBoss伺服器**。
* 認證存放區建立僅能在&#x200B;**離線模式中執行**。

若要停止JBoss （若其正在執行）：

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

### 下載指令碼

根據您的作業系統下載適當的指令碼：

| 指令碼名稱 | 作業系統 |
| -------------------------------- | ---------------- |
| `create-elytron-cred-domain.bat` | Windows |
| `create-elytron-cred-domain.sh` | Linux / UNIX |

對於Linux，讓指令碼可執行：

```
chmod +x create-elytron-cred-domain.sh
```

### 設定步驟

#### 步驟1：下載並放置指令碼

下載適當的指令碼，並將其放在以下目錄中：

```
<JBOSS_HOME>/bin
```

#### 步驟2：執行指令碼

* **Windows**

  ```
  cd <JBOSS_HOME>\bin
  create-elytron-cred-domain.bat
  ```

* **Linux / UNIX**

  ```
  cd <JBOSS_HOME>/bin
  ./create-elytron-cred-domain.sh
  ```

#### 步驟3：提供必要資訊

在執行期間，指令碼會提示您輸入下列內容：

1. **JBOSS_HOME路徑**
輸入JBoss安裝目錄的完整路徑。

2. **資料庫組態檔名稱**
根據您的資料庫，輸入下列其中一項：

   * `domain_oracle.xml`
   * `domain_mysql.xml`
   * `domain_mssql.xml`

3. **認證存放區密碼**
輸入強式密碼以保護認證存放區。

   > 此密碼在輸入期間是隱藏的，必須在後續步驟中記住。

4. **資料庫密碼**
輸入實際的資料庫連線密碼。

#### 步驟4：指令碼執行與驗證

指令碼會自動執行下列動作：

* 建立`cred-store.p12`於：

  ```
  <JBOSS_HOME>/domain/configuration/
  ```

* 建立下列認證別名：

   * `EncryptDBPassword`
   * `EncryptDBPassword_IDP_DS`
   * `EncryptDBPassword_EDC_DS`
   * `EncryptDBPassword_AEM_DS`
* 驗證是否成功新增所有別名

成功執行可確認認證存放區建立和別名驗證。

#### 步驟5：設定JVM選項

更新JBoss網域啟動設定，以提供認證存放區密碼。

* **Linux**
編輯：

  ```
  <JBOSS_HOME>/bin/domain.conf
  ```

  新增：

  ```
  JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourCredStorePassword"
  ```

* **Windows**
編輯：

  ```
  <JBOSS_HOME>/bin/domain.conf.bat
  ```

  新增：

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourCredStorePassword"
  ```

以建立認證存放區時輸入的密碼取代`YourCredStorePassword`。

網域組態檔使用`${CS_PASS}`變數參考此值。


#### 步驟6：驗證網域設定

開啟資料庫網域設定檔：

```
<JBOSS_HOME>/domain/configuration/<domain_*.xml>
```

確認資料來源參考Elytron認證存放區：

```xml
<security>
    <user-name>your_database_username</user-name>
    <credential-reference store="db-creds" alias="EncryptDBPassword_IDP_DS"/>
</security>
```

每個資料來源都使用特定別名：

* **IDP_DS：** `EncryptDBPassword_IDP_DS`
* **EDC_DS：** `EncryptDBPassword_EDC_DS`
* **AEM_DS：** `EncryptDBPassword_AEM_DS`
* **DefaultDS / ExampleDS：** `EncryptDBPassword`

所有別名都參照儲存在認證存放區中的相同資料庫密碼。

>[!NOTE]
>
>* 只在主要節點上設定認證存放區。
>* 次要節點會自動使用與主要節點同步的網域設定。
