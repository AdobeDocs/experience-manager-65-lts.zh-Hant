---
title: 次要節點驗證設定（Elytron型）
description: JBoss EAP 8使用Elytron來啟用次要節點與主要網域控制站的安全通訊與註冊。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 3%

---


# 次要節點驗證設定（Elytron型）

## 使用Elytron設定次要節點驗證

JBoss EAP 8使用&#x200B;**Elytron**&#x200B;來驗證叢集部署中&#x200B;**主要和次要節點**&#x200B;之間的通訊。 此設定可確保次要節點與主要網域控制站的安全註冊與通訊。

視環境和安全需求而定，提供兩種設定選項。

## 先決條件

* 必須在&#x200B;**主要節點`secondary`**&#x200B;上建立名為&#x200B;**的**&#x200B;管理使用者。
* 只在次要節點&#x200B;**上執行此組態**。
* 重複叢集中&#x200B;**每個次要節點**&#x200B;的設定。
* 主要和次要節點上的&#x200B;**JBoss必須完全停止**。
* 所有認證存放區作業都必須在&#x200B;**離線模式**&#x200B;中執行。

若要停止JBoss （若其正在執行）：

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

## 選擇設定選項

* **選項1：使用預設認證存放區進行快速設定**
建議用於較低層級的環境和測試。

* **選項2：自訂認證存放區設定**
建議用於生產和安全環境。

## 選項1：使用預設認證存放區進行快速設定

**最適合：**&#x200B;開發、測試和快速設定案例。

### 概觀

* 預設的認證存放區檔案(`cs_secondary_hc.p12`)已預先設定。
* 預設的認證存放區密碼已在`domain.conf`中設定。
* 只需要新增驗證密碼別名。

### 設定步驟

#### 步驟1：驗證預設認證存放區

確認預設的認證存放區檔案存在：

* **Windows**

  ```
  <JBOSS_HOME>\domain\configuration\cs_secondary_hc.p12
  ```

* **Linux**

  ```
  <JBOSS_HOME>/domain/configuration/cs_secondary_hc.p12
  ```

如果檔案不存在，請使用&#x200B;**選項2**。

#### 步驟2：新增驗證密碼別名

從`<JBOSS_HOME>/bin`執行以下命令：

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

> 密碼值必須與在主要節點上建立`secondary`使用者時使用的密碼相符。

#### 步驟3：驗證domain.conf設定

確認下列專案已經存在（不需要變更）：

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=password"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=password"
  ```

#### 步驟4：啟動節點

1. 啟動&#x200B;**主要節點**&#x200B;並等待它完全初始化。
2. 啟動&#x200B;**次要節點**。

### 驗證

檢查記錄：

* **主要節點**

  ```
  <JBOSS_HOME>/domain/log/host-controller.log
  ```

  ```
  Registered remote secondary host "secondary"
  ```

* **次要節點**

  ```
  Connected to primary host controller
  ```

## 選項2：自訂認證存放區設定（生產）

**最適合：**&#x200B;需要增強式安全性的生產環境。

### 設定步驟

#### 步驟1：移除預設認證存放區（如果有的話）

如果預設的認證存放區存在，請將其重新命名：

* **Windows**

  ```
  rename cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

* **Linux**

  ```
  mv cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

#### 步驟2：建立自訂認證存放區

從`<JBOSS_HOME>/bin`：

* **Windows**

  ```
  elytron-tool.bat credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

#### 步驟3：新增驗證密碼別名

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

#### 步驟4：更新domain.conf

更新認證存放區密碼參考：

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=YourCustomPassword"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=YourCustomPassword"
  ```

#### 步驟5：驗證XML組態

請確定`host-secondary.xml`包含已設定的認證存放區和驗證使用者端專案。
如果預設設定存在，則不需要變更。


#### 步驟6：啟動節點

1. 啟動&#x200B;**主要節點**，然後等待完全啟動。
2. 啟動&#x200B;**次要節點**。

### 驗證

使用兩個節點上的主機控制器記錄確認註冊成功。

## 摘要

* **選項1**&#x200B;提供使用預先設定的認證存放區的快速設定。
* **選項2**&#x200B;使用自訂認證存放區密碼來啟用更強的安全性。
* 組態必須在次要節點上完成&#x200B;**，且只能完成**。
* 主要節點設定會在網域中自動重複使用。

