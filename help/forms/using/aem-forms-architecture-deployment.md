---
title: AEM Forms的架構和部署拓撲
description: AEM Forms的架構詳細資料，以及建議新老的AEM客戶以及從LiveCycle ES4升級至AEM Forms的客戶使用的拓撲。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
exl-id: 23ffbaa6-1bd9-48c3-afa3-19737bb15de0
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 0%

---

# AEM Forms的架構和部署拓撲 {#architecture-and-deployment-topologies-for-aem-forms}

## 套用至 {#applies-to}

本檔案適用於&#x200B;**AEM 6.5 LTS Forms**。

如需AEM as a Cloud Service檔案，請參閱Cloud Service[上的](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html)AEM Forms 。

## 架構 {#architecture}

AEM Forms是部署至AEM的應用程式，做為AEM套件。 此套件稱為AEM Forms附加元件套件。 AEM Forms附加元件套件包含部署至AEM OSGi容器中的服務（API提供者），以及由AEM Sling架構管理的servlet或JSP （提供前端和REST API功能）。 下圖說明此設定：

![架構](assets/architecture.png)

AEM Forms的架構包括下列元件：

* **核心AEM服務：** AEM提供給已部署應用程式的基本服務。 這些服務包括符合JCR規範的內容存放庫、OSGI服務容器、工作流程引擎、信任存放區、金鑰存放區等。 AEM Forms應用程式可使用這些服務，但AEM Forms套件不提供這些服務。 這些服務是整體AEM棧疊不可或缺的一部分，各種AEM Forms元件都會使用這些服務。
* **Forms服務：**&#x200B;提供表單相關功能，例如建立、組合、散發及封存PDF檔案、新增數位簽章以限制檔案的存取權，以及解碼條碼式表單。 這些服務可供AEM中共同部署的自訂程式碼公開使用。
* **網頁層：** JSP或servlet，建置在通用和表單服務之上，可提供下列功能：

   * **製作前端**：用於製作和管理表單的表單製作和表單管理使用者介面。
   * **表單轉譯與提交前端**：使用者對面的介面，可供AEM Forms的一般使用者（例如，存取政府網站的公民）使用。 此功能提供表單轉譯（在網頁瀏覽器中顯示表單）和提交功能。
   * **REST API**： JSP和servlet會匯出表單服務的子集，以供HTTP型使用者端(例如Forms行動SDK)遠端使用。

**OSGi上的AEM Forms：** OSGi環境上的AEM Forms是標準的AEM Author或AEM Publish ，且已在其上部署AEM Forms套件。 您可以在[單一伺服器環境、伺服器陣列和叢集設定](/help/sites-deploying/recommended-deploys.md)中的OSGi上執行AEM Forms。 叢集設定僅適用於AEM Author執行個體。

<!--

**AEM Forms on JEE:** AEM Forms on JEE is AEM Forms server running on JEE stack. It has AEM Author with AEM Forms add-on packages and additional AEM Forms JEE capabilities co-deployed on a single JEE stack running on an application server. You can run AEM Forms on JEE in single-server and clustered setups. AEM Forms on JEE is required only to run document security, process management, and for LiveCycle customers upgrading to AEM Forms. Here are a few additional scenarios to use AEM Forms on JEE:

* **HTML workspace support (for customers using HTML workspace):** AEM Forms on JEE enables single sign-on with Processing instances, serves certain assets rendered on Processing instances, and handles submission of forms rendered within the HTML workspace.
* **Advanced additional form/interactive communication data processing**: AEM Forms on JEE can be utilized for additionally processing form/interactive communication data (and saving the results to a suitable data store) in complex use-cases where advanced process-management capabilities are required.

AEM Forms on JEE also includes provides following supporting services to the AEM components:

* **Integrated user management:** Allows users of AEM Forms on JEE to be recognized as AEM forms on OSGi users and helps enable SSO for both OSGi and JEE users. This is required for scenarios where single sign-on between AEM forms on OSGi and AEM Forms on JEE is required (for example, HTML workspace).
* **Asset hosting:** AEM Forms on JEE can serve assets (for example, HTML5 forms) rendered on AEM Forms on OSGi.

-->

AEM Forms製作使用者介面不支援建立記錄檔案(DOR)、PDF forms和HTML5 Forms。 這類資產是使用獨立的Forms Designer應用程式來設計，並個別上傳至AEM Forms Manager。<!--Alternatively, for AEM Forms on JEE, forms can be designed as application (in AEM Forms Workbench) assets and deployed into AEM Forms on JEE server.-->

OSGi <!--and AEM Forms on JEE both-->上的AEM Forms具有工作流程功能。 您可以在OSGi.<!--, without having to install the full-fledged Process Management capability of AEM Forms on JEE. There is some difference in the [features of Form-centric workflow on AEM Forms on OSGi and Process Management capability of AEM Forms on JEE](capabilities-osgi-jee-workflows.md). The development and management of Form-centric workflows on AEM Forms on OSGi uses the familiar AEM Workflow and AEM Inbox capabilities.-->上的AEM表單上，快速建置和部署各種工作的基本工作流程

