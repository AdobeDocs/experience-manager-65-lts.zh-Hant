---
title: Adobe Experience Manager 6.5 LTS、SP2最新發行說明
description: 尋找 Adobe Experience Manager 6.5 LTS Service Pack 2 的最新版本資訊。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 56a6a366aa563cab3a0385c619041238f04b31c5
workflow-type: tm+mt
source-wordcount: '5867'
ht-degree: 21%

---

# Adobe Experience Manager 6.5 LTS、SP2最新發行說明 {#release-notes}

## 版本資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | Service Pack 2 (SP2) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack 發行 |
| 日期 | 2026年2月19日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.2.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## [!DNL Adobe Experience Manager] 6.5 LTS、SP2包含哪些專案 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS，SP2包含新功能、客戶要求的重要增強功能和錯誤修正。 其中也包括自 2025 年 3 月首次推出 6.5 LTS 版本以來針對效能、穩定性與安全性所發佈的增強功能。[在 6.5 LTS 上安裝此 Service Pack](#install-update)。

## 主要功能和增強功能

**AEM Sites**

AEM 6.5 LTS SP2現已包含用於內容片段及模型管理和啟動的OpenAPI。 這些API提供內容片段和啟動項的存取權，以進行製作和排程。 它們使用與AEM as a Cloud Service相同的現代OpenAPI。


<!-- UPDATE THE EACH RELEASE -->

## 6.5 LTS Service Pack 2 的已修正問題 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP2}

#### 無障礙功能 {#sites-accessibility-65-lts-sp2}

