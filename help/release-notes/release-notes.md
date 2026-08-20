---
title: Adobe Experience Manager 6.5 LTS、SP3最新發行說明
description: 尋找Adobe Experience Manager 6.5 LTS Service Pack 3的最新發行資訊。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 0ce890503d43af340b6ee3c85b1b563613627c78
workflow-type: tm+mt
source-wordcount: '6749'
ht-degree: 26%

---


# Adobe Experience Manager 6.5 LTS、SP3最新發行說明 {#release-notes}

## 版本資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | Service Pack 3 (SP3) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack 發行 |
| 日期 | 2026年8月20日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.3.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

<!-- **Mandatory Hotfix** – To avoid SNFE (SegmentNotFoundException) issues with offline compaction when installing SP2, install the hotfix described in [Known issues – Repository corruption during online compaction](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146). -->

## [!DNL Adobe Experience Manager] 6.5 LTS、SP3包含哪些專案 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS，SP3包含新功能、客戶要求的重要增強功能和錯誤修正。 自2025年3月首次推出6.5 LTS以來，它提升了整個平台的效能、安全性和本地化程度。 [在 6.5 LTS 上安裝此 Service Pack](#install-update)。

### 已修正問題概觀 {#fixed-issues-overview}

[!DNL Adobe Experience Manager] 6.5 LTS， SP3解決[!DNL Sites]和[!DNL Experience Manager Foundation]的問題。 這些修正改善了協助工具、編寫可靠性、Headless內容傳送、多網站管理和平台穩定性。 下列各節列出每個修正及其參考編號。

大部分變更套用至[!DNL Sites]：

* 最大群組的協助工具改善。 這些更新加強了頁面編輯器、Assets側欄、篩選器和相關編寫介面的鍵盤導覽、熒幕助讀程式回饋、焦點管理、語意標籤、文字對比和觸控目標大小調整。
* [!DNL Content Fragments]中的修正範圍涵蓋片段編輯器、模型編輯器、REST API和GraphQL API。 更新會更正本地化、欄位驗證、編輯行為和回應處理。
* MSM即時副本修正可讓作者可靠地從Blueprint頁面轉出變更，並保留現有的轉出設定。
* Adobe Managed Services提供行人穿越道支援，包括必要的組合、系統使用者和設定。
* 進一步的修正針對管理和傳統介面、核心元件、元件主控台、促銷活動整合、體驗片段和啟動。

其餘變更套用至[!DNL Experience Manager Foundation]：

* 本地化更新會翻譯健康情況報表、作業控制檯和數個撰寫介面中先前僅含英文的文字。
* 穩定性修正會還原健康情況監視端點、在間歇性設定錯誤後保持郵件服務執行，並更正工作流程變數和工作流程封裝編輯。
* 此版本也新增AEM內容服務支援，並解決安全性、翻譯和使用者介面問題。

