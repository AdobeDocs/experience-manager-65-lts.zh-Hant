---
title: 技術常見問題(FAQ)
description: 關於AEM 6.5 LTS的常見技術問題。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: ec722773ce3acff1d0de861523db8ff7df552c4b
workflow-type: tm+mt
source-wordcount: '247'
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

### AEM 6.5 LTS是否支援使用者同步功能？

是的，AEM 6.5 LTS支援使用者同步處理。 AEM 6.5和6.5 LTS之間的使用者同步功能沒有變更。

### Maven Central上的Uber JAR似乎已損毀 — 這是什麼問題？

確認您正在搭配`apis`分類器使用Uber JAR。 請注意，AEM 6.5 LTS中Uber JAR的封裝結構已變更。 如需詳細資訊，請參閱[更新AEM Uber Jar版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

## 取得其他說明

如果您遇到此處未涵蓋的問題：
* 檢閱[發行說明](/help/release-notes/release-notes.md)中的已知問題。
* 請聯絡 Adobe 支援以取得協助。
