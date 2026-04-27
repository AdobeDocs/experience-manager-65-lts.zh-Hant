---
product: adobe experience manager
description: Adobe Experience Manager 6.5 LTS檔案。
git-repo: https://github.com/AdobeDocs/experience-manager-65-lts.zh-Hant
index: true
type: Documentation
solution: Experience Manager, Experience Manager 6.5 LTS
landing-page-name: experience-manager-lts
landing-page-breadcrumb-title: AEM 6.5 LTS
version: Experience Manager 6.5 LTS
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: 530dd0c09d5ef82f304ffff118cd52935c24cd98
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 2%

---


# 內部使用的中繼資料

GitHub編寫系統中的中繼資料具有階層式架構，而且會定義以下相對於前一項的遞增層級。

1. metadata.md
1. ToC
1. 文章

metadata.md檔案中定義的中繼資料會套用至整個存放庫，但可以在ToC和文章層級覆寫。 中繼資料的任何覆寫都應該儘可能在最低層級進行。

experience-manager-cloud-service.en存放庫中的中繼資料是最低要求。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`
* `contentOwner` （僅在`/help/assets`下的核心資產內容上）
