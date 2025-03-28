---
title: 準備AEM Forms以進行備份
description: 瞭解如何使用「備份與還原」服務，以使用Java API和Web服務API進入AEM Forms伺服器的備份模式並離開。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 0fe1aef7-f607-4c40-bfa9-9ec9ebd8abeb
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 0%

---

# 準備AEM Forms以進行備份 {#preparing-aem-forms-for-backup}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於備份與還原服務 {#about-the-backup-and-restore-service}

備份與還原服務可讓您將AEM Forms置於&#x200B;*備份模式*，以便執行熱備份。 備份和還原服務實際上並不會執行AEM Forms的備份或還原您的系統。 而是讓伺服器處於穩定可靠的備份狀態，同時允許伺服器繼續執行。 您負責備份全域檔案儲存(GDS)和連線至Forms伺服器的資料庫的動作。 GDS是用來儲存長期處理程式中所使用檔案的目錄。

備份模式是伺服器進入的狀態，這樣在執行備份程式時就不會清除GDS中的檔案。 而是在GDS目錄下建立子目錄，以在儲存備份模式結束後維護要清除的檔案記錄。 檔案可在系統重新啟動後繼續儲存，可能持續數天甚至數年。 這些檔案是Forms伺服器整體狀態的重要部分，可能包含PDF檔案、原則或表單範本。 若這些檔案中有任何遺失或損毀，Forms伺服器上的程式可能會變得不穩定，且可能會遺失資料。

您可以選擇執行快照備份，通常會在期間進入備份模式，然後在完成備份活動後離開備份模式。 需要離開備份模式，以便從GDS清除檔案，確保檔案不會變得不必要地大。 您可以明確離開備份模式，或等待備份模式工作階段到期的時間。

您也可以讓伺服器處於永久備份模式，這是典型的備份策略，用於復原備份或持續系統涵蓋範圍。 正在捲動備份模式表示系統永遠處於備份模式，前一階段作業一經釋出就會啟動新的備份模式階段作業。 當處於連續備份模式時，檔案會在兩個備份模式工作階段之後清除，且不再參考。

您可以使用「備份與還原」服務，將您建立之現有應用程式或新應用程式，新增至執行連線至Forms伺服器之GDS或資料庫的備份。

>[!NOTE]
>
>和AEM Forms實作的任何其他方面一樣，您的備份與復原策略應在生產使用之前，在開發或中繼環境中進行開發與測試，以確保整個解決方案如預期般運作且不會遺失資料。

您可以使用「備份與還原」服務執行下列工作：

* 進入備份模式。
* 離開備份模式。

