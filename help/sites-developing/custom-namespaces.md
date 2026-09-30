---
title: 自訂名稱空間
description: 瞭解如何定義自訂名稱空間並將其部署到AEM 6.5 LTS。
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
subfeature_v2:
  - id: cd14456d-a492-4b5c-8a82-1fbd4460dbd2
    internal-label: Java Content Repository
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: d1f055e0688c24b55f80c7e2be974fe1d28ae8d5
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 3%
---

# 自訂名稱空間{#custom-namespaces}

瞭解如何定義自訂[名稱空間](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/jcr/1.0/4.5_Namespaces.html)並將其部署到AEM 6.5 LTS。

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
