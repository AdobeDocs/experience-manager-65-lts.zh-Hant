---
title: 處理支援的檔案格式的最佳實務
description: 使用 [!DNL Experience Manager Assets]處理各種支援的檔案型別的最佳實務。
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
solution: Experience Manager, Experience Manager Assets
exl-id: 28765aeb-1303-40da-bde0-df1b4c625d37
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Assets檔案格式最佳實務 {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets]支援許多專屬和協力廠商檔案格式資料庫，以符合使用者的不同檔案支援需求。 支援的Adobe資料庫包括[!DNL Adobe Camera Raw]、Gibson、Adobe PDF模擬轉譯器和[!DNL Adobe InDesign Server]。 此外，[!DNL Experience Manager Assets]支援協力廠商程式庫，包括[!DNL ImageMagick]、[!DNL TwelveMonkeys]等。

如需支援的檔案格式，請參閱[Assets支援的格式](/help/assets/assets-formats.md)。

>[!TIP]
>
>如果您在Adobe Managed Services (AMS)上使用[!DNL Experience Manager]，如果您計畫處理大量大型PSD或PSB檔案，請聯絡Adobe客戶支援。 與Adobe客戶支援代表合作，為您的AMS部署實作這些最佳實務，並為Adobe的專有格式選擇最佳可行的工具和模型。 [!DNL Experience Manager]可能無法處理超過30000 x 23000畫素的高解析度PSB檔案。

## [!DNL Adobe Camera Raw]資料庫 {#adobe-camera-raw-library}

為獲得最佳效能，Adobe建議針對RAW和DNG檔案使用[!DNL Adobe Camera Raw]資料庫。

[!DNL Adobe Camera Raw]資料庫支援CMYK色彩設定檔作為輸入。 不過，它會以RGB色域產生輸出，並僅支援JPEG格式的輸出。 它不會保留縮圖中的來源檔案色域（例如CMYK）。

如需詳細資訊，請參閱[Camera Raw支援](/help/assets/camera-raw.md)。

## Adobe PDF模擬轉譯器程式庫 {#adobe-pdf-rasterizer-library}

為達到最佳效果，Adobe建議針對下列檔案使用Adobe PDF模擬轉譯器資料庫：

* 大量且需要大量內容的PDF檔案
* 未立即產生含縮圖的AI檔案
* 針對具有特別色(PMS)顏色的AI檔案

使用PDF點陣化程式產生的縮圖和預覽，其品質優於現成可用的點陣化輸出。 Adobe PDF模擬轉譯器資料庫不支援任何色域轉換。 無論來源PDF檔案的色域為何，Adobe PDF模擬轉譯器只會產生RGB輸出。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe建議您使用[!DNL Adobe InDesign Server]來擷取[!DNL Adobe InDesign]特定轉譯，例如IDML和HTML。 如需詳細資訊，請參閱[在Adobe InDesign中新增Experience Manager資產作為參考](/help/assets/managing-linked-subassets.md#refai)。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media]透過其全域、可擴充且效能最佳化的網路，即時產生並傳送多種豐富內容的變體。 它提供互動式檢視體驗，並簡化數位行銷活動管理程式。 如需有關啟用[!DNL Dynamic Media]的詳細資訊，請參閱[設定Dynamic Media](/help/assets/config-dynamic.md)。

目前，[!DNL Dynamic Media]可支援每個檔案最多15 GB內容的視訊。

## ImageMagick資料庫 {#imagemagick-library}

Adobe建議在下列情況下使用ImageMagick資料庫：

* 若要產生EPS檔案的縮圖轉譯。
* 保留影像設定檔資訊。
* 保留透明度。
* 處理PSD和PSB檔案。

若要瞭解如何在[!DNL Experience Manager]中設定[!DNL ImageMagick]資料庫，請參閱[使用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 如需最佳使用方式，請參閱[設定ImageMagick的最佳實務](/help/assets/best-practices-for-imagemagick.md)。

## 影像轉碼程式庫 {#image-transcoding-library}

Adobe影像轉碼資料庫是影像處理解決方案，可執行核心影像處理功能，包括影像編碼、轉碼、重新取樣、調整大小等。

「影像轉碼程式庫」支援下列MIME型別：

* JPG/JPEG
* PNG （8位元和16位元）
* GIF
* BMP
* TIFF/壓縮的TIFF （32位元Tiff和PTiff除外）。
* ICO
* ICN

如需詳細資訊，請參閱[影像轉碼程式庫](/help/assets/imaging-transcoding-library.md)。
