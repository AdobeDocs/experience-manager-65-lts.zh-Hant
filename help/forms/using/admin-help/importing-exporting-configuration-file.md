---
title: 匯入和匯出組態檔
description: 瞭解如何匯入和匯出設定檔案，以編輯伺服器偏好設定或設定其他AEM表單產品執行個體。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 92fdcee3-2007-4bbc-be4b-426d65b8dbc1
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 匯入和匯出組態檔 {#importing-and-exporting-the-configuration-file}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

使用「手動組態」頁面，以XML格式下載組態設定的復本。 此檔案中的設定可控制所有伺服器偏好設定。 然後，您可以編輯檔案並將其上傳回伺服器。 您也可以使用檔案來設定另一個AEM表單產品例項。

為了避免安全性風險，匯出的組態檔中不包含目錄伺服器的繫結密碼值。 在將檔案匯入新系統之前，請先更新XML檔案中的密碼。

>[!NOTE]
>
>匯入設定檔案會根據檔案中的資訊重新設定AEM表單。 只有熟悉AEM表單產品和XML的系統管理員或專業服務顧問才應考慮修改組態檔。 例如，他們可能需要編輯設定檔案，以重新設定損毀的設定。

**匯出組態資訊**

1. 在Administration Console中，按一下「設定>使用者管理>組態>匯入及匯出組態檔」。
1. 按一下「匯出」。 如果您使用Microsoft Internet Explorer，系統會提示您指定儲存檔案的位置。 如果您使用Firefox，檔案會儲存在案頭上。

**匯入組態資訊**

1. 在Administration Console中，按一下「設定>使用者管理>組態>匯入及匯出組態檔」。
1. 按一下「瀏覽」以尋找組態檔，按一下「匯入」，然後按一下「確定」。