* 當作者在編輯期間將專案暫留在元件瀏覽器中時，文字元件遺失鍵盤焦點。 這會中斷輸入，並觸發WCAG 3.2.1下的協助工具失敗。此修正可防止暫留樣式移動焦點，並使文字元件在元件瀏覽器互動期間維持焦點。 (SITES-35370)
* 修正說明RTF欄位中使用Tab鍵封鎖向前導覽的焦點管理。 使用者在RTE中卡住，因為元件依賴非標準鍵盤命令來轉移焦點，這會中斷預期的對話方塊導覽。 此變更會強制標準鍵盤互動，並保留整個對話方塊的邏輯Tab排序。 (SITES-35228)
* 修正Sites編輯器中，在頁面製作期間中斷預期行為並導致不一致的元件互動的問題。 作者遇到不可靠的UI回應，干擾了標準編輯任務並降低工作流程效率。 此更新會精簡基礎的編輯器邏輯，並還原受影響元件間穩定、可預測的互動。 (SITES-35227)
* 一種回歸，中斷頁面編輯器中的資產選擇器，並阻止其在特定頁面編輯情景中載入。 作者現在可以在編輯頁面時選擇或瀏覽資產時，正常開啟和使用資產選擇器。 此變更會還原對載入失敗中斷的資產選擇工作流程的一致存取權。 (SITES-35226)
* 消除網站編輯器中，在頁面互動期間導致不一致行為並中斷標準編寫工作流程的問題。 該缺陷導致未預期的UI回應，會干擾元件設定和內容更新。 此更新可穩定受影響的功能，並恢復跨頁面可靠執行編輯動作。 (SITES-35225)
* 消除Sites製作介面中的缺陷，該缺陷會導致頁面編輯期間的不一致行為並中斷正常工作流程。 作者遇到非預期的UI回應，干擾元件互動和內容更新。 此更新可穩定受影響的功能，並還原所有編輯案例中可靠且可預測的行為。 (SITES-35224)
* AEM Sites現在包含影像上的`alt`文字支援，以符合ADA和WCAG需求。 頁面輸出不再省略`alt`屬性，因此熒幕助讀程式會收到正確的替代文字。 (SITES-27153)
* 修正`Note Add`工具列配置，讓「新增」按鈕不再與檢視區寬度320px的標題重疊。 改善小熒幕Reflow，讓控制項在400%縮放期間仍可讀取和使用。 (SITES-25376)
* 修正連結選取對話方塊錯誤遺失熒幕助讀程式宣告的問題。 UI現在會透過狀態訊息容器發佈錯誤文字，因此NVDA會在訊息出現時立即讀取訊息。 (SITES-25368)
* 已從側邊欄資產清單中移除ARIA格線和格線儲存格角色。 還原標準清單語意和鍵盤焦點順序，改善熒幕助讀程式導覽並減少額外的定位點。 (SITES-25361)
* 修正側欄Assets中的焦點排序。 鍵盤使用者現在透過一致的索引標籤路徑觸及每個資產動作，包括編輯。 (SITES-25360)
* 已修正「搜尋Assets」強制回應中320px檢視區寬度處的版面溢位。 強制回應視窗內容現在會重新整理並維持可讀狀態，因此控制項不再重疊或超出對話方塊。 (SITES-25330)
* 修正「編輯」按鈕的NVDA輸出。 NVDA現在會朗讀「編輯」動作，而不是「按下預覽按鈕」。 (SITES-25320)
* 修正未命名的人口統計工具列文字輸入，造成無訊息或一般熒幕助讀程式輸出。 現在，每個輸入都會顯示明確的標籤式協助工具名稱，以改進鍵盤和輔助技術導覽。 (SITES-25316)
* 修正「版面配置預覽」導覽期間「人口統計」工具列的鍵盤焦點順序。 標籤導覽現在直接從「人口統計」按鈕移動到工具列控制項，而不跳到次要工具列。 (SITES-25305)
* 修正「編輯版面」尺標上「較小的Screens」和「平板電腦」標籤的宣告順序有誤。 熒幕助讀程式現在會在符合頁面配置的正確尺標標籤處朗讀這些標籤。 (SITES-25291)
* 修正200%縮放時編輯配置工具列溢位的錯誤。 內容現在會保留在檢視區內，並可透過捲動存取。 (SITES-25288)
* 解決註解覆蓋中焦點順序不正確的問題。 鍵盤Tab鍵現在可在覆蓋控制項和註釋專案中循環。 上層頁面不再從覆蓋圖後面獲得焦點。 (SITES-25282)
* 修正色票彈出視窗焦點處理問題。 對話方塊現在會將焦點移至清晰的標題，並在該進入點開始熒幕助讀程式輸出。 NVDA不再以非順序讀取完整的對話方塊內容。 (SITES-25275)
* 修正「日期選擇器」關閉後的Timewarp強制回應視窗焦點處理問題。 `Escape`現在將焦點傳回至日期選擇器按鈕。 日期選取範圍現在會將焦點放在「日期選擇器」控制項旁的輸入欄位上，以防止焦點遺失和背景頁面存取。 (SITES-25264)
* 修正「刪除註釋」對話方塊的鍵盤焦點處理。 取消現在會將焦點傳回至開啟對話方塊的`Delete`控制項，而非Confirm hex value控制項。 取消後，熒幕助讀程式不再朗讀不相關的對話方塊內容。 (SITES-25258)
* 修正「註釋模型」對話方塊的焦點處理方式。 開啟對話方塊現在會將焦點設定在對話方塊標題上，並阻止NVDA讀取畫布內容和不相關的對話方塊文字。 鍵盤導覽現在會保留在對話方塊內，直到關閉為止。 (SITES-25257)
* 修正320px寬度的搜尋模式配置問題。 強制回應內容現在會乾淨地重新整理，並避免與樹狀目錄重疊。 使用者可以檢視結果並瀏覽目錄，而不需要模糊的控制項。 (SITES-25246)
* 搜尋模組文字在文字間距增加後不再剪輯。 樹狀目錄版面配置現在會保持清晰的區隔，讓標籤和專案保持可讀性。 使用者現在可以在沒有重疊或截斷文字的情況下完成搜尋和導覽。 (SITES-25245)
* 啟動「註釋」現在會將鍵盤焦點移至註釋內容，而不是「退出」註釋按鈕。 Tab鍵順序遵循邏輯順序，並保持相關控制項可連線而不需反嚮導覽。 (SITES-25241)
* 設定日期和退出時間扭曲連結在鍵盤導覽期間缺少可見的焦點指示器。 UI現在會呈現明顯的高對比焦點樣式，讓使用者一眼就能識別作用中的連結。 (SITES-25232)
* Teaser Modal標題不再封鎖鍵盤使用者移動對話方塊。 鍵盤控制現在允許拾取、移動和放置動作，這可以改善熒幕助讀程式的易用性和整體操作性。 (SITES-25226)
* AEM現在對Teaser強制回應資訊按鈕使用有意義的易存取標籤。 熒幕助讀程式會朗讀清除動作名稱，而非預設圖示替代文字字串。 (SITES-25223)
* 熒幕助讀程式現在會在使用者啟動編輯按鈕時朗讀正確的動作。 NVDA不再報告「預覽按鈕已按下」，這會導致鍵盤導覽期間產生誤導性意見及混淆。 (SITES-25208)
* 展開左側邊欄現在會將鍵盤焦點移至第一個左側邊欄控制項。 Tab鍵順序不再跳至次要工具列或登陸中間清單，因此鍵盤使用者無需反嚮導覽即可觸及左側邊欄內容。 (SITES-24998)
* 裝置模擬器列內容現在在320畫素檢視區寬度下仍完全可見。 工具列文字和控制項換行，而非截斷，減少重疊並改善可讀性。 (SITES-24953)
* AEM現在會在模擬器工具列中顯示完整的iPhone裝置標籤。 文字不再以預設寬度截斷，進而改善可讀性和裝置選擇的清晰度。 (SITES-24952)
* 清單檢視表標題現在透過ARIA公開排序狀態。 熒幕助讀程式會在欄排序動作後宣告遞增或遞減順序。 (SITES-24943)
* 在文字間距變更期間，AEM現在會在「卡片檢視」中保留「更多動作」選單標籤可見性。 選單選項會保留完整的文字，包括「快速發佈」，而且選單在任何WCAG文字間距設定期間都會保持清晰可見。 (SITES-24941)
* 卡片動作功能表列現在會在「卡片檢視」中顯示可存取的名稱。 熒幕助讀程式會清楚宣告功能表列的用途，而語音控制功能可依名稱鎖定控制項。 (SITES-24938)
* 卡片檢視不再依賴ARIA格線語意，造成熒幕助讀程式行為混亂。 UI現在為卡片內容和卡片動作列提供有意義的角色和標籤，以減少鍵盤使用期間遺漏的控制項。 (SITES-24933)
* 每次使用者將工具提示圖示暫留時，`Delete Modal`工具提示都會顯示。 焦點動作現在會顯示相同的工具提示文字，這可改善滑鼠和鍵盤使用者的重複存取權。 (SITES-24778)
* 使用者設定邊欄後，左側邊欄導覽現在會依照預期的鍵盤焦點順序進行。 Tab焦點會出現在選取的左側邊欄區域，而非Switch Display，這可改善熒幕助讀程式導覽的清晰度。 (SITES-24754)
* 修正「使用者偏好設定」強制回應視窗中色票導覽期間不正確的NVDA意見。 NVDA現在會讀取接收焦點的色票標籤，如此可移除誤導性的色彩輸出。 色票集現在支援一致的鍵盤導覽和清除選取範圍感知功能。 (SITES-24739)
* 減少`Spin`控制項的詳細NVDA輸出。 移除重複輸入標籤的重複群組標籤，因此NVDA會朗讀一次控制項名稱。 鍵盤和熒幕助讀程式導覽功能現在可提供單一清楚的宣告。 (SITES-24725)
* 「轉盤」對話方塊現在會將焦點置於對話方塊標題上，而非「專案」索引標籤。 取消並Esc將焦點還原至啟動對話方塊的控制項，這會減少詳細的NVDA輸出。 (SITES-24716)
* 連結選取對話方塊現在會將程式設計標籤與最後層級樹狀結構專案的熒幕標籤對齊。 箭頭鍵導覽會針對每個專案觸發可靠的熒幕助讀程式宣告，並移除誤導性的標籤輸出。 (SITES-24710)
* 現在，在320-px檢視區下，「連結開啟選取專案」對話方塊會正確重排。 內容不再超出模組或截斷，且模組不再顯示水準卷軸。 (SITES-24709)
* 現在，在「關閉」或「取消」之後，「連結開啟選取範圍」對話方塊的鍵盤焦點會恢復至對話方塊觸發程式。 焦點不再跳至連結輸入，讓熒幕助讀程式內容保持穩定，並減少額外的導覽。 (SITES-24707)
* 影像模組對話方塊現在會依照邏輯焦點順序顯示。 取消後，焦點不再略過先前的控制項或落在頁面里程碑上，使用者在退出後會重新獲得對「設定」按鈕的焦點。 (SITES-24693)
* 參考邊欄強制回應對話方塊現在會設陷鍵盤焦點。 Tab和Shift+Tab停留在對話方塊控制項內，且焦點不再逸出至頁面內容。 熒幕助讀程式只會朗讀對話方塊內容。 (SITES-24683)
* 「超連結路徑選取」強制回應現在會在開啟時將焦點設定在對話方塊標題上。 取消關閉對話方塊並將焦點恢復到「開啟選取對話方塊」按鈕，可防止焦點遺失及多餘的熒幕閱讀器輸出。 (SITES-24672)
* 「搜尋」欄位現在會使用持續性的熒幕上標籤，而非預留位置文字。 標籤在輸入時仍可見，可讓鍵盤、熒幕閱讀器和語音使用者更清楚易懂。 (SITES-24529)
* Teaser模型對話方塊現在會在開啟時將焦點設定在對話方塊標題上。 關閉對話方塊會將焦點傳回`Configure`控制項，避免焦點遺失及熒幕助讀程式輸出過多。 (SITES-24522)
* 側邊欄Assets面板現在包含關閉控制項。 「關閉」會將鍵盤焦點傳回側邊欄切換，並防止透過面板內容強制使用Tab鍵。 (SITES-24489)
* 鍵盤Tab鍵現在可觸及管理員表格內的按鈕和連結。 使用者不再依賴方向鍵儲存格導覽來尋找互動式控制項。 (SITES-24285)
* 「影像元件」對話方塊不再以影像形式顯示裝飾性說明和全熒幕圖示。 熒幕助讀程式現在會略過這些圖示，將焦點保持在可操作的控制項和欄位內容上。 (SITES-2940)
* 網站管理員現在會從資料夾縮圖圖示中移除影像角色。 輔助技術會略過這些裝飾性元素，將焦點持續放在資料夾名稱和動作上。 (SITES-2852)
* 「內容樹」現在會將鍵盤焦點路由至活動樹狀專案或第一個樹狀專案。 樹狀結構容器不再充當空的Tab停駐點，防止Shift+Tab焦點陷阱。 (SITES-1577)

