---
title: Adobe Experience Manager 6.5 LTS SP1 的最新發行說明
description: 尋找 Adobe Experience Manager 6.5 LTS Service Pack 1 的最新發行資訊。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: d6b324ed961dc59a22e8e33109a5ba5262553aa7
workflow-type: tm+mt
source-wordcount: '7221'
ht-degree: 71%

---

# Adobe Experience Manager 6.5 LTS SP1 的最新發行說明 {#release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | Service Pack 1 (SP1) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack 發行 |
| 日期 | 2025 年 8 月 28 日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.1.jar) |

<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## [!DNL Adobe Experience Manager] 6.5 LTS SP1 包含哪些內容？ {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS SP1 包含新功能、客戶要求的重要增強功能和錯誤修正。其中也包括自 2025 年 3 月首次推出 6.5 LTS 版本以來針對效能、穩定性與安全性所發佈的增強功能。[在 6.5 LTS 上安裝此 Service Pack](#install-update)。

<!-- ## Key features and enhancements -->

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## 6.5 LTS Service Pack 1 的已修正問題 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### 無障礙輔助 {#sites-accessibility-65-lts-sp1}

* 已修正一個問題，原本內容片段中文字編輯器元素預設會被截斷。文字編輯器現在顯示未被截斷的完整內容。(SITES-33005)
* 已修正一個問題，原本點選 URL 路徑時，會開啟 Indigo 首頁而非正確目標 URL。(SITES-33004)
* 已修正一個自訂 AEM 元件的無障礙輔助問題，原本在自動測試期間會發生不符 ADA 規定的狀況。(SITES-30660)
* 已修正警報對話框與工作流程訊息中的 ADA 合規性問題，確保文字在淺色背景上顯示為黑色，且符合 WCAG 2.0 對比度要求。(SITES-30138)
* 已修正一個無障礙輔助問題，原本 AEM Sites 編輯器的「類別」按鈕缺乏明確的標籤，導致 JAWS 將其播報為「影像按鈕選單」，而未提供描述性標籤。(SITES-27497)
* 已修正一個無障礙輔助問題，原本「有效權限」畫面中核取記號圖示缺少替代文字，導致 JAWS 無法讀出和傳達其含義。(SITES-27272)
* 已修正一個無障礙輔助問題，原本「權限」頁面並未針對移除使用者或群組權限提供清楚的 JAWS 播報內容，造成螢幕閱讀器使用者的困擾。(SITES-27238)
* 已修正一個無障礙輔助問題，原本錯誤訊息僅顯示圖示而沒有描述性文字，導致在發生錯誤時 JAWS 無法播報該錯誤。(SITES-27155)
* 已修正一個無障礙輔助問題，原本 JAWS 在 AEM 內部部署環境中讀出錯誤且模糊不清的按鈕說明，包括遺漏模組區段第二級標題的文字。(SITES-27152)
* 已修正一個無障礙輔助問題，原本在 AEM Assets 標籤中篩選數值之後，JAWS 並未播報結果的數量。(SITES-27150)
* 已修正一個無障礙輔助問題，原本在建立資料夾時並未顯示確認訊息，而且 JAWS 在 Assets UI 中並未播報此操作。(SITES-27141)
* 已修正 AEM Sites 中一個無障礙輔助問題。JAWS 並未播報表單錯誤，焦點移至非互動式錯誤元素，且必填欄位的錯誤未能在游標移出時顯示。(SITES-27138)
* 已修正一個無障礙輔助問題，原本時間軸按鈕選單缺少明確的標籤，導致 JAWS 僅讀出「活動按鈕選單」而未能提供清楚的描述。(SITES-27134)
* 已修正一個無障礙輔助問題，原本 JAWS 並未播報容器項目的動作或角色，僅讀出「階層連結第 1 版」和「按鈕第 2 版」，而非描述性標籤。(SITES-27131)
* 已修正一個無障礙輔助問題，原本快速發佈快顯視窗並未提供正確的成功訊息，導致螢幕閱讀器無法播報執行完成的回饋。(SITES-26912)
* 已修正 coral-column 視圖中一個無障礙輔助問題，原本具有 ARIA 角色的元素並未包含所需的子系角色，導致不符合無障礙標準。(SITES-26898)
* 已修正一個無障礙輔助問題，原本在 Reflow 模式中看不到建立頁面頂端導覽中的「範本」和「屬性」文字，導致鍵盤和螢幕閱讀器使用者無法存取。(SITES-26895)
* 已修正一個無障礙輔助問題，原本頂端導覽中「搜尋」、「解決方案」、「說明」、「收件匣」和「使用者」圖示的工具提示無法使用鍵盤導覽存取。(SITES-26889)
* 已修正一個無障礙輔助問題，原本「基本」標籤表單欄位並未提供錯誤建議，導致使用者在必填欄位空白未填時無法收到指引。(SITES-26885)
* 已修正一個無障礙輔助問題，原本 NVDA 和 Narrator 螢幕閱讀器並未在「建立」頁面中播報範本檔案的詳細資訊，導致使用者無法以程式化方式接收完整資訊。(SITES-26884)
* 已修正一個無障礙輔助問題，原本「基本」標籤中的「頁面標題文字方塊」使用錯誤的名稱，導致螢幕閱讀器無法為使用者提供準確的資訊。(SITES-26879)
* 已更新按鈕的前景顏色與背景顏色，以符合 WCAG 2.2 AA 的最低對比率要求，讓所有使用者享有更好的可讀性與無障礙體驗。(SITES-26877)
* 已解決在調整視窗大小之後，建立頁面頂端導覽中的「範本」與「屬性」文字會消失的問題，確保低視能使用者能清楚看見並順利操作。(SITES-26872)
* 已修正首頁在套用 Reflow 之後出現多個水平捲軸的問題，確保只顯示單一捲軸，提供正確的無障礙輔助與內容可見度。(SITES-26800)
* 已修正 AEM 頁面編輯器中一個無障礙輔助問題，原本使用者在啟用「人物誌」、「購物車」或「捨棄」等按鈕後，鍵盤焦點會突然重設並回到「人口統計工具列」的開始位置。現在焦點會停留在已啟用的按鈕上，以支援一致的鍵盤導覽與螢幕閱讀器工作流程。(SITES-25306)
* 已修正頁面標題和標籤欄位的無障礙標籤關聯問題。現在，在使用 JAWS 等螢幕閱讀器時，AEM 介面已經正確地將無障礙標籤與「標題」及「頁面標題」欄位相關聯。修正問題後，可確保正確讀取標籤，並改善頁面建立、屬性與移動工作流程方面的 ADA 合規性。(SITES-27149)
* 已修正時間軸中註解輸入欄位缺少視覺標籤的問題。已更正時間軸區段下方「註解」輸入欄位缺少視覺標籤的問題，以利改善無障礙輔助。此更新確保螢幕閱讀器可以準確地播報欄位標籤。此體驗增強所有使用者 (特別是依賴輔助技術的使用者) 的表單導覽和提交功能。(SITES-26903)
* 已修正時間軸註解中省略號按鈕的鍵盤無障礙輔助問題。可使用鍵盤導覽至時間軸區段下方註解旁邊的省略號 (三個點) 按鈕。使用者現在可以使用 Tab 鍵存取該按鈕及進行互動，針對只能使用鍵盤導覽之使用者改善無障礙輔助。(SITES-26891)
* 已改善 NVDA/Narrator 對於選取對話框中搜尋結果的播報。已更新「開啟選取」對話框，以便在使用 NVDA 或 Narrator 等螢幕閱讀器時播報是否找到搜尋結果。此改善功能可協助依賴輔助技術的使用者無需透過視覺確認，即可了解其搜尋動作的結果。(SITES-26883)
* 已修正註解輸入欄位旁省略號圖示的 ARIA 角色。已更新註解輸入欄位旁的省略號 (三個點) 圖示，以使用正確的 ARIA 角色，確保螢幕閱讀器可以準確地識別元素。此項改善功能增進無障礙合規性，並讓依賴輔助技術的使用者享有更好的使用體驗。(SITES-26881)
* 已修正 Coral UI 元件中無效的 ARIA 屬性。已更新 Coral UI 元件以確保所有 ARIA 屬性都使用有效的值，提高無障礙合規性。特別針對錯誤指派 `aria-modal="dialog"` 一類無效值的情況進行處理。此增強功能使螢幕閱讀器能正確地解讀對話框元素，讓依賴輔助技術的使用者享有更好的無障礙體驗。(SITES-26873)
* 已改善 Reflow 情境中圖示的可見度與工具提示。已增強 Reflow 行為，確保「**下載**」、「**重新處理資產**」和「**結帳**」圖示的工具提示皆正確顯示。針對一項無障礙輔助問題進行修正，原本在調整檢視區大小或變更瀏覽器縮放設定時，圖示及其標籤會變成不可見。此修正在 Reflow 期間中維持圖示可見度並提供正確的圖示描述，支援低視能使用者的需求。(SITES-26871)


