---
title: 常見問題集 (FAQ)
description: 關於 AEM 6.5 LTS 的常見問題集。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: d18c9dc3-fdcc-4558-b9b6-ecf1ce61048a
source-git-commit: 9f9da819550b93d7a06b151962bf41751ecbc8b3
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 49%

---

# AEM 6.5 LTS 常見問題集 (FAQ) {#faq}

此頁面旨在回答一些關於 AEM 6.5 LTS 的常見問題。

## Adobe 為什麼要發行 AEM 的 6.5 LTS 版本？

Adobe 始終致力於確保其提供之應用程式的安全性和穩定性。AEM 6.5 Long-term Support 為 AEM 6.5 的未來更新奠下基礎。值得注意的是，AEM 6.5 LTS 包含對於 Oracle Java 17 和 Java 21 的支援，且會成為接收 AEM 新功能和創新的 AEM 分支。

## 我是內部部署客戶，如果我不升級至 AEM 6.5 LTS 會發生什麼事？

AEM 6.5 LTS 包含重要的安全性和穩定性更新，包括對於 Oracle Java 17 和 Java 21 的支援。雖然 Adobe 會於未來至少 2 年內繼續支援 AEM 6.5，但建議各個組織開始規劃升級至 6.5 LTS。

## 如果我升級至AEM 6.5 LTS，現有的自訂和整合是否會受到影響？

雖然 AEM 6.5 LTS 以維持回溯相容性為目標，但有一些舊版功能和成品已移除。
請務必審閱[發行說明](/help/release-notes/release-notes.md#deprecated-and-removed-features)，並使用 [AEM Analyzer 工具](/help/sites-deploying/aem-analyzer.md)評估對自訂和整合功能的影響。

## 我要如何確保能順利轉變為 AEM 6.5 LTS？

為確保能順利轉變，建議您：

* 詳細審閱[發行說明](/help/release-notes/release-notes.md)和文件。
* 使用 [AEM Analyzer 工具](/help/sites-deploying/aem-analyzer.md)評估升級的複雜性。
* 針對升級過程進行規劃並分配足夠的時間和資源。
* 參與 Adobe 支援和賦能培訓課程以獲得指引和協助。

## 什麼是AEM 6.5 LTS Service Pack？

AEM 6.5 LTS Service Pack為累積更新，包含自AEM 6.5 LTS初次發行以來對其所做的所有修正和改良。 建議您套用最新的Service Pack，以確保您的AEM執行個體使用最新的功能和安全修補程式。

## 目前我使用AEM 6.5，我可以直接升級至AEM 6.5 LTS Service Pack而不升級至AEM 6.5 LTS GA版本嗎？

是，您可以直接從AEM 6.5升級至任何AEM 6.5 LTS Service Pack。 建議檢閱[發行說明](/help/release-notes/release-notes.md)和[升級至AEM 6.5 LTS](/help/sites-deploying/upgrade.md)區段。

## 我目前在AEM 6.5 LTS GA，是否需要變更任何程式碼才能升級至AEM 6.5 LTS Service Pack？

不需要，您不需要變更任何程式碼，即可從AEM 6.5 LTS升級至AEM 6.5 LTS Service Pack。 不過，在將Service Pack套用至生產執行個體之前，建議您一律檢閱[發行說明](/help/release-notes/release-notes.md)，並在測試環境中測試您的自訂與整合。

## 我想以新的AEM 6.5 LTS設定從頭開始，我可以直接從AEM 6.5 LTS Service Pack開始嗎？

是，您可以直接設定新的AEM 6.5 LTS Service Pack，而不需要設定AEM 6.5 LTS GA版本。 建議檢閱[發行說明](/help/release-notes/release-notes.md)和[自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)區段以取得詳細資訊。
