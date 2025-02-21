---
title: 從Dynamic Media — 混合模式移轉至Dynamic Media - S7模式
description: 瞭解如何將Dynamic Media — 混合模式的執行個體移轉至Dynamic Media - S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 2%

---

# 關於從Dynamic Media-Hybrid移至Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid是與Adobe Experience Manager整合的舊版Dynamic Media。 混合版本最初是在Adobe Experience Manager 6.1中引入。雖然Adobe持續支援混合模式，但並非偏好模式；建議使用Dynamic Media-Scene7模式。 混合模式也不支援智慧型裁切和全景影像等新功能，而Dynamic Media-Scene7則支援。

Dynamic Media-Hybrid和Dynamic Media-Scene7之間的其他主要差異包括：

* URL的結構。
* 視訊擷取。
* 影像轉譯的建立和儲存。
* 雲端設定和認證（布建）。

從Dynamic Media-Hybrid移至Dynamic Media-Scene7時，有兩個選項可供使用。 第一個選項是僅在Experience Manager上布建新的Dynamic Media-Scene7例項。 第二個選項是將您現有的Dynamic Media-Hybrid例項移轉至Dynamic Media-Scene7。 這個選項會以表格形式概述下方的步驟，以及您在移動過程中要採取的考量事項。

>[!IMPORTANT]
>
>Adobe建議您不要在即時生產執行個體上將Dynamic Media-Hybrid實作移轉至Dynamic Media-Scene7。

## 選項1 — 在Experience Manager上布建Dynamic Media-Scene7的新執行個體 {#provision-new-dms7}

只需考慮在Adobe Experience Manager上以Dynamic Media-Scene7的新布建例項從頭開始。 除了透過Dynamic Media Cloud Service擷取及處理資產外，強烈建議使用Adobe稽核資產使用情況、工作流程和元件。 通常，您可以使用較新的、現成可用的功能來取代自訂元件和工作流程。

## 選項2 — 將您現有的Dynamic Media-Hybrid例項移轉至Dynamic Media-Scene7 {#process-for-migrating}

| 步驟 | 任務 | 考量事項 |
|---|---|---|
| 1 | 原地複製Dynamic Media混合式製作例項。 | 維護您現有的Dynamic Media-Hybrid Author例項以供遞補用途，直到此移轉程式中的其餘步驟成功完成為止。 |
| 2 | 在Dynamic Media-Scene7模式下啟動複製的製作例項。 |  |
| 3 | 在Adobe Experience Manager雲端服務中，使用Dynamic Media-Scene7憑證設定Dynamic Media 。 | Adobe必須核准Dynamic Media-Scene7布建。 因此，您擁有Adobe支援的並行Dynamic MediaM-Hybrid和Dynamic Media-Scene7環境，但僅限於有限時間。 |
| 4 | 建立移轉套件組合，讓您可以視需求內嵌資產。<br>刪除初始擷取至Dynamic Media-Hybrid期間建立的本機PTIFF。 | 如果Dynamic Media-Hybrid執行個體中目前所有資產都可用，則會複製已包含所有資產的資產。 因此，不需要組合。 |
| 5 | 執行資產更新工作流程，以便您將資產同步至Dynamic Media Cloud Service。 | Adobe建議您以批次形式執行更新工作流程以允許壓縮。 |
| 6 | 移轉檢視器、影像和視訊預設集。 |  |
| 7 | 瀏覽每個網頁內容管理參考的資產，並更新其相關聯的URL。 |  |
| 8 | 移轉您要支援新Dynamic Media-Scene7模式的任何自訂工作流程（手動更新）。 |  |
| 9 | 驗證您的Web內容管理上傳和設定。 |  |
| 10 | 驗證後，取得停用Dynamic Media-Hybrid Author （維持為遞補內容）的核准。 |  |
| 11 | 在成功使用Dynamic Media-Scene7約一個月後，刪除Dynamic Media-Hybrid Author例項。 |  |