如需完整清單，請參閱[已修正6.5 LTS Service Pack 3](#fixed-issues)中的問題。


<!-- ## Key features and enhancements -->



<!-- UPDATE THE EACH RELEASE -->

## 已修正6.5 LTS、Service Pack 3中的問題 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP3}

* AEM 6.5 LTS， Service Pack 3包含Crossswalk組合、內容套件、系統使用者、服務使用者對應、功能切換和必要的OSGi設定。 全新安裝會自動提供人行通道先決條件，而且只需要客戶特定的執行階段設定。 (SITES-41596)
* AEM 6.5 LTS， Service Pack 3更新`cq-wcm-core`以支援Adobe Managed Services上的交叉通道。 此更新新增了範本建立和通用編輯器存取權，同時移除了過時的自訂程式碼和功能切換。 (SITES-37657)


#### 協助工具 {#sites-accessibility-65-lts-sp3}

* 頁面編輯器畫布現在支援僅鍵盤元件管理。 作者可以使用「插入元件」、「剪下」、「貼上」和「刪除」來新增、重新排序和移除元件。 (SITES-25359)嚴重
* 鍵盤使用者現在可以在網站清單檢視中重新排序表格列，而不需使用拖放手勢。 鍵盤控制項可讓使用者選取列、將其移動到其他位置並完成放置。 (SITES-24946)嚴重

* 自訂屬性編輯器現在支援鍵盤互動及其格式控制項。 作者可以在工具列選項之間移動焦點、選取文字樣式，以及僅使用鍵盤設定屬性值的格式。 (SITES-40333)主要

* 當可用的互動需要拖放時，鍵盤焦點現在會略過側面板「元件」清單。 這項變更可防止鍵盤使用者進入無法使用的元件選擇工作流程。 (SITES-40752)
* 關閉覆蓋現在會將焦點恢復至其觸發控制項。 鍵盤和熒幕助讀程式的使用者不會再回到覆蓋圖或失去在介面中的位置。 (SITES-40819)
* 鍵盤導覽不再將焦點移至隱藏的頁面內容。 此變更可維持可預測的焦點順序，避免導覽中斷。 (SITES-41430)
* 「鎖定」按鈕現在會根據標題提供精確熒幕助讀程式的意見回饋。 使用者會聽到清楚的動作標籤，而不是冗長的說明。 (SITES-41431)
* 現在，視覺指示器會識別「變更檔案」或「資料夾」清單方塊中選取的選項。 指標可協助使用者瞭解階層連結路徑，並辨識目前的資料夾。 (SITES-25532)
* 熒幕助讀程式現在會朗讀一次遞增或遞減排序方向。 描述性標籤可清楚識別按鈕動作，並移除重複的反饋。 (SITES-25534)
* AEM Sites現在提供更廣泛的協助工具支援，涵蓋常見的編寫工作流程。 更新可改善鍵盤互動、介面標籤、焦點管理和輔助技術意見回饋。 (SITES-38239)
* 工具列專案現在會在收到鍵盤焦點時顯示可見標籤。 鍵盤使用者可在啟動之前識別每個控制項。 (SITES-40751)
* 鍵盤和熒幕助讀程式的使用者現在可以離開[收件匣]功能表，而不需要將其保持開啟。 選單會自動關閉，並保留清除的導覽路徑。 (SITES-25518)
* 色票現在會顯示具有足夠對比度的選取狀態圖示。 較清晰的指標可協助使用者識別不同背景顏色的活動色票。 (SITES-25523)
* 「編輯版面」工具列現在會向輔助技術準確報告目前裝置。 裝置按鈕不再建議使用者開啟和關閉每個按鈕。 (SITES-25524)
* 搜尋強制回應現在會顯示具有足夠文字對比的&#x200B;**排序依據**&#x200B;標籤。 更新的樣式改善了視力缺佳使用者的可讀性。 (SITES-25531)
* 網站清單檢視排序按鈕現在符合最低對比要求。 使用者可以更輕鬆地在表格背景中識別每個排序控制項及其狀態。 (SITES-25372)
* 當篩選器欄位收到鍵盤焦點時，側欄Assets清單不再重新載入。 使用者可以輸入欄位，而不會出現意外的內容移動或熒幕助讀程式重複載入宣告。 (SITES-25377)
* 內容片段側邊欄標籤現在提供一致的存取標籤。 NVDA會朗讀分頁名稱，而非朗讀選取的子導覽專案。 (SITES-25509)
* 現在，當鍵盤或熒幕助讀程式的焦點移出它時，「說明」功能表就會關閉。 使用者可以繼續導覽標題控制項或頁面內容，而不需要讓功能表保持開啟。 (SITES-25517)
* 在「人口統計」工具列欄位中輸入的文字，現在符合最低對比要求。 使用者可在文字欄位背景中更清楚讀取設定檔值。 (SITES-25318)
* 「頁面資訊」功能表現在會顯示具有足夠文字對比的焦點選項。 更清晰的樣式可協助使用者在整個功能表中追蹤鍵盤焦點。 (SITES-25321)
* Teaser、影像和轉盤對話方塊中的核取方塊現在會向熒幕朗讀程式顯示其相關指示。 當鍵盤焦點到達每個核取方塊時，使用者會聽到支援說明。 (SITES-25364)
* 文字編輯器控制項現在會將其目前狀態傳達給輔助技術。 熒幕助讀程式會識別使用中的段落格式和選取的超連結目標選項。 (SITES-25367)
* 熒幕助讀程式現在會清楚宣告&#x200B;**旋轉裝置**&#x200B;按鈕和目前的裝置方向。 啟動控制項會報告新的方向，而不使用說明相反動作的標籤。 (SITES-25292)
* 鍵盤導覽現在會略過隱藏在收合的人口統計工具列中的控制項。 使用者可以在版面預覽中移動，而不會遇到無法使用的工具列選項。 (SITES-25304)
* 「人口統計」工具列中的文字標籤現在符合版面預覽期間的最低對比要求。 使用者可以在工具列背景中更清楚閱讀「建議」等標籤。 (SITES-25307)
* 「人口統計」工具列現在會顯示具有足夠對比度的按鈕焦點指示器。 使用者可在鍵盤導覽期間識別作用中的Commerce、角色或裝置控制項。 (SITES-25308)
* 「編輯配置」工具列使用裝置選擇器的群組焦點指示器。 大綱包含相關的&#x200B;**選取裝置**&#x200B;和&#x200B;**旋轉裝置**&#x200B;控制項，作為預期工具列行為的一部分。 (SITES-25283)
* 使用者選取其他裝置時，「編輯配置」工具列不再截斷&#x200B;**iPhone 8 Plus**&#x200B;標籤。 所有按鈕狀態中都會顯示完整的裝置名稱。 (SITES-25284)
* 「編輯版面」尺標現在為熒幕朗讀程式提供測量內容。 使用者會聽到描述性標籤和測量格式，而非無法解釋的數字。 (SITES-25287)
* 當案頭檢視作用中時，[編輯配置]工具列現在會反白顯示&#x200B;**案頭**&#x200B;按鈕。 視覺指示器可讓目前的裝置選取專案變得清晰。 (SITES-25290)
* 現在，所有可用顏色的鍵盤焦點仍會顯示在色票按鈕上。 新增的間距可防止焦點指示器混入選取的色票中。 (SITES-25253)
* 熒幕助讀程式現在可正確識別「時間扭曲日期」欄位。 此欄位不再提供誤導性意見反應，因此建議開啟對話方塊。 (SITES-25263)
* 「註解」按鈕標籤現在在其預設和暫留狀態中符合最低對比要求。 使用者可在按鈕背景中清楚閱讀標籤。 (SITES-25267)
* 熒幕助讀程式現在會在「註釋」對話方塊中宣告控制項的有意義的標籤。 每個按鈕都會在傳達其動作時不使用不必要的註解前置詞。 (SITES-25277)
* Assets側邊欄「編輯」按鈕現在提供較大的觸控目標。 使用者無需選取附近的元素，即可更可靠地啟動控制項。 (SITES-25221)
* 頁面編輯器現在使用邏輯標題階層。 熒幕助讀程式將頁面標題識別為主要標題，將側邊欄標題識別為次要標題。 (SITES-25222)
* 「註解」對話方塊現在會將標題顯示為語意標題。 熒幕助讀程式的使用者可以識別標題，並透過標題命令導覽對話方塊結構。 (SITES-25248)
* 熒幕助讀程式的使用者現在會在篩選「插入新元件」清單時收到回饋。 搜尋欄位會說明其篩選行為，而狀態訊息會報告結果計數。 (SITES-25251)
* 「側邊欄元件」面板現在會使用語意清單標籤。 熒幕助讀程式可朗讀專案計數，並支援有效率的清單導覽。 (SITES-25214)
* 資訊按鈕現在會在「元件」面板中使用較大的圖示。 使用者更容易找到並辨識每個控制項。 (SITES-25217)
* 現在，當使用者增加文字間距時，元件標題仍可見。 長標題會換行，而非截斷或重疊附近的內容。 (SITES-25219)
* Assets側邊欄&#x200B;**編輯**&#x200B;按鈕現在表示它會開啟新的瀏覽器索引標籤。 在導覽之前，視覺和熒幕助讀程式提示會為使用者做好準備。 (SITES-25220)
* 現在，當工具列開啟時，「註釋模式」會將鍵盤焦點置於註釋工具列上。 鍵盤和熒幕助讀程式的使用者可以邏輯順序移動控制項，而不需從&#x200B;**關閉**&#x200B;按鈕向後導覽。 (SITES-24996)
* 選取路徑和標籤欄位的按鈕時，不再使用核取方塊圖示。 更新的圖示會顯示控制項開啟選取對話方塊，而非變更核取狀態。 (SITES-25210)
* 「側邊欄元件」面板中的「篩選」欄位現在提供可存取的有效標籤。 熒幕助讀程式會朗讀欄位用途，而非依賴圖示或預留位置文字。 (SITES-25212)
* Assets Side Rail現在會隱藏熒幕助讀程式的裝飾性縮圖。 使用者在資產格線中導覽時，不會再聽到資產名稱兩次。 (SITES-25213)
* 「篩選器」邊欄中的摺疊式功能表按鈕現在會顯示具有足夠對比的焦點指標。 鍵盤使用者可在導覽篩選器類別時追蹤焦點。 (SITES-24986)
* 「篩選器」邊欄現在會在選項按鈕周圍顯示清晰的鍵盤焦點。 對比增強可協助使用者在不同的篩選器選項中追蹤其位置。 (SITES-24987)
* 現在在「篩選器」頁面上載入狀態訊息符合最低文字對比要求。 在卡片檢視和清單檢視之間切換時，使用者可以閱讀進度回饋。 (SITES-24991)
* 編輯器畫布中的頁面標題現在使用語意標題標籤。 輔助技術可以宣告標題並將其包含在標題導覽中。 (SITES-24993)
* 展開「模擬器」功能表，現在會將鍵盤焦點移至第一個功能表專案。 收合功能表可讓焦點保持在邏輯次要工具列順序中。 (SITES-24954)
* 「即時檢視」表格中的文字現在符合最低對比要求。 使用者可在正常和暫留狀態期間清楚讀取即時副本的詳細資料。 (SITES-24956)
* 參考邊欄現在會使用語意標題標示來顯示標題。 熒幕助讀程式會在初始載入期間和使用者瀏覽資料夾時朗讀標題。 (SITES-24967)
* 卡片連結現在可清楚描述其目的地。 熒幕助讀程式的使用者無需聆聽卡片完整的中繼資料，即可識別每個連結。 (SITES-24975)
* 頁首功能表按鈕不再告訴熒幕助讀程式它們會開啟對話方塊。 熒幕助讀程式會朗讀每個按鈕的展開或收合狀態，以準確說明功能表行為。 (SITES-24742)
* 「刪除」按鈕上的文字現在可以針對紅色背景提供足夠的對比。 使用者在確認刪除之前，可更輕鬆辨識動作。 (SITES-24772)
* 畫布卡不再公開通往相同目的地的個別影像和標題連結。 單一連結可減少重複的鍵盤停止和重複的熒幕助讀程式宣告。 (SITES-24947)
* 「清單檢視」現在會顯示具有較高視覺顯著性的拖放按鈕。 圖示大小、重量和對比更新後，控制項更容易找到和使用。 (SITES-24951)
* 頁首按鈕現在提供簡明的協助工具名稱：搜尋、應用程式、說明、收件匣和使用者。 熒幕助讀程式不會再在鍵盤導覽期間宣告「可點按」或「圖形」等多餘詞語。 (SITES-24715)
* 應用程式導覽中的連結現在會顯示更強的視覺重點。 增加文字大小和重量，可改善視力不佳或色覺差異使用者的可讀性。 (SITES-24723)
* 收件匣連結現在使用語意清單標籤。 熒幕助讀程式可將連結識別為相關群組、宣佈專案計數，並支援更有效率的導覽。 (SITES-24730)
* 「使用者偏好設定」對話方塊中的工具提示控制項現在會顯示描述性存取名稱。 熒幕助讀程式會在閱讀工具提示內容之前朗讀每個控制項的用途，而非說「空白」。 (SITES-24732)
* 每個篩選器邊欄地標現在都包含可存取的不重複標籤。 熒幕助讀程式可將「篩選邊欄」與其他頁面區域區分開來，並在導覽期間加以識別。 (SITES-24686)
* 編輯器對話方塊現在會將「說明」和「切換全熒幕」按鈕與標題元素分開。 熒幕助讀程式會精確識別這些互動式控制項，且不再將它們宣告為標題。 (SITES-24696)
* CSV報告按鈕現在會在開啟新的瀏覽器標籤之前警告使用者。 其可存取的標籤可在啟動前將行為傳達給熒幕朗讀程式和鍵盤使用者。 (SITES-24704)
* 篩選邊欄現在會載入已儲存搜尋的標籤，並一致選取搜尋目錄。 「濾鏡」按鈕不再於焦點、鍵盤或滑鼠互動期間插入標籤元素。 (SITES-24706)
* 現在，「關閉」和「移除位置」按鈕可提供較大的觸控目標。 使用者無需選取相鄰元素，即可更可靠地啟動任一控制項。 (SITES-24530)
* 「移除位置」按鈕及其焦點指示器現在符合最低對比度要求。 更強的對比可幫助使用者識別控制項並追蹤鍵盤焦點。 (SITES-24531)
* 編輯器iframe現在包含畫布、側邊欄、元件對話方塊和版面預覽的描述性標題。 熒幕助讀程式可在焦點進入時識別每個影格。 (SITES-24650)
* 改善文字對比，讓參考邊欄訊息更易於閱讀。 此變更澄清了請求選擇或報告不可用參考的提示。 (SITES-24666)
* 「元件」面板會為每個資訊圖示提供一個有意義的可存取標籤。 熒幕助讀程式可一致地識別顯示元件說明的控制項。 (SITES-24500)
* 鍵盤焦點現在會包圍Byline的整個「顯示說明」按鈕。 可見的大綱可協助使用者追蹤其位置並避免啟用其他控制項。 (SITES-24503)
* Teaser元件對話方塊不再顯示「說明」和「切換全熒幕」按鈕作為標題。 熒幕助讀程式會朗讀兩個控制項作為按鈕，並保留正確的標題結構。 (SITES-24525)
* Adobe Experience Manager標題控制項會正確報告其展開或收合狀態。 此控制項會開啟及關閉導覽內容，以便熒幕助讀程式接收有效的狀態資訊。 (SITES-24528)
* 篩選結果將地球圖示標籤為裝飾性，並移除其可存取的名稱。 熒幕助讀程式會忽略圖示，而非宣告誤導性的說明。 (SITES-3057)
* 「時間扭曲」對話方塊現在會將時間輸入錯誤與對應的「小時」或「分鐘」欄位建立關聯。 熒幕助讀程式會在驗證訊息旁邊朗讀受影響的欄位。 (SITES-10980)
* 選取的內容樹專案不再成為「變更」檔案或資料夾控制標籤的一部分。 熒幕助讀程式可聽到不含額外狀態文字的清晰控制項名稱。 (SITES-24496)
* Assets側邊欄中的地區地標現在會顯示不同的可存取名稱。 熒幕助讀程式的使用者可清楚識別並導覽每個區域。 (SITES-24497)
* 熒幕助讀程式現在會忽略轉盤對話方塊的裝飾性說明和全熒幕圖示。 鍵盤導覽不再觸發不必要的圖示宣告。 (SITES-2912)
* 熒幕助讀程式現在會略過Teaser對話方塊中的裝飾性工具列圖示。 說明、全熒幕、格式和連結控制不再產生多餘的公告。 (SITES-2934)


#### 管理員使用者介面{#sites-adminui-65-lts-sp3}

* AEM現在可讓管理員群組成員解鎖頁面並模擬使用者。 群組成員可以透過其現有的存取權完成這兩項管理工作。 (SITES-14732)
* Assets管理員檢視現在會在作者在時間軸中選取「**還原為此版本**」後更新資產卡。 縮圖會立即顯示還原的版本，不再顯示過時的預覽內容。 (SITES-46590)


#### Classic 使用者介面{#sites-classicui-65-lts-sp3}

印尼文語言副本屬性會顯示正確的ID語言代碼。 當作者建立或檢閱印尼語言副本時，「參考」邊欄不再取代IN。 (SITES-44918)


#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp3}

Assets主控台現在會在使用者套用搜尋篩選器時回應。 變更內容片段模型篩選器會重新整理結果，而非保持目前的資產清單不變。 (SITES-38686)主要


#### [!DNL Content Fragments] - 管理員{#sites-admin-65-lts-sp3}

* Assets頁面現在會將鎖定的內容片段的工具提示翻譯為當地語言。 當使用者將游標停留在鎖定指示器上時，他們會看到轉譯的&#x200B;**簽出者**&#x200B;標籤。 (SITES-42531)主要

* AEM會在內容片段建立期間，將提供的無效名稱驗證訊息當地語系化。 不支援的標題字元不會再跨非英文介面觸發英文文字。 (SITES-19796)
* AEM會在內容片段建立期間翻譯內容片段模型字串。 Assets介面不再於當地語系化環境中顯示該標籤的英文文字。 (SITES-22336)
* 內容片段服務不再依賴過時的功能切換邏輯。 簡化的實作會移除切換相依的分支，並保持Service Pack行為一致。 (SITES-38688)
* AEM會在排程的內容片段發佈期間翻譯上個選項。 發佈工作流程符合使用中的介面語言。 (SITES-42532)
* AEM會轉譯內容片段下載對話方塊中的主字串。 元素區段會比對作用中的介面語言。 (SITES-42534)


#### [!DNL Content Fragments] — 片段編輯器{#sites-fragments-editor-65-lts-sp3}

* 內容片段編輯器現在可以正確放置RTF編輯器下拉式選單。 每個功能表都會與其工具列控制項保持對齊，並使附近的格式控制項保持可見。 (SITES-44005)嚴重

* 「編輯內容片段」按鈕現在出現，並立即對參考多欄位專案運作。 作者在編輯內嵌片段之前，不再需要儲存、關閉和重新開啟上層內容片段。 (SITES-43733)主要

* 當作者選取多行文字欄位時，內容片段編輯器會顯示一個焦點大綱。 大綱不再重複或重疊附近的控制項。 (SITES-39253)
* 內容片段建立會顯示不含斜體樣式的CJK預留位置文字。 日文、韓文、簡體中文和繁體中文字元仍保留其預期外觀。 (SITES-43548)
* 在作者儲存或發佈片段後，內容片段編輯器會重新整理狀態橫幅。 作者無需重新載入瀏覽器索引標籤，即可確認「已修改」、「已儲存」或「已發佈」狀態。 (SITES-45897)
* Granite UI變更後，內容片段編輯器會一致地驗證欄位。 更新的使用者端程式庫會還原預期的驗證行為。 (SITES-46650)


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp3}