#### 管理員使用者介面{#sites-adminui-65-lts-sp2}

網站控制檯清單檢視設定未反映清單檢視中顯示的欄。 對話方塊開啟，其中已清除核取方塊，且選取的欄計數不正確。 「修復同步」對話方塊狀態與作用中格線欄，並更新計數器以符合實際的欄可見度。 (SITES-38576)

#### Classic 使用者介面{#sites-classicui-65-lts-sp2}

升級後，傳統UI文字元件編輯會顯示原始HTML標籤，而非RTF文字。 Service Pack 2會更正傳統UI RTE （RTF編輯器）呈現，讓編輯器顯示格式化的內容並保留儲存的標籤。 此修正也會在重複編輯和儲存期間停止標示擴展。 (SITES-38709)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp2}

Headless事件支援缺少6.5 LTS中內容片段和模型的必要OSGi事件。 更新新增事件套件組合加上必要的相依性，並包含6.5 LTS組建。 內容片段和模型事件現在可以正確引發，並支援「啟動API」工作流程。 (SITES-35329)

#### [!DNL Content Fragments] — 管理員{#sites-admin-65-lts-sp2}

* 調整Sites編寫介面中的元件處理，以停止頁面更新期間的不規則行為。 此缺陷導致無法預測的編輯器回應，干擾例行內容修改並降低工作流程效率。 此更新會根據預期的互動模式來調整編輯器邏輯，並在編寫活動期間提供可靠的效能。 (SITES-35078)嚴重

* 回歸中斷了內容片段的Assets主控台清單檢視，並在清單轉譯期間觸發錯誤。 在移除preview-info後，更新會修正list-view邏輯，並還原穩定的清單輸出。 主控台現在會顯示內容片段而不會失敗，並讓清單互動保持可用。 (SITES-38683)
* 內容片段編輯器現在會將標籤標籤當地語系化。 編輯器也會將集合標籤當地語系化，因此UI文字會符合所選地區設定。 (SITES-977)


