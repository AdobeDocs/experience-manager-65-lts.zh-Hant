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
removedfrom6.5.2025: 'yes'
exl-id: f76ce3be-6d50-4531-a982-2e902f866208
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%
---
# PDF Generator備份限制 {#pdf-generator-backup-limitations}

PDF Generator用來轉換檔案的暫存目錄無法備份。 即使服務已正確還原，資料仍可能會遺失，因為PDF Generator會依設定的時間間隔檢視及清除臨時目錄的內容。
