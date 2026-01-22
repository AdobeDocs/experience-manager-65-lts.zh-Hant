---
title: 無法啟動JBoss網域控制站
description: 在使用JBoss EAP 8的AEM Forms 6.5.1 LTS叢集部署中，設定檔案可能包含重複的標籤。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---


# 無法啟動JBoss網域控制站

## 問題

在使用&#x200B;**JBoss EAP 8**&#x200B;的&#x200B;**AEM Forms 6.5.1 LTS**&#x200B;叢集部署中，組態檔
`<JBOSS_HOME>/domain/configuration/domain_oracle.xml` （和資料庫特定變體）可能包含&#x200B;**重複的開頭`<security>`標籤**。

這會導致&#x200B;**無效的XML組態**，導致&#x200B;**JBoss網域控制站啟動失敗**，並阻礙叢集初始化成功。

## 適用於

* **產品：** AEM Forms 6.5.1 LTS
* **部署型別：**&#x200B;叢集
* **應用程式伺服器：** JBoss EAP 8.x
* **組態檔：**

   * `<JBOSS_HOME>/domain/configuration/domain_oracle.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mysql.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mssql.xml`

## 疑難排解步驟

1. 在網域控制站啟動期間，可能會發現下列錯誤：

   * `WFLYCTL0198: Unexpected element 'security'`
   * `IJ010061: Unexpected element: security`

2. 開啟相關的設定檔：

   ```
   <JBOSS_HOME>/domain/configuration/domain_oracle.xml
   (or domain_mysql.xml / domain_mssql.xml)
   ```

3. 找出重複的`<security>`開始標籤。

   **不正確的設定：**

   ```xml
   <security>
       <security>
           <user-name>adobe</user-name>
           <credential-reference store="db-creds" alias="EncryptDBPassword"/>
       </security>
   ```

4. 移除多餘的開頭`<security>`標籤，以便更正設定，如下所示：

   **正確的設定：**

   ```xml
   <security>
       <user-name>adobe</user-name>
       <credential-reference store="db-creds" alias="EncryptDBPassword"/>
   </security>
   ```

5. 儲存檔案並啟動JBoss網域控制站。

6. 請確認所有叢集節點都一致地套用相同的驗證組態。