#### [!DNL Content Fragments] — 片段編輯器{#sites-fragments-editor-65-lts-sp2}

* 重構後，當功能切換保持停用狀態時，內容片段變數標籤消失。 此修正會還原變數標籤支援，即使該切換功能保持關閉亦然。 作者可以在內容片段編輯器中再次新增和檢視變數標籤。 (SITES-38682)嚴重
* 作者從內容片段編輯器導覽回之後，編輯的內容片段從Assets主控台清單中消失。 瀏覽器快取傳回過時的清單，並隱藏更新的片段，直到手動重新整理為止。 此修正針對編輯器傳迴路徑新增快取控制處理，使清單可正確重新載入，並保持編輯後的片段可見。 (SITES-35374)嚴重

* 在最近的UI樣式變更後，內容片段RTE顯示版面和視覺問題。 Service Pack 2會精簡RTE樣式，讓工具列和可編輯區域可正確呈現並保持可讀性。 內容片段編輯器現在會與頁面編輯器的外觀和行為一致。 (SITES-38684)
* 從Polaris資產選擇器移除IMS範圍會中斷內容片段與傳送端點的整合。 作者在開啟遠端資產選擇器並選取資產時失敗。 更新會重新新增所需的IMS範圍，並還原穩定的傳遞層級存取權。 (SITES-35837)
* 「關聯內容」面板不再呈現硬式編碼的「未定義」預留位置。 內容片段編輯器現在會透過本地化資源解析該文字，因此編輯器可以看到翻譯過的UI文字。 (SITES-33675)
  <!-- REMOVED FROM BUG LIST FEBRUARY 13, 2026 * Preview error messaging now uses localized strings instead of raw `Cannot print fragment's Json` text. The Content Fragment Editor now shows translated output across locales during GraphQL endpoint resolution failures. (SITES-33666)-->
* 內容片段編輯器現在會在不同區域設定中顯示翻譯的「一般」標籤標籤。 編輯器會取代未本地化的索引標籤文字，並從索引標籤標題中移除內部ID。 (SITES-30715)
* 內容片段編輯器現在會顯示所允許資產型別的翻譯名稱。 當作者設定內容參考限制時，選擇器清單不再混合內部字串和僅限英文的標籤。 (SITES-29699)

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp2}

* 改善GraphQL查詢驗證處理，以停止篩選執行錯誤所導致的部署失敗。 缺陷會在應用程式啟動期間產生例外狀況，並封鎖受影響環境中的成功轉出。 修訂版本可確保一致的驗證行為，並可在沒有執行階段查詢驗證中斷的情況下順利部署。 (SITES-34301)嚴重

* 「編輯GraphQL端點」對話方塊現在會顯示當地語系化的UI字串。 此對話方塊不再顯示純英文文字，例如「從設定中獲取GraphQL結構描述」，而相關標籤在各個地區設定中正確呈現。 (SITES-34018)

#### [!DNL Content Fragments] - GraphQL查詢編輯器{#sites-graphql-query-editor-65-lts-sp2}

* 改善GraphQL查詢驗證處理，以停止篩選執行錯誤所導致的部署失敗。 缺陷會在應用程式啟動期間產生例外狀況，並封鎖受影響環境中的成功轉出。 修訂版本可確保一致的驗證行為，並可在沒有執行階段查詢驗證中斷的情況下順利部署。 (SITES-35529)
* 當設定瀏覽器名稱包含CJK字元時，GraphQL Explorer不再失敗。 端點建立和儲存的查詢存取正常運作，且GraphQL查詢編輯器頁面保持無錯誤。 (SITES-31616)

#### [!DNL Content Fragments] — 模型編輯器{#sites-model-editor-65-lts-sp2}

* 當重構將功能繫結到已停用的切換時，巢狀內容片段模型已停止運作。 修復會還原巢狀模型支援，而不需要切換變更。 作者可以在「模型編輯器」中再次建立並使用巢狀模型。 (SITES-38681)嚴重

* 內容片段模型篩選器面板不再顯示未本地化的字串。 AEM現在會顯示所有地區設定的當地語系化篩選器標籤和當地語系化狀態值。 (SITES-30863)
* 內容片段模型編輯器現在會轉譯鎖定警告對話方塊的本地化字串。 UI以各種支援語言的地區設定資源取代未本地化的英文訊息。 (SITES-28592)

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp2}

AEM Headless需要專用的發行分支，以避免相依性和套裝版本與主線組建衝突。 此更新新增了版本/6.5lts Headless分支，並對齊相依性集和套件版本。 Jenkins現在可以完全建置Headless程式碼基底，而不會發生版本衝突。 (SITES-36585)

<!-- #### Component console{#sites-component-console-65-lts-sp2} -->

#### 內容API{#sites-content-api-65-lts-sp2}

功能切換缺陷誤報的頁面管理API狀態。 此更新會新增專用的啟用旗標，並與現有切換一併評估。 頁面管理API現在顯示穩定狀態。 網站管理API仍維持實驗性質。 (SITES-39284)

#### 核心後端{#sites-core-backend-65-lts-sp2}

* 網站製作體驗中的變更，可解決中斷標準頁面編輯工作流程的不一致行為。 作者在元件互動期間遇到非預期的結果，這會干擾內容更新並降低可靠性。 這項變更會恢復穩定的編輯器行為，並確保在受影響的情景中一致地執行創作操作。 (SITES-35162)嚴重

* 改善Sites編寫行為，以解決在元件互動期間中斷頁面編輯並造成不一致結果的問題。 作者遇到非預期的UI回應，這會干擾內容更新並降低工作流程可靠性。 此變更可恢復穩定的編輯器狀態管理，並確保在受影響的情境中可預測地執行創作操作。 (SITES-34499)

