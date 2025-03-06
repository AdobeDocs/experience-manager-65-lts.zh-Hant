---
title: 在升級為MySQL的6.5.12.0期間無法備份資料庫。
description: 當使用者升級至Experience Manager 6.5.12.0並按一下[升級MySQL]時，設定管理員無法備份先前的Experience Manager Forms資料庫。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
exl-id: afc09a9f-58ef-4292-a2f2-b62d3246c006
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 在升級為MySQL的6.5.12.0期間無法備份資料庫 {#issue}

當使用者升級至Experience Manager 6.5.12.0並按一下[升級MySQL]時，組態管理員無法備份先前的Experience Manager Forms資料庫，它會顯示錯誤：

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 套用至 {#applies-to}

* Experience Manager 6.5 Forms

## 解決方案 {#solution}

若要解決此問題，請將資料庫的max_packet_size增加至100 M，或視位於{AEM_HOME}/mysql的my.ini檔案需要增加。
