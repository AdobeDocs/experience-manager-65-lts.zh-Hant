---
title: Oracle資料庫最大開啟游標臨界值
description: 瞭解如何在Oracle中設定開啟游標的最大值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 98663f16-6c05-4485-9bf2-a2de9d1975c8
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Oracle資料庫最大開啟游標臨界值 {#oracle-database-maximum-open-cursors-threshold}

若要在Oracle中設定開啟游標的最大值，您可能必須將此值調整為適合您應用程式的數字。 很明顯，在中等負載下，平均開啟的游標為2700。 建議您從上限3000開始。 如需詳細資訊，請前往[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758)。
