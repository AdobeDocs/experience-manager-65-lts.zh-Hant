---
title: 管理憑證撤銷清單
description: 瞭解如何管理憑證撤銷清單。 您可以使用「信任存放區管理」來匯入、編輯和刪除憑證撤銷清單(CRL)。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: a5e49cc8-cd46-47e6-8ff3-655dcf23296a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 管理憑證撤銷清單{#managing-certificate-revocationlists}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

使用「信任存放區管理」，您可以匯入、編輯和刪除憑證撤銷清單(CRL)。 支援Base64和DER編碼的憑證撤銷清單。

## 匯入CRL {#import-a-crl}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「憑證撤銷清單」，然後按一下「匯入」。
1. 在「別名」方塊中，輸入CRL的識別碼。
1. 按一下「瀏覽」來尋找CRL，然後按一下「確定」。

## 匯出CRL {#export-a-crl}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「憑證撤銷清單」。
1. 按一下CRL的別名以便匯出，然後按一下「匯出」。
1. 請依照指示匯出CRL。 CRL會以Base64編碼匯出。
1. 按一下「確定」。

## 刪除CRL {#delete-a-crl}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「憑證撤銷清單」。
1. 選取要刪除的CRL核取方塊，按一下「刪除」，然後按一下「確定」。
