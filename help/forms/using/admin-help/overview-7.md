---
title: 設定表單的基本概念
description: 瞭解各種可幫助您建立互動式資料擷取應用程式的表單服務。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 68e43842-cba9-47b8-b7a3-6f625dbfca08
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 設定表單的基本概念 {#basics-of-configuring-forms}

Forms服務可讓您建立互動式資料擷取使用者端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者會開發單一表單設計，Forms服務會以各種格式呈現：

* 在Adobe Reader或瀏覽器中以PDF身分顯示
* 在多種瀏覽器環境中以HTML的形式呈現，包括相容的XHTML 1.0轉譯
* 在支援Adobe Flash Player的各種瀏覽器環境中以表單指南的形式顯示。

如需Forms服務的詳細資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

使用Administration Console中的Forms頁面，您可以設定Forms服務的行為。 這些設定會套用至服務的所有呼叫。 任何透過AEM表單SDK傳送的引數都會覆寫在管理控制檯中設定的設定；但是，這些引數只會影響該特定引動。

在管理主控台中變更Forms設定後，按一下儲存。 您不需要重新啟動伺服器即可讓變更生效。 不過，在設定快取模式設定時，您可能需要停止並重新啟動Forms服務。 （請參閱[啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)。）