<!--
#### Core Components{#sites-core-components-65-lts-sp2}

#### Campaign integration{#sites-campaign-integration-65-lts-sp2}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp2}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp2}
-->

#### 啟動{#sites-launches-65-lts-sp2}

* 網站時間軸在啟動促銷活動期間顯示硬式編碼英文文字：「啟動之前建立版本……」。 更新會將硬式編碼字串替換為本地化的訊息處理。 時間軸現在會顯示當地語系化文字，並使專案符合標準AEM當地語系化行為。 (SITES-39157)
* 當作者使用提升目前頁面和子頁面來提升子區段時，啟動提升範圍會漂移。 AEM也會提升不相關的頁面，並造成非預期的即時網站修改。 此修正會修正Launch範圍計算，因此僅會提升所選的子樹狀結構。 (SITES-38315)
* Launches內的內容片段未參與`damAssetLucene`索引，且搜尋結果和查詢效率有限。 此變更會將Launch內容片段路徑新增至索引定義。 搜尋和自訂查詢現在會在`/content/launches`下找到內容片段。 (SITES-35634)
* 即使產品沒有在觸控式UI中公開內容片段啟動，啟動UI仍顯示內容片段啟動控制項。 此變更會從cq-launches-content中移除內容片段啟動程式碼路徑，並調整Launch清單篩選條件。 作者現在會看到一致的頁面啟動選項，但沒有內容片段啟動專案。 (SITES-35633)
* AEM 6.5 LTS Quickstart缺少必要的Launches套件組合和先決條件，導致無法啟用Launches OpenAPI。 此更新會新增Launch套件組合和必要的相依性，例如量度支援、DAM-cfm更新和佇列設定。 現在於6.5 LTS Quickstart上執行的Launches API，必須有必要的執行階段元件。 (SITES-35297)
* CF Launches封裝會提取較新的相依性版本和不必要的GraphQL程式庫，這會使AEM 6.5 LTS整合複雜化。 此變更會將相依性版本與AEM 6.5 LTS基準保持一致，並移除未使用的GraphQL相依性。 套件組合解析度現在會維持一致，且CF Launches啟動會維持穩定。 (SITES-35295)
* AEM Launches現在會執行6.5 LTS分支的專用Jenkins管道。 管道會在夜間執行，並透過電子郵件傳送失敗警報。 此設定會增加測試涵蓋範圍並及早擷取回歸。 (SITES-35293)
* AEM 6.5 LTS現在隨校準的成品版本推出更新的Launches API套件。 該套件追蹤主要程式碼行，同時保持正確的6.5 LTS發行版本。 此更新穩定6.5 LTS棧疊中的Launch API消耗。 (SITES-35292)
* AEM 6.5 LTS現在包含更新的啟動核心套件組合與對齊的相依性版本。 此更新新增片段UUID和參考UUID資料型別的啟動核心處理。 Launch處理現在可在各啟動和內容片段工作流程中保持一致的行為。 (SITES-35290)
* 改善Sites編輯器，以解決會中斷正常頁面製作工作流程的不一致行為。 作者遇到意外的元件互動，干擾內容更新並降低編輯可靠性。 此變更可恢復一致的UI狀態管理，並確保在受影響的情景中可預測地執行創作操作。 (SITES-35138)
* Launches Edit現在顯示當地語系化的錯誤文字，而非硬式編碼的`Provided path is not a launch`字串。 Edit現在收到無效的啟動路徑時，UI會呈現跨語言的翻譯訊息。 (SITES-33360)
* AEM 6.5 LTS現在包含啟動OpenAPI側端連線埠工作。 此更新將Launches API套件組合、內容套件和必要的Quickstart成品帶入同位檢查，並透過穩定的CI驗證啟用內容片段啟動OpenAPI案例。 (SITES-32050)
* 啟動UI現在會將覆寫範本標籤當地語系化。 範本覆寫詳細資訊現在會顯示翻譯文字，而非僅英文字串。 (SITES-29525)
* AEM已解決&#x200B;**Sites** > **啟動** > **編輯**&#x200B;中遺漏的本地化金鑰。 使用者現在看到已翻譯的錯誤訊息，而不是原始「無法更新啟動項來源清單」字串。 (SITES-21499)
* 上市促銷活動UI現在會顯示當地語系化的狀態標籤和動作。 預覽區域會顯示&#x200B;**已刪除**、**新增**&#x200B;和&#x200B;**檢視**&#x200B;的翻譯文字，而非原始英文字串。 (SITES-13540)
* Launch建立現在會顯示本地化的錯誤訊息。 UI不再顯示原始英文字串，例如`Unable to create launch page`、`Source root resource is not a page`或`Mandatory parameter is missing`。 (SITES-13085)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp2} -->


#### MSM - Live Copies{#sites-msm-live-copies-65-lts-sp2}

* 在內容變更期間，管理員對MSM推送修改處理的可見度有限。 此修正會新增有關MSM事件接收和轉出執行的詳細記錄。 Debug輸出現在會顯示已引發哪些事件、已變更哪些內容路徑，以及誰觸發了變更。 (SITES-38029)
* AEM已修正Blueprint轉出日期欄位上的本地化版面配置問題。 日期提示現在符合控制項，且在所有支援的語言（包括`fr_FR`）中仍可讀取。 (SITES-14961)

<!-- #### Page editor{#sites-pageeditor-65-lts-sp2} -->

#### 複製{#sites-replication-65-lts-sp2}