* 當DAM檔案名稱包含空格或非ASCII字元時，GraphQL JSON回應現在會包含內嵌影像參考。 使用者端應用程式可擷取並轉譯這些影像，而不需重新命名資產。 (SITES-42191)主要
* 內容片段GraphQL API現在包含數個查詢處理和回應處理更新。 這些變更可防止重複的快取標題和值、改善編碼、保留持續的查詢狀態資訊、處理空白標題並傳回適當的端點錯誤。 (SITES-40159)主要
* PersistedQueryServlet現在會在有效的GraphQL持續查詢中處理編碼變數，而不會記錄虛假錯誤或警告。 查詢會繼續傳回成功的回應，而記錄則反映其實際執行狀態。 (SITES-39354)主要

* 重新載入GraphQL端點頁面會保留本地化的空白狀態訊息。 沒有端點時，頁面不再回覆成英文。 (SITES-43586)


<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp3}-->


#### [!DNL Content Fragments] - 模型編輯器{#sites-model-editor-65-lts-sp3}

* 內容片段模式控制檯現在會顯示其名稱包含本地化字元之設定的上傳縮圖。 當設定名稱使用非英文文字時，作者不再遺失縮圖預覽。 (SITES-39242)主要

* 當作者將元件新增至畫布時，內容片段模型編輯器會顯示當地語系化的&#x200B;**欄位標籤**&#x200B;文字。 作者不再需要儲存和重新開啟模型即可檢視翻譯。 (SITES-45383)
* 內容片段模式編輯器會將作者為複合元件選取無效模式型別時顯示的驗證訊息當地語系化。 訊息現在與使用中的地區設定相符，而不是只以英文顯示。 (SITES-41117)
* 內容片段模式編輯器會將模式鎖定對話方塊中的所有文字內容當地語系化。 對話方塊不再將英文按鈕標籤和指示與翻譯的介面文字混合在一起。 (SITES-28592)



