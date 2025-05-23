---
title: 為IBM&amp；reg；內容管理員設定聯結器
description: 設定IBM&amp； reg； Content Manager的聯結器，以啟用AEM表單與IBM&amp； reg； Content Manager之間的通訊。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 106f01a2-39fb-474b-8c58-5ab08666b918
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 設定IBM® Content Manager的聯結器{#configuring-connector-for-ibm-content-manager}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

IBM® Content Manager聯結器可啟用AEM表單與IBM® Content Manager之間的通訊。 如需其他背景資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_63)中的「Connectors for ECM」。

## 設定IBM®內容管理員連線 {#configure-the-ibm-content-manager-connection}

1. 在管理控制檯中，按一下「服務>IBM聯結器®內容管理員」。
1. 在「資料存放區名稱」方塊中，輸入您要連線的IBM® Content Manager資料存放區名稱。 如果資料庫是本機資料庫，請輸入資料庫的名稱。 如果資料庫是遠端資料庫，請輸入其別名。
1. 在「使用者名稱」方塊中，輸入即將連線至IBM® Content Manager資料存放區之使用者的使用者ID。
1. 在密碼方塊中，輸入使用者的密碼。
1. （選擇性）在「別名連線字串」方塊中，輸入其他連線引數。 通常，此方塊應該是空的。 如需詳細資訊，請參閱您的IBM®檔案。
1. 按一下「儲存」。

## 驗證服務設定 {#validation-of-service-settings}

如果您輸入不正確的dataStore別名、使用者名稱或密碼，則會獲得以下結果，具體取決於IBM® Content Manager服務的Content Repository Connector是否正在執行：

* 如果服務已停止，當您儲存服務組態資訊時，不會出現任何錯誤。 但是，下次啟動服務時，會擲回例外狀況，而且服務不會啟動。
* 如果服務已啟動，當您儲存服務組態資訊時，服務會立即嘗試驗證認證資訊。 在這種情況下，會發生錯誤且未儲存設定資訊。