頁面編輯器發佈現在會處理包含選取器或尾碼的URL。 發佈的請求現在會傳送JCR頁面路徑，而非選取器或尾碼URL字串，因此啟用會完成且內容會上線。 復寫現在會在失敗時傳回錯誤狀態，以防止出現誤判的「已開始發佈」訊息。 (NPR-43288)

<!-- #### Rich Text Editor{#sites-rte-65-lts-sp2} -->

#### 範本編輯器{#sites-template-editor-65-lts-sp2}

某些地區設定在&#x200B;**工具** > **一般** > **範本**&#x200B;中垂直顯示的範本狀態文字。 「已過時」標籤破壞了版面，並讀為一欄字元。 此修正會更正範本狀態樣式，使標籤在單一水平線上呈現。 (SITES-36797)

#### 通用編輯器 {#sites-universal-editor-65-lts-sp2}

* OSGi預設設定已設為`preview=true`，並強制通用編輯器在預覽模式下啟動。 此更新會更正預設值並恢復標準的生產專案行為。 除非管理員明確啟用預覽模式，否則通用編輯器現在會在生產模式中開啟。 (SITES-37193)
* 在Dev和Stage環境中，「通用編輯器開啟」命令現在預設為「預覽」模式。 該命令新增preview=true，可保持作者檢查與預覽上下文一致，並避免意外的「生產」開啟。 (SITES-33839)

### [!DNL Assets]{#assets-65-lts-sp2}

Assets Relate現在適用於包含空格的檔案名稱。 更新關聯使用者端邏輯現在可以正確處理包含空格的路徑，並避免在關聯選取期間發生`undefined`來源錯誤。 「關係」對話方塊現在會開啟，並儲存關係，而不使用UI掛起或旋轉器。 DAM使用者無需重新命名檔案，即可建立、衍生及解除資產的相關性。 (Assets-56418)

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp2}

* 全新Dynamic Media視訊播放器整合（有限推出） — 全新Dynamic Media視訊播放器體驗現在於AEM 6.6 Quickstart中提供。 此增強功能目前僅對初始客戶啟用，作為控制轉出的一部分。 (Assets-60165)
* 解決視訊屬性對話方塊中的「選取縮圖」選項未開啟資產選擇器的問題，恢復使用者為視訊資產選擇自訂縮圖的能力。 (Assets-58926)
* 在Dynamic Media影片中，新增在「字幕與音訊曲目」語言下拉式清單中選取阿拉伯語的支援，讓作者可直接在AEM中管理阿拉伯語字幕。 (Assets-61771)

<!-- #### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp2} -->


<!--
### [!DNL Forms]{#forms-65-lts-sp2}

#### Forms Designer

#### Forms

#### Forms JEE 

#### Forms Captcha {#forms-captcha-65-lts-sp2}

#### XMLFM {#forms-xmlfm-65-lts-sp2}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp2}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp2}

#### Forms Designer

#### AdaptIve Forms

#### Forms Captcha

#### Forms Management UI
-->


### 基礎 {#foundation-65-lts-sp2}

#### Apache Felix {#foundation-apachefelix-65-lts-sp2}

* Sling Resource Access Security現在會在1.1.2版上執行。多個ResourceAccessGateHandler服務註冊時，ResourceAccessSecurityImpl在初始化期間不再擲回ClassCastException。 初始化現在會可靠完成，並避免在有多個處理常式的環境中啟動失敗。 (NPR-42750)
* JMX主控台和Web主控台現在會傳送主控台CSS資源的`Content-Type: text/css header`。 嚴格的MIME檢查不再封鎖樣式表載入，因此`/system/console/jmx` UI會以一般樣式呈現。 (GRANITE-63677)
* AEM現在會避免在產生的`contributor`中對`WEB-INF/resources/provisioning/model.txt`群組使用重複的ACL專案。 WAR輸出現在包含一個一致的ACL區塊，以防止在檢閱期間混淆許可權差異。 (GRANITE-63269)
* 在套件重新整理作業期間，AEM不再清除還原序列化防火牆封鎖清單和允許清單設定。 更新篩選器註冊邏輯可讓作用中的防火牆執行個體與儲存的設定保持一致，因此保護功能不會重新啟動而維持啟用狀態。 (GRANITE-61382)
* Felix Web主控台在`NullPointerException`存取期間不再擲回間歇性`/system/console`錯誤。 更新的ServiceTracker處理可防止null追蹤器狀態。 在重複請求和自動驗證期間，主控台登入和導覽會保持穩定。 (GRANITE-61042)

<!--
#### Campaign{#foundation-campaign-65-lts-sp2}

#### Cloud Services{#foundation-cloudservices-65-lts-sp2}

#### Communities {#foundation-communities-65-lts-sp2}

#### Content distribution{#foundation-content-distribution-65-lts-sp2}
-->

#### CRX {#foundation-crx-65-lts-sp2}

升級Service Pack後開啟JSP檔案時，CRXDE Lite不再顯示空白標籤。 AEM現在隨附相符的CodeMirror核心和附加程式碼，可避免嚴重的瀏覽器錯誤，並保持編輯器可用。 (GRANITE-64333)

#### Granite{#foundation-granite-65-lts-sp2}

Expression Security Validator現在會處理空白或Null的OSGi設定值。 它會套用安全預設值、忽略空陣列，並記錄清晰的記錄，避免NullPointerException和無法預測的驗證結果。 (NPR-43163)

<!-- #### HTL{#foundatoin-htl-5-lts-sp2} -->

#### 整合{#foundation-integrations-65-lts-sp2}