## 術語 {#terminologies}

下圖顯示典型AEM部署中使用的各種AEM Forms表單伺服器設定及其元件：

![aem_forms_-_recommendedtopology](assets/aem_forms_-_recommendedtopology.png)

**作者：**&#x200B;作者執行個體是以標準作者執行模式執行的AEM Forms伺服器。 <!--It can be AEM Forms on JEE or AEM Forms on OSGi environment.-->專為內部使用者、表單和互動式通訊設計人員以及開發人員所設計。 可啟用下列功能：

* **製作及管理表單與互動式通訊：**&#x200B;設計人員和開發人員可以建立和編輯最適化表單與互動式通訊、上傳外部建立的其他型別的表單(例如在Adobe Forms Designer中建立的表單)，以及使用Forms Manager主控台管理這些資產。
* **表單與互動式通訊發佈：**&#x200B;裝載於製作執行個體的Assets可以發佈至發佈執行個體，以執行執行階段作業。 資產發佈使用AEM的復寫功能。 Adobe建議在所有作者執行個體上設定復寫代理程式，以手動方式將發佈的表單推播到處理執行個體，並在處理執行個體上設定另一個復寫代理程式，且啟用&#x200B;*接收時*&#x200B;觸發程式，以自動將收到的表單復寫到發佈執行個體。

**發佈：**&#x200B;發佈執行個體是以標準發佈執行模式執行的AEM Forms伺服器。 發佈例項適用於表單式應用程式的一般使用者，例如存取公開網站及提交表單的使用者。 可啟用下列功能：

* 呈現及提交一般使用者的Forms。
* 將原始提交的表單資料傳輸至處理執行個體，以便在最終記錄系統中進一步處理和儲存。 AEM Forms中提供的預設實施，會使用AEM的反向復寫功能來達成此目的。 您也可以使用替代實作，將表單資料直接推送至處理伺服器，而非先在本機儲存（後者是啟用反向復寫的先決條件）。 擔心發佈執行個體上儲存潛在敏感資料的客戶，可以加入此[替代實作](/help/forms/using/configuring-draft-submission-storage.md)，因為處理執行個體通常位於較安全的區域中。
* 呈現和提互動動式通訊和信件：互動式通訊和信件會呈現在發佈執行個體上，而對應的資料會提交至處理執行個體，以進行儲存和後處理。 資料可以儲存在發佈執行個體本機上，並在稍後反向複製到處理執行個體（預設選項），也可以直接推送至處理執行個體，而不儲存在發佈執行個體上。 後者實作對注重安全性的客戶很有用。

**處理中：** AEM Forms的執行個體以作者執行模式執行，未將使用者指派給表單管理員群組。 您可以在OSGi上部署<!--AEM Forms on JEE or--> AEM Forms作為處理執行個體。 未指派使用者以確保表單製作和管理活動未在處理執行個體上執行並僅在製作執行個體上發生。 處理執行個體可啟用下列功能：

* **處理從發佈執行個體到達的原始表單資料：**&#x200B;這主要是透過資料到達時觸發的AEM工作流程在處理執行個體上達成。 工作流程可以使用現成可用的表單資料模型步驟，將資料或檔案封存至適當的資料存放區。
* **表單資料的安全儲存**：處理作業提供防火牆後存放庫，供與使用者隔離的原始表單資料使用。 無論是作者執行個體的表單設計人員或發佈執行個體的一般使用者都無法存取此存放庫。

  >[!NOTE]
  >
  >Adobe建議使用協力廠商資料存放區來儲存最後處理的資料，而非使用AEM存放庫。

* **對來自發佈執行個體的通訊資料進行儲存和後置處理：** AEM工作流程會執行對應信件定義的選擇性後置處理。 這些工作流程可將最終處理的資料儲存至適當的外部資料存放區。

* **HTML Workspace託管**：處理執行個體會託管HTML Workspace的前端。 HTML工作區為相關任務/群組指派提供UI，以供檢閱和核准程式。

處理執行個體設定為在作者執行模式中執行，因為：

* 它可讓您從發佈執行個體反向復寫原始表單資料。 預設的資料儲存處理常式需要反向復寫功能。
* AEM工作流程是處理從發佈執行個體到達的原始表單資料的主要方法，建議在作者樣式系統上執行。

<!--

## Sample physical topologies for AEM Forms on JEE {#sample-physical-topologies-for-aem-forms-on-jee}

The AEM Forms on JEE topologies recommended below are mainly for customers upgrading from LiveCycle or a previous version of AEM Forms on JEE. Adobe recommends using AEM Forms on OSGi for fresh installations. A fresh installation of AEM Forms on JEE only recommended for using Document Security and Process Management capabilities.

### Topology for using document services or document security capabilities {#topology-for-using-document-services-or-document-security-capabilities}