#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp3}

Headless內容片段REST API套件組合會移除過時的功能切換與相關的條件式程式碼。 支援的API行為保持不變，而組合僅保留活動功能所需的切換。 (SITES-39113)



#### 元件控制台{#sites-component-console-65-lts-sp3}

內容尋找器現在會列出名稱中包含不可編碼字元的資產，而不會失敗或產生例外。 「元件即時使用情況」頁面也會持續載入大型結果集，而不會在捲動期間顯示空白列。 (SITES-44672)主要

<!--
#### Content API{#sites-content-api-65-lts-sp3}

#### Core backend{#sites-core-backend-65-lts-sp3}
-->

#### 核心元件{#sites-core-components-65-lts-sp3}

* 多欄位元件現在會為每個專案儲存個別的遠端資產選取專案。 作者可以選取、變更和儲存遠端影像，而不需要跨每個多欄位專案複製一個影像。 (SITES-42376)主要
* ThumbnailServlet現在會在重新導向遺失資源的請求後停止處理。 此變更可防止在DAM和控制檯瀏覽期間出現重複的Null指標例外和過多的錯誤記錄。 (SITES-41238)主要


#### Campaign整合{#sites-campaign-integration-65-lts-sp3}

Campaign ContentServlet現在會在內容請求期間保留JSON回應內容型別。 此變更會停止從AEM 6.5.24升級後發生的重複`WARN`和`ERROR`記錄專案。 (SITES-46902)主要