即使存在開始和結束日期，AEM現在也會同步Adobe Target活動。 Target裝載現在會將活動日期格式化為完整的ISO 8601時間戳記，包括秒、毫秒和時區。 Target不再拒絕具有`InvalidJson.Json`的要求。 已排程的活動現在會移至同步狀態，而不會離開同步。 (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-65-lts-sp2}

#### Localization{#foundation-localization-65-lts-sp2}

#### Oak {#foundation-oak-65-lts-sp2}

#### Omnisearch{#foundation-omnisearch-65-lts-sp2}

#### Platform{#foundation-platform-65-lts-sp2}

#### Projects{#foundation-projects-65-lts-sp2}
-->

#### 快速入門{#foundation-quickstart-65-lts-sp2}

AEM 6.5 LTS SP2更新了Sling、Oak和Felix的基礎層套件組合集。 這些升級會增強核心執行階段穩定性，並調整整個平台的相依性版本。 (GRANITE-61874)

<!--
#### Security{#foundation-security-65-lts-sp2}

AEM now prevents NullPointerException errors when a logged-in user lacks read access for some groups and opens the Groups tab. The tab now hides groups without access and renders group membership details without a blank or unresponsive UI. (NPR-43311) -->

#### Sling{#foundation-sling-65-lts-sp2}

AEM現在包含Sling Engine 2.16.6。此變更可消除安全性工具標示的XSS違規，並改善核心演算的安全性和穩定性。 (NPR-43105)

<!--
#### Translation{#foundation-translation-65-lts-sp2}

#### User interface{#foundation-ui-65-lts-sp2}
-->

#### WCM{#foundation-wcm-65-lts-sp2}

由於XLIFF格式問題，AEM翻譯在Java 17或Java 21上不再失敗。 匯出管道現在會產生符合翻譯提供者所接受的標準XLIFF。 此變更移除了翻譯工作中斷，並恢復AEM與翻譯服務之間的可預測切換。 支援的Java執行階段中，翻譯工作流程現在保持穩定。 (CQ-4360217)

#### 工作流程{#foundation-workflow-65-lts-sp2}

在工作流程通知處理期間，EmailNotificationService-Processor不再觸發重複的「找不到區段」錯誤。 更新的例外狀況處理會偵測SegmentNotFoundException並停止處理回圈，而非繼續無效讀取。 工作流程執行會保持穩定，並在收件匣和工作專案存取期間記錄雜訊下降。 (GRANITE-62635)




## 關於 [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS 平台是以更新版本的 OSGi 式框架 (Apache Sling 和 Apache Felix) 以及 Java™ 內容存放庫 (Apache Jackrabbit Oak 1.68.x) 為基礎進行建置。

Eclipse Jetty 11.0.x 會用於作為快速入門的 servlet 引擎。

### Java™ 支援  {#java-support}

* Java™ 17 和 Java™ 21 的支援。
* 為實現最佳效能，請使用其他值覆寫預設的 GC 值。如需詳細資訊，請參閱[安裝與更新](/help/sites-deploying/custom-standalone-install.md)區段。
* 若是 Oracle 尚未正式推出，Adobe 會分發 Java™ 17 和 Java™ 21 維護更新供客戶在 AEM 相關專案中使用。

### Uberjar 封裝 {#uber-jar-packaging}

