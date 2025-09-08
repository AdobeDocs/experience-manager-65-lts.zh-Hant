---
title: 技術常見問題集 (FAQ)
description: 關於 AEM 6.5 LTS 的常見技術問題集。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: f983fc1edc613feaa070c4e82a92aabab9d50cbb
workflow-type: ht
source-wordcount: '247'
ht-degree: 100%

---

# AEM 6.5 LTS 技術常見問題集 {#technical-faq}

此頁面旨在回答關於 AEM 6.5 LTS 的一些常見技術問題。

## 技術常見問題集

### `/systemalive` 端點在 AEM 6.5 LTS 中不再可用。

已設定為提供 `/systemalive` 端點的 Felix System Ready 搭售方案已棄用，並以 Apache Felix Health Check 取代。AEM 6.5 LTS 不再包含此搭售方案。

新的健康情況檢查端點可在 `/system/health` 取得，並使用 Apache Felix Health Check 實施。

如需關於 Felix Health Check 框架的詳細文件，請參閱 [Felix 文件](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md)。

### AEM Groovy 主控台支援

在 AEM 6.5 中使用的 AEM Groovy 主控台版本因為缺少 guava 相依性，可能無法在 AEM 6.5 LTS 中運作。新支援的 AEM Groovy 主控台版本為 [19.0.8](https://github.com/orbinson/aem-groovy-console/releases/download/19.0.8/aem-groovy-console-all-19.0.8.zip)。

### AEM 6.5 LTS 是否支援使用者同步？

是的，AEM 6.5 LTS 支援使用者同步。AEM 6.5 和 6.5 LTS 之間的使用者同步功能沒有變更。

### Maven Central 上的 Uber JAR 似乎已損壞，發生什麼問題？

請確認您使用的是具有 `apis` 分類器的 Uber JAR。請注意，在 AEM 6.5 LTS 中，Uber JAR 的封裝結構有所變更。如需詳細資訊，請參閱[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

## 取得其他協助

若您遇到此處未涵蓋的問題：
* 請審閱[發行說明](/help/release-notes/release-notes.md)，了解已知問題。
* 請聯絡 Adobe 支援以取得協助。
