---
title: 技術常見問題集 (FAQ)
description: 關於 AEM 6.5 LTS 的常見技術問題集。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: f994a8712a403083de1edc62579846ba99bd3afd
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 78%

---

# AEM 6.5 LTS 技術常見問題集 {#technical-faq}

此頁面旨在回答關於 AEM 6.5 LTS 的一些常見技術問題。

## 技術常見問題集

### `/systemalive` 端點在 AEM 6.5 LTS 中不再可用。

已設定為提供 `/systemalive` 端點的 Felix System Ready 搭售方案已棄用，並以 Apache Felix Health Check 取代。 AEM 6.5 LTS 不再包含此搭售方案。

新的健康情況檢查端點可在 `/system/health` 取得，並使用 Apache Felix Health Check 實施。

如需關於 Felix Health Check 框架的詳細文件，請參閱 [Felix 文件](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md)。

### AEM Groovy 主控台支援

AEM 6.5 中所使用的 AEM Groovy 主控台版本因為缺少 guava 相依性，可能無法在 AEM 6.5 LTS 中運作。 新支援的 AEM Groovy 主控台版本為 [19.0.8](https://github.com/orbinson/aem-groovy-console/releases/download/19.0.8/aem-groovy-console-all-19.0.8.zip)。

#### AEM Groovy 主控台所需的其他設定

如果您在使用 AEM Groovy 主控台，必須針對 `com.adobe.granite.apicontroller.FilterResolverHookFactory` 明確新增下列 OSGi 設定。 將 `aem-groovy-console-bundle` 新增至 `org.apache.sling.distribution.api` 金鑰的允許組合包清單，擴充平台預設值：

```
"org.apache.sling.distribution.api": "com.adobe.*,com.day.*,org.apache.sling.*,aem-groovy-console-bundle"
```

### AEM 6.5 LTS 是否支援使用者同步？

是的，AEM 6.5 LTS 支援使用者同步。 AEM 6.5 和 6.5 LTS 之間的使用者同步功能沒有變更。

### Maven Central 上的 Uber JAR 似乎已損壞，發生什麼問題？

請確認您使用的是具有 `apis` 分類器的 Uber JAR。 請注意，在 AEM 6.5 LTS 中，Uber JAR 的封裝結構有所變更。 如需詳細資訊，請參閱[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

### AEM 6.5 LTS是否支援`jakarta.*`封裝名稱空間（例如`jakarta.annotation`）？

否。 AEM 6.5 LTS不支援移轉到`jakarta.*`封裝名稱空間的Sling成品。 在您的程式碼和相依性中使用`javax.*`對等專案，例如Sling模型中的`javax.annotation.PostConstruct`而非`jakarta.annotation.PostConstruct`。 AEM 6.5 LTS中的Sling模型實作只辨識`javax.*`註釋，因此在初始化期間會無訊息地忽略`jakarta.*`註釋。

如需詳細資訊，請參閱知識庫文章[在AEM 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-30339)上具有`jakarta.annotation.PostConstruct`的Sling模型失敗。

## 取得其他協助

若您遇到此處未涵蓋的問題：
* 請審閱[發行說明](/help/release-notes/release-notes.md)，了解已知問題。
* 請聯絡 Adobe 支援以取得協助。
