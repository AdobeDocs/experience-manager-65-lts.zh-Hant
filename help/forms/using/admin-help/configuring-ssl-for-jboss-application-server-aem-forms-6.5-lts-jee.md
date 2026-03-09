---
title: 為JBoss應用程式伺服器設定SSL (AEM 6.5 LTS JEE)
description: 瞭解如何設定JBoss Application Server的SSL。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
exl-id: 8a2fbfdc-2b6a-4c9d-beab-1908a9261003
source-git-commit: e48d0604cc8fd1cf745aafa9c70aab17944f4882
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# 為JBoss應用程式伺服器設定SSL (AEM 6.5 LTS JEE)

## 概觀

若要在適用於Adobe Experience Manager (AEM) 6.5 LTS （在Java EE上執行）的JBoss Application Server上設定SSL，您必須啟用安全HTTPS通訊。 啟用SSL會加密使用者端與伺服器之間交換的資料，使其成為任何生產AEM Forms部署的關鍵安全需求。

此程式包含兩個主要階段：

- **取得SSL認證** — 透過產生自我簽署憑證或向憑證授權單位(CA)要求憑證的方式。
- **在JBoss上啟用SSL** — 透過JBoss CLI命令使用Elytron子系統。

在本指南中，使用了下列預留位置值：

- `[appserver root]` — 執行AEM Forms之JBoss應用程式伺服器的主目錄。
- `[type]` — 資料夾名稱會依執行的安裝型別而有所不同。
- `[JAVA_HOME]` — JDK安裝所在的目錄。

## 第1部分：建立SSL認證（自我簽署）

如果您沒有來自CA的憑證，可以使用Java `keytool`公用程式產生自我簽署SSL認證。 這適用於開發或測試環境。

### 步驟1 — 產生金鑰存放區

在命令提示字元中瀏覽至`[JAVA_HOME]/bin`，然後執行下列命令，將值取代為您的環境適當的值。 主機名稱必須是應用程式伺服器的完整網域名稱(FQDN)：

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

出現提示時，請輸入`keystore_password`。 請注意，金鑰庫的密碼和金鑰必須相同。

### 步驟2 — 將金鑰存放區複製到組態目錄

將產生的金鑰儲存庫複製到適合您安裝型別的設定資料夾：

```bash
# Windows Single Server
copy keystorename.keystore [appserver root]\standalone\configuration

# Windows Server Cluster
copy keystorename.keystore [appserver root]\domain\configuration

# Linux Single Server
cp keystorename.keystore [appserver root]/standalone/configuration

# Linux Server Cluster
cp keystorename.keystore [appserver root]/domain/configuration
```

### 步驟3 — 匯出憑證檔案

使用下列其中一個命令，從金鑰存放區匯出憑證：

```bash
# Single Server
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/standalone/configuration/keystorename.keystore

# Server Cluster
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/domain/configuration/keystorename.keystore
```

出現提示時輸入`keystore_password`。

### 步驟4 — 複製並驗證憑證

將`AEMForms_cert.cer`複製到組態目錄，然後驗證其內容：

```bash
# Copy (Linux Single Server example)
cp AEMForms_cert.cer [appserver root]/standalone/configuration

# Verify certificate contents (Single Server)
keytool -printcert -v -file [appserver root]/standalone/configuration/AEMForms_cert.cer

# Verify certificate contents (Server Cluster)
keytool -printcert -v -file [appserver root]/domain/configuration/AEMForms_cert.cer
```

### 步驟5 — 將憑證匯入Java信任存放區

匯入之前，請確定`cacerts`檔案是可寫入的：

```bash
# Windows: Right-click cacerts → Properties → deselect Read-only

# Linux:
chmod 777 [JAVA_HOME]/jre/lib/security/cacerts
```

然後匯入憑證：

```bash
keytool -import -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [JAVA_HOME]/jre/lib/security/cacerts
```

提示輸入密碼時，請輸入`changeit` （預設的Java Truststore密碼 — 如果密碼已變更，請洽詢您的管理員）。 當詢問&#x200B;**信任此憑證時？ [no]**，型別`yes`。 您應該會看到確認訊息： *「憑證已新增至金鑰存放區。」*

>[!NOTE]
>
> 如果您要從Workbench透過SSL連線至AEM Forms，您也必須在Workbench電腦上安裝憑證。

