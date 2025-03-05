---
title: 使用AEM Analyzer評估升級複雜性
description: 瞭解如何使用AEM Analyzer來評估升級的複雜性。
topic-tags: upgrading
content-type: reference
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 2645745a83477509bac81cb5e122eabc44db3961
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 15%

---


# 使用AEM Analyzer評估升級複雜性 {#assessing-the-upgrade-complexity-with-the-aem-analyzer}

## 概觀 {#overview}

AEM 6.5 LTS分析器可指出需要更新的區域，以提供6.5 LTS無縫升級體驗，進而評估您目前的AEM實作。

此工具會產生一個報告來識別可能重構的區域。

## AEM 6.5 LTS分析器報告 {#aem-65lts-analyzer-report}

AEM 6.5 LTS Analyzer報告可用來取得對一般升級整備程度的概略瞭解。 此報表包含必須解決的問題類別，才能確保成功升級至AEM 6.5 LTS。

AEM 6.5 LTS Analyzer報表包含下列類別：

* 必須重構的應用程式功能
* 必須移至支援位置的存放庫項目
* 設定問題
* 已由新功能移除或目前不支援的AEM AEM 6.5 LTS功能
* 移除Java和Guava API使用方式

這些類別和可能的影響以及與這些類別相關聯的解決方案的其他資訊，可透過AEM 6.5 LTS分析器報告中的連結提供。

## 可用性 {#analyzer-availability}

可以從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下載AEM Analyzer的ZIP檔。 您可以在來源AEM執行個體上透過[封裝管理員](/help/sites-administering/package-manager.md)安裝封裝。

## 使用AEM Analyzer的重要考量 {#important-considerations-for-using-aem-analyzer}

請參考以下章節，瞭解執行AEM Analyzer時的重要考量：

* 分析器報告是使用AEM [模式偵測器](/help/sites-deploying/pattern-detector.md)的輸出所建置。 分析器使用的模式偵測器版本包含在AEM分析器安裝套件中
* AEM Analyzer只能由&#x200B;**管理員**&#x200B;使用者或&#x200B;**管理員**&#x200B;群組中的使用者執行
* 在6.5版及更高版本的AEM執行個體上支援Analyzer。

>[!NOTE]
>
>為避免對業務關鍵例項造成影響，建議您在儘可能接近生產環境的預備環境中，於自訂、設定、內容和使用者應用程式等方面執行AEM Analyzer。 或者，您可以在複製的生產製作環境中執行CRA。

* 產生AEM Analyzer報表內容可能需要相當長的時間，從幾分鐘到數小時不等。 所需的時間主要取決於AEM存放庫內容的大小和性質、AEM版本和其他因素
* 由於產生報表內容可能需要相當長的時間，因此會由背景程式產生，並儲存在快取中。 檢視和下載報表的速度則相對迅速，因為此時會使用內容快取，直到快取過期或報表明確重新整理為止。在產生報表內容期間，您可以關閉瀏覽器索引標籤，等稍後內容已放入快取時，再回過頭檢視報表。

## 檢視AEM Analyzer報表 {#viewing-the-aem-analyzer-report}

若要檢視AEM Analyzer報表，請遵循下列步驟：

1. 選取Adobe Experience Manager並導覽至&#x200B;**工具 — 作業 — 6.5 LTS現代化器**

   ![檢視分析器報告1](/help/sites-deploying/assets/view-analyzer-report-1.png)

1. 按一下&#x200B;**AEM 6.5 LTS分析器**&#x200B;以開啟

   ![檢視分析器報告2](/help/sites-deploying/assets/view-analyzer-report-2.png)

1. 按一下&#x200B;**產生報表**&#x200B;以執行AEM Analyzer

   ![檢視分析器報告3](/help/sites-deploying/assets/view-analyzer-report-3.png)

1. 在AEM分析器產生報表時，您可以在畫面上看到工具執行的進度。 它以完成的百分比顯示進度。 它也會顯示已分析的專案數以及結果數

   ![檢視分析器報告4](/help/sites-deploying/assets/view-analyzer-report-4.png)

1. 產生6.5 LTS Analyzer報告後，會以表格格式顯示結果的摘要和數目，並依結果型別和重要性層級加以整理。 若要取得特定發現專案的詳細資訊，您可以按一下與表格中的發現專案型別相對應的數字

   ![檢視分析器報告5](/help/sites-deploying/assets/view-analyzer-report-5.png)

1. 您可以按一下&#x200B;**匯出至CSV**，選擇下載逗號分隔值(CSV)格式的報表。 您可以按一下&#x200B;**重新整理報告**，以強制分析器清除其快取並重新產生報告。 如果快取過期，您必須重新產生報表。

## 解譯AEM Analyzer報表 {#interpreting-the-aem-analyzer-report}

