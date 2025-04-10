---
title: 輸出服務概觀
description: 輸出可讓您將XML表單資料與Designer中建立的表單設計合併，以建立多種格式的檔案輸出資料流。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5708ff03-4af7-47a3-b385-34a3a94f7a7b
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 輸出服務概觀 {#overview-of-output-service}

輸出可讓您將XML表單資料與Designer中建立的表單設計合併，以建立多種格式的檔案輸出資料流。 輸出資料流可以傳送到網路印表機、本機印表機或磁碟檔案

您可以使用管理主控台中的「輸出」頁面來管理「輸出」服務。 若未透過AEM Forms API指定同等設定，則會在執行階段使用您設定的設定。 透過AEM Forms SDK完成的設定會覆寫使用管理控制檯設定的設定。

如需輸出服務的詳細資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_61)。

在管理控制檯的「輸出」頁面上，您可以執行幾項工作：

* 指定國際化的字元集。 （請參閱[變更字元集](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)。）
* 指定URL、URI、XCI和檔案位置的絕對和相對路徑。 （請參閱[指定輸出](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)的檔案位置。）
* 設定快取大小和原則。 （請參閱[指定快取模式](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode)和[設定快取設定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)。）
* 讓字型可在應用程式伺服器上使用。 （請參閱[讓字型可用](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)。）
* 指定要嵌入的字型。 （請參閱[指定要內嵌的字型](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)。）
* 指定XCI設定選項。 （請參閱[指定XCI組態選項](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)。）
* 指定安全性設定。 （請參閱[指定安全性設定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)。）

變更設定後，按一下「儲存」以將其套用至「輸出」。 您不需要重新啟動伺服器即可讓變更生效，但在設定快取設定時，您可能需要重新啟動輸出服務。
