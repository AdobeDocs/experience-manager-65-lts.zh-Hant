---
title: EMC Documentum&amp；reg；使用者的聯結器備份策略
description: 瞭解如何為EMC Documentum&amp；reg；使用者建立聯結器備份策略。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 019e1a9b-c26c-429f-8153-fceeb85f7096
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# EMC Documentum®使用者的Connector備份策略 {#backup-strategy-for-connector-for-emc-documentum-users}

如果您已安裝Connector for EMC Documentum® ，則除了本章的說明以外，您的備份與復原策略還必須包括備份（或復原）安裝ECM系統的電腦。 (請參閱ECM Documentum®檔案)。

使用ECM存放庫並執行下列工作，備份AEM表單環境：

* 依照本檔案所述的指示，備份AEM表單。
* 依照[備份EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server)中的指示來備份您的ECM Documentum®系統。

使用ECM存放庫並執行下列工作來還原AEM表單環境：

* 依照[還原EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server)中的指示，還原您個別的ECM系統。
* 依照本檔案所述指示還原AEM表單。