在AEM例項中執行6.5 LTS分析器工具時，報表會在工具視窗中顯示為結果。

報表格式為：

* **報表概覽**：報表本身的相關資訊，包括下列資訊：

   * **報告時間**：產生報告內容並首次提供的時間
   * **到期時間**：報告內容快取的到期時間
   * **產生期間**：產生報表的時間長度
   * **發現專案計數**：報告中包含的發現專案總數

* **系統概覽**：執行分析器所在之AEM系統的相關資訊
* **結果類別**：分別處理一或多個同類結果的多個區段。每個區段各包含下列項目：類別名稱、子類型、結果計數和重要性、摘要、類別文件的連結，以及個別結果資訊。

  ![分析器報告摘要](/help/sites-deploying/assets/analyzer-report-summary.png)

  系統會為每個結果指派一個重要性層級，以指出動作的概略優先順序。

>[!NOTE]
>
>若要深入瞭解每個發現專案類別，請參閱[模式偵測器類別](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/aso)。

若要瞭解重要性層級，請遵循下表：

| 重要性 | 說明 |
|---|---|
| 資訊 | 此結果僅供參考。 |
| 建議 | 此結果可能是升級問題。建議進一步調查。 |
| 關鍵 | 此結果很可能是升級問題，必須解決以防止失去功能或效能。 |

## 解譯AEM 6.5 LTS Analyzer CSV報表 {#interpreting-the-aem-65lts-analyzer-report}

當您按一下AEM執行個體中的&#x200B;**CSV**&#x200B;選項時，將會從內容快取建置CSV格式的Analyzer報表，並傳回至您的瀏覽器。 根據您的瀏覽器設定，此報表會自動下載為預設名稱為`report.csv`的檔案。

如果快取已過期，則會在CSV檔案建置和下載之前重新產生報表。

CSV 格式的報表包含從「模式偵測器」輸出產生的資訊，且會依類別類型、子類型和重要性層級排序和組織。其格式適用於 Microsoft Excel 等應用程式的檢視和編輯作業。其目的是要以可重複的格式提供所有結果資訊，以利比較不同時間的報表，藉此衡量進度。

CSV 格式報表的欄包括：

* **代碼**：類別代碼
* **類型**：類別名稱
* **子類型**：類別的子類型
* **重要性**：重要性層級
* **識別碼**：結果的主要識別碼
* **訊息**：為結果提供的訊息
* **內容**：結果資料的 JSON 字串

個別結果的欄中若有&quot;`\N`&quot;值，表示未提供任何資料。

## HTTP介面 {#http-interface}

6.5 LTS分析器提供HTTP介面，可作為AEM使用者介面的替代介面。 介面同時支援`HEAD`和`GET`命令。 它可用來產生Analyzer報表，並以三種格式之一傳回：JSON、CSV和定位鍵分隔值(TSV)。

下列URL可用於HTTP存取，其中`<host>`是安裝Analyzer之伺服器的主機名稱，以及連線埠（如有需要）：

* `http://<host>/apps/aem66-analyzer/analysis/report.json` (JSON 格式)
* `http://<host>/apps/aem66-analyzer/analysis/report.csv` (CSV 格式)
* `http://<host>/apps/aem66-analyzer/analysis/report.tsv` (TSV 格式)

### 執行HTTP要求 {#executing-an-http-request}

執行HTTP要求的簡單方法之一，是在您已以管理員身分登入AEM的相同瀏覽器中開啟索引標籤。 您可以在瀏覽器索引標籤中輸入 URL，並且讓瀏覽器顯示或下載結果。

您也可以使用命令列工具，例如`curl`或`wget`，以及任何HTTP使用者端應用程式。 未在已驗證的工作階段中使用瀏覽器索引標籤時，您必須在註解中提供管理使用者名稱和密碼。

以下是其操作方式的範例：

```shell
curl -u admin:admin 'http://localhost:4502/apps/aem66-analyzer/analysis/report.csv' > report.csv.
```

## 調整快取存留期 {#adjusting-the-cache-lifetime}

預設的AEM 6.5 LTS Analyzer快取存留期為24小時。 在AEM例項和HTTP介面中使用重新整理報表和重新產生快取的選項時，此預設值可能適用於AEM 6.5 LTS Analyzer的大部分用途。 如果您AEM例項的報表產生時間特別長，您可以調整快取存留期以最小化報表的重新產生。

快取存留期值會儲存為下列存放庫節點上的`maxCacheAge`屬性：

```
/apps/aem66-analyzer/content/modernizer/analyzer/jcr:content
```

此屬性的值是快取存留期 (以秒為單位)。管理員可以使用 CRX/DE Lite 調整快取存留期。

