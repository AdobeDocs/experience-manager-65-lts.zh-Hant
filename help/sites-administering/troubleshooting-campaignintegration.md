---
title: 疑難排解Adobe Campaign Classic整合
description: 瞭解如何疑難排解Adobe Campaign Classic整合的問題。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: fc60d6a3-b2fd-4991-931f-22924ba8003d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# 疑難排解Adobe Campaign Classic整合{#troubleshooting-your-adobe-campaign-classic-integration}

瞭解如何疑難排解Adobe Campaign Classic (ACC)整合的問題。

下列疑難排解提示可協助您解決在將AEM與ACC整合時可能遇到的最常見問題。

## 一般疑難排解提示 {#general-troubleshooting-tips}

檢查這兩個解決方案(AEM > Adobe Campaign Classic、Adobe Campaign Classic > AEM)是否分別傳送及接收HTTP呼叫。 此秘訣可協助您避免防火牆/SSL問題。

* 針對AEM功能，您可以看到已從AEM作者介面要求JSON呼叫
   * 這些呼叫不應導致HTTP-500錯誤。
   * 如果您看到HTTP-500錯誤，請檢查`error.log`以取得詳細資訊。
* 在AEM中提高campaign類別的偵錯層級也有助於疑難排解問題。

## 如果連線失敗 {#when-the-connection-fails}

檢查您是否已在Adobe Campaign Classic中設定&#x200B;**`aemserver`**&#x200B;運運算元。

## 如果影像未顯示在Adobe Campaign Classic主控台中 {#if-images-do-not-appear-in-the-adobe-campaign-console}

檢查HTML來源，並確認您可以從使用者端電腦開啟URL。 如果URL中包含`localhost:4503`，請變更AEM作者執行個體上Day CQ Link Externalizer的設定。 讓它指向可從Adobe Campaign Classic主控台電腦存取的發佈執行個體。

請參閱[設定外部化程式。](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## 如果您無法從AEM連線至Adobe Campaign Classic  {#if-you-cannot-connect-from-aem-to-adobe-campaign}

在Adobe Campaign Classic中尋找下列錯誤訊息。

* `No datasource defined in the instance 'default'.`

* `Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

若要修正此問題，請在`$CAMPAIGN_HOME/conf/config-<instance-name>.xml`中變更下列專案：

* `<dataStore hosts="*" lang="en_GB">`

## 如果Adobe Campaign Classic對話方塊中未顯示任何資料 {#if-no-data-displays-in-the-adobe-campaign-dialog}

在Adobe Campaign Classic中，請確認連線埠號碼後面沒有尾隨斜線(`/`)。

![Adobe Campaign Classic — 確保連線埠號碼](assets/chlimage_1-149.png)後面沒有尾隨斜線

## 如果您收到有關setlocale的警告 {#if-you-get-a-warning-about-your-setlocale}

啟動Adobe Campaign Classic的Apache HTTPD服務時，您可能會看到錯誤`Warning: setlocale: LC_CTYPE cannot change locale`

確定您的Adobe Campaign Classic伺服器上已安裝`en_CA.ISO-8859-15 locale`。

* 您可以使用`local -a`檢查是否已安裝它。
* 如果未安裝，您可以修補`/usr/local/neolane/nl6/env.sh`指令碼，並將地區設定變更為已安裝的指令碼。

## 如果您在編譯指令碼&#39;get_nms_amcGetSeedMetaData_jssp&#39;時發生錯誤 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

如果您在AEM記錄檔中看到下列錯誤訊息：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

在Adobe Campaign Classic伺服器上使用下列因應措施。

1. 開啟檔案`$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js`
1. 修改方法`amcGetSeedMetaData`的第467行
1. 將`label : [inclView.@label](mailto:inclView.@label)`變更為`label : String([inclView.@label](mailto:inclView.@label))`
1. 儲存。
1. 重新啟動伺服器。

## 如果Adobe Campaign Classic在按一下「同步」按鈕時顯示錯誤 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

按一下Adobe Campaign Classic中的&#x200B;**同步**&#x200B;按鈕時，您可能會看到以下錯誤。

* `Error while executing the method 'aemListContent' of service [nms:delivery](https://nmsdelivery/)`

若要修正此問題，請確定在Adobe Campaign Classic的&#x200B;**外部帳戶**&#x200B;中設定的AEM連線URL可以從電腦連線。

從`localhost`切換至URL的IP位址通常可以解決這個問題。

## 如果您收到「無法剖析XTK日期+時間「未定義」錯誤 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

在AEM中按一下&#x200B;**同步**&#x200B;後，您可能會收到頁面上的指令碼已發生的錯誤。

* `Cannot parse XTK Date+Time 'undefined': not a valid XTK value.`

如果AEM執行個體上有過時的Adobe Campaign Classic資訊，就會發生此錯誤。 您可以執行下列操作來解決此問題：

1. 移除AEM上的所有Adobe Campaign Classic整合設定。
1. 重建整合。
1. 建立範本。

## 如果連線到SSL在設定Cloud Service時顯示錯誤 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

如果您在AEM的`error.log`中看到下列內容，請向Adobe Campaign支援團隊提交票證。

```text
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

## 如果您在同步對話方塊中看到HTTP而不是預期的HTTPS連結 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

嘗試同步Adobe Campaign Classic傳送中的內容時，AEM會傳回電子報清單。 不過，清單中電子報的URL可能是HTTP位址，而非HTTPS。 選取清單中的其中一個專案時，會發生錯誤。 此錯誤會在下列設定中發生。

* 使用https與AEM作者通訊的託管Adobe Campaign
* 反向Proxy終止SSL
* 內部部署AEM作者例項

若要解決此問題，請執行下列動作：

* AEM Dispatcher或反向Proxy必須設定為以標頭傳遞原始通訊協定。
* AEM的OSGi設定中的&#x200B;**Apache Felix Http服務SSL篩選器**&#x200B;必須使用必要的標頭設定進行設定。
   * `https://<host>:<port>/system/console/configMgr`
   * 請參閱[https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter](https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter)

## 無法在頁面屬性中選取自訂範本 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

在Adobe Campaign Classic的AEM中建立郵件範本時，您必須在範本的`jcr:content`節點中包含值為`mapRecipient`的屬性`acMapping`。 如果沒有該屬性，就無法在AEM的&#x200B;**頁面屬性**&#x200B;中選取Adobe Campaign Classic範本。 欄位顯示為停用。

## 如果您在AEM記錄檔中看到錯誤「com.day.cq.mcm.campaign.servlets.util.ParameterMapper」 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

使用自訂範本時，您可能會在AEM記錄中看到錯誤`com.day.cq.mcm.campaign.servlets.util.ParameterMapper`。

如果`acMapping`屬性設定為`recipient.firstName`以外的值，則在Adobe Campaign管理員中建立空白值，即會發生此錯誤。

如果發生此錯誤，請從[封裝共用](/help/sites-administering/package-manager.md#package-share)安裝AEM的Feature Pack 6576。