#### 管理員使用者介面{#sites-adminui-65-lts-sp1}

* 已修正一個無障礙輔助問題，原本 JAWS 在「建立網站」對話框中並未播報清單角色或提供導覽和啟動指示。(SITES-30661)
* 支援螢幕閱讀器讀取 Sites 篩選器視圖中狀態訊息的功能如常運作，確保使用者在切換各個視圖時可以收到清楚且即時的回饋。(SITES-24992)
* 篩選器邊欄的日期挑選器在其容器中完整顯示，提供足夠的觸控目標大小，並消除內容剪裁問題。(SITES-24988)
* 選取的篩選器標記現在採用符合視覺呈現的語義化 HTML 及 aria 標籤，確保輔助技術能準確地支援角色並執行明確的動作。(SITES-24980)
* 在參考資料邊欄區域新增 ARIA 標籤屬性，為螢幕閱讀器使用者提供唯一的描述性標籤，並確保頁面維持一致的地標識別。(SITES-24973)
* 已更新參考資料邊欄，現在使用相對單位來設定大小和位置，使內容在 1280x1024 的檢視區放大至 400% 時，仍然可以正確縮放且所有功能正常運作。(SITES-24972)
* 已確認 Sites 首頁清單視圖的表格元素包含正確的欄標頭角色，讓螢幕閱讀器能夠播報每個資料儲存格的標頭。(SITES-24942)
* 現在 NVDA 會在樹狀目錄中播報修改日期，確保螢幕閱讀器使用者收到完整的資產詳細資訊。(SITES-24782)
* 已修正一個問題，原本 NVDA 螢幕閱讀器在 AEM Sites 的樹狀目錄元件中所播報的項目相關文字並不完整。NVDA 現在可以讀出每個項目的完整文字，改善無障礙輔助與合規性。(SITES-24780)
* 在樹狀目錄中已新增視窗分割器的鍵盤無障礙輔助，讓使用者只使用鍵盤也可以調整左側欄位的大小。(SITES-24779)
* 已更新「說明」選單搜尋結果，現在包含清單項目的正確 ARIA 角色，確保螢幕閱讀器正確播報連結以改善無障礙輔助。(SITES-24729)
* 已修正一個問題，原本螢幕閱讀器在 Sites 篩選器面板套用篩選器後，並未播報「Y 個結果中有 X 個」的狀態訊息或是「未找到結果」的訊息。修正後可確保使用者收到正確的結果確認。(SITES-24720)
* 已更正應用程式導覽中導覽連結遺漏角色指派的問題。已新增適當的 ARIA 角色以確保螢幕閱讀器正確識別和播報導覽元素。(SITES-24719)
* 已將所選取的篩選器標籤中錯誤的網格角色標記替換為按鈕元素，並新增無障礙名稱，確保螢幕閱讀器能正確播報並辨識這些標籤。(SITES-24717)
* 針對執行多項選取時顯示的參考資料邊欄狀態訊息，已經新增螢幕閱讀器播報，確保使用者收到變更的確認。(SITES-24678)
* 已更正搜尋欄位的行為，使其不會自動播報第一個結果。螢幕閱讀器現在會播報所找到的結果數量，讓使用者可以導覽清單而不會聽到錯誤的焦點播報。(SITES-24658)
* 已將清單視圖的非互動式靜態元素中不正確的 `aria-label` 屬性移除，以避免螢幕閱讀器播報誤導性或不相關的資訊。(SITES-24515)
* 已更新清單視圖第一欄的核取方塊，以便使用標題欄文字做為無障礙名稱，確保螢幕閱讀器準確傳達表單欄位的用途。(SITES-24514)
* 已新增適當的 ARIA 屬性和即時區域支援，以便在導覽內容時向螢幕閱讀器使用者播報載入狀態訊息。(SITES-24481)
* 已更新回應式設計，當內容在寬度為 1280×1024 的檢視區放大至 400% 時，免除水平捲動，確保無需側向捲動即可看見完整的內容。(SITES-24308)
* 已更正 Sites 管理 UI 的焦點導覽，使其遵循邏輯順序，在按下 Esc 鍵後，焦點將返回至「全部選取」按鈕，而在按下 Tab 鍵後，焦點則移至下一個互動式元素。(SITES-24307)
* 已更新 Sites 管理 UI 中的焦點順序，以便 `<betty-titlebar-title>` 元素中的階層連結按鈕在鍵盤導覽期間按照正確的順序接收焦點。(SITES-24305)
* 已驗證跳過連結功能，確保其將鍵盤焦點正確移至主要內容區域，讓鍵盤使用者能略過頁首元素，並有效率地存取內容。(SITES-24061)