#### 體驗片段{#sites-experiencefragments-65-lts-sp3}

作者現在可以在建立體驗片段變數時瀏覽40個以上的範本。 每個額外的頁面都會保留原始資料夾篩選，並顯示下一個相符的範本。 (SITES-41531)主要


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp3} -->


#### 啟動{#sites-launches-65-lts-sp3}

上市促銷活動歷史記錄現在會在「網站時間軸」中顯示當地語系化文字。 時間軸會翻譯訊息「已建立的版本」和「提升啟動之前」（橫跨支援的區域設定）。 (SITES-13389)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp3} -->



#### MSM - Live Copies{#sites-msm-live-copies-65-lts-sp3}

* 當作者儲存未變更的屬性時，內容片段即時副本資料夾現在會保留cq:rolloutConfigs。 作者稍後可以更新轉出設定，而不會失去現有設定。 (SITES-43729)嚴重

* 作者現在可以從Blueprint頁面上的可編輯工具列轉出元件變更。 轉出完成且沒有JavaScript錯誤，並將變更傳播到即時副本。 (SITES-46052)主要
* 升級後，作者現在可以從Blueprint頁面完成MSM轉出。 轉出對話方塊會載入可用的即時副本，並啟用其轉出控制項，而非維持永久載入狀態。 (SITES-43116)主要

* 即時副本概述現在會在整個關係狀態中套用當地語系化的日期格式。 **即時副本Source上次修改時間**、**即時副本上次修改時間**&#x200B;及&#x200B;**上次轉出時間**&#x200B;欄位符合使用者的地區設定。 (SITES-40756)
* 現在於一個請求中停用Blueprint父頁面及其子頁面時，每個路徑會產生一個轉出事件。 轉出管理員不再針對相同子頁面執行重複動作。 (SITES-44987)


#### 頁面編輯器{#sites-pageeditor-65-lts-sp3}

* 現在，作者可以在一次「頁面屬性」儲存期間，建立並套用包含大寫字母或空格的標籤。 AEM會立即儲存標準化標籤值並保留頁面指定任務。 (SITES-42550)嚴重

* 捲動樣式選單時，不會再從選取的樣式中移除反白專案。 作者可在檢閱其他可用選項時確認其目前的選擇。 (SITES-30874)主要

* RTF編輯器連結按鈕現在會在作者透過HTTP存取AEM時開啟。 連結建立不再觸發`crypto.randomUUID`錯誤。 (SITES-39467)
* 作者現在可以將已設定的內容片段元件複製並貼到空的版面配置容器中。 貼上的元件保留其原始內容片段參考，不再顯示&#x200B;*選擇體驗變數*&#x200B;錯誤。 (SITES-41586)
* 影像編輯器現在會在混合內嵌編輯期間遵循自訂裁切比例。 每個影像下拉目標都會使用自己的組態，因此裁切選取範圍會以正確的方式套用至全熒幕模式之外。 (SITES-45771)

<!--
#### Replication{#sites-replication-65-lts-sp3}

#### Rich Text Editor{#sites-rte-65-lts-sp3}

#### Template Editor{#sites-template-editor-65-lts-sp3}

#### Universal editor {#sites-universal-editor-65-lts-sp3}

### [!DNL Assets]{#assets-65-lts-sp3}

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp3}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp3}
-->



<!--
### [!DNL Forms]{#forms-65-lts-sp3}
-->



### 基礎 {#foundation-65-lts-sp3}

#### AEM Context Service {#foundation-aem-context-service-65-lts-sp3}

AEM 6.5 LTS推出AEM Context Service支援。 轉出功能新增了服務API、代理程式整合、AMS布建、Experience Cloud整合、生產監控、作業Runbook和使用情況報表。 (GRANITE-65148)

#### Apache Felix {#foundation-apachefelix-65-lts-sp3}

AEM郵件服務現在會在發生間歇性設定錯誤時繼續傳送電子郵件。 管理員不再需要重新啟動Day Communique 5 Mailer套件組合以還原電子郵件傳送。 (GRANITE-66817)主要

<!--
#### Campaign{#foundation-campaign-65-lts-sp3}

#### Cloud Services{#foundation-cloudservices-65-lts-sp3}

#### Communities {#foundation-communities-65-lts-sp3}

#### Content distribution{#foundation-content-distribution-65-lts-sp3}

#### CRX {#foundation-crx-65-lts-sp3}

#### Granite{#foundation-granite-65-lts-sp3}

#### HTL{#foundation-htl-5-lts-sp3}

#### Integrations{#foundation-integrations-65-lts-sp3}

#### Jetty{#foundation-jetty-65-lts-sp3}
-->

#### 本地化{#foundation-localization-65-lts-sp3}

* 「操作」主控台現在會在健康狀態報表中，將先前未翻譯的文字內容當地語系化。 使用者可看到已翻譯的狀態訊息、警告、維護結果和效能資訊。 (NPR-44280)主要

* 「稽核記錄維護」任務現在會顯示本地化的免責宣告。 管理員在設定自動稽核記錄清除之前，會先以選取的語言檢視法規遵循與法律指引。 (NPR-44188)
* 現在，當使用者重新排序修改的設定檔時，「編輯使用者」頁面會顯示本地化錯誤。 此訊息清楚說明變更的設定檔必須等到使用者儲存變更後才能移動。 (NPR-44282)
* AEM現在會在整個內容片段清單屬性中將工具提示內容當地語系化。 翻譯後的指引說明模型選擇、標籤篩選、內容路徑、專案限制和排序設定。 (SITES-14969)
* 範本編輯器中的元件說明連結現在會開啟當地語系化的檔案。 作者可達到符合所選語言的指引，而非僅有英文的元件頁面。 (SITES-15058)
* 元件原則編輯器現在會將報告無法修改的資源或節點建立失敗的錯誤當地語系化。 範本作者會以選取的語言接收這些訊息。 (SITES-17475)

<!-- #### Omnisearch{#foundation-omnisearch-65-lts-sp3} -->

#### 操作控制面板{#foundation-operations-dashboard-65-lts-sp3}

客戶升級AEM LTS後，`/system/health/systemalive.json`端點現在仍可使用。 更正過的servlet上下文設定會防止HTTP 404回應，並支援依賴端點的健康情況監控系統。 (GRANITE-69457)嚴重

#### Platform{#foundation-platform-65-lts-sp3}

預設HTL運算式選項允許清單現在可辨識`decorationTagName`和`cssClassName`。 呈現標準回應式格線時，`error.log`不再填入重複的未知選項警告。 (GRANITE-67152)

<!--
#### Projects{#foundation-projects-65-lts-sp3}

