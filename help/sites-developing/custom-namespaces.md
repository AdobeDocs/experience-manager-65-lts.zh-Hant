---
title: 自訂名稱空間
description: 瞭解如何定義自訂名稱空間並將其部署到AEM 6.5 LTS。
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 475a77e8e4ff0ecd19a939fd3b3c9294adf24997
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 8%

---


# 自訂名稱空間{#custom-namespaces}

瞭解如何定義自訂[名稱空間](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/4.5_Namespaces.html)並將其部署到AEM 6.5 LTS。

自訂名稱空間是`:`前面的JCR屬性的選用部分。 AEM使用數個名稱空間，例如：

+ JCR系統屬性為`jcr`
+ 適用於AEM （先前稱為Adobe CQ）屬性的`cq`
+ 針對DAM資產特有的AEM屬性的`dam`
+ 都柏林核心屬性的`dc`

...和其他許多專案。

名稱空間可用來表示屬性的範圍和目的。 建立自訂名稱空間（通常是您的公司名稱）有助於清楚識別AEM實作特有的節點或屬性，並包含您的企業特有的資料。

自訂名稱空間在[Sling存放庫初始化(repoinit)](https://sling.apache.org/documentation/bundles/repository-initialization.html)指令碼中受到管理，並在您專案的組態套件（例如，`ui.config`）中部署為OSGi組態。

## 資源 {#resources}

+ [Sling存放庫初始化(repoinit)檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)

## 代碼 {#code}

下列程式碼可用來設定`wknd`名稱空間。

### RepositoryInitializer OSGi設定

`/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~wknd-examples-namespaces.cfg.json`

```json
{
    "scripts": [
        "register namespace (wknd) https://site.wknd/1.0"
    ]
}
```

這允許在AEM中使用使用`wknd`名稱空間（如`register namespace`指示後的第一個引數所表示）的自訂屬性。 如需更進階的指令碼定義，請檢閱[Sling存放庫初始化(repoinit)檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)中的範例。
