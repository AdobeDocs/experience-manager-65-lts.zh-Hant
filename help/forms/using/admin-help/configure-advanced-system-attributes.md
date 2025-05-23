---
title: 設定進階系統屬性
description: 您可以在「設定進階系統屬性」頁面修改組態檔中的某些設定值，而不需要匯出、編輯及匯入檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f1a68461-c66a-4ea4-902b-644c620ea3f6
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 設定進階系統屬性 {#configure-advanced-system-attributes}

您可以在「設定進階系統屬性」頁面修改組態檔中的某些設定值，而不需要匯出、編輯及匯入檔案。 （請參閱[匯入及匯出組態檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。）

1. 在管理控制檯中，按一下&#x200B;**[!UICONTROL 設定>使用者管理>設定>設定進階系統屬性]**。
1. （選擇性）變更下列任一作業階段屬性：

   **工作階段逾時限制（分鐘）：**&#x200B;使用者自動登出系統前的時間（分鐘）。 依預設，無論活動或閒置狀態為何，AEM都會在2小時後形成元件（例如Workbench）逾時，且使用者必須重新登入。 有效值為`1`到`1440`。 預設值為`120` （2小時）。 此設定會更新組態檔中的`SAML/Producer/assertionValidityInMinutes`專案金鑰。

   >[!NOTE]
   >
   >您不應該將工作階段逾時限制設定在10分鐘以下，因為系統可能無法正常運作。 建議值為10-120 （分鐘）。

   **判斷提示臨界值（秒）：**&#x200B;因叢集中AEM表單應用程式伺服器之間的系統時間差異，而延遲的緩衝時間。 AEM表單會根據此屬性中指定的時間量（以秒為單位），將使用者的登入時間回溯。 有效值為`0`到`3600`。 預設值為`60`。 此設定會更新組態檔中的`SAML/Producer/assertionThresholdInSeconds`專案金鑰。

   **宣告的最大允許續約次數：**&#x200B;使用者工作階段不需登入即可透明續約的最大次數。 有效值為`0`到`9999`。 值為`0`表示斷言不會更新。 預設值為 10。此設定會更新組態檔中的`SAML/Producer/maxAssertionRenewalCount`專案金鑰。

1. （選擇性）變更下列任何目錄同步處理屬性：

   **同步統計記錄日誌：**&#x200B;指定使用者管理是否在同步處理期間記錄詳細的統計資料。 （請參閱[在同步處理期間啟用或停用詳細記錄](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)。）

   **同步處理完成程式Cron運算式：**&#x200B;使用者管理重試同步失敗的間隔。 （請參閱[設定目錄同步處理重試選項](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)。）

   **叢集作業鎖定逾時（分鐘）：**&#x200B;用於叢集環境。 如果某個節點上的同步作業失敗，且叢集鎖定未釋放，此值會指定另一個節點在強製取得鎖定之前等待的分鐘數。 預設值為`15`分鐘。 有效值為`1`到`1440`分鐘。

1. （選擇性）變更下列屬性，然後按一下&#x200B;**[!UICONTROL 確定]**：

   **使用者管理員事件稽核：**&#x200B;選取此選項可啟用目錄同步化事件和驗證事件（例如成功、失敗和鎖定）的稽核。 依預設，除非您安裝需要稽核的元件(例如Rights Management)，否則不會選取此選項。 此設定會更新組態檔中的`APSAuditService`專案金鑰。

   **自動建立動態群組：**&#x200B;啟用根據電子郵件網域自動建立動態群組。 （請參閱[建立動態群組](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)。）

您也可以按一下「重新載入」，回覆成原始的「使用者管理」設定。