#### Oak {#foundation-oak-65-lts-sp3}

#### Quickstart{#foundation-quickstart-65-lts-sp3} 
-->


#### 安全性{#foundation-security-65-lts-sp3}

**複製群組**&#x200B;動作現在會開啟預期的表單，而不是顯示空白頁面。 管理員可以輸入新的群組ID和說明，然後複製現有的安全性群組。 (NPR-44302)主要


<!-- #### Sling{#foundation-sling-65-lts-sp3} -->


#### 翻譯{#foundation-translation-65-lts-sp3}

現在當工作流程進行時，翻譯專案會維持精確的狀態計數。 啟動項建立和狀態傳播會遵循預期的工作流程行為，消除不一致的專案中繼資料。 (NPR-43420)


#### 使用者介面{#foundation-ui-65-lts-sp3}

* 國家/地區標籤現在會以選取的介面語言顯示。 本地化的介面不再顯示英文標籤。 (NPR-43883)
* 選取同層級頁面現在會在複合多欄位路徑選擇器中啟用&#x200B;**Select**。 作者無需放大瀏覽器視窗或重複選取專案即可確認新路徑。 (GRANITE-69323)


<!-- #### WCM{#foundation-wcm-65-lts-sp3} -->


#### 工作流程{#foundation-workflow-65-lts-sp3}

* Workflow封裝頁面現在支援觸控式UI頁面編輯器中的內容樹狀結構以及可編輯的資源定義元件。 作者無需使用傳統UI，即可導覽套件內容並檢查或更新其元件。 (GRANITE-67348)主要
* 觸控式UI頁面編輯器現在會呈現Workflow封裝頁面的內容樹狀結構。 作者可以檢查套件結構，並透過相同的編輯器編輯資源定義元件。 (GRANITE-67186)主要

* 工作流程變數對話方塊現在會顯示表單資料模型、JSON、XML和檔案變數的正確控制項。 作者建立這些非原始變數時，不會再看到原始HTML標籤。 (GRANITE-67915)



## 關於 [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS 平台是以更新版本的 OSGi 式框架 (Apache Sling 和 Apache Felix) 以及 Java™ 內容存放庫 (Apache Jackrabbit Oak 1.68.x) 為基礎進行建置。

Eclipse Jetty 11.0.x 會用於作為快速入門的 servlet 引擎。

### Java™ 支援  {#java-support}

* Java™ 17 和 Java™ 21 的支援。
* 為實現最佳效能，請使用其他值覆寫預設的 GC 值。 如需詳細資訊，請參閱[安裝與更新](/help/sites-deploying/custom-standalone-install.md)區段。
* 若是 Oracle 尚未正式推出，Adobe 會分發 Java™ 17 和 Java™ 21 維護更新供客戶在 AEM 相關專案中使用。

### Uberjar 封裝 {#uber-jar-packaging}

適用於AEM 6.5 LTS SP3的UberJar使用AEM 6.5 LTS UberJar 6.6.3版。 您可以從 Maven 中央存放庫檢索對應的 UberJar 成品。 與 AEM 6.5 不同，AEM 6.5 LTS 會將公用 API 和已棄用的 API 分隔成兩個不同的成品。

若要針對公開 API 進行編譯，請使用下列內容：

    &grave;&grave;xml
    &lt;相依性>
    &lt;groupId>com.adobe.aem&lt;/groupId>
    &lt;artifactId>uber-jar&lt;/artifactId>
    &lt;version>6.6.3&lt;/version>
    &lt;classifier>apis&lt;/classifier>
    &lt;scope>已提供&lt;/scope>
    &lt;/dependency>
    &grave;&#39;

如果您的程式碼也相依於已棄用的 API，請新增下列內容：

    &grave;&grave;xml
    &lt;相依性>
    &lt;groupId>com.adobe.aem&lt;/groupId>
    &lt;artifactId>uber-jar&lt;/artifactId>
    &lt;version>6.6.3&lt;/version>
    &lt;classifier>deprecated-api&lt;/classifier>
    &lt;scope>已提供&lt;/scope>
    &lt;/dependency>
    &grave;&#39;

