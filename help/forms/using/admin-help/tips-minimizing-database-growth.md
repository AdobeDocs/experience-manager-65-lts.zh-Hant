---
title: 將資料庫成長減至最低的秘訣
description: 長期處理程式會將處理程式資料儲存在AEM表單資料庫中。 使用一些簡單的程式設計和產品設定策略，可以將AEM表單資料庫的成長減至最少。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ac3766c5-b741-4e65-8053-0c9cfd66a2f9
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 將資料庫成長減至最低的秘訣 {#tips-for-minimizing-database-growth}

長期處理程式會將處理程式資料儲存在AEM表單資料庫中。 使用一些簡單的程式設計和產品設定策略，可以將AEM表單資料庫的成長減至最少。

## 流程設計提示 {#process-design-tips}

儘可能使用短期程式。 短期處理程式不會將處理程式資料儲存在資料庫中。 使用短期處理程式的缺點在於，它們的狀態和狀態不會在管理控制檯中進行追蹤，並且沒有處理程式的歷史記錄。

有些服務作業(例如「指派工作」作業（使用者服務）)需要用於長期處理程式中。 在此情況下，您可以將程式分成數個子程式，並儘可能縮短其存留期。 如果您使用此策略，短期的子程式應該處理大型資料專案，例如檔案值。

請謹慎使用變數。 使用長效處理序時，會針對每個處理序執行個體，在資料庫上為處理序中的每個變數分配空間。 策略性使用變數可節省大量空間。 例如，程式不再需要舊值時，您可以覆寫變數值。 並刪除您已建立且未使用的任何變數。 您可以驗證程式以尋找未使用的變數。

使用簡單的變數型別（例如，字串或int），並儘可能避免使用複雜的變數型別。 即使變數不包含值，資料庫空間也會分配給變數。 複雜變數通常比簡單變數需要更多空間。

## 產品管理秘訣 {#product-administration-tips}

有效使用全球檔案儲存(GDS)。 Forms伺服器上的GDS目錄可用來儲存（除其他專案外）傳遞至處理程式中AEM表單一部分的服務的檔案。 為了改善效能，較小的檔案會儲存在記憶體中，並保留在資料庫中。

管理主控台會公開「預設檔案最大內嵌大小」屬性，以設定儲存在記憶體中並保留在資料庫中的檔案大小上限。 (請參閱[設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。)如果您將此屬性設定為低值，大部分檔案都會儲存在GDS目錄，而非資料庫中。 優點在於，當檔案儲存在GDS目錄中時，您可以更輕鬆地刪除檔案。