>[!NOTE]
>
>如需執行AEM Forms備份時考量哪些專案的詳細資訊，請參閱[管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>如需有關備份和還原服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 在Forms伺服器上進入備份模式 {#entering-backup-mode-on-the-forms-server}

您進入備份模式，以便允許對Forms伺服器進行熱備份。 進入備份模式時，您可以根據組織的備份程式指定下列資訊：

* 用於識別備份模式工作階段的唯一標籤，可能對您的備份程式很有用。
* 備份程式的完成時間。
* 表示是否處於連續備份模式的旗標，只有在執行滾動備份時才有用。

在寫入應用程式以進入備份模式之前，建議您先瞭解將Forms伺服器置於備份模式後所使用的備份程式。 如需執行AEM Forms備份時考量哪些專案的詳細資訊，請參閱[管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>如需有關備份和還原服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要建立進入備份模式的應用程式，請執行下列步驟：

1. 包含專案檔案。
1. 建立BackupService使用者端物件。
1. 決定唯一標籤、執行備份的時間長度，以及是否處於連續備份模式。
1. 進入備份模式。
1. （選擇性）擷取伺服器上備份模式工作階段的相關資訊。
1. 執行GDS （全域資料存放區）和資料庫的備份。

**包含專案檔**

在您的開發專案中包含必要的檔案。 這些檔案必須包含在您的專案中，以便正確編譯您的程式碼並使用備份和還原服務API。

如需這些檔案位置的相關資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立BackupService使用者端API物件**

若要以程式設計方式離開備份模式，請建立BackupService使用者端物件，以使用備份和還原服務API。

**決定唯一標籤、決定執行備份的時間長度，以及決定是否處於連續備份模式**

在進入備份模式之前，您應該先決定唯一的標籤、決定要配置執行備份的時間長度，以及是否要讓Forms伺服器維持備份模式。 這些考量事項對於整合貴組織建立的備份程式非常重要。 （請參閱[管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)。）

**進入備份模式**

使用與貴組織備份程式一致的引數進入備份模式。

**擷取伺服器上備份模式工作階段的相關資訊**

進入備份模式後，您可以擷取有關工作階段的資訊。 這些資訊可用來整合您的備份程式

**執行GDS和資料庫的備份**

成功進入備份模式後，您可以執行全域檔案儲存(GDS)和Forms伺服器所連線之資料庫的備份。 此步驟特定於您的組織，因為您可以手動執行此步驟或執行其他工具以執行備份程式。

### 使用Java API進入備份模式 {#enter-backup-mode-using-the-java-api}

使用備份和還原服務API進入備份模式：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含必要的使用者端JAR檔案，例如adobe-backup-restore-client-sdk.jar。 若要建立Java使用者端應用程式，必須將下列JAR檔案新增至專案的類別路徑：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
   * jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

1. 建立BackupService使用者端API物件

   您同時使用`ServiceClientFactory`物件和BackupService使用者端API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。 （請參閱[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`BackupService`物件。

1. 決定唯一的標籤、決定執行備份的時間長度，以及決定是否處於連續備份模式

   決定唯一標籤、決定要配置以執行備份的時間長度，以及是否希望Forms伺服器維持連續備份模式。

1. 進入備份模式

   使用下列引數叫用`enterBackupMode`方法，以進入備份模式：

   * `String`值，指定可識別備份模式工作階段的唯一可讀取標籤。 建議您不要使用無法編碼為XML格式的空格或字元。
   * `int`值，指定保留在備份模式的分鐘數。 您可以指定從`1`到`10080`的值（一週的分鐘數）。 使用連續備份模式時，會忽略此值。
   * 指定是否處於連續備份模式的`Boolean`值。 `True`的值指定處於連續備份模式。 當處於連續備份模式時，您為保留在備份模式的分鐘數指定的值會被忽略。

     連續備份模式表示新的備份模式工作階段會在目前工作階段完成後啟動。 值為`False`表示未使用連續備份模式，離開備份模式後，會從GDS繼續清除檔案。

1. 擷取伺服器上備份模式工作階段的相關資訊

   使用叫用`enterBackupMode`方法後傳回的`BackupModeEntryResult`物件擷取資訊。 在進入備份模式後，您可以擷取的資訊對於與備份程式整合而言可能很有用。 例如，標籤、備份ID和開始時間可能很適合用來作為備份程式檔案名稱的輸入。

1. 執行GDS和資料庫的備份

   備份全域檔案儲存(GDS)和Forms伺服器所連線的資料庫。 執行備份的動作並不屬於AEM Forms SDK的一部分，甚至可能包括貴組織中備份程式特有的手動步驟。

### 使用Web服務API進入備份模式 {#enter-backup-mode-using-the-web-service-api}

使用備份與還原服務API提供的Web服務進入備份模式：

1. 包含專案檔案

   * 建立使用備份和還原服務API WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立BackupService使用者端API物件

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`BackupServiceService`物件，並使用`Credentials`方法指定認證。

1. 決定唯一的標籤、決定執行備份的時間長度，以及決定是否處於連續備份模式

   決定唯一標籤、決定要配置以執行備份的時間長度，以及是否希望Forms伺服器維持連續備份模式。

1. 進入備份模式

   若要進入備份模式，請叫用enterBackupMode方法並傳遞下列值：

   * `String`值，指定可識別備份模式工作階段的唯一可讀取標籤。 建議您不要使用無法編碼為XML格式的空格或字元。
   * `Uint32`值，指定保留在備份模式的分鐘數。 您可以指定從`1`到`10080`的值（一週的分鐘數）。 使用連續備份模式時，會忽略此值。
   * 指定是否處於連續備份模式的`Boolean`值。 `True`的值指定處於連續備份模式。 當處於連續備份模式時，您為保留在備份模式的分鐘數指定的值會被忽略。 連續備份模式表示新的備份模式工作階段會在目前工作階段完成後啟動。

     值為`False`表示未使用連續備份模式，離開備份模式後，會從GDS繼續清除檔案。

1. 擷取伺服器上備份模式工作階段的相關資訊

   從傳回的BackupModeEntryResult中叫用enterBackupMode方法之後，擷取有關備份模式階段作業的資訊，以驗證其是否成功。 在進入備份模式後，您可以擷取的資訊對於與備份程式整合而言可能很有用。 例如，標籤、備份ID和開始時間可能很適合用來作為備份程式檔案名稱的輸入。

1. 執行GDS和資料庫的備份

   備份全域檔案儲存(GDS)和Forms伺服器所連線的資料庫。 執行備份的動作並不屬於AEM Forms SDK的一部分，甚至可能包括貴組織中備份程式特有的手動步驟。

## 在Forms伺服器上保持備份模式 {#leaving-backup-mode-on-the-forms-server}

您離開備份模式，讓Forms伺服器繼續從Forms伺服器上的GDS （全域檔案儲存）中清除檔案。

將應用程式寫入離開模式之前，建議您先瞭解與AEM Forms搭配使用的備份程式。 如需執行AEM Forms備份時考量哪些專案的詳細資訊，請參閱[管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>如需有關備份和還原服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要離開備份模式，請執行下列步驟：

1. 包含專案檔案。
1. 建立BackupService使用者端物件。
1. 離開備份模式。
1. （選用）擷取在Forms伺服器上執行之備份模式工作階段的相關資訊。

**包含專案檔**

在您的開發專案中包含所有必要的檔案。 這些檔案對於正確編譯程式碼及使用備份與還原服務API非常重要。

如需這些檔案位置的相關資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立BackupService使用者端API物件**

若要以程式設計方式離開備份模式，請建立BackupService使用者端物件，以使用備份和還原服務API。

**離開備份模式**

離開備份模式以繼續從全域檔案儲存體(GDS)正常清除檔案。 離開備份模式之前，請先確認備份程式已完成。

**擷取有關結束的備份模式工作階段的資訊**

離開備份模式後，您可以擷取工作階段的相關資訊。 這些資訊可用來整合您的備份程式。

### 使用Java API離開備份模式 {#leave-backup-mode-using-the-java-api}

使用備份與還原服務API (Java)離開備份模式：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含必要的使用者端JAR檔案，例如adobe-backup-restore-client-sdk.jar。 若要建立Java使用者端應用程式，必須將下列JAR檔案新增至專案的類別路徑：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
   * jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

1. 建立BackupService使用者端API物件

   您同時使用`ServiceClientFactory`物件和BackupService使用者端API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。 （請參閱[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用物件的建構函式建立`BackupService`物件，並將`ServiceClientFactory`物件作為引數傳遞。

1. 進入備份模式

   叫用`leaveBackupMode`方法以離開備份模式。

1. 擷取伺服器上備份模式工作階段的相關資訊

   使用傳回的`BackupModeResult`物件擷取作業的相關資訊。 在進入備份模式後，您可以擷取的資訊對於與備份程式整合而言可能很有用。 例如，標籤、備份ID和開始時間可能很適合用來作為備份程式檔案名稱的輸入。

### 使用Web服務API離開備份模式 {#leave-backup-mode-using-the-web-service-api}

使用備份和還原服務API （Web服務）離開備份模式：

1. 包含專案檔案

   若要使用Web服務，您必須確定包含Proxy檔案。 請依照下列步驟設定您的專案，以使用備份與還原服務API做為Web服務。

   * 建立使用備份和還原服務API WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立BackupService使用者端API物件

   使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`BackupServiceService`物件。

1. 進入備份模式

   叫用`leaveBackupMode` Web服務作業以離開備份模式。

1. 擷取伺服器上備份模式工作階段的相關資訊

   在作業後擷取備份模式識別碼，以驗證作業是否成功。 當您離開備份模式後，可以擷取的資訊對於與備份程式整合可能很有用。