另請參閱[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

### 升級 {#upgrade}

* 如需升級程序的詳細資訊，請參閱[升級文件](/help/sites-deploying/upgrade.md)。
* 如需詳細的升級指示，請參閱 [JEE 上的 AEM Forms 6.5 LTS SP1 升級指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

## AEM 6.5 LTS Service Pack 升級的最佳做法

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

適用於：安裝Service Pack 3 (SP3)的AEM 6.5 LTS （內部部署）客戶。 SP3會以Quickstart JAR形式提供。

**為什麼這種升級做法很重要**
EM 6.5 LTS 適用的 SP2 會以 Quickstart JAR 形式提供，而非透過「封裝管理員」進行安裝的 ZIP 檔。 內部部署客戶可透過取代Quickstart JAR、解壓縮並重新啟動來進行升級。 此方法與Adobe的標準升級程式一致。


**建議的升級流程 (作者或發佈)**

1. 驗證您的 AEM 6.5 LTS 執行個體是否運作正常且可存取。
1. 從 Software Distribution 下載 Quickstart JAR (例如 `cq-quickstart-6.6.x.jar`)。
1. 停止正在運作的實例。
1. 在AEM安裝目錄（`crx-quickstart/`以外）中，將先前的快速入門JAR取代為SP3 JAR。
1. 將 JAR 解壓縮：

       &grave;&grave;java
     java -jar cq-quickstart-6.6.x.jar -unpack
     &grave;&grave;
   
   (視需要調整堆積旗標。)

1. 根據其角色和連接埠，將解壓縮的 JAR 重新命名，例如 `cq-author-4502.jar` 或 `cq-publish-4503.jar`。
1. 開始 AEM，並在 UI (「說明」>「關於」) 和記錄中確認升級。

**最佳實務**

* 進入生產前，在低階/測試環境中執行升級。
* 在開始之前，先進行可還原的完整備份 (存放庫外加任何外部資料存放庫)。
* 審閱 Adobe 的就地升級指引和技術要求 (LTS 建議使用 Java 17/21)。

>[!NOTE]
>
>以上所示的檔案名稱 (例如 `cq-quickstart-6.6.x.jar`) 會反映在此 LTS 版本所看到的 Quickstart 成品命名方式；請一律使用與您從 Software Distribution 下載之檔案完全相同的檔案名稱。

## 安裝與更新{#install-update}

如需關於設定需求的資訊，請參閱[安裝指示](/help/sites-deploying/custom-standalone-install.md)。

>[!NOTE]
>
> 若您要從舊版 6.5 SP 直接升級至 LTS SP1，按照從 6.5 升級至 6.5 LTS GA 的[升級](/help/sites-deploying/upgrade.md)說明進行操作。


如需詳細指示，請參閱[升級檔案](/help/sites-deploying/upgrade.md)，因為同樣的檔案適用於LTS Service Pack更新。

>[!NOTE]
>
> 對於全新的 AEM 6.5 LTS 安裝，必須獨立安裝索引定義。 如需更多詳細資訊，請參閱[此文章](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)。

## 安裝並更新 AEM Forms 附加元件 {#install-update-aem-forms-add-on}

如需詳細說明，請參閱[執行就地升級](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions)。


## 支援平台 {#supported-platforms}

尋找受支援平台的完整矩陣，包括 [AEM 6.5 LTS 技術要求](/help/sites-deploying/technical-requirements.md)的支援等級。

>[!NOTE]
>
>建議與 AEM 6.5 LTS 搭配使用的版本為 Java™ 17/Java™ 21。


## 已棄用和已移除的功能 {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe 會持續審閱或演進產品功能，藉由更新或取代舊版功能，帶來更高的客戶價值。 實施這些變更時，考量回溯相容性。

為確保透明度並允許適當規劃，Adobe 會遵循 Adobe Experience Manager (AEM) 的棄用流程：

* 首先宣佈棄用。 棄用的功能仍可使用，但不再有所增強。
* 移除不早於下一個主要版本。 規劃的移除時間軸會單獨發佈通訊。
* 至少會提供一個發行週期，讓客戶在功能移除前轉換為支援的替代方案。

### 已棄用功能 {#deprecated-features}

此區段列出 Adobe 在 AEM 6.5 LTS 中已棄用的特點與功能。 通常，在未來版本中移除某些功能之前，Adobe 會先將棄用該功能並提供替代方案。

建議客戶檢視是否在目前的部署中使用了棄用的功能。 制定計畫，變更您的實作，以使用提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
| --- | --- | --- | --- |
| Sites | 內容片段文字摘要 | 無可用的替代方案。 | |
| 快速入門 | Mongo API | Mongo API 現已棄用，並規劃在未來版本中移除。 | 6.5 TS SP2 |
| Sites | AEM Assets REST API 中的內容片段支援 | AEM 6.5 LTS SP2 為內容片段和模型管理提供現代化的 OpenAPI，因此 AEM Assets REST API 中較舊的內容片段支援端點現已棄用。<br>Adobe 預計在生命週期結束公告前保留這些較舊的端點。 Adobe 未計劃針對已棄用的端點提供進一步的增強功能。 | 6.5 LTS SP2 |
| Sites | [SPA 編輯器](/help/sites-developing/spa-overview.md) | 在 AEM 中管理無周邊內容的首選編輯器是：<br>- [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。<br>- [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。 | 6.5 LTS 正式發佈版 |
| [!DNL Foundation] | 支援 com.adobe.granite.oauth.server | Adobe IMS 整合 | |

### 已移除的功能 {#removed-features}

此區段列出 AEM 6.5 LTS 已移除的特點和功能。 先前的版本已將這些功能標記為已棄用。

* 針對Adobe CRX存放庫持續性的RDBMK支援已移除。
* 在叢集環境中，MongoMK 現在是存放庫持續存在的唯一支援選項。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
| --- | --- | --- | --- |
| Commerce | 不支援 AEM CIF Classic。 | 移轉至 [AEM CIF](/help/commerce/cif/migration.md)。 | 6.5 LTS 正式發佈版 |
| 解決方案 | 不支援 Social/Communities。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Screens | 不支援 Screens。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Assets | 不支援 `dam-pim` 及 `dam-rating`，因為搭售方案需依賴 Social。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Assets | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` 已移除。 | 使用已新增的替代 API `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()`。 | 6.5 LTS 正式發佈版 |
| Portal | 不支援 AEM Portal Director。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Granite | 搭售方案 `com.adobe.granite.socketio` 已移除。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Granite | 不支援 `com.adobe.granite.crx-explorer`。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Granite | 不支援 `crx2oak`。 | 選擇 [oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) 的相關版本 | 6.5 LTS 正式發佈版 |
| Adobe | 不支援 `com.adobe.cq.cq-searchpromote-integration`。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| Guava | AEM 中所有的 guava 相依性都已移除，因此 `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` 搭售方案不再屬於 AEM 的一部分。 | 客戶若需依賴 guava，可以自行新增 guava，或在可能的情況下使用 Java 集合或其他替代方案取代 guava 程式碼。 | 6.5 LTS 正式發佈版 |
| `We.Retail` | 不支援 `We-retail` 範例網站。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | 不支援 `oak-solr-osgi` 搭售方案。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | 不支援 `org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom`，以及 `org.apache.sling.atom.taglib`。 | 無可用的替代方案。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | `org.apache.commons.io` 封裝現在從 `org.apache.commons.commons-io` 匯出。 | 不需要變更。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | `javax.mail` 封裝從 `com.sun.javax.mail` 搭售方案匯出。 | 不需要變更。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | `org.apache.jackrabbit.api` 封裝現在從 `org.apache.jackrabbit.oak-jackrabbit-api` 搭售方案匯出。 | 不需要變更。 | 6.5 LTS 正式發佈版 |
| 開放原始碼 | 不支援 `com.github.jknack.handlebars` | 選擇相關的[版本](https://mvnrepository.com/artifact/com.github.jknack/handlebars) | 6.5 LTS 正式發佈版 |

## 已知問題 {#known-issues}

### AEM Forms

* 在 Configuration Manager 中，未選取模組或僅選取有限元件時，在 AEM Forms 6.5 LTS JEE Turnkey 自訂模式中的 Bootstrap 期間，資料庫初始化會失敗。 失敗是因為遺失相依性 (xalan-2.7.2.jar)，導致錯誤。 將JAR檔案新增至Adobe-livecycle-jboss.ear\lib即可解決問題。 (FORMS-24690)
* 在WebSphere® Liberty Profile上執行的Forms JEE LTS Service Pack 2部署中，電子郵件功能會失敗。 嘗試使用電子郵件功能時，伺服器會記錄錯誤： `Could not convert socket to TLS`。 (FORMS-24692)
* 在JBoss®上執行的Forms JEE LTS上，電子郵件相關功能會失敗。 嘗試使用電子郵件功能時，伺服器會記錄錯誤： `Error IMAPProvider not a subtype`。 若要解決此問題，請從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-core-jboss.ear)安裝Hotfix。 (FORMS-24892)

### 離線壓縮後線上壓縮期間存放庫損毀 (GRANITE-65146) {#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146}

若先前曾在 JCR 存放庫上執行過離線壓縮，使用者在執行線上壓縮時可能會遇到存放庫損毀的情況。 此情境中可能會發生 `SegmentNotFoundException` (SNFE)，並可能導致存放庫損毀。

若要解決此問題，請安裝「[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-65388-1.0.zip)」處的 Hotfix。 由於 Hotfix 包含低階 `oak-segment-tar` 組合包，所以執行個體會在安裝後重新啟動。

計劃套用執行個體時的停機時間。 若要離線壓縮，請使用對應的 [`oak-run` jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar) (也可在 Software Distribution 中使用)。

>[!NOTE]
>
> * 對於任何 `oak-run` 作業，請使用 [`oak-run` 1.88.1-B006 jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar)。
>
> * 設定系統屬性 `oak.compaction.legacy=true` 以啟動 AEM。

### AEM 6.5 LTS SP2中缺少`com.adobe.granite.apicontroller`套件(GRANITE-67640) {#missing-apicontroller-bundle-granite-67640}

AEM 6.5 LTS SP2中缺少`com.adobe.granite.apicontroller`套件。 此套件組合會控制OSGi套件組合解析的方式，並可防止套件組合解析為其他套件，這對於限制公開的API很有用。

若要使用此功能，請從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-67640-1.0.zip)安裝Hotfix。

>[!NOTE]
>
> 若要確保`com.adobe.granite.apicontroller`的預設設定不會引入影響現有自訂實作的意外解析度限制，請在安裝Hotfix之後確認所有已安裝套件的套件狀態。

### Sling-Initial-Content (SP2) 中已不再支援 JSON 註解 {#json-comments-no-longer-supported-in-sling-initial-content}

此問題會影響 OSGi 組合包開發人員和管理員，其部署了使用 `Sling-Initial-Content` 與 JSON 檔案的組合包。

從 AEM 6.5 LTS SP2 開始，`Sling-Initial-Content` 組合包中使用的 JSON 檔案已不再接受註解 (`//` 或 `/* */`)。 較舊的 AEM 版本可接受註解，因為 `javax.json` 提供者對此較為寬容。 AEM 6.5 LTS SP2 將 `org.apache.sling.jcr.contentloader` 升級至 2.6.0 版，並將 JSON 剖析器切換為 `jakarta.json`。 雖然 [JSON 規格 (RFC 8259)](https://datatracker.ietf.org/doc/html/rfc8259) 並未定義註解的語法，但由於 `javax.json` 提供者的寬容，較舊的 AEM 版本可以接受註解。 `jakarta.json` 提供者並未提供此擴充功能。

此失敗是無訊息的：組合包啟用時無法載入內容節點，且安裝程式不會顯示任何錯誤。 如果在升級至 SP2 後意外遺失內容，請檢查 OSGi 安裝程式記錄中的 JSON 剖析錯誤。 若要識別受影響的組合包，請在 `Sling-Initial-Content` 資訊清單標頭下方列出的 JSON 檔案內搜尋 `//` 或 `/* */`。

>[!CAUTION]
>
> 為避免升級至AEM 6.5 LTS SP2後內容載入失敗，請從`Sling-Initial-Content`套件組合中的JSON檔案移除所有註解。

### Jackson套件組合升級會影響GlobalLink聯結器 {#jackson-upgrade-globallink-connector}

AEM 6.5 LTS SP3升級`jackson`套件。 此變更會影響使用GlobalLink翻譯聯結器的部署。

如果您使用3.4.0之前版本的`gs4tr-globallink-adaptors-aem.core`套件組合，請將套件組合升級至相容版本。 3.4.0版或更新版本可搭配SP3中升級的`jackson`套件組合使用。

>[!NOTE]
>
> 在SP3更新之前或期間，將`gs4tr-globallink-adaptors-aem.core`套件組合升級至3.4.0或更新版本，以避免GlobalLink聯結器的相容性問題。


### 安裝 Sites Headless API 必要的 Oak 索引{#site-headless-api}

部分移至 Sites Headless 的 API 需要額外的 Oak 索引才能完整發揮功能。

若要使用下列功能，請安裝`cq-dam-cfm-indices`套件：

* 列出內容片段模型
* 列出內容片段
* 搜尋 API
* 工作流程

從 Adobe 軟體發佈入口網站下載索引套件 [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fcq-dam-cfm-indices-1.1.5.zip)。

### 使用僅限 SSL 連線功能時 Dispatcher 連線失敗 (AEM 6.5 LTS SP1 及以上版本已修正){#ssl-only-feature}

>[!NOTE]
>
> 這項問題僅出現在 AEM 6.5 LTS GA 版本。

在 AEM 部署中啟用僅限 SSL 功能時，有一項已知問題會影響 Dispatcher 和 AEM 實例之間的連線。 啟用此功能後，健康情況檢查會失敗，且Dispatcher與AEM執行個體之間的通訊會中斷。 當客戶嘗試透過 `https + IP` 從 Dispatcher 連線至 AEM 執行個體時，特別容易發生此問題。 此問題與 SNI (伺服器名稱指示) 驗證問題有關。

**影響**

* 健康情況檢查失敗，回應代碼為 HTTP 400。
* Dispatcher 與 AEM 執行個體之間的流量中斷。
* 無法透過 Dispatcher 正確地提供內容。
* 利用 Dispatcher 設定中的 IP 位址進行 HTTPS 連線失敗。
* 透過 HTTPS + IP 連線時出現 HTTP 400「無效 SNI」錯誤。

**受影響的環境**

* 具有 Dispatcher 設定的 AEM 部署。
* 已啟用僅限 SSL 功能的系統。
* 使用 `https + IP` 方法連線至 AEM 執行個體的 Dispatcher 設定。

**解決方案**

如果您遇到此問題，請聯絡Adobe客戶支援。 可以使用 Hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 解決此問題。 在套用必要的 Hotfix 之前，請勿嘗試啟用僅限 SSL 功能。

## 包含的 OSGi 套件和內容套件{#osgi-bundles-and-content-packages-included}

下列zip檔案包含列出此Experience Manager 6.5 LTS Service Pack版本中包含的OSGi套件組合和內容套件的文字檔案：

* [OSGi組合](/help/release-notes/assets/65lts_sp3_bundles.zip)
* [內容封裝](/help/release-notes/assets/65lts_sp3_packages.zip)

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [在 licensing.adobe.com 下載產品](https://licensing.adobe.com/)
* [聯絡 Adobe 客戶支援](https://experienceleague.adobe.com/zh-hant/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience)。

