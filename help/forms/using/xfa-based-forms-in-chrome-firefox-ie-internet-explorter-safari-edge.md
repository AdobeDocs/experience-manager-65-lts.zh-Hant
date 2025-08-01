---
title: 無法在Google Chrome、Firefox、Microsoft&amp；reg；Edge、Microsoft&amp；reg；Internet Explorer或Apple Safari中開啟XFA型PDF forms
description: 無法在Google Chrome、Firefox、Microsoft&amp；reg；Edge、Microsoft&amp；reg；Internet Explorer或Apple Safari中開啟XFA型PDF forms
feature: Adaptive Forms,Document Services
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a28b084e-ec74-4c05-a90c-d447792faa41
source-git-commit: 9421c7d0b5cf80a0f2d2d82034091ffe4f875af6
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 無法在Google Chrome、Firefox、Microsoft、Edge®Microsoft®Internet Explorer或Apple Safari中開啟XFA型PDF forms{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

許多近期的瀏覽器版本都包含本身對於XFA型PDF forms的有限支援。 雖然這些瀏覽器可以開啟XFA型PDF forms，但提供的功能有限。 如果您無法在現代化瀏覽器中開啟或提交以XFA為基礎的PDF表單，請使用下列其中一種方法：

* 使用[Adobe® Acrobat®](https://www.adobe.com/acrobat.html)或[Adobe® Adobe® Reader®](https://get.adobe.com/reader/)、版本8或更新版本來開啟及提交XFA型PDF forms。
* Acrobat和Reader位於Microsoft® Windows®上，可讓您設定在「受保護的檢視」模式中開啟PDF，如此可防止XFA型PDF forms開啟。 請確定Acrobat或Reader中的受保護檢視模式已停用。 如需詳細資訊，請參閱[受保護的檢視（僅限Windows）](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html)。
* (針對Forms開發人員) Adobe Experience Manager Forms也提供以下支援：

   * [將以XFA為基礎的表單轉譯為HTML5 Forms](/help/forms/using/introduction.md#key-capabilities-of-html-forms-br)，讓這些表單可以在支援HTML5的瀏覽器中開啟，包括在iPad等行動裝置上執行的瀏覽器。 表單的HTML5轉譯可維護表單設計的版面，並支援內嵌於XFA表單範本中的大部分表單邏輯(例如JavaScript、表單計算和表單驗證)。
   * [將XFA型表單轉換為行動回應式最適化Forms](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)。 這些表單提供回應式版面、個人化功能，並視需要新增或移除欄位或區段以動態調整以符合使用者的回應。 此外，這些套件也提供各種資料來源的現成聯結器、記錄檔案功能，以及與Adobe Analytics的輕鬆連線，以進行效能評估。 如需詳細資訊，請參閱[主要功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=zh-Hant)
如此一來，您在XFA表單中的技術投資就能受到保護，並持續為使用者提供最佳體驗。 如需詳細資訊，請參閱[Adobe Experience Manager Forms產品檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=zh-Hant)。
