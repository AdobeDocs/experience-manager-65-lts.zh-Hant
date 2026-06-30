---
title: 緩解JEE 6.5 LTS SP2上AEM Forms的伺服器端請求偽造(SSRF)漏洞
description: 在JBoss上執行的JEE 6.5 LTS Service Pack 2部署中，AEM Forms上伺服器端請求偽造(SSRF)漏洞的緩解步驟。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 1d825cd821609504c5e2cff7f7002bf3afe30434
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 3%

---

# 緩解JEE 6.5 LTS SP2上AEM Forms的伺服器端請求偽造(SSRF)漏洞

## 快速參考 {#quick-reference}

| 影響層級 | 受影響的版本 | 建議的動作 |
| --- | --- | --- |
| 嚴重 | JEE 6.5 LTS Service Pack 2上的AEM Forms (6.5 LTS SP2) | 手動安裝[Hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear) |
| 未受影響 | OSGi、Workbench、Cloud Service上的AEM Forms | 無需採取任何動作 |

**已處理的漏洞：**

* 伺服器端請求偽造(SSRF) (CWE-918)

## 概觀 {#overview}

### 受影響的內容 {#whats-affected}

| 漏洞 | 影響 | 受影響的元件 |
| --- | --- | --- |
| 伺服器端請求偽造(SSRF) (CWE-918) | 攻擊者可能會誘使伺服器向內部或外部資源提出非預期的要求 | JEE 6.5 LTS SP2上的AEM Forms |

### 未受影響的專案 {#whats-not-affected}

* Experience Manager Forms Workbench （所有版本）
* OSGi上的Experience Manager Forms （所有版本）
* Experience Manager Forms as a Cloud Service

## 解析度選項 {#resolution-options}

### 開始之前 {#before-you-start}

進行任何變更之前，請先備份您要取代的EAR檔案：

* 在您的部署目錄中找到`adobe-edcserver-jboss.ear`：

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* 將檔案複製到部署目錄外部的安全備份位置。
* 繼續進行任何更新之前，請確定備份完整且可存取。

此預防措施可讓您還原原始狀態，以防您在更新過程中遇到任何問題。

### 在JEE 6.5 LTS SP2 (JBoss)上手動安裝AEM Forms的Hotfix

1. 從[Adobe軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear)下載`adobe-edcserver-jboss.ear`。

1. 在您的部署目錄中找到`adobe-edcserver-jboss.ear`，並將其取代為下載的檔案：

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. 啟動AEM Forms Configuration Manager以重新部署更新的EAR並套用Hotfix。

1. 重新啟動應用程式伺服器，並從伺服器記錄檔確認部署成功。

## 參照 {#references}

* [Adobe Experience Manager Forms安全性最佳實務](/help/forms/using/hardening-securing-aem-forms-environment.md)
