---
title: 監控AEM表單部署
description: 您可以從系統層級和內部層級監控AEM表單部署。 透過本檔案進一步瞭解監控AEM表單部署。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: aa02139f-7e47-4979-9560-5d270c36080b
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# 監控AEM表單部署 {#monitoring-aem-forms-deployments}

您可以從系統層級和內部層級監控AEM表單部署。 您可以使用HP OpenView、IBM®Tivoli和CA UniCenter等專業管理工具，以及名為&#x200B;*JConsole*&#x200B;的協力廠商JMX監視器，專門監視Java™活動。 監控策略的實作可改善AEM表單部署的可用性、可靠性和效能。

<!-- For more information about monitoring AEM forms deployments, see [A technical guide for monitoring AEM forms deployments](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

## 使用MBean監視 {#monitoring-using-mbeans}

AEM Forms提供兩個註冊的MBean，以提供導覽和統計資訊。 這些零件是唯一支援整合與檢查的MBean：

* **ServiceStatistic：**&#x200B;此MBean提供服務名稱及其版本的相關資訊。
* **OperationStatistic：**&#x200B;此MBean提供每個AEM Forms伺服器服務的統計資料。 此MBean可讓管理員取得特定服務的相關資訊，例如呼叫時間和錯誤數目。

### ServiceStatisticMbean公用介面 {#servicestatisticmbean-public-interfaces}

您可以存取這些ServiceStatistic MBean公用介面以進行測試：

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### OperationStatisticMbean公用介面 {#operationstatisticmbean-public-interfaces}

您可以存取OperationStatistic MBean的下列公用介面以進行測試：

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### MBean樹狀結構與作業統計資料 {#mbean-tree-operation-statistics}

使用JMX主控台(JConsole)，可以使用OperationStatistical MBean中的統計資料。 這些統計資料是MBean的屬性，可以在下列階層樹狀結構下瀏覽：

**MBean樹狀結構**

**Adobe網域名稱：**&#x200B;依存於應用程式伺服器。 如果應用程式伺服器未定義網域，預設值為adobe.com。

**ServiceType：** AdobeService是用於列出所有服務的名稱。

**AdobeServiceName：**&#x200B;服務名稱或服務識別碼。

**版本：**&#x200B;服務版本。

**作業統計資料**

**引動時間：**&#x200B;執行方法所花費的時間。 此叫用不包含序列化要求、從使用者端傳輸到伺服器以及還原序列化的時間。

**呼叫計數：**&#x200B;服務被呼叫的次數。

**平均呼叫時間：**&#x200B;伺服器啟動後所有已執行呼叫的平均時間。

**最大呼叫時間：**&#x200B;伺服器啟動後執行的最長呼叫持續時間。

**分鐘呼叫時間：**&#x200B;伺服器啟動後所執行的最短呼叫持續時間。

**例外狀況計數：**&#x200B;導致失敗的呼叫數目。

**例外狀況訊息：**&#x200B;上次發生例外狀況的錯誤訊息。

**上次取樣日期時間：**&#x200B;上次叫用的日期。

**時間單位：**&#x200B;預設為毫秒。

若要啟用JMX監視，應用程式伺服器通常需要一些設定。 如需詳細資訊，請參閱您的應用程式伺服器檔案。

### 如何設定開放JMX存取的範例 {#examples-of-how-to-set-up-open-jmx-access}

**JBoss® 4.0.3/4.2.0 — 設定JVM啟動**

若要從JConsole檢視MBean，請設定JBoss應用程式伺服器的JVM啟動引數。 請確定JBoss是從run.bat/sh檔案啟動。

1. 編輯位於InstallJBoss/bin下的run.bat檔案。
1. 找到JAVA_OPTS行並新增下列內容：

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 — 設定JVM啟動**

1. 編輯位於`[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`下的startWebLogic.bat檔案。
1. 找到JAVA_OPTS行並新增下列內容：

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. 重新啟動WebLogic。

>[!NOTE]
>
>對於WebLogic，您可以使用遠端或IIOP來存取MBean。

**從遠端存取MBean**

1. 啟動JConsole以建立新連線，然後按一下遠端索引標籤。
1. 輸入主機名稱和連線埠（9088，您在JVM啟動選項期間指定的數字）。

**WebSphere® 6.1 — 設定JVM啟動**

1. 在Admin Console （應用程式伺服器> server1 >處理序定義> JVM）上，將下列行新增至一般JVM引數的欄位中：

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. 在/opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties檔案(或&lt;Your Websphere JRE>/ lib/management/management.properties)中新增或取消註解下列三行：

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. 重新啟動WebSphere。
