---
title: 變更字元集
description: 您可以指定用來編碼輸出資料流的字元集。 瞭解如何變更字元集。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 1d614736-5897-4fd3-9ca4-94b115139ba3
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# 變更字元集 {#change-the-character-set}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以指定用來編碼輸出資料流的字元集。

1. 在管理主控台中，按一下&#x200B;**[!UICONTROL 服務>輸出]**。
1. 在「國際化」下的「字元集」清單中，選取字元集。 此設定相依於透過API指定的`TransformationFormat`和`PrintFormat`。 若要指定所列字元集以外的字元集，請選取「自訂」，並在顯示的方塊中指定編碼值。

   如果`TransformationFormat`是PDF，而PDF/A或`PrintFormat`是PCL、PostScript、Zebra標籤、IPL、DPL、TPCL、GenericColorPCL或GenericPSLevel3，則僅支援特定字元集。

   字元集必須是有效的正式名稱。 預設值為ISO-8859-1。

1. 按一下「**[!UICONTROL 儲存]**」。
