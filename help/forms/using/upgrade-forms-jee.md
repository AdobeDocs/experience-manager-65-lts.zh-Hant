---
title: 在JEE上升級至AEM 6.5 Forms
description: 您可以從AEM 6.1 Forms、AEM 6.2 Forms和LiveCycle ES4 SP1直接升級至AEM 6.3 Forms。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade,AEM Forms on JEE
exl-id: 643bc966-b2d8-4626-8c25-b63c8909287e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# 在JEE上升級至AEM 6.5 Forms {#upgrade-to-aem-forms-jee}

JEE上的AEM 6.5.18.0 Forms提供兩種型別的安裝程式：完整安裝程式和修補程式安裝程式。

**完整安裝程式**：您可以使用JEE完整安裝程式上的[AEM 6.5.18.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)來設定新的AEM Forms執行個體，或從JEE上的AEM 6.5.x.x Forms升級為JEE上的AEM 6.5.18.0 Forms。

**修補程式安裝程式**： JEE修補程式安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)上的[AEM 6.5.18.0適用於已使用AEM 6.5.x.x版本的客戶。 您可以使用修補程式安裝程式來升級至最新版AEM Forms。

下表說明使用完整安裝程式和修補程式安裝程式的情境。

![完整和修補程式安裝程式案例](assets/full-and-patch-installer.png)

執行以下程式，使用完整安裝程式將JEE上的現有AEM Forms 6.5.x.x升級為JEE上的AEM 6.5.18.0 Forms：

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載JEE安裝程式上的AEM 6.5 Forms。 您需要有效的維護與支援合約才能使用安裝程式。
1. 請參閱[升級檢查清單與規劃](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65)，瞭解如何執行檢查以確保升級成功。
1. 請參閱[準備升級至AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65)以瞭解並執行工作，確保升級正確執行並將伺服器停機時間降到最低。
1. 根據您現有的環境和應用程式伺服器，選擇下列其中一份檔案並依照指示操作。

   * [從AEM 6.3或AEM 6.4 Forms升級至適用於JBoss的AEM 6.5 Forms](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [從AEM 6.3或AEM 6.4 Forms升級至適用於WebSphere的AEM 6.5 Forms](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [從AEM 6.3或AEM 6.4 Forms升級至適用於JBoss Turnkey的AEM 6.5 Forms](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

無法從LiveCycle ES2、LiveCycle ES3、AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms直接升級至AEM 6.5 Forms。 您可以對一或多個版本的LiveCycle或AEM Forms執行中繼升級，然後升級至AEM 6.5 Forms。 如需中繼版本和對應升級指示的清單，請參閱[選擇升級路徑](upgrade.md)。
