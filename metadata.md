---
product: adobe experience manager
description: Adobe Experience Manager 6.5 LTS檔案。
git-repo: https://github.com/AdobeDocs/experience-manager-65-lts.zh-Hant
index: y
type: Documentation
solution: Experience Manager
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: 766b9eaad3ebe43db3659e8ba4afb8b4496a1f3a
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 52%

---


# 內部使用的中繼資料

GitHub編寫系統中的中繼資料具有階層式架構，而且會定義以下相對於前一項的遞增層級。

1. metadata.md
1. ToC
1. 文章

metadata.md 檔案中所定義的中繼資料會套用到整個存放庫，但可以在 ToC 和文章層級被覆寫。 中繼資料的任何覆寫都應該盡量在最低層級進行。

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
