---
title: 預設為SSL/TLS
description: 瞭解如何在AEM 6.5中使用預設的SSL功能。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: 3fd6a54b-9220-4bb2-9625-4f459c4d3aa8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# 預設為SSL/TLS{#ssl-tls-by-default}

為了持續改善AEM的安全性，Adobe已推出一項預設稱為SSL的功能。 目的是鼓勵使用HTTPS來連線至AEM執行個體。

## 預設啟用SSL/TLS {#enabling-ssl-tls-by-default}

您可以從AEM首頁畫面按一下相關的收件匣訊息，開始依預設設定SSL/TLS。 若要存取「收件匣」，請按一下畫面右上角的鈴鐺圖示。 然後，按一下&#x200B;**全部檢視**。 這會顯示清單檢視中排序的所有警報清單。

在清單中，選取並開啟&#x200B;**設定HTTPS**&#x200B;警示：

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>如果&#x200B;**設定HTTPS**&#x200B;警示不在收件匣中，您可以前往&#x200B;*<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*&#x200B;直接導覽至HTTPS精靈

已為此功能建立名為&#x200B;**ssl-service**&#x200B;的服務使用者。 開啟警報後，系統就會引導您完成下列設定精靈：

1. 首先，設定存放區認證。 這些是&#x200B;**ssl-service**&#x200B;系統使用者金鑰存放區的認證，將包含HTTPS接聽程式的私密金鑰和信任存放區。

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 輸入認證後，請按一下頁面右上角的&#x200B;**下一步**。 然後，上傳用於SSL/TLS連線的相關私密金鑰和憑證。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >如需有關如何產生私密金鑰和憑證以搭配精靈使用的資訊，請參閱下面的[此程式](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard)。

1. 最後，指定HTTPS監聽器的HTTPS主機名稱和TCP連線埠。

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## 依預設自動化SSL/TLS {#automating-ssl-tls-by-default}

根據預設，有三種方法可自動化SSL/TLS。

### 透過HTTP POST {#via-http-post}

第一個方法涉及張貼至設定精靈正在使用的SSLSetup伺服器：

```shell
POST /libs/granite/security/post/sslSetup.html
```

您可以在POST中使用以下裝載來自動化設定：

```xml
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePassword"

test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePassword"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="privatekeyFile"; filename="server.der"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="certificateFile"; filename="server.crt"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="httpsPort"
8443
```

此servlet如同任何sling POST servlet，將以「200確定」或錯誤HTTP狀態碼回應。 您可以在回應的HTML內文中找到有關狀態的詳細資料。

以下是成功回應和錯誤的範例。

**成功範例** （狀態= 200）：

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>OK</title>
</head>
<body>
<h1>OK</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>200</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>SSL successfully configured</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>OK</dd>
<dt class='foundation-form-response-description'>Description</dt>
<dd>HTTPS has been configured on port 8443. The private key and
certificate were stored in the key store of the user ssl-service.
Take note of the key store password you provided. You need
it for any subsequent updating of the private key or certificate.</dd>
</dl>
<h2>Links</h2>
<ul class='foundation-form-response-links'>
<li><a class='foundation-form-response-redirect' href='/'>Done</a></li>
</ul>
</body>
</html>
```

**錯誤範例** （狀態= 500）：

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>Error</title>
</head>
<body>
<h1>Error</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>500</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>The provided file is not a valid key, DER format expected</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>Error</dd>
</dl>
</body>
</html>
```

### 透過封裝 {#via-package}

或者，您可以上傳已包含這些必要專案的套件，以自動化SSL/TLS設定：

* ssl服務使用者的金鑰存放區。 此檔案位於存放庫中的&#x200B;*/home/users/system/security/ssl-service/keystore*&#x200B;下。
* `GraniteSslConnectorFactory`設定

### 產生要與精靈一起使用的私密金鑰/憑證配對 {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

以下範例說明如何建立DER格式的自簽憑證，供SSL/TLS精靈使用。 根據作業系統安裝OpenSSL，開啟OpenSSL命令提示字元，並將目錄切換到您要產生私密金鑰/憑證的資料夾。

>[!NOTE]
>
>自我簽署憑證僅供範例使用。 請勿在生產環境中使用。

1. 首先，建立私密金鑰：

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. 接著，使用私密金鑰產生憑證申請檔(CSR)：

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj "/CN=localhost"
   ```

1. 產生SSL/TLS憑證並使用私密金鑰簽署。 在此範例中，將於一年後到期：

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

1. 將私密金鑰轉換為DER格式。 這是因為SSL精靈要求金鑰必須是DER格式：

   ```shell
   openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
   ```

1. 最後，在本頁開頭說明的圖形SSL/TLS精靈步驟2中，將&#x200B;**localhostprivate.der**&#x200B;上傳為私密金鑰，並將&#x200B;**localhost.crt**&#x200B;上傳為SSL/TLS憑證。

### 透過cURL更新SSL/TLS設定 {#updating-the-ssl-tls-configuration-via-curl}

>[!NOTE]
>
>請參閱[搭配AEM使用cURL](https://helpx.adobe.com/tw/experience-manager/6-4/sites/administering/using/curl.html)，以取得AEM中有用cURL命令的集中清單。

您也可以使用cURL工具自動化SSL/TLS設定。 您可以將設定引數張貼至此URL來執行此操作：

*https://&lt;serveraddress>：&lt;serverport>/libs/granite/security/post/sslSetup.html*

以下是您可以在設定精靈中用來變更各種設定的引數：

* `-F "keystorePassword=password"` — 金鑰庫密碼；

* `-F "keystorePasswordConfirm=password"` — 確認金鑰庫密碼；

* `-F "truststorePassword=password"` — 信任庫密碼；

* `-F "truststorePasswordConfirm=password"` — 確認信任庫密碼；

* `-F "privatekeyFile=@localhostprivate.der"` — 指定私密金鑰；

* `-F "certificateFile=@localhost.crt"` — 指定憑證；

* `-F "httpsHostname=host.example.com"` — 指定主機名稱；
* `-F "httpsPort=8443"` - HTTPS接聽程式將使用的連線埠。

>[!NOTE]
>
>執行cURL以自動化SSL/TLS設定的最快方式是來自DER和CRT檔案所在的資料夾。 或者，您可以在`privatekeyFile`和certificateFile引數中指定完整路徑。
>
>您也必須通過驗證才能執行更新，因此請務必附加cURL命令與`-u user:passeword`引數。
>
>正確的cURL post命令應如下所示：

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### 使用cURL的多個憑證 {#multiple-certificates-using-curl}

您可以重複certificateFile引數，向servlet傳送憑證鏈，如下所示：

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

執行命令後，請確認所有憑證都進入金鑰存放區。 檢查下列專案中的&#x200B;**金鑰存放區**&#x200B;專案：
[http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service)

### 啟用TLS 1.3連線 {#enabling-tls-connection}

1. 前往Web主控台
1. 接著，導覽至&#x200B;**OSGi** - **組態** - **Adobe Granite SSL Connector Factory**
1. 移至&#x200B;**包含的密碼套件**&#x200B;欄位，並新增下列專案。 您可以在下列專案新增每個專案後，按下欄位左側的&quot;**+**&quot;按鈕以確認每個新增：

   * `TLS_AES_256_GCM_SHA384`
   * `TLS_AES_128_GCM_SHA256`
   * `TLS_CHACHA20_POLY1305_SHA256`
   * `TLS_AES_128_CCM_SHA256`
   * `TLS_AES_128_CCM_8_SHA256`