AEM Forms customers planning to use only document services or document security capabilities can have a topology similar to the one displayed below. This topology recommends using a single instance of AEM Forms. You can also create a cluster or farm of AEM Forms servers, if necessary. This topology is recommended when most users programmatically access capabilities of AEM Forms server and intervention through the user interface is minimum. The topology is helpful in batch processing operations of document services. For example, using output service to create hundreds of non-editable PDF documents on daily basis.

Although, AEM Forms lets you set up and run all the functionalities from a single server, yet, you should do capacity planning, load balancing, and set up dedicated servers for specific capabilities in a production environment. For example, for an environment using the PDF Generator service to convert thousands of pages a day and add digital signatures to limit access to documents, set up separate AEM Forms servers for the PDF Generator service and digital signature capabilities. It helps provide optimum performance and scale the servers independent of each other.

![basic-features](assets/basic-features.png)

### Topology for using AEM Forms process management {#topology-for-using-aem-forms-process-management}

AEM Forms customers planning to use AEM Forms process management features, for example, HTML Workspace can have a topology similar to the one displayed below. The AEM Forms on JEE server can be in a single server or cluster configuration.

If you are upgrading from LiveCycle ES4, this topology closely mirrors with what you already have in LiveCycle except for the addition of AEM Author built-in to AEM Forms on JEE. Moreover, there is no change in the clustering requirements for customers performing an upgrade. If you were using AEM Forms in a clustered environment, you can continue with same in AEM 6.5 Forms. For a fresh installation of AEM Forms of JEE for using HTML Workspace, running AEM author instance built-in to the JEE environment is an additional requirement.

Form data store is a third-party data store used for storing final processed data of forms and interactive communications. This is an optional element in the topology. You can also choose to set up a processing instance and use its repository as the final system-of-record system, if necessary.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

The topology is recommended to the customers planning to use AEM Forms on JEE server for process management capabilities (HTML Workspace) without using any post-processing, adaptive forms, HTML5 forms, and interactive communication capabilities.

### Topology for using adaptive forms, HTML5 forms, interactive communication capabilities {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

AEM Forms customers planning to use AEM Forms data capture capabilities, for example, adaptive forms, HTML5 Forms, PDF Forms, can have a topology similar to the one displayed below. This topology is also recommended for using interactive communication capabilities of AEM Forms.

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

You can make the following changes/customizations to the above-suggested topology:

* Using HTML Workspace and AEM Forms app requires an AEM author or processing instance. You can use the AEM author instance built-in to AEM Forms on JEE server instead of setting up an additional external AEM author server.
* An AEM Author or Processing instance is required only for Forms-centric workflows on OSGi, adaptive forms, forms portal, and interactive communication.
* interactive communication Agent UI is generally run within the organization. So, you can keep a publish server for Agent UI within the private network.
* AEM forms on OSGi instance built-in to AEM Forms on JEE server can also run Forms-centric workflows on OSGi and Watched Folders.

-->

## 在OSGi上使用AEM Forms的實體拓撲範例 {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### 資料擷取、互動式通訊、OSGi功能表單導向工作流程的拓撲 {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

計畫使用AEM Forms資料擷取功能(例如最適化表單、HTML5 Forms、PDF forms)的AEM Forms客戶，可擁有類似於以下顯示的拓撲。 在OSGi功能上使用互動式通訊和Forms為中心的工作流程時(例如，使用AEM收件匣和AEM Forms應用程式進行業務流程工作流程)，也建議使用此拓撲。

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### 使用watched資料夾功能進行離線批次處理的拓撲 {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

計畫使用Watched資料夾進行批次處理的AEM Forms客戶可擁有類似於以下所示的拓撲。 拓撲會顯示叢集環境，但您會根據負載決定使用單一執行個體或AEM Forms伺服器陣列。 第三方資料來源是您自己的記錄系統。 它可作為Watched資料夾的輸入來源。 拓撲也會以列印檔案的形式顯示輸出。 您也可以將輸出內容儲存至檔案系統、透過電子郵件傳送，以及使用其他自訂方法來使用輸出。

![offline-batch-processing-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### 使用檔案服務功能進行離線API型處理的拓撲 {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

計畫僅使用檔案服務功能的AEM Forms客戶可擁有類似於以下所示的拓撲。 此拓撲建議在OSGi伺服器上使用AEM Forms叢集。 當大部分使用者以程式設計（使用API）存取AEM Forms伺服器的功能時，且透過使用者介面的干預最小時，建議使用此拓撲。 此拓撲在多個軟體使用者端案例中相當實用。 例如，多個客戶使用PDF Generator服務來隨選建立PDF檔案。

雖然AEM Forms可讓您從單一伺服器設定並執行所有功能，但您應執行容量規劃、負載平衡，並為生產環境中的特定功能設定專用伺服器。 例如，在使用PDF Generator服務每天轉換數千頁頁面及多個調適型表單來擷取資料的環境中，請為PDF Generator服務和調適型表單功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並獨立擴充伺服器。

![離線api處理](assets/offline-api-based-processing.png)
