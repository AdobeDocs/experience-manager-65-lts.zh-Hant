---
title: PDF Generator備份限制
description: 瞭解PDF Generator備份限制。 PDF Generator使用的暫存目錄無法備份，因為它以設定的間隔清除內容。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f76ce3be-6d50-4531-a982-2e902f866208
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---

# PDF Generator備份限制 {#pdf-generator-backup-limitations}

PDF Generator用來轉換檔案的暫存目錄無法備份。 即使服務已正確還原，資料仍可能會遺失，因為PDF Generator會依設定的時間間隔檢視及清除臨時目錄的內容。
