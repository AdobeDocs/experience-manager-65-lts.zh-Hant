---
title: 選擇使用Adobe Analytics和Adobe Target
description: 瞭解如何選擇加入Adobe Analytics和Adobe Target。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: d872078f-3aa0-4abe-ac2a-74a1cd47b219
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 0%

---

# 選擇使用Adobe Analytics和Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM有一個選擇加入程式，可協助您整合Adobe Analytics和Adobe Target。 這是現成可用的功能，可作為指派給管理員使用者群組的預先載入任務。

當您以系統管理員身分登入時，此工作（**設定分析和定位**）可從[收件匣](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks)取得。 系統會根據您提供的認證，協助您設定及整合這些服務。

您可透過下列選項設定整合：

* 透過工作設定整合。

  您可以立即執行或稍後執行，任務將保留在收件匣中，直到執行某些動作為止。 無論哪種情況，設定都可以直接在UI中完成，或使用預先定義的`.properties`檔案完成。

* 選擇退出整合。

  如果您偏好[手動設定整合](/help/sites-administering/marketing-cloud.md)，請考慮此選項。 另請參閱[使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

* 使用指令碼來設定設定及布建。

## 設定整合 {#configuring-the-integration}

選擇加入整合，透過：

* Analytics啟用其頁面追蹤與分析功能。
* Target啟用其個人化功能。

無論是哪一個選項，您都需要提供使用者帳戶資訊，並指定追蹤的頁面。

>[!NOTE]
>
>您可以選擇使用在伺服器啟動時讀取的屬性檔案來提供Analytics和Target帳戶資訊。 請參閱[使用屬性檔案](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file)提供帳戶資訊。

當您選擇加入整合時，AEM會執行下列工作：

* 建立可連線至Analytics和Target的雲端設定。
* 建立可決定所追蹤資料的架構。
* 設定網頁以使用這些服務。

>[!NOTE]
>
>AT.js是預設的使用者端資料庫。 這是在您的[目標雲端服務設定](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration)下設定。
>
>Adobe建議您使用AT.js作為使用者端資料庫。

若要選擇加入預先載入的現成工作：

1. 從您的[收件匣，選取並&#x200B;**開啟**&#x200B;設定分析和定位](/help/sites-authoring/inbox.md#taking-action-on-an-item)工作。

   ![optin-01](assets/optin-01.png)

1. 對於Analytics：

   1. 輸入Analytics的使用者帳戶資訊，然後按一下對應的&#x200B;**新增**&#x200B;按鈕。
   1. 已驗證適當的認證。
   1. Analytics帳戶通過驗證後，請選取要使用的Analytics報表套裝。 AEM會擷取這些Analytics報表套裝。 狀態已更新為&#x200B;**已新增**。

1. 針對Target：

   1. 輸入Target的使用者帳戶資訊，然後按一下對應的&#x200B;**新增**&#x200B;按鈕。
   1. 已驗證適當的認證。 狀態已更新為&#x200B;**已新增**。

1. 選取&#x200B;**「下一步」**。
1. 選取應使用Analytics和/或Target的網站。

1. 選取&#x200B;**完成**&#x200B;以完成。

   >[!CAUTION]
   >
   >選擇加入設定後，您需要發佈受影響的網站/頁面，將這些變更復寫至您的發佈執行個體。

## 選擇退出整合 {#opting-out-of-the-integration}

符合以下條件時，請選擇退出與Analytics和Target的整合：

* 不想與這些產品整合。
* 偏好手動設定整合。

  如需手動設定整合的資訊，請參閱[與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md)和[與Adobe Target整合](/help/sites-administering/target.md)。

若要選擇退出，您必須完成預先載入的工作：

* 從您的[收件匣，選取並&#x200B;**完成**&#x200B;設定分析和定位](/help/sites-authoring/inbox.md#taking-action-on-an-item)工作。

## 使用屬性檔案提供帳戶資訊 {#providing-account-information-using-a-properties-file}

安裝AEM在伺服器啟動時讀取的屬性檔案，以設定帳戶屬性以便與Analytics和Target整合。 當您使用屬性檔案時，選擇加入精靈會自動使用檔案中的屬性，並據此建立雲端設定。

屬性檔案是名為marketingcloud.properties的文字檔，儲存在AEM處理序使用的工作目錄中（通常與JAR檔案相同的目錄）。 檔案包含下列屬性：

* analytics.server：您使用的Analytics資料中心的URL。
* analytics.company：與您的Analytics使用者帳戶相關聯的公司。
* analytics.username：您的Analytics使用者名稱。
* analytics.secret：與您的Analytics使用者名稱相關聯的密碼。
* analytics.reportsuite：要使用的Analytics報表套裝名稱。
* target.clientcode：與您的Target帳戶相關聯的使用者端代碼。
* target.email：用於驗證Target帳戶的電子郵件地址。
* target.password：與您的電子郵件地址關聯的密碼。

屬性和值會以等號(=)分隔。 Analytics屬性會加上前置詞`analytics`，而Target屬性會加上前置詞`target`。 若要設定服務，請為該服務的所有屬性提供值。 如果您不想設定服務，則不要為該服務提供值。

下列範例`.properties`檔案包含用來建立Analytics雲端設定的屬性值：

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

下列程式說明如何使用屬性檔案選擇加入整合。

1. 在AEM處理序正在使用的工作目錄中（編寫執行個體）建立`marketingcloud.properties`檔案。

   >[!NOTE]
   >
   >工作目錄通常是儲存jar或`license.properties`檔案的目錄。
   >
   >不過，它也可以由系統屬性定義為絕對路徑：
   >
   >`mac.provisioning.file.container`

1. 根據您的Analytics和/或Target帳戶新增屬性值。
1. 啟動或重新啟動伺服器，然後使用系統管理員帳戶登入。
1. 開啟設定分析和目標工作，如[設定整合](/help/sites-administering/opt-in.md#configuring-the-integration)中所述。 精靈不會要求您的帳戶資訊，而是使用`.properties`檔案中的值。

   為適當的服務選取&#x200B;**新增**，然後繼續執行精靈。

   ![optin-02](assets/optin-02.png)

## 關於雲端設定 {#about-the-cloud-configurations}

當您設定與Analytics和Target的整合時，AEM會自動建立所需的雲端設定和架構。 例如，Analytics雲端設定稱為「已布建的Analytics帳戶」。

您不需要變更雲端設定。 不過，您可以視需要設定架構。 (請參閱[將元件資料與Adobe Analytics屬性對應](/help/sites-administering/adobeanalytics-mapping.md)以及[新增目標架構](/help/sites-administering/target.md)。)

>[!NOTE]
>
>依預設，當您選擇加入Adobe Target設定精靈時，會啟用「準確定位」 。
>
>準確定位表示雲端服務設定會等待內容載入後再載入內容。 因此，就效能而言，準確定位可能會在載入內容前造成幾毫秒的延遲。
>
>作者例項上一律會啟用「準確定位」 。 不過，在發佈執行個體上，您可以清除雲端服務設定(**http://localhost:4502/etc/cloudservices.html**)中「準確定位」旁的勾號，來選擇全域關閉準確定位。 無論您在雲端服務設定中的設定為何，您仍可開啟和關閉個別元件的準確定位。
>
>如果您有&#x200B;***已***&#x200B;建立的目標元件，而且您變更此設定，您的變更不會影響這些元件。 直接對這些元件進行任何變更。

>[!CAUTION]
>
>當您選擇加入Analytics設定並選取特定`reportsuite`時，則架構會限製為發佈執行模式。 這表示追蹤僅適用於發佈例項。
>
>如果編寫執行個體上需要追蹤，則值應變更為`all`。

## 透過Script設定設定和布建 {#configuring-the-setup-and-provisioning-via-script}

身為管理員，您可能想要使用指令碼觸發設定和布建，而不是手動逐步執行精靈。 您可以透過以下方式達成此目的：

* 使用必要的引數將POST要求傳送至&#x200B;**/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json**。

您傳送的引數取決於下列專案：

* 如果您想要使用填入所有必要認證的&#x200B;**marketingcloud.properties**&#x200B;檔案，則必須傳送下列引數：

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=指向AEM頁面的路徑，以附加已建立的雲端服務設定

  例如，同時建立Analytics和Target設定，並將它們附加至we.retail頁面的curl請求將是：

  ```shell
  curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
  ```

* 如果您不想要使用&#x200B;**marketingcloud.properties**&#x200B;檔案，則必須傳送認證和引數。 例如：
   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path to an AEM page to attach the created cloud services configurations；可以定義多個路徑
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

  在此情況下，同時建立Analytics和Target設定，並將它們附加至We-Retail頁面的curl要求將是：

  ```shell
  curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
  ```
