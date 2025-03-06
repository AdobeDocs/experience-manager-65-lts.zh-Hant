---
title: 啟用和停用安全備份模式
description: 在「備份設定值」頁面上，您可以在安全的備份模式中操作AEM表單，以便可靠地備份資料庫和全域檔案儲存(GDS) (GDS)目錄。 瞭解如何啟用和停用安全備份模式。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 34381caa-154e-479c-b475-7b3549909e9a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 啟用和停用安全備份模式 {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

在「備份設定值」頁面上，您可以在安全的備份模式中操作AEM表單，以便可靠地備份資料庫和全域檔案儲存(GDS) (GDS)目錄。

AEM表單處於安全備份模式時，除了不會主動從GDS目錄移除檔案外，其他功能仍會正常運作。

>[!NOTE]
>
>設定這個選項不會備份您的系統；它會將您的系統準備好，以進行備份。

## 啟用安全備份模式 {#enable-safe-backup-mode}

1. 在管理控制檯中，按一下「設定>核心系統設定>備份設定」。
1. 在「備份設定值」頁面上，選取「在安全備份模式下作業」，然後按一下「確定」。

>[!NOTE]
>
>如果系統已經在安全備份模式下執行，當您按一下「確定」時，將不會建立新的保留。

## 停用安全備份模式 {#disable-safe-backup-mode}

1. 在管理控制檯中，按一下「設定>核心系統設定>備份設定」。
1. 在「備份設定值」頁面上，取消選取「在安全備份模式下作業」，然後按一下「確定」。
