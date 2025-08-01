---
title: '[!DNL Experience Manager Assets]與 [!DNL Adobe Workfront]整合'
description: ' [!DNL Assets] 與 [!DNL Workfront]之間的整合簡介'
role: Admin,Leader,Architect
feature: Workfront Integrations and Apps
hide: true
solution: Experience Manager, Workfront
exl-id: 5181d278-2e6e-41f7-891e-1067a03de016
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager Assets]與[!DNL Adobe Workfront]整合 {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

[!DNL Adobe Workfront]是工作管理應用程式，可協助您在一個地方管理整個工作生命週期。 [!DNL Workfront]與[!DNL Adobe Experience Manager Assets]之間的整合可讓組織在本質上連線工作和數位資產管理，藉以改善內容速度和上市時間。 在Workfront中管理其工作的情況下，使用者可以存取所需的檔案和影像。

[!DNL Workfront for Experience Manager enhanced connector]可啟用具有端對端工作流程的增強型業務流程，並提供個人化的端對端使用者端體驗和中央儲存空間。 Adobe提供標準聯結器和增強型聯結器，整合這兩個解決方案。 如需比較，請參閱下列支援的功能，並參閱[ [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience)的新功能。

[!DNL Workfront for Experience Manage enhanced connector]可讓您的組織：

* 在Workfront中自動建立連結的Experience Manager資料夾，並根據Workfront投資組合、計畫和專案組織資料夾。
* 將Workfront專案中繼資料與連結的Experience Manager資料夾同步。
* 新版本的Experience Manager中繼資料更新。
* 使用Workfront工作流程，根據可設定的條件設定Experience Manager物件狀態。
* 將資產發佈到Experience Manager發佈環境或Brand Portal。

檢視增強型聯結器的平台支援和[必要條件](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience)。

>[!IMPORTANT]
>
>* Adobe僅需要透過認證合作夥伴或[!DNL Adobe Professional Services]來部署及設定[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未透過認證合作夥伴或[!DNL Adobe Professional Services]進行部署與設定，則Adobe不支援此功能。
>
>* Adobe可能會發行[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]的更新，使此聯結器成為多餘的；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
>
>* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請瀏覽至[封裝管理員](/help/sites-administering/package-manager.md)左側窗格中可用的`digital.hoodoo`群組。
>
>* 請參閱Experience Manager Assets增強型聯結器的[Workfront合作夥伴認證測驗](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 如需有關考試的資訊，請參閱[考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。

## 比較[!DNL Assets]與[!DNL Workfront]之間的不同整合 {#feature-parity-matrix}

以下是[!DNL Assets]與[!DNL Workfront]之間各種整合型別所提供功能的詳細資料。

| 功能 | 描述 | [!DNL Workfront]和[!DNL Assets Essentials] *沒有聯結器（現成）* | [!DNL Workfront for Experience Manager enhanced connector] *需要聯結器* | Workfront和[!DNL Experience Manager as a Cloud Service] *無聯結器（現成）* |
|----|----|----|-----|-----|
| 部署方法 | 適合哪個[!DNL Assets]產品。 | Assets Essentials | Adobe Managed Services，內部部署 | Cloud Service |
| **一般** |
| 將數位檔案從[!DNL Workfront]傳送至[!DNL Assets] | 最新版本的WF檔案可以上傳到AEM Assets，這會連結為檔案的新版本。 | ✓ | ✓ | ✓ |
| 手動將AEM資料夾連結至Workfront物件 | 現有的AEM資料夾可以連結為Workfront資料夾，其子資產則會連結為新的Workfront檔案。 | ✓ | ✓ | ✓ |
| 將[!DNL Assets]連結至Workfront物件 | AEM中的現有資產可以連結至新的Workfront檔案，或作為現有檔案的新版本。 | ✓ | ✓ | ✓ |
| 新增至連結資料夾的Assets會自動傳送至AEM | 如果檔案新增至連結的資料夾，則關聯的資產會自動上傳至AEM Assets作為新資產。 | ✓ | ✓ | ✓ |
| 從Workfront下載連結的AEM Assets | 在Workfront中連結資產時，使用者可以下載資產的位元組。 | ✓ | ✓ | ✓ |
| 在Workfront中搜尋AEM Assets | Workfront中的AEM Assets選擇器允許以全文搜尋資產。 | ✓ | ✓ | ✓ |
| 在Workfront中搜尋AEM資料夾 | Workfront中的AEM Assets選擇器允許以全文搜尋資料夾。 | ✓ | ✓ | ✓ |
| 從Workfront檢視及導覽AEM資料夾階層 | Workfront中的AEM Assets選擇器可讓您瀏覽受以下限制的AEM Assets階層：   在AEM中設定的使用者關聯存取控制項和許可權。 | ✓ | ✓ | ✓ |
| 在AEM時間軸中追蹤資產版本 | 維護Workfront和AEM之間的檔案版本記錄。 | ✓ | ✓ | ✓ |
| 在Workfront中從AEM Assets取消連結Assets | 從AEM連結的現有資產可以從關聯的Workfront檔案中取消連結。 這不會刪除AEM內的原始資產。 | ✓ | ✓ | ✓ |
| 從Workfront將新版本的資產新增到AEM Assets | 在Workfront中將新新增的版本新增到檔案上時，使用者可以將新版本傳送到AEM以取代現有版本。 | ✓ | ✓ | ✓ |
| 按一下將使用者直接連結至AEM時，在Workfront中連結Assets | 系統會將使用者導向至AEM，以便從Workfront預覽連結的資產。 | ✓ | ✓ | 近期 |
| 在Workfront中自動建立連結的AEM資料夾 | 使用專案狀態，在Workfront中自動建立連結的AEM資料夾。 根據AEM產品組合、計畫和專案自動設定Workfront資料夾。 | 否 | ✓ | 否 |
| 從Workfront直接導覽至AEM存放庫 | 允許使用者導覽至Workfront中設定的可用AEM存放庫。 | ✓ | 否 | ✓ |
| 在Workfront中建立連結的AEM資料夾 | 使用「檔案」標籤中的選項，在Workfront中手動建立連結的AEM資料夾。 | ✓ | 否 | ✓ |
| 評論同步 | 自動將資產評論從[!DNL Workfront]同步至[!DNL Assets] | 否 | ✓ | 否 |
| 支援多個Workfront環境連線至單一AEM環境 | 來自多個Workfront環境的使用者可以連線至單一AEM環境。 | ✓ | 否 | ✓ |
| 支援多個AEM環境連線至單一Workfront環境 | 單一Workfront環境內的使用者可以在多個AEM環境之間傳送或連結資產。 | ✓ | ✓ | ✓ |
| **中繼資料** |
| 將Workfront資產中繼資料對應至AEM Assets | Workfront物件和自訂表單屬性可能會對應至AEM資產中繼資料屬性。 值會在初始上傳/連結時推送。 | ✓ | ✓ | ✓ |
| 在Workfront中自動建立檔案自訂Forms | 使用AEM工作流程將自訂表單附加至Workfront檔案、任務和問題。 | 否 | ✓ | 否 |
| 在AEM Assets和Workfront之間雙向自動更新中繼資料 | 在AEM Assets和Workfront之間自動更新中繼資料。 資產必須先從Workfront推送至AEM，且Workfront資產中繼資料必須對應至AEM資產，雙向中繼資料更新才能正常運作。 | 否 | ✓ | 否 |
| Workfront中可將中繼資料對應至AEM的即時檢視 | 在Workfront「檔案詳細資訊」和「檔案摘要」面板中，檢視更新後對應至AEM的中繼資料。 | ✓ | 否 | ✓ |
| 將更新的Workfront中繼資料即時推送到AEM | 自動將對應的Workfront中繼資料更新至AEM，無需重新推送資產或新版本的資產。 | ✓ | 否 | ✓ |
| 將Workfront中繼資料對應至AEM Assets資料夾 | 將Workfront專案中繼資料與連結的AEM資料夾同步。 | 否 | ✓ | ✓ |
| 新版本的AEM中繼資料更新 | AEM中的設定可決定Workfront中新版本的資產是否也會推進對其中繼資料所做的任何變更。 | 否 | ✓ | 否 |
| 在Workfront中變更自訂AEM時自動更新Forms中繼資料 | AEM可讓您訂閱Workfront中檔案表單的更新。 因此，Workfront檔案自訂表單中繼資料的任何更新都會編輯對應AEM中繼資料欄位的值。 | 否 | ✓ | 否 |
| **工作流程（現成可用）** |
| 在連結的Assets上建立新校訂版本 | 在Workfront中連結資產時，會自動產生校訂。 | 否 | 自訂 | 否 |
| 在Workfront物件上設定狀態 | 使用Workfront工作流程根據可設定的條件設定AEM物件狀態 | 否 | ✓ | 近期 |
| 將Assets發佈到AEM發佈環境或Brand Portal | 讓Workfront使用者可選擇自動將連結的資產發佈至AEM發佈環境或Brand Portal。 | 否 | ✓ | 近期 |