* AEM 6.5 LTS 的 Uberjar 封裝略有不同。如需詳細資訊，請參閱[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

### 升級 {#upgrade}

* 如需升級程序的詳細資訊，請參閱[升級文件](/help/sites-deploying/upgrade.md)。
* 如需詳細的升級指示，請參閱JEE上的[AEM Forms 6.5 LTS SP1升級指南](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

#### AEM 6.5 LTS Service Pack 升級的最佳做法

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**環境**
適用於：安裝Service Pack 2 (SP2)的AEM 6.5 LTS （內部部署）客戶。 SP2會以Quickstart JAR的形式提供。

**這很重要的原因**
適用於AEM 6.5 LTS的SP2會以Quickstart JAR形式出貨，而非透過「封裝管理員」安裝的ZIP。 內部部署客戶的升級方式是取代 Quickstart JAR，將檔案解壓縮然後重新啟動。此方法與 Adobe 的就地升級程序一致。

**建議的升級流程 (作者或發佈)**

1. 確認您的AEM 6.5 LTS執行個體運作良好且可供存取。
1. 從Software Distribution下載Quickstart JAR （例如`cq-quickstart-6.6.x.jar`）。
1. 停止正在運作的實例。
1. 在AEM安裝目錄（`crx-quickstart/`以外）中，將先前的快速入門JAR取代為SP2 JAR。
1. 將 JAR 解壓縮：

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (視需要調整堆積旗標。)

1. 根據其角色和連接埠，將解壓縮的 JAR 重新命名，例如 `cq-author-4502.jar` 或 `cq-publish-4503.jar`。
1. 開始 AEM，並在 UI (「說明」>「關於」) 和記錄中確認升級。

**良好的操作規範**

* 進入生產前，在低階/測試環境中執行升級。
* 開始之前，請先進行完整、可還原的備份（儲存庫加上任何外部資料存放區）。
* 審閱 Adobe 的就地升級指引和技術要求 (LTS 建議使用 Java 17/21)。

>[!NOTE]
>
>以上所示的檔案名稱（例如`cq-quickstart-6.6.x.jar`）會反映此LTS發行版本所觀察到的快速入門成品命名；請一律使用您從Software Distribution下載的確切檔案名稱。

## 安裝與更新{#install-update}

如需關於設定需求的資訊，請參閱[安裝指示](/help/sites-deploying/custom-standalone-install.md)。

>[!NOTE]
>
> 如果您從舊的6.5 SP直接升級至LTS SP1，請依照6.5到6.5 LTS GA [升級提供的指示操作](/help/sites-deploying/upgrade.md)。


如需詳細說明，請參閱[升級文件](/help/sites-deploying/upgrade.md)。

>[!NOTE]
>
> 對於全新的 AEM 6.5 LTS 安裝，必須獨立安裝索引定義。如需更多詳細資訊，請參閱[此文章](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)。

## 安裝並更新 AEM Forms 附加元件 {#install-update-aem-forms-add-on}

如需詳細說明，請參閱[執行就地升級](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions)。


## 支援平台 {#supported-platforms}

尋找受支援平台的完整矩陣，包括 [AEM 6.5 LTS 技術要求](/help/sites-deploying/technical-requirements.md)的支援等級。

>[!NOTE]
>
>建議與 AEM 6.5 LTS 搭配使用的版本為 Java™ 17/Java™ 21。


## 已棄用和已移除的功能 {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe會持續檢討並發展產品功能，以透過更新或取代舊功能為客戶提供更高價值。 實施這些變更時，會考量回溯相容性。

為了確保透明度並允許適當規劃，Adobe會遵循Adobe Experience Manager (AEM)的淘汰流程：

* 首先宣佈淘汰。 過時的功能仍可使用，但已不再增強。
* 移除不會早於下一個主要版本。 計畫的移除時間表會單獨通訊。
* 至少會提供一個發行週期，讓客戶在功能移除前轉換為支援的替代方案。

### 已棄用功能 {#deprecated-features}

此區段列出 Adobe 在 AEM 6.5 LTS 中已棄用的特點與功能。通常，在未來版本中移除某些功能之前，Adobe 會先將棄用該功能並提供替代方案。

建議客戶檢查其目前的部署中是否使用這些特點/功能，並規劃變更其實施方案，改用所提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
| --- | --- | --- | --- |
| 快速入門 | Mongo API | Mongo API現已過時，並計畫在未來版本中移除。 | 6.5 TS SP2 |
| Sites | AEM Assets REST API中的內容片段支援 | AEM 6.5 LTS SP2為內容片段和模型管理提供現代化的OpenAPI，因此AEM Assets REST API中較舊的內容片段支援端點現已棄用。<br>Adobe打算在生命週期結束宣告前保留這些較舊的端點。 Adobe不打算為已棄用的端點提供進一步的增強功能。 | 6.5 LTS SP2 |
| Sites | [SPA 編輯器](/help/sites-developing/spa-overview.md) | AEM 中用於管理 Headless 內容的首選編輯器為：<br>- [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。<br>- [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。 | 6.5 LTS 正式發佈版 |
| [!DNL Foundation] | 支援 com.adobe.granite.oauth.server | Adobe IMS 整合  |  |

### 已移除的功能 {#removed-features}

此區段列出 AEM 6.5 LTS 已移除的特點和功能。先前的版本已將這些功能標記為已棄用。

* 針對CRX存放庫持續性的RDBMK支援已移除。
* 在叢集環境中，MongoMK現在是存放庫持續存在的唯一支援選項。

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

### 安裝Sites Headless API所需的Oak索引{#site-headless-api}

部分移至Sites Headless的API需要額外的Oak索引才能完整發揮功能。

安裝`cq-dam-cfm-indices`封裝以使用下列功能：

* 列出內容片段模型
* 列出內容片段
* 搜尋API
* 工作流程

從Adobe軟體發佈入口網站下載索引套件[cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-dam-cfm-indices-1.1.2.zip)。

### 使用僅限 SSL 連線功能時 Dispatcher 連線失敗 (AEM 6.5 LTS SP1 及以上版本已修正){#ssl-only-feature}

>[!NOTE]
>
> 這項問題僅出現在 AEM 6.5 LTS GA 版本。

在 AEM 部署中啟用僅限 SSL 功能時，有一項已知問題會影響 Dispatcher 和 AEM 實例之間的連線。啟用此功能後，健康情況檢查可能會失敗，且 Dispatcher 和 AEM 實例之間的通訊可能會中斷。當客戶嘗試透過 `https + IP` 從 Dispatcher 連線至 AEM 執行個體時，特別容易發生此問題。此問題與 SNI (伺服器名稱指示) 驗證問題有關。

**影響**

* 健康情況檢查失敗，回應代碼為 HTTP 400
* Dispatcher 與 AEM 實例之間的流量中斷
* 無法透過 Dispatcher 正確地提供內容
* 利用 Dispatcher 設定中的 IP 位址進行 HTTPS 連線失敗
* 透過 HTTPS + IP 連線時出現 HTTP 400「無效 SNI」錯誤

**受影響的環境**

* 具有 Dispatcher 設定的 AEM 部署
* 已啟用僅限 SSL 功能的系統
* 使用 `https + IP` 方法連線至 AEM 實例的 Dispatcher 設定

**解決方案**

如果您遇到此問題，請聯絡Adobe客戶支援。 可以使用 Hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 解決此問題。在套用必要的 Hotfix 之前，請勿嘗試啟用僅限 SSL 功能。

## 包含的 OSGi 套件和內容套件{#osgi-bundles-and-content-packages-included}

以下文字文件列出在此 [!DNL Experience Manager] 6.5 LTS Service Pack 1 版本中所包含的 OSGi 套件與內容套件：

* [&#x200B; Experience Manager 6.5 LTS Service Pack 1 包含的 OSGi 套件清單](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS Service Pack 1 中包含的內容套件清單](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [在 licensing.adobe.com 下載產品](https://licensing.adobe.com/)
* [聯絡 Adobe 客戶支援](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience)。