#### Classic 使用者介面{#sites-classicui-65-lts-sp1}

已修正 Classic UI 的問題，原本遺漏核取方塊標籤，而且 HTML 在多個 UI 元素 (包括日期搜尋與非標準介面) 中顯示為編碼文字。(SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

AEM 現在會避免因影像資產中格式錯誤的 XMP 後設資料而造成效能降低。包含無效或不合規之 XMP 屬性名稱的資產 (例如含有數值區段或不合格之結構者)，在處理過程中不再重複觸發警告記錄。系統篩選有問題的後設資料，以確保資產攝取和驗證順利完成且無錯誤。(SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments] - 片段編輯器{#sites-fragments-editor-65-lts-sp1}

即使有作者將其他作者簽出，其他作者仍可發佈內容片段，這與簽出功能的預期行為相反。此修正可避免其他使用者在簽出內容片段後仍可看到或使用製作介面中的發佈按鈕。(SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### 元件控制台{#sites-component-console-65-lts-sp1}

已修正產品清單元件的一個問題，原本「全部選取」核取方塊僅加入初始頁面上的前 20 個 SKU，而非搜尋結果中的所有 SKU。(SITES-29191)

#### 核心後端{#sites-core-backend-65-lts-sp1}

在 `ValidationDataServlet` 中處理影像資產時，因 XMP 後設資料格式不正確而導致錯誤發生。此修正確保使用合規方式處理後設資料，並避免對無效屬性進行多餘的剖析。(SITE-30683)

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM - Live Copies{#sites-msm-live-copies-65-lts-sp1}

* 已修正在 AEM 6.5 內部部署中重新啟用 Ghost 元件繼承時發生的 JavaScript 錯誤 `ns.ui.alert is not a function`。(SITES-31993)
* 已修正一個問題，原本 AEM 6.5 中的「稍後轉出」選項在未選取日期的情況下卻允許繼續操作。(SITES-31374)

#### 頁面編輯器{#sites-pageeditor-65-lts-sp1}

* 已解決 Teaser 模態視窗的一個問題，原本在「連結與動作」標籤中，在輸入有效資料並排除錯誤後，仍持續顯示錯誤樣式、圖示以及 aria-invalid 屬性。(SITES-25527)
* 已修正 Teaser 模態視窗文字編輯器的一個問題，原本「清單」和「段落」按鈕並未將其展開或收合狀態傳達給螢幕閱讀器，修正後可確保準確地更新 aria-expanded 屬性。(SITES-25365)
* 已修正人口統計工具列中的一個問題，原本在使用鍵盤輸入調整購物車滑桿會時，焦點會移動到購物車按鈕而不是停留在滑桿上，修正後可改善鍵盤使用者的導覽效率。(SITES-25324)
* 已在人口統計工具列中對購物車滑桿相關聯的 `<label>` 元素指定值，為其新增無障礙名稱。此修正提高與輔助技術的相容性，並改善螢幕閱讀器使用者的易用性。(SITES-25322)
* 已在人口統計工具列下拉式選單內的按鈕新增 ARIA 角色和無障礙名稱。此修正有助於正確識別輔助技術，並改善鍵盤和螢幕閱讀器使用者的導覽效能。(SITES-25315)
* 已調整人口統計工具列版面，避免內容在瀏覽器放大至 200% 時溢出檢視區，確保無需水平捲動仍可存取所有控制項。(SITES-25309)
* 已更正人口統計工具列中的焦點管理，將鍵盤焦點維持在作用中的按鈕上，而不是將焦點重設至工具列的開始位置。(SITES-25306)
* 按鈕標籤的重疊行為依原本設計運作，在使用類似螢幕寬度的多個模式在作用中時，會使用工具提示顯示標籤。(SITES-25285)
* 附註模態視窗包含一個可見的提交按鈕，讓使用者無需依賴 Escape 鍵，或在模態視窗之外點選，即可提交附註。(SITES-25281)
* 附註模態視窗包含一個鋼筆圖示按鈕，使用者可使用此按鈕提交附註，提供明確且無障礙的提交方法。(SITES-25269)
* 已更正「附註」和「關閉附註」按鈕的螢幕閱讀器播報，以提供準確且相關的回饋，並移除不相關或令人困惑的資訊。(SITES-25268)
* AEM 編輯器頁面的版面區段現在支援完整的鍵盤無障礙輔助。使用者只使用鍵盤即可啟動區段標題和編輯按鈕，無需依賴滑鼠停留。此更新確保符合 WCAG 2.1.1 標準，並提升多個元件 (如 Teaser、影像、輪播、版面、時間扭曲及附註模態視窗) 之間的易用性。(SITES-25256)
* 已移除寬度為 320px 的輪播模態視窗中不必要的水平捲動，以確保所有內容都顯示在檢視區內，而無需左右導覽。(SITES-25254)
* 已移除寬度為 320px 的影像模態視窗中不必要的水平捲動，以確保所有內容都顯示在檢視區內，而無需左右導覽。(SITES-25244)
* 已移除寬度為 320px 的 Teaser 模態視窗中不必要的水平捲動，以確保所有內容都顯示在檢視區內，而無需左右導覽。(SITES-25242)
* 已在 Teaser 模態視窗中為 `List` 和 `Paragraph Format` 快顯視窗選單啟用鍵盤導覽。此修正讓使用者可以使用方向鍵存取和導覽這些選單。(SITES-25235)
* 已更正「附註」和「關閉附註」按鈕的螢幕閱讀器播報，提供與相關聯動作相符的準確且相關的回饋。(SITES-25234)
* 已改善 Teaser 模態視窗中的「說明」按鈕標籤，清楚地說明其用途，並為所有使用者 (包括輔助技術使用者) 提供有意義的背景資訊。(SITES-25224)
* 將尺規量測方式與螢幕閱讀器使用者的裝置相關聯，改善尺規模擬器的功能。另外，將工具提示替換為 aria-describedby 元素。(SITES-24955)
* 並未實施修正，因為「編輯」按鈕按預期運作，並提供背景資訊而非執行動作。(SITES-24950)
* 已確認編輯器頁面上的焦點順序符合邏輯順序，使用者可瀏覽所有互動式元素，而不會無預期地跳過或回到原點。(SITES-24937)
* 已確認預覽模式版面在使用者套用自訂文字間距設定時，可以正確地更新文字間距，確保所有內容區域保持一致的格式。(SITES-24936)
* 已確認「預覽」按鈕在成為焦點時不再觸發環境或狀態變更，確保使用者在頁面檢視更新前需刻意啟動該按鈕。(SITES-24784)
* 已為應用程式導覽連結新增正確的 ARIA 角色指派，讓螢幕閱讀器能準確辨識並播報導覽項目，以改善無障礙輔助。(SITES-24718)
* 已更新「變更篩選器」按鈕，以便向螢幕閱讀器播報展開和收合狀態、已移除多餘的 ARIA 屬性，並調整標籤以提供清晰且不重複的說明。(SITES-24713)
* 已在「連結選取」對話框中新增螢幕閱讀器播報搜尋結果狀態訊息的功能，確保使用者在結果載入或未找到符合項目時，可以得到確認。(SITES-24700)
* 已為影像模態視窗的載入狀態新增螢幕閱讀器播報，確保當模態視窗正在載入以及準備好進行互動時，使用者可以獲得回饋。(SITES-24697)
* 已解決一個無障礙輔助問題，原本在頁面放大至 200% 和 400% 時，固定頁首會遮蔽 Teaser 模態視窗內容，修正後可確保在使用頁面放大功能時，內容完全可見且可使用。(SITES-24523)
* 已在搜尋/篩選器欄位中新增包含搜尋結果數量的狀態訊息，讓螢幕閱讀器能夠向使用者播報結果。(SITES-24506)
* 已在搜尋/篩選器欄位中新增包含搜尋結果數量的狀態訊息，確保使用者在結果載入時收到立即的回饋。(SITES-24505)
* 已在側邊欄面板的標籤清單中新增無障礙名稱，讓螢幕閱讀器可以在遵守 WAI-ARIA 準則的情況下播報其用途。(SITES-24492)
* 已為模糊不清的編輯器圖示新增描述性標籤，確保所有使用者都能清楚了解每個按鈕的功能。(SITES-24480)
* 已為「版面」視圖中的區段標題與動作按鈕啟用完整的鍵盤無障礙輔助，確保滑鼠與鍵盤使用者維持一致的操作方式。(SITES-24479)

<!--
#### Replication{#sites-replication-65-lts-sp1}

#### Rich Text Editor{#sites-rte-65-lts-sp1} -->

#### 通用編輯器 {#sites-universal-editor-65-lts-sp1}

* 已修正 QueryTokenService 中的競爭條件問題，原本在登入權杖服務尚未回傳結果之前，同時觸發多個帶有查詢參數的要求時，會導致登入失敗。(SITES-30659)
* 已修正 UniversalEditorURLService 中一個問題，原本在 Felix ConfigMgr 儲存一組對應路徑陣列時，只保留第一個項目。(SITES-30292)

### [!DNL Assets]{#assets-65-lts-sp1}

已修正一個問題，原本從遠端 DAM 同步資產至 Sites 本機 AEM 時，會移除資產中的已發佈狀態及複寫相關屬性。(Assets-48958)

<!--
#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp1}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp1}



### [!DNL Forms]{#forms-65-lts-sp1}


#### Forms Designer 

#### Forms

#### Forms JEE 
 
#### Forms Captcha {#forms-captcha-65-lts-sp1} 

#### XMLFM {#forms-xmlfm-65-lts-sp1}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp1}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp1} -->



### 基礎 {#foundation-65-lts-sp1}

<!--
#### Apache Felix {#foundation-apachefelix-65-lts-sp1}

#### Campaign{#foundation-campaign-65-lts-sp1}

#### Cloud Services{#foundation-cloudservices-65-lts-sp1}



#### Communities {#foundation-communities-65-lts-sp1}

#### Content distribution{#foundation-content-distribution-65-lts-sp1}

#### CRX {#foundation-crx-65-lts-sp1}

#### Granite{#foundation-granite-65-lts-sp1} -->

#### HTL{#foundatoin-htl-5-lts-sp1}

已解決導致 HTL Script Engine Factory 無法運作的 OSGi 相依性循環問題，確保正確進行服務解析和執行指令碼。(Granite-58275)

#### 整合{#foundation-integrations-65-lts-sp1}

* 在 `com.adobe.cq.cq-analytics-integration` 套件中已不再使用 commons-httpclient 3.x，並取代為 `org.apache.httpcomponents.httpclient` 4.5.13.B0001，以符合最新 AEM 6.5 LTS 標準。(CQ-4360586)
* 已從 AEM 移除已棄用的 Search&amp;Promote 整合套件，以清除未使用的元件並降低維護開銷。(CQ-4358030)
* 已為 SiteCatalyst 整合加入新的後端測試案例，以便改善分析驗證並確保更全面的涵蓋範圍。(CQ-4359991)
* 已修正 Launch Config 的「屬性」區段的問題，原本「公司」與「屬性」下拉式選單並未顯示。此外，即使已填寫所有必填欄位，「儲存並關閉」仍會觸發錯誤，而且在只有「標題」欄位為空時，「公司」與「屬性」會顯示不正確的錯誤訊息。(CQ-4359853)
* 從 6.6 版本中移除 `searchpromote` 的 servlet 路徑項目，以配合 Search&amp;Promote 套件移除。(CQ-4359523)
* 已修正 Target 存放庫的 HTTP 測試案例，以確保驗證準確性並改善測試可靠性。(CQ-4359022)
* 在 integration-adobeims-console 模組中不再使用 Guava 快取，以消除 Guava 程式庫相依性。(CQ-4358710)
* 已驗證 AEM 6.6 的 DTM 整合工作流程、收件匣任務和專案功能，以確保在 AEM 6.5 中正常運作。(CQ-4358151)
* 已驗證 AEM 6.6 的內容洞察功能，以確保在 AEM 6.5 中能夠相容並正常運作。(CQ-4357774)
* 已驗證 AEM 6.6 的雲端服務功能，以確保在 AEM 6.5 中能夠相容並正常運作。(CQ-4357773)
* 已驗證 AEM 6.6 的 Adobe IMS 控制台整合，以確保在 AEM 6.5 中能夠相容並正常運作。(CQ-4357772)
* 已更新 Test&amp;Target 整合的 Jenkins 管道，改為使用 Java 17 執行，解決 Selenium 測試失敗的問題，並將選取測試移轉至 Playwright，同時確保所有單元測試皆能通過。(CQ-4357770)
* 已透過更新版本編號與測試管道，讓 DX 整合、工作流程、收件匣，以及具有 6.6.0 分支的專案保持一致。此外，亦解決升級相容性問題，並驗證所有受影響的服務，以確保其穩定性與功能正常運作。(CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### 本地化{#foundation-localization-65-lts-sp1}

* 從「權限」清單將「移除存取控制」對話框的字串本地化，以顯示正確的翻譯。(GRANITE-59427)
* 已修正模型編輯器的「OR 拆分屬性」新增規則對話框的問題，原本多個 UI 字串 (包括運算子與欄位標籤) 皆未本地化。現在所有的字串都顯示正確的本地化內容。(CQ-4354014)
* 已新增「工作流程模型編輯」對話框中所遺漏的「顯示說明」工具提示翻譯。(CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

已解決一個問題，原本 AEM 在升級過程中重新建立或重新命名 `/apps/system/config` 之下的現有設定檔案，並將 `.cfg.json` 檔案取代為 `.config` 檔案。(GRANITE-58899)

#### 全方位搜尋{#foundation-omnisearch-65-lts-sp1}

已修正一個無障礙輔助問題，原本輸入欄位之預留位置錯誤地顯示為標籤。此問題導致搜尋、AEM 體驗片段、內容片段和內容片段模型缺少欄位標籤。(Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### 專案{#foundation-projects-65-lts-sp1}

* 已解決一個問題，原本在行事曆檢視中刪除專案時，即使已成功刪除專案，仍會顯示不正確的錯誤快顯視窗。(CQ-4358890)
* 已修正 Firefox 中一個問題，原本「專案」視圖中的「資產集合」卡片頁尾與卡片邊框重疊。頁尾現在正確對齊，沒有重疊。(CQ-4353317)

#### 快速入門{#foundation-quickstart-65-lts-sp1}

* 已更新解除安裝指令碼以調整 Guava 套件的版本範圍，避免在透過封裝管理員安裝時被加入封鎖清單。(GRANITE-59559)
* 已修正複寫 UI 中一個問題，原本在編輯複寫代理程式時會顯示錯誤 (`#1660`)，修正介面中傳統核取方塊的處理方式後已解決此問題。(GRANITE-58302)
* 透過補齊缺漏的服務權限、更新設定處理方式，並確保必要的服務可以正確初始化，已解決在 AEM 6.5 LTS 搭配 JDK 21 執行時，S3 資料存放庫出現的多項啟動錯誤。(GRANITE-57082)
* 已定義 AEM 6.5 的維護和持續營運策略。此修正包括以下內容：
   * Service Pack 發布週期。
   * Hotfix 發布週期。
   * 與 AEM 6.6 並行支援。
   * 已更新支援矩陣。
   * 附加元件所有權責任。(GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* 已將 Sling ResourceAccessSecurity 更新至版本 1.1.2，以解決初始化多個`ClassCastException`參考資料時發生的`ResourceAccessGate`問題`ResourceAccessSecurityImpl`。(NPR-42750)
* 已修正 Adobe Stock 整合中原本授權對話框顯示為灰色的問題。此問題是由於 `sunt:initList` 函數移除必要的輸入欄位所導致。該函數位在 Coral Foundation 用戶端程式庫中。已更新用戶端程式庫以保留必要的欄位，以便授權對話框的功能正常運作。(NPR-42748)
* 已回溯修正在安裝封裝期間導致出現 `DataTimeParseException` 和 `String.length()` null 指標異常的 Sling 指令碼問題。已將 Sling 指令碼更新至版本 2.8.3-1.0.10.6，以減少安裝錯誤並提高穩定性。(NPR-42640)

<!--
#### Translation{#foundation-translation-65-lts-sp1} -->

#### 使用者介面{#foundation-ui-65-lts-sp1}

* 已解決 AEM Author UI 中使用者群組顯示限制為 41 個的問題。此問題是由於 Granite UI 群組選擇器元件的預設批次限制所導致。已更新該元件以顯示所有群組，沒有任何截斷情形。(NPR-42749)
* 已解決內部部署頁面建立精靈的問題，原本在編輯頁面屬性時，多欄位元件的必填欄位未重新驗證。此問題因此導致作者略過驗證流程，並使用不完整的資料繼續操作。(GRANITE-58826)
* 已更正 AEM 中說明按鈕的 ARIA 屬性，以確保 JAWS 螢幕閱讀器播報清晰且使用者易理解的標籤，而非顯示未翻譯的圖示和文字後設資料。(GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* 已為 AEM 翻譯新增 Java 17 支援，藉由更新翻譯套件、驗證 Java 封裝相容性、移除已棄用的相依性，以及經由全面測試確保功能完整性來完成。(CQ-4357525)
* 已移除不穩定的 Evergreen 測試 `com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater` 以避免自動化測試過程中出現失敗誤報。(CQ-4298376)

#### 工作流程{#foundation-workflow-65-lts-sp1}

* 已新增收件匣項目中遺漏的 `data-detailsurl` 屬性，以避免在搭配 Java 21 使用 AEM 6.5 LTS 時，URL 出現未定義的值。(GRANITE-60158)
* 已修正 AEM 6.5 LTS 搭配 Java 21 執行時，`WorkflowToPublishEventService` 套件的 `deactivate` 方法中出現的 NullPointerException，確保工作流程服務正確關閉且無錯誤。(GRANITE-58151)
* 已更新工作流程索引，以支援共用功能、休假狀態自訂，以及修正時間軸查詢相關問題。(GRANITE-52640)
* 已更新工作流程索引，以支援共用功能、休假狀態自訂，以及修正時間軸查詢相關問題。(GRANITE-52294)
* 已解決程式升級到 AEM 版本 10912 時，記錄比較驗證期間錯誤記錄失敗增加的問題，確保工作流程穩定執行。(GRANITE-44268)
* 已更新工作流程存放庫中的 URL 清理方法，將 `url.searchParams` 取代為 `url.search`，為易受攻擊的 URL 提供更好的 XSS 保護。(CQ-4359585)
* 已驗證 AEM 6.6 Forms 中的工作流程、收件匣和專案功能，以確保正確操作和整合。(CQ-4358777)
* 透過 Jenkins 發布工作流程內容成品的作業已實施自動化，讓 AEM 6.5 實現精簡且一致的部署流程。(CQ-4358472)
* 已修正收件匣建立任務工作流程的一個問題，儘管已建立任務，但是「新增任務」對話框在按一下「提交」後並未關閉，而這是 JavaScript 語法錯誤所造成的情況。(CQ-4355336)
* 已修正由於 `isEndUserConfigurationEnabled` 缺少屬性定義導致無法儲存收件匣視圖設定的問題。(CQ-4287757)

## Forms

### Forms Designer

* 當使用者使用exportDataAPI匯出以XFA為基礎的PDF的資料時，產生的XML與使用Acrobat Reader手動匯出的XML資料相比，會顯示差異。 與Acrobat Reader產生的輸出相比，輸出中缺少某些欄位的值。 (LC-3922791)
* 在Workbench中使用「輸出服務」產生已標籤PDF時，會在目錄專案的參考標籤下新增非預期的標籤標籤。 (LC-3922756)
* 使用輸出服務將動態的、可填寫的PDF平面化為PDF/A格式時，不會保留動態狀態。 這會導致資料遺失和潛在的合規性問題，尤其是在啟用標籤的情況下。 (LC-3922708)
* 當使用者在AEM Forms Designer中以底部或右側對齊方式放置欄位註解時，標籤樹僅包含註解而沒有對應的值，導致不完整的協助工具標籤。 (LC-3922619)
* 產生的PDF中的QR碼變得無法讀取。 QR碼的替代文字也未能通過協助工具測試，影響熒幕助讀程式的相容性。 (LC-3922551)
* 當使用者在代理程式UI中轉譯信函時，由於FormService render() API，內容無法正確顯示。 (LC-3922461)
* 當使用者嘗試從XDP中以AEM Forms中的下沈方形樣式建立PDF/A檔案時，會導致邊框轉譯問題。 (LC-3922180)
* 繫結至XSD結構描述的動態表單平面化會導致部分資料遺失，因為某些繫結的表單資料不會保留在最終PDF中。 (LC-3922008)
* 當使用者嘗試使用AEM Forms 6.5.13及更高版本中的extractData API從互動式PDF匯出資料時，相較於手動匯出，這會造成資料遺失。 (LC-3921983)
* 使用者面臨協助工具法規遵循問題，其中使用AEM Forms Designer或輸出服務將XDP表單轉換為靜態PDF時，會建立多個連結OBJR標籤，而不是建立單一統一的連結標籤。 (LC-3921977)

### 自適應表單

* 在AEM Forms中，在根面板上啟用「允許標題為RTF文字」會導致巢狀面板上的「從記錄檔案排除標題」無法正確地隱藏根面板的標題。 這會在產生的記錄檔案中進行。 (FORMS-19696)
* 系統會忽略透過JSON結構描述中的aem:resourceType指派的自訂sling:afProperties。 呈現期間會忽略自訂資源型別。 (FORMS-19691)
* 當使用者提交具有使用URI預填附件的調適型表單時，由於缺少二進位資料，表單提交會失敗並出現NullPointerException。 (FORMS-19371) (FORMS-19486)
* 當使用者上傳「Forms和檔案」區段下的PDF時，時間軸功能停止運作。 (FORMS-19407)(FORMS-19234)
* 當使用者使用AEM Forms中的現成(OOTB)檔案附件元件上傳檔案時，會識別安全漏洞。 此問題可能會導致未經授權的實體攔截提交流程。 (FORMS-19271)
* 當使用者在AEM Forms中設定現成的最適化表單以自動產生記錄檔案(DoR)時，Acrobat Reader檔案屬性中的「標題」欄位不顯示擷取的DoR標題。 依預設，表單標題不會出現在檔案名稱的位置。 (FORMS-19263)
* 當使用者在代理程式UI中開啟互動式通訊時，預先填入的資料無法完全清除；移除後，它會自動以相同的資料重新填入。 (FORMS-19151)
* 當使用者在代理UI中預覽日期欄位時，日期意外變化。 此問題發生的原因是VM的UTC設定與系統對日期的詮釋之間存在時區差異。 (FORMS-19115)
* 使用者提交表單時，檔案附件可能會重複，導致同一檔案多次上傳。 (FORMS-19045)(FORMS-19051)
* 在Document Security中將協調員新增到原則集會在生產環境和較低環境中失敗。 (FORMS-18603、FORMS-18212、FORMS-19697)
* 當使用者在案頭模式下使用空白欄位按一下「datepicker-calendar-icon」時，由於未定義的_$focusedDate變數會發生錯誤，並中斷關聯的自訂指令碼。 (FORMS-18483)(FORMS-18268)
* 當客戶預覽信函時，「字數金額」欄位無法正確顯示或更新數字值，導致對齊錯誤和內容中缺少空格。 (FORMS-18437、FORMS-17330、FORMS-18209、FORMS-18557、CTG-4150848、FORMS-19614、LC-3922004)
* 當客戶預覽在RHEL上儲存的字母時，內容未妥善對齊、缺少空格，且出現未預期的字元，例如「x」。 (FORMS-18422)(FORMS-17641)
* 當使用者在AEM Forms中的標籤之間導覽時，在第一個標籤上選取元件會變得無回應。 (FORMS-18345)
* 當使用者使用WebToPDF選項將HTML檔案轉換為PDF時，輸出PDF缺少標題區段，包括中繼資料和標題標籤。 (FORMS-18223、FORMS-17835、FORMS-19642、FORMS-18224)
* 在AEM JEE Process Manager SDK中，當使用者叫用retryAction(long actionOid)方法時，系統會錯誤地重試tb_action_instance表格中的第一個動作。 即使提供特定動作ID或ID為空值，也會發生此工作流程，導致非預期的行為。 (FORMS-18187)
* 使用者遇到問題，即儲存的草稿和提交功能失敗，未顯示任何錯誤訊息。 (FORMS-18069)
* 從XSD式基礎元件轉換至核心元件，可防止在JSON結構描述中實作跨檔案參照，影響最適化Forms移轉。 (FORMS-18065)
* 當使用者在代理UI中預覽信函時，由於IC時間轉換問題，日期欄位顯示不正確的值。 這些差異是由於VM環境與系統對時間的詮釋（UTC與當地時間）之間的時區差異所造成。 (FORMS-17988) (FORMS-17248)
* 當使用者在AEM Forms中使用通知IC範本預覽信函時，PDF的產生時間差異顯著，從1.5秒到超過10秒，即使在同一部伺服器上也是如此。 這種不一致會影響關鍵業務工作流程。 (FORMS-17951)
* 當使用者使用「資料來源」選項將調適型表單中的手寫簽名物件繫結到XDP時，無法儲存變更。 原因是持續外觀比例驗證錯誤，即使使用有效值亦然。 (FORMS-17587)
* 當使用者使用具有許多用於檔案片段的隱藏欄位的特定XDP時，AEM會建立CRX節點，並將cm:optional屬性設定為false，這會造成互動式通訊(IC)提交失敗。 (FORMS-17538)
* 當客戶預覽信函時，若已定義Lead和Frac的數字限制，數值方塊欄位將無法正確處理負值。 此問題是因為使用parseFloat而發生，這會將減號視為數字的一部分。 (FORMS-17451)
* 預覽信函時，系統注意到Adobe.json檔案中使用「*」萬用字元，因此擔心其用途和可能的修改。 (FORMS-17317)
* 當使用者在套用固定利率儲蓄者聯合帳戶上使用熒幕助讀程式時，標題錯誤地宣佈為可點按，導致協助工具問題。 (FORMS-17038)
* 內嵌表單時，產生的iframe會遺失title屬性，導致協助工具相容問題。 (FORMS-17010)
* 使用Forms Manager UI下載表單一律包含關聯的相依性，例如主題和片段。 (FORMS-15811)
* 當使用者存取行動裝置上的表單(iOS和Android™)時，第一個頁面上的「下一個」和「上一個」按鈕會停用。 不過，熒幕助讀程式不會將其識別為停用。 (FORMS-15773)
* 當使用者儲存已啟用片段和延遲載入的大型表單時，將無法擷取草稿，並中斷工作流程。 (FORMS-19890， FORMS-19808)
* 根據核心元件為最適化表單儲存表單屬性的使用者遇到問題。 發生此狀況是因為納入以基礎元件編輯器為基礎的最適化表單中的備援指令碼，導致以核心元件為基礎的最適化表單中出現衝突。 編輯者。 (FORMS-17474)
* 使用者遇到Adobe Sign GovCloud簽名頁面未在iframe中呈現的問題。 (FORMS-16803)
* 使用者在選取核心元件Adaptive Forms (AF)片段的參考時會遇到錯誤。 出現錯誤訊息「無法轉譯參考：不是絕對路徑」，導致無法正確轉譯參考。 (FORMS-19678)
* 新增支援Acrobat DC的多執行緒轉換，讓使用者能夠更有效率地同時執行Word、Excel和PowerPoint檔案轉換至PDF檔案。 (FORMS-21310)
* 新增在AEM Service Pack 24中包含`com.adobe.granite.toggle.impl.dev`套件組合，可透過從Forms附加元件中移除該套件組合來簡化開發流程。 (FORMS-20139)
* 已從forms-foundation移除FeatureToggleRenderConditionServlet，並從forms附加元件移除com.adobe.granite.toggle.impl.dev套件組合。 此更新可確保在Forms附加元件安裝後，轉譯條件能正確解析，進而改善客戶的元件功能。 (FORMS-20138)
* 由於最適化Forms中的查詢長時間執行，使用者遇到效能緩慢的問題。 此更新會將查詢變更反向移植，以提高效率。 客戶現在可以使用標籤名稱aemformsAFReferences建立索引。 (FORMS-21411)
* 使用WebtoPDF將HTML轉換為可攜式檔案格式(PDF)時，使用者遇到標題位置未對齊的問題。 此問題會影響檔案版面配置一致性和輸出的可讀性。 (FORMS-21502， FORMS-21540)
* 儘管成功進行PreFlight驗證，使用者仍遇到PDF/A-1b驗證失敗。 此問題會影響使用PDF驗證工具的企業客戶的檔案合規性檢查。 (FORMS-20196)
* 使用者在UI上遇到未翻譯的字串，導致混淆和難以瞭解介面。 (FORMS-6542)
* 使用者遇到電子郵件通知問題。 「傳送電子郵件」工作流程步驟無法傳送電子郵件，影響自動化通訊程式。 (FORMS-17961)
* 使用者在表單工作流程中遇到失敗測試，這影響了他們有效完成工作流程流程的能力。 (FORMS-16231)
* 使用者無法在AEM表單中使用PDF檔案的時間軸功能。 此問題會影響使用者有效追蹤檔案變更和修訂的能力。 在PDF表單區域的「Forms和檔案」區段底下上傳任何AEM時，時間軸檢視會停止運作。 (FORMS-19408)
* 使用者在與OData互動時會遇到Null指標例外狀況。 這會導致資料擷取程式中斷。 (FORMS-20348)
* 移除開放原始碼Java程式庫Guava後，移除了google.common.collect程式庫。 此更新可確保使用Adaptive Forms的企業客戶獲得更好的相容性和效能。 (FORMS-17031)

### Forms驗證碼

* 針對以基礎元件為基礎的最適化Forms新增Hcaptcha和Turnstile支援。 (FORMS-16562)
* 使用者在建立Captcha設定對話方塊中遇到圖示重疊問題。 填寫必填欄位時，資訊圖示與錯誤圖示重疊，導致在設定組態期間產生混淆。 (FORMS-16916)
* 使用者在根據基礎元件的最適化Forms中遇到擷取到reCAPTCHA的設定不正確。 未選取表單的設定容器時，`conf/global`資料夾中的多個設定會造成問題。 (FORMS-19237)
* 使用者遇到reCAPTCHA未轉譯的問題。 這會影響企業客戶的表單提交與安全性驗證。 (FORMS-17136， FORMS-19596)
* 使用者遇到reCAPTCHA Enterprise的大小未反映在使用者介面(UI)中的問題。 (FORMS-16574)
* 使用者因「ReCaptchaConfigurationServiceImpl」中的ResourceResolver未關閉而遇到ReCaptcha功能問題，導致表單提交期間間歇性驗證失敗。 (FORMS-19241)
* 使用者在Sites中製作表單時，遇到reCAPTCHA驗證問題。 AEM表單無法正確辨識表單名稱，導致驗證失敗。 (FORMS-20486)
* 即使企業reCAPTCHA分數為1.0，使用者仍會提交表單，導致潛在安全性風險。 (FORMS-16766){{$include }}
* 將提交錯誤代碼更新為400，改善調適型Forms中的reCAPTCHA警報。 此外，精細化記錄警報以區分逾時、過期和機器人偵測失敗，提高疑難排解精確度和系統可觀察性。 (FORMS-19240)
* 已關閉ReCaptchaConfigurationServiceImpl中未關閉的ResourceResolver執行個體，以防止在AEM Forms中使用reCAPTCHA整合時可能發生的資源洩漏並改善系統穩定性。 (FORMS-19242)
* 當/conf/global資料夾中有多個專案時，請確定每個表單都有正確的設定繫結，以改善AEM Forms的驗證碼設定處理。 避免在未明確選取組態容器時，意外使用不正確的驗證碼設定。 (FORMS-19239)

### 表單管理 UI

* 使用者在「Forms >建立Watchfolder > Watchfolder建立程式」中遇到未當地語系化的字串。 建立watchfolder時，找不到「Watchfolder建立」和「Watchfolder已成功建立」等字串，這會影響使用者介面體驗。 (FORMS-15234)

## [!DNL Experience Manager Foundation] {#experience-manager-foundation}

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

## 安裝與更新 {#install-update}

如需設定需求，請參閱[安裝指示](/help/sites-deploying/custom-standalone-install.md)。

>[!NOTE]
>
> 如果您要從舊的6.5 SP直接升級至LTS SP1，請依照6.5到6.5 LTS GA [升級](/help/sites-deploying/upgrade.md)的指示操作。


如需詳細說明，請參閱[升級文件](/help/sites-deploying/upgrade.md)。

>[!NOTE]
>
> 對於全新的 AEM 6.5 LTS 安裝，必須獨立安裝索引定義。如需更多詳細資訊，請參閱[此文章](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)。

## 安裝並更新AEM Forms附加元件 {#install-update-aem-forms-add-on}

如需詳細指示，請參閱[AEM Forms Service Pack安裝指示](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions)。



## 支援平台 {#supported-platforms}

尋找受支援平台的完整矩陣，包括 [AEM 6.5 LTS 技術要求](/help/sites-deploying/technical-requirements.md)的支援等級。

>[!NOTE]
>
>建議與 AEM 6.5 LTS 搭配使用的版本為 Java™ 17/Java™ 21。


## 已棄用和已移除的功能 {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe 會持續審閱產品功能，藉由更新或取代舊功能，提高客戶價值。進行這些變更時，皆會仔細留意回溯相容性。

若要傳達即將移除或取代 Adobe Experience Manager (AEM) 功能的訊息，請套用下列規則：

1. 首先公告功能已棄用。雖已棄用，功能仍可繼續使用，但往後不會再進行增強。
1. 最早會於下一個主要版本中移除已棄用的功能。移除的實際目標日期依規劃稍後公告。

此程序讓客戶在實際移除功能之前，至少還有一個發行週期的時間可以調整其實施方案，使其適應已棄用功能的新版本或後續功能。

### 已棄用功能 {#deprecated-features}

此區段列出 Adobe 在 AEM 6.5 LTS 中已棄用的特點與功能。通常，在未來版本中移除某些功能之前，Adobe 會先將棄用該功能並提供替代方案。


建議客戶檢查其目前的部署中是否使用這些特點/功能，並規劃變更其實施方案，改用所提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
| --- | --- | --- | --- |
| Sites | [SPA 編輯器](/help/sites-developing/spa-overview.md) | AEM 中用於管理 Headless 內容的首選編輯器為：<br>- [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。<br>- [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。 | 6.5 LTS 正式發佈版 |

### 已移除的功能 {#removed-features}

此區段列出 AEM 6.5 LTS 已移除的特點和功能。先前的版本已將這些功能標記為已棄用。

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

<!-- DO THESE KNOWN ISSUES CARRY OVER EACH RELEASE? THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

### AEM 6.5.21-6.5.23 和 AEM 6.5 LTS 正式發佈版中的 JSP 指令碼搭售方案的問題

AEM 6.5.21、6.5.22、6.5.23 和 AEM 6.5 LTS 正式發佈版隨附 `org.apache.sling.scripting.jsp:2.6.0` 搭售方案，其中包含一個已知問題。通常在 AEM 實例同時處理許多請求而造成高負載的情況下，就會發生這個問題。

發生此問題時，錯誤記錄中可能會出現以下其中一項異常，並且參照 `org.apache.sling.scripting.jsp:2.6.0`：

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

可以使用 Hotfix [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) 解決此問題。

### Dispatcher連線失敗並提供僅限SSL的功能(已在AEM 6.5 LTS SP1及更新版本中修正){#ssl-only-feature}

>[!NOTE]
>
> 此問題僅出現在AEM 6.5 LTS GA版本中。

在 AEM 部署中啟用僅限 SSL 功能時，有一項已知問題會影響 Dispatcher 和 AEM 實例之間的連線。啟用此功能後，健康情況檢查可能會失敗，且 Dispatcher 和 AEM 實例之間的通訊可能會中斷。當客戶嘗試透過 `https + IP` 從 Dispatcher 連線至 AEM 執行個體時，特別容易發生此問題。此問題與 SNI (伺服器名稱指示) 驗證問題有關。

**影響：**

* 健康情況檢查失敗，回應代碼為 HTTP 400
* Dispatcher 與 AEM 實例之間的流量中斷
* 無法透過 Dispatcher 正確地提供內容
* 利用 Dispatcher 設定中的 IP 位址進行 HTTPS 連線失敗
* 透過 HTTPS + IP 連線時出現 HTTP 400「無效 SNI」錯誤

**受影響的環境：**

* 具有 Dispatcher 設定的 AEM 部署
* 已啟用僅限 SSL 功能的系統
* 使用 `https + IP` 方法連線至 AEM 實例的 Dispatcher 設定

**解決方案：**
若您遇到此問題，請聯絡 Adobe 客戶支援。可以使用 Hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 解決此問題。在套用必要的 Hotfix 之前，請勿嘗試啟用僅限 SSL 功能。

## 包含的 OSGi 套件和內容套件{#osgi-bundles-and-content-packages-included}

以下文字文件列出在此 [!DNL Experience Manager] 6.5 LTS Service Pack 1 版本中所包含的 OSGi 套件與內容套件：

* [ Experience Manager 6.5 LTS Service Pack 1 包含的 OSGi 套件清單](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS Service Pack 1 中包含的內容套件清單](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [在 licensing.adobe.com 下載產品](https://licensing.adobe.com/)
* [聯絡 Adobe 客戶支援](https://experienceleague.adobe.com/zh-hant/docs/customer-one/using/home)。

