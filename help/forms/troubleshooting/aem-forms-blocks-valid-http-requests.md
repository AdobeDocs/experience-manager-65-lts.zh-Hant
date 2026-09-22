---
title: AEM Forms會封鎖有效的HTTP請求
description: AEM Forms XSS驗證檢查可為使用自訂元件的客戶封鎖有效的HTTP請求。 瞭解如何識別問題並暫時放鬆驗證檢查。
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin,Developer
exl-id: 10a02e57-7ff8-42d8-b31e-f714c0dd8338
source-git-commit: 4df5a9888532afd86562678a76c35841ac5634b8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%
---
# AEM Forms會封鎖有效的HTTP請求 {#aem-forms-blocks-valid-http-requests}

## 問題 {#issue}

AEM Forms包含安全性檢查，以防止跨網站指令碼(XSS)攻擊。 對於在AEM Forms中使用自訂元件的客戶，這些檢查可能會封鎖某些有效的HTTP請求。 當要求遭到封鎖時，下列訊息會出現在伺服器記錄中：

```text
Got Exception while Validating XSS: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000: org.owasp.esapi.errors.ValidationException: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000.
```

>[!NOTE]
>
>對於POST要求，引數的預設值為&#x200B;**1048576**。 對於GET要求，引數的預設值為&#x200B;**2000**。 若要修改POST要求的引數值，請在伺服器啟動期間傳遞`com.adobe.idp.dsc.provider.rest.httpParamMaxSize`引數。

## 原因 {#cause}

XSS驗證Regex比自訂元件傳送之引數值的格式更嚴格，因此AEM Forms會拒絕要求。

## 解決方法 {#resolution}

>[!CAUTION]
>
>移除安全性檢查會使系統容易受到跨網站指令碼(XSS)攻擊。 移除安全性檢查僅作為臨時解決方案。

暫時移除安全性檢查並允許所有HTTP請求：

1. 停止AEM Forms伺服器。

1. 建立`[AEM-Forms-Installation-Directory]/configurationManager/export/adobe-livecycle-<application_server_name>.ear`檔案的備份。

1. 從`adobe-livecycle-<server_name>.ear`檔案擷取`esapi-helper-2.x.x.jar`檔案。 每個應用程式伺服器的`esapi-helper-2.x.x.jar`檔案位置不同：

   | 應用程式伺服器 | esapi-helper-2.x.x.jar檔案的位置 |
   | --- | --- |
   | Jboss | `adobe-livecycle-jboss.ear/lib` |
   | Oracle Weblogic | `adobe-livecycle-weblogic.ear/APP-INF/lib` |
   | IBM WebSphere | `adobe-livecycle-websphere.ear/` |

1. 開啟`[extracted esapi-helper-2.x.x.jar]/esapi/validation.properties`和`[extracted esapi-helper-2.x.x.jar]/esapi/ESAPI.properties`檔案以進行編輯。

1. 將下列屬性的值設定為`^[\\s\\S]*$`。 例如 `Validator.HTTPParameterName=^[\\s\\S]*$`。 儲存並關閉檔案。

   * `Validator.HTTPQueryString`
   * `Validator.PMCallParameterName`
   * `Validator.PMCallParameterValue`
   * `Validator.HTTPParameterName`
   * `Validator.HTTPParameterValue`
   * `Validator.xssSafeString`

1. 在`adobe-livecycle-<application_server_name>.ear`中封裝更新的`esapi-helper-2.x.x.jar`。 將更新的`adobe-livecycle-<application_server_name>.ear`部署至應用程式伺服器。

1. 啟動AEM Forms伺服器。

## 參照 {#references}

* [緩解JEE 6.5 LTS SP2上AEM Forms的伺服器端請求偽造(SSRF)漏洞](/help/forms/troubleshooting/mitigating-server-side-request-forgery-vulnerabilities-for-aem-forms-on-jee-65-lts-sp2.md)
