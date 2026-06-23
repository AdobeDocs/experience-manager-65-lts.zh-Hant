---
title: 緩解JEE 6.5 LTS SP2上AEM Forms的VULN-36128和VULN-36120漏洞
description: 在JBoss上執行的JEE 6.5 LTS Service Pack 2部署中，AEM Forms上的VULN-36128和VULN-36120的緩解步驟。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 1b876f20cbc3a00a02a4449f0d353fb858695235
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---

# 緩解JEE 6.5 LTS SP2上AEM Forms的VULN-36128和VULN-36120漏洞

## 快速參考 {#quick-reference}

| 影響層級 | 受影響的版本 | 建議的動作 |
| --- | --- | --- |
| 嚴重 | JEE 6.5 LTS Service Pack 2上的AEM Forms (6.5 LTS SP2) | 手動安裝[Hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear) |
| 未受影響 | OSGi、Workbench、Cloud Service上的AEM Forms | 無需採取任何動作 |

**已處理的漏洞：**

* **VULN-36128**：遠端程式碼執行漏洞允許未經授權的遠端攻擊者執行任意程式碼。
* **VULN-36120**：不正確的輸入驗證漏洞，可能會允許未經授權存取敏感資訊。

## 緩解步驟 {#mitigation-steps}

### 開始之前 {#before-you-start}

進行任何變更前，請先備份要取代的EAR檔案：

* 在您的部署目錄中找到`adobe-edcserver-jboss.ear`：

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* 將檔案複製到部署目錄外部的安全備份位置。
* 繼續進行任何更新之前，請確定備份完整且可存取。

如果您在更新過程中遇到任何問題，此預防措施可讓您還原原始狀態。

### 在JEE 6.5 LTS SP2 (JBoss)上手動安裝AEM Forms的Hotfix {#manual-hotfix-installation-aem-forms-jee-65-lts-sp2-jboss}

1. 從[Adobe軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear)下載`adobe-edcserver-jboss.ear`。

1. 在您的部署目錄中找到`adobe-edcserver-jboss.ear`，並將其取代為下載的檔案：

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. 啟動AEM Forms Configuration Manager以重新部署更新的EAR並完全套用修補程式。

1. 重新啟動應用程式伺服器，並從伺服器記錄檔確認部署成功。

## 參照 {#references}

* [Adobe Experience Manager Forms安全性最佳實務](/help/forms/using/hardening-securing-aem-forms-environment.md)
