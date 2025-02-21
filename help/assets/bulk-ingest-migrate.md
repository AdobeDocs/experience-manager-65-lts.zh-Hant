---
title: 安裝Feature Pack 18912以進行大量資產移轉
description: Feature Pack 18912可讓您透過FTP大量擷取資產，或將資產從Dynamic Media Classic移轉至Adobe Experience Manager上的Dynamic Media。 Adobe支援提供此選用的Feature Pack。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# 安裝Feature Pack 18912以進行大量資產移轉{#installing-feature-pack-for-bulk-asset-migration}

功能套件18912的安裝是&#x200B;*選擇性*。

Feature Pack 18912可讓您透過FTP將資產直接大量擷取到Adobe Experience Manager上的Dynamic Media - Scene7模式。 它也可讓您將資產從Dynamic Media Classic移轉至Experience Manager上的Dynamic Media - Scene7模式。 功能套件可從[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)取得。

>[!IMPORTANT]
>
>您可以使用Feature Pack自行將資產從Dynamic Media Classic大量移轉至Experience Manager中的Dynamic Media - Scene7模式。 您也可以使用Dynamic Media Classic中的FTP功能來大量移轉資產。 不過，由於涉及的複雜性，Adobe並&#x200B;*不*&#x200B;建議您使用其中一種方法。
>
>因此，透過[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)完成時，此移轉功能套件僅&#x200B;*支援*&#x200B;作為移轉專案的一部分。

安裝Feature Pack之前，請先建立服務使用者，並將該資訊提供給Adobe支援。

另請參閱[設定Dynamic Media - Scene7模式](/help/assets/config-dms7.md)。

**若要安裝Feature Pack 18912以進行大量資產移轉：**

1. 在您的Experience Manager執行個體中，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**，然後選取&#x200B;**[!UICONTROL 建立使用者]**。 此服務使用者必須擁有`/content/dam.`的&#x200B;*讀取/寫入*&#x200B;許可權
1. 在&#x200B;**[!UICONTROL 識別碼]**&#x200B;與&#x200B;**[!UICONTROL 密碼]**&#x200B;欄位中，輸入使用者名稱與密碼；例如，**FTP使用者**。 此名稱會以建立資產之使用者的身分顯示在時間軸中。 從FTP上傳資產時，資產會在上傳至FTP伺服器並推送至Experience Manager時被視為已建立。
1. 請連絡[Experience Manager的Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support)，要求存取Feature Pack 18912以進行下載。 當您聯絡支援時，可能需要下列資訊：

   * 您的Author執行個體的伺服器IP位址，包括連線埠號碼（根據預設，連線埠號碼為4502）。
   * 上一步驟中的Experience Manager服務使用者名稱和密碼。

1. Experience Manager的Adobe客戶支援為您提供FTP憑證和Feature Pack 18912的存取權。
1. 收到Feature Pack 18912時，請加以安裝。

   如需在Experience Manager中使用軟體散發與套件的詳細資訊，請參閱[如何使用套件](/help/sites-administering/package-manager.md)。