## 第2部分：使用Elytron子系統在JBoss上啟用SSL

取得SSL認證後，您現在可以透過JBoss CLI使用其Elytron安全性子系統在JBoss上啟用HTTPS。 繼續之前，請確認您的金鑰存放區檔案位於適當的設定目錄中。

>[!NOTE]
>
> 在Windows上，每個CLI指令都必須以單行輸入，不含換行符號。 將`keystorename.keystore`取代為您的實際檔案名稱，並將`changeit`取代為您的金鑰儲存區/金鑰密碼。

### 步驟6a — 建立Elytron金鑰存放區

```bash
/subsystem=elytron/key-store=aemKeyStore:add(
  path="keystorename.keystore",
  relative-to=jboss.server.config.dir,
  type="JKS",
  credential-reference={clear-text="changeit"})
```

如果您的金鑰存放區使用該格式，請以`JKS`取代`PKCS12`。

### 步驟6b — 建立Elytron金鑰管理員

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  credential-reference={clear-text="changeit"})
```

如果您的金鑰存放區包含多個憑證專案，請明確指定別名：

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  alias="AEMForms Cert",
  credential-reference={clear-text="changeit"})
```

### 步驟6c — 更新伺服器SSL內容

```bash
/subsystem=elytron/server-ssl-context=applicationSSC:write-attribute(
  name=key-manager,
  value=aemKeyManager)
```

### 步驟6d — 設定Undertow HTTPS接聽程式

將SSL內容連線至Undertow （JBoss Web伺服器）以啟用HTTPS監聽器：

```bash
/subsystem=undertow/server=default-server/https-listener=https:add(
  socket-binding=https,
  ssl-context=applicationSSC)
```

## 第3部分：重新啟動應用程式伺服器

完成Elytron設定後，請重新啟動JBoss以套用變更。

### Turnkey安裝（Windows服務）

- 開啟&#x200B;**控制檯>系統管理工具>服務**。
- 為Adobe Experience Manager表單&#x200B;**選取** JBoss。
- 選取「**動作>停止**」並等待服務停止。
- 選取&#x200B;**動作>開始**。

### 預先設定或手動JBoss安裝

從命令提示字元瀏覽至`[appserver root]/bin`：

```bash
# Stop the server
Windows: shutdown.bat -S
Linux:   ./shutdown.sh -S

# Wait until JBoss fully shuts down, then start the server
Windows: run.bat -c <profile>
Linux:   ./run.sh -c <profile>
```

## 第4部分：向憑證授權單位要求認證

在生產環境中，您應該使用由受信任的憑證授權單位(CA)所發行的憑證。 此程式包含產生金鑰組、建立憑證簽署要求(CSR)，然後匯入CA簽署的憑證。

### 產生金鑰存放區並建立CSR

導覽至`[JAVA_HOME]/bin`並產生金鑰存放區：

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

然後產生CSR以提交至您的CA：

```bash
keytool -certreq -alias "AEMForms Cert" \
  -keystore keystorename.keystore \
  -file AEMFormscertRequest.csr
```

將`.csr`檔案提交至您的CA。 收到已簽署的憑證後，請遵循以下步驟。

### 匯入CA簽署的憑證

請先匯入CA根憑證：

```bash
keytool -import -trustcacerts -file rootcert.pem \
  -keystore keystorename.keystore -alias root
```

如果瀏覽器尚未信任根憑證，也請將其匯入。 然後匯入CA簽署的憑證：

```bash
keytool -import -trustcacerts -file CACertificateName.crt \
  -keystore keystorename.keystore
```

>[!NOTE]
>
> 如果金鑰存放區中存在已匯入的CA簽署憑證將會取代任何現有的自我簽署公開憑證。

匯入CA憑證後，繼續進行「第2部分」（Elytron組態）中的&#x200B;**步驟6a-6d**，重新啟動伺服器（第3部分），並驗證SSL存取。

## 驗證SSL存取

重新啟動伺服器後，請透過HTTPS存取AEM Forms管理主控台，確認SSL正常運作。 JBoss的預設SSL連線埠是`8443`：

```
https://[host name]:8443/adminui
```

如果管理主控台透過HTTPS成功載入，則SSL已正確設定。 所有後續SSL連線均使用連線埠`8443`連線至AEM Forms。
