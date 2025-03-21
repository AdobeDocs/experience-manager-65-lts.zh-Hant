---
title: 將字體設為可用
description: 確定表單內使用的字型可用於託管AEM表單的J2EE應用程式伺服器。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2861bde5-b373-4ab2-9808-7d32ef1dc925
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%

---

# 將字體設為可用 {#make-fonts-available}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

確定表單內使用的字型可用於託管AEM表單的J2EE應用程式伺服器。 例如，請考量下列情況。 表單設計人員將字型新增到Designer使用的字型目錄中，並建立在不同電腦上使用該字型的表單。 為了讓Output服務使用字型，請將其放置在Customer fonts目錄中。 如果Customer fonts目錄不存在，請在裝載AEM表單的J2EE應用程式伺服器上建立目錄。

如需其他字型設定的詳細資訊，請參閱[設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。

**指定Customer字型目錄的位置**

1. 在管理控制檯中，按一下設定>核心系統設定>設定。
1. 在「系統字型目錄的位置」方塊中，輸入Customer字型目錄的路徑。 可以新增多個目錄，以分號&#x200B;**；**&#x200B;分隔
1. 按一下「確定」。
1. 重新啟動已安裝AEM表單的系統。

>[!NOTE]
>
>字型是從Windows系統字型快取中挑選的，需要重新啟動系統才能更新快取。 指定Customer字型目錄後，請務必重新啟動安裝AEM表單的系統。
