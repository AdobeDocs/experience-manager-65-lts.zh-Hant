---
title: Forms 服務
description: 本文說明Forms服務，以及您可以使用Forms服務執行的表單相關工作。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,Forms Service,PDF Generator
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 1e7aa0fa-4440-42fb-8e0b-3c757568b78f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Forms 服務 {#forms-service}

## 概觀 {#overview}

Forms服務可讓您建立互動式資料擷取使用者端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 Forms服務會將您開發的任何表單設計呈現為PDF檔案。

Forms服務也可讓組織將電子錶單部署為Adobe PDF，以擴充其智慧型資料擷取流程。 您也可以使用本服務，將資料分別匯入及匯出現有的PDF forms。

使用Forms服務來執行下列動作：

* 根據範本和XML資料轉譯PDF forms。
* 啟用表單資料整合，以將資料匯入PDF forms並從中擷取資料。
* 根據片段轉譯表單。

## 建立PDF forms  {#creating-pdf-forms-nbsp}

使用表單服務建立用於資料擷取的PDF forms。 通常，您會先從AEM Forms Designer範本開始。 使用Forms服務的`renderPDFForm` （連結至Javadoc）操作將此範本轉換為PDF表單。

`renderPDFForm`作業的第一個引數是範本檔案的名稱（例如，`ExpenseClaim.xdp`）。 您可以將範本檔案儲存在本機檔案系統、CRX存放庫或HTTP或FTP位置。 您可以在`renderPDFForm`作業的`PDFFormRenderOptions`引數中設定內容根目錄，以指定範本檔案的位置。 請參閱Javadoc以取得您可以為`PDFFormRenderOptions`引數指定的其他選項的詳細資料。

`renderPDFForm`作業也可以接受XML資料。 建立PDF表單時，會將XML資料與範本合併，使產生的PDF表單包含指定資料。 `renderPDFForm`作業的第二個引數可以接受包含XML資料的Document (Javadoc)物件。

## 從PDF forms擷取資料  {#extracting-data-from-pdf-forms-nbsp}

使用Forms服務的`exportData` (Javadoc)作業，從PDF表單擷取資料XML。 此作業接受檔案作為其第一個引數。 您可以將資料匯出為XDP檔案或XML檔案。 如果將資料匯出為XML檔案，則匯出的資料會移除XDP包絡，並傳回純XML檔案。 您可以使用第二個引數指定此配置。

## 將資料匯入PDF forms {#importing-data-into-pdf-forms}

Forms服務也可讓您將使用PDF Designer或`renderPDFForm`作業建立的AEM Forms表單與XML資料合併。 Forms服務的`importData` (Javadoc)作業接受PDF表單和XML資料，並傳回包含資料XML的PDF表單。

## 根據片段轉譯表單 {#rendering-forms-based-on-fragments}

Forms服務可以根據您使用AEM Forms Designer建立的片段轉譯表單。 片段是可重複使用的表單部分。 它會儲存為單獨的XDP檔案，可插入多個表單設計中。 例如，片段可以包含位址區塊或合法文字。

使用片段可簡化並加速大量表單的建立與維護。 建立表單時，插入片段在表單中出現所需片段的參考。 片段參考包含指向實體XDP檔案的子表單。

使用片段的優點如下：

* **內容重複使用**：您可以在多種表單設計中重複使用內容。 若要在多個表單中快速重複使用相同內容的部分，請建立片段。 複製或重新建立內容需要較長時間。 使用片段也可確保表單設計中經常使用的部分在所有參考表單中都具有一致的內容和外觀。
* **全域更新**：您只能在檔案中對多個表單進行一次全域變更。 您可以變更片段中的內容、指令碼物件、資料繫結、配置或樣式。 所有參照片段的XDP表單都會反映變更。
* **共用表單建立**：您可以在多個資源間共用表單的建立。 在AEM Forms Designer的指令碼或其他進階功能方面擁有專業知識的表單開發人員可以開發和共用使用指令碼和動態屬性的片段。 表單設計人員可以使用片段來設計表單。 此外，他們可以使用片段來確保表單的所有部分在多個表單中都具有一致的外觀和功能。