## 使用內容轉換器 {#using-content-transformer}

### 可用性 {#content-transformer-availability}

內容轉換器與AEM 6.5 LTS分析器整合，可從軟體發佈入口網站下載為ZIP檔案。

### 使用內容轉換器的重要考量 {#important-considerations-for-using-content-transformer}

請參閱以下小節，瞭解使用內容轉換器(CT)時的重要考量事項：

* 若要使用內容轉換器，您必須先在AEM環境中執行AEM Analyzer
* 雖然您可以在生產環境中執行內容轉換器，但建議您在複製的生產環境中執行內容轉換器。 更重要的是，您必須確保AEM Analyzer和CT在相同的環境中執行
* 您必須是要執行內容轉換器的環境管理員
* 依預設，在轉換之前，可變更來源內容的移除操作將會在`/etc/packages/modernizer-content-transformation`下建立來源路徑的備份封裝。 雖然移除操作對話方塊有可停用/啟用建立備份套件的選項，但強烈建議一律選取啟用建立套件的選項
* 內容轉換器中的每個頁面都設定為列出最多50個發現。 因此，一次最多可以轉換50個發現。 這麼做是為了在UI中提供及時回應。

### 開啟內容轉換器 {#opening-the-content-transformer}

1. 以管理員身分登入來源AEM執行個體，並前往起始頁面： *https://host:port/aem/start.htm*
1. 導覽至&#x200B;**工具 — 作業 — 6.5 LTS現代化器**

   ![正在開啟內容轉換器1](/help/sites-deploying/assets/opening-content-transformer-1.png)

1. 按一下&#x200B;**6.5 LTS分析器報告的內容轉換器**&#x200B;卡片

   ![正在開啟內容轉換器2](/help/sites-deploying/assets/opening-content-transformer-2.png)

1. 如果未產生Analyzer報告，則&#x200B;**轉換內容**&#x200B;頁面會顯示&#x200B;**無報告**。 如果移除所有與內容相關的發現，也會顯示相同的&#x200B;**無報告**&#x200B;訊息

   ![開啟內容轉換器3](/help/sites-deploying/assets/opening-content-transformer-3.png)

1. 以下範例說明AEM Analyzer報表成功建立且發現內容相關問題後，內容轉換器概觀頁面看起來會是怎樣。

AEM Analyzer報告的剩餘到期時間會顯示在側邊欄中。 建議您使用最新的AEM Analyzer報告執行內容轉換器，以避免遺漏任何內容相關發現

![開啟內容轉換器4](/help/sites-deploying/assets/opening-content-transformer-4.png)

1. 您可以根據模式代碼、子型別、重要性和Source來篩選問題

   ![正在開啟內容轉換器5](/help/sites-deploying/assets/opening-content-transformer-5.png)

### 移除路徑 {#removing-paths}

1. 您可以選取所有或特定問題，並選取&#x200B;**移除**&#x200B;以解決這些問題

   ![正在移除路徑1](/help/sites-deploying/assets/removing-paths-1.png)

   >[!NOTE]
   >依預設，在轉換之前，「移除」作業會在`/etc/packages/modernizer-content-transformation`下建立來源路徑的備份封裝。 雖然移除操作對話方塊有可停用/啟用建立備份套件的選項，但強烈建議一律選取啟用建立套件的選項。

   ![正在移除路徑2](/help/sites-deploying/assets/removing-paths-2.png)

1. 以下顯示為路徑移除作業而建立的備份封裝範例。 您可以按一下&#x200B;**安裝**&#x200B;以恢復來源路徑

   ![正在移除路徑3](/help/sites-deploying/assets/removing-paths-3.png)

   >[!CAUTION]
   >
   >請勿刪除`/etc/packages/modernizer-content-transformation`，因為這是備份封裝所在的位置。 只有在您確定不再需要這些套件時，才能刪除此位置以縮小存放庫大小。

1. 或者，您也可以封裝選取的內容發現專案以供日後使用。 若要這麼做，請選取您要包含的發現，然後從左上方按一下&#x200B;**封裝**。 輸入封裝名稱，選擇封裝路徑，然後按一下&#x200B;**封裝**&#x200B;按鈕以完成程式。

   ![正在移除路徑3](/help/sites-deploying/assets/removing-paths-4.png)

### 已知問題 {#known-issues}

* 有時移除操作可能會顯示通知： *&quot;部分路徑未成功移除，請檢查記錄並再試一次。「*」。 不過，如果路徑已實際移除，您可以安全地忽略此訊息
* 同樣地，封裝作業可能失敗，並出現錯誤： *&quot;執行所需作業時發生錯誤，請檢查記錄檔並再試一次。「*」。 這可能是由於工作階段到期所導致。 在這種情況下，重試操作應該可以解決問題。





