---
title: 技術常見問題(FAQ)
description: 關於AEM 6.5 LTS的常見技術問題。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 2352420843c613884ad3cae487ed048bd775e294
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# AEM 6.5 LTS技術常見問題集 {#technical-faq}

本頁旨在回答有關AEM 6.5 LTS的一些常見技術問題。

## 技術常見問題集

### `/systemalive`端點在AEM 6.5 LTS中不再可用。

設定為提供`/systemalive`端點的Felix System Ready套件組合已過時，並由Apache Felix健康情況檢查取代。 AEM 6.5 LTS中不再包含此套件組合。

新的健康情況檢查端點可在`/system/health`取得，並且是使用Apache Felix健康情況檢查實作。

如需Felix健康情況檢查架構的詳細檔案，請參閱[felix檔案](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md)。

### AEM Groovy主控台支援

由於缺少Guava相依性，AEM 6.5中使用的AEM Groovy主控台版本可能無法在AEM 6.5 LTS中運作。 新支援的AEM Groovy主控台版本是[19.0.8](https://mvnrepository.com/artifact/be.orbinson.aem/aem-groovy-console/19.0.8)。

## 取得其他說明

如果您遇到此處未涵蓋的問題：
* 檢閱[發行說明](/help/release-notes/release-notes.md)中的已知問題。
* 請聯絡 Adobe 支援以取得協助。
