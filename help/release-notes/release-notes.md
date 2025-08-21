---
title: Adobe Experience Manager 6.5 LTS SP1最新發行說明
description: 尋找Adobe Experience Manager 6.5 LTS Service Pack 1的最新發行資訊。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: b6a5e6bacfee72e162ce3bc035f909c02fbbf6db
workflow-type: tm+mt
source-wordcount: '4935'
ht-degree: 14%

---

# Adobe Experience Manager 6.5 LTS、SP1最新發行說明 {#release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | Service Pack 1 (SP1) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack發行 |
| 日期 | 2025年8月21日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://artifactory.corp.adobe.com/artifactory/maven-aem-release-local/com/adobe/aem/cq-quickstart/6.6.1/cq-quickstart-6.6.1.jar) |

<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## [!DNL Adobe Experience Manager] 6.5 LTS、SP1包含的內容 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS，SP1包含新功能、客戶要求的重要增強功能和錯誤修正。 其中也包括自2025年3月6.5 LTS首次推出以來的效能、穩定性和安全性改善專案。 在6.5 LTS上[安裝此Service Pack](#install-update)。

<!-- ## Key features and enhancements -->

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## 已修正6.5 LTS， Service Pack 1中的問題 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### 協助工具 {#sites-accessibility-65-lts-sp1}

* 修正內容片段中文字編輯器元素預設為截斷的問題。 文字編輯器現在會顯示完整內容，而不會截斷。 (SITES-33005)
* 修正按一下URL路徑開啟Indigo首頁而非正確目的地URL的問題。 (SITES-33004)
* 修正自訂AEM元件在自動化測試期間導致ADA相容性失敗的可存取性問題。 (SITES-30660)
* 已透過確保文字以黑色淺色背景顯示並符合WCAG 2.0對比度要求，修正「警報」對話方塊和工作流程訊息中的ADA合規性問題。 (SITES-30138)
* 修正AEM Sites編輯器中的「類別」按鈕缺少特定標籤，導致JAWS宣告為「影像按鈕選單」而不是提供描述性標籤的協助工具問題。 (SITES-27497)
* 修正「有效許可權」畫面中核取記號圖示缺少替代文字，導致JAWS無法閱讀及傳達意義的協助工具問題。 (SITES-27272)
* 修正協助工具問題，其中許可權頁面未提供清除使用者或群組許可權的JAWS公告，而造成熒幕助讀程式使用者混淆。 (SITES-27238)
* 修正無障礙問題，該問題導致錯誤訊息僅以圖示顯示，沒有描述性文字，導致JAWS無法在錯誤發生時宣佈錯誤。 (SITES-27155)
* 修正JAWS在AEM On-Premise環境中讀取不正確和不清楚按鈕說明的協助工具問題，包括模組區段缺少標題層級2文字。 (SITES-27152)
* 修正JAWS在AEM Assets索引標籤中篩選值後未宣告結果數量的協助工具問題。 (SITES-27150)
* 修正建立資料夾未顯示確認且JAWS未在Assets UI中宣告的協助工具問題。 (SITES-27141)
* 修正AEM Sites中的協助工具問題。 JAWS未宣告表單錯誤、焦點移至非互動式錯誤元素，且定位鍵輸出時必填欄位錯誤未顯示。 (SITES-27138)
* 修正「時間表」按鈕選單缺少特定標籤，導致JAWS只讀取「活動按鈕選單」而沒有提供清楚說明的協助工具問題。 (SITES-27134)
* 修正JAWS未宣告容器專案動作或角色的協助工具問題，僅讀取「階層連結v1」和「按鈕v2」而非描述性標籤。 (SITES-27131)
* 修正快速發佈快顯視窗無法提供正確成功訊息、導致熒幕助讀程式無法宣告完成意見的協助工具問題。 (SITES-26912)
* 修正coral-column檢視中，具有需要子角色之ARIA角色的元素未包含協助工具的問題，此問題造成不符合協助工具標準。 (SITES-26898)
* 修正在「重排」模式中，建立頁面頂端導覽列中的「範本」和「屬性」文字不可見，鍵盤和熒幕助讀程式使用者無法存取的協助工具問題。 (SITES-26895)
* 修正無法使用鍵盤導覽存取頂端導覽列中「搜尋」、「解決方案」、「說明」、「收件匣」和「使用者」圖示的工具提示的協助工具問題。 (SITES-26889)
* 修正基本索引標籤表單欄位未提供錯誤建議、導致使用者在必要輸入欄位留空時無法收到指引的協助工具問題。 (SITES-26885)
* 修正NVDA和「朗讀程式」熒幕助讀程式未在「建立」頁面中宣告範本檔案詳細資訊，導致使用者無法以程式設計方式接收完整資訊的協助工具問題。 (SITES-26884)
* 修正在「基本」標籤中「頁面標題」文字方塊使用錯誤名稱的協助工具問題，其導致熒幕助讀程式無法提供精確資訊給使用者。 (SITES-26879)
* 更新按鈕前景和背景顏色，以符合WCAG 2.2 AA最低對比率要求，進而改善所有使用者的可讀性和協助工具。 (SITES-26877)
* 解決造成建立頁面頂端導覽列中的「範本」和「屬性」文字在調整大小後消失的問題，確保低視力使用者的可見度和可存取性。 (SITES-26872)
* 修正在套用「重排」後，造成首頁面上出現多個水準卷軸的問題，確保顯示單一卷軸，以適當協助工具及顯示內容。 (SITES-26800)
* 修正AEM頁面編輯器中的協助工具問題，該問題導致在啟用「角色」、「購物車」或「放棄」等按鈕後，鍵盤焦點意外地重設至人口統計工具列的開頭。 焦點現在仍停留於已啟用的按鈕，以支援一致的鍵盤導覽和熒幕助讀程式工作流程。 (SITES-25306)
* 修正頁面標題和標籤欄位的協助工具標籤關聯問題。 AEM介面現在會在使用JAWS等熒幕助讀程式時，正確地將協助工具標籤與「標題」和「頁面標題」欄位建立關聯。 此修正可確保正確讀取標籤，並改善頁面建立、屬性和移動工作流程中的ADA合規性。 (SITES-27149)
* 修正時間軸中註解輸入欄位缺少視覺標籤的問題。 修正時間軸區段下「註解」輸入欄位缺少視覺標籤的問題，以改善協助工具。 此更新可確保熒幕助讀程式可以準確地朗讀欄位標籤。 此體驗可增強所有使用者的表單導覽和提交功能，尤其是依賴輔助技術的個人。 (SITES-26903)
* 修正時間軸註解中省略符號按鈕的鍵盤協助工具。 啟用時間軸區段下註解旁的省略符號（三個點）按鈕的鍵盤導覽。 使用者現在可以使用Tab鍵存取並與按鈕互動，改善了依賴僅鍵盤導覽的使用者的協助工具。 (SITES-26891)
* 改善選擇對話方塊中搜尋結果的NVDA/朗讀程式宣告。 更新「開啟選取專案」對話方塊，以宣告在使用熒幕助讀程式（例如NVDA或「朗讀程式」）時是否找到搜尋結果。 這項改善可協助依賴輔助技術的使用者瞭解其搜尋動作的結果，而不需要視覺確認。 (SITES-26883)
* 修正評論輸入欄位旁省略符號圖示的ARIA角色。 更新評論輸入欄位旁的省略符號（三個點）圖示，以使用正確的ARIA角色，確保熒幕助讀程式可準確識別元素。 這項改善可增強協助工具的合規性，並改善依賴輔助技術的使用者的體驗。 (SITES-26881)
* 更正Coral UI元件中無效的ARIA屬性。 更新Coral UI元件，確保所有ARIA屬性都使用有效值，進而改善協助工具合規性。 特別是，已處理錯誤指派`aria-modal="dialog"`等無效值的案例。 此增強功能可讓熒幕助讀程式正確解讀對話方塊元素，協助依賴輔助技術的使用者提升協助工具。 (SITES-26873)
* 改進重排情境中圖示的可見度和工具提示。 已增強重排行為，以確保工具提示可正確顯示給&#x200B;**下載**、**重新處理資產**&#x200B;和&#x200B;**簽出**&#x200B;圖示。 著重於在檢視區調整大小或瀏覽器縮放設定變更時，圖示及其標籤會變成隱藏的協助工具問題。 此修正可透過維護可見度並在Reflow期間提供適當的圖示說明，支援視力缺佳的使用者。 (SITES-26871)


#### 管理員使用者介面{#sites-adminui-65-lts-sp1}

* 修正JAWS未在「建立網站」對話方塊中宣告清單角色或提供導覽與啟用指示的協助工具問題。 (SITES-30661)
* Sites篩選檢視中狀態訊息的熒幕助讀程式支援可如預期運作，確保使用者在檢視之間切換時收到清楚及時的意見反應。 (SITES-24992)
* 篩選器邊欄中的日期選擇器完全顯示在其容器中，提供足夠的觸控目標大小並消除剪裁問題。 (SITES-24988)
* 選取的篩選器標籤現在會使用符合視覺呈現的語意HTML和aria標籤，確保對輔助型技術提供準確的角色支援和清晰的動作。 (SITES-24980)
* 在「參考邊欄」區域新增aria-label屬性，為熒幕助讀程式使用者提供不重複的描述性標籤，並確保頁面上的地標識別一致。 (SITES-24973)
* 更新參考邊欄，使用相對單位來調整大小和定位，讓內容能夠縮放，並在1280x1024檢視區縮放至400%時仍可完全正常運作。 (SITES-24972)
* 「網站首頁清單檢視」中確認的表格元素包含適當的欄標題角色，讓熒幕朗讀程式可宣告每個資料儲存格的標題。 (SITES-24942)
* NVDA現在會在樹狀目錄中公佈修改日期，確保熒幕助讀程式的使用者會收到完整的資產詳細資訊。 (SITES-24782)
* 修正NVDA熒幕助讀程式在AEM Sites的樹狀目錄元件中宣告專案文字不完整的問題。 NVDA現在會讀取每個專案的完整文字，以改善協助工具及法規遵循。 (SITES-24780)
* 在「樹狀目錄」的「視窗分隔器」中新增鍵盤協助工具，讓使用者僅需使用鍵盤即可調整左側列的大小。 (SITES-24779)
* 更新「說明」功能表搜尋結果，以包含清單專案正確的ARIA角色，確保熒幕助讀程式正確宣告連結，以提升協助工具。 (SITES-24729)
* 修正熒幕助讀程式未宣告「X of Y results」狀態訊息的問題。 或者，在網站篩選面板中套用篩選器後出現「找不到結果」訊息，確保使用者收到適當的結果確認。 (SITES-24720)
* 修正應用程式導覽中導覽連結缺少角色指派的問題。 新增適當的ARIA角色，以確保熒幕助讀程式可正確識別並宣告導覽元素。 (SITES-24719)
* 以按鈕元素取代所選篩選器標籤的不正確格線角色標示，並新增協助工具名稱，確保熒幕助讀程式正確宣告及識別標籤。 (SITES-24717)
* 新增執行多項選取時，參考邊欄狀態訊息的熒幕助讀程式公告，確保使用者會收到變更確認。 (SITES-24678)
* 修正搜尋欄位行為，使第一個結果不會自動宣佈。 熒幕助讀程式現在會朗讀找到的結果數量，讓使用者導覽清單時不會看到不正確的焦點朗讀。 (SITES-24658)
* 已從清單檢視中的非互動式靜態元素移除不正確的`aria-label`屬性，以防止熒幕助讀程式宣告誤導或不相關的資訊。 (SITES-24515)
* 更新清單檢視第一欄的核取方塊，以使用標題欄文字作為無障礙名稱，確保熒幕助讀程式準確傳達表單欄位的用途。 (SITES-24514)
* 新增適當的ARIA屬性和即時區域支援，可在內容導覽時向熒幕助讀程式使用者宣告載入狀態訊息。 (SITES-24481)
* 更新回應式設計，以檢視區寬度1280×1024將內容縮放至400%時消除水準捲動，確保完全可見且無需側邊捲動。 (SITES-24308)
* 更正網站管理員UI中的焦點導覽以遵循邏輯順序，在按Esc後恢復焦點至「全選」按鈕，並在按Tab後移動焦點至下一個互動元素。 (SITES-24307)
* 更新網站管理UI中的焦點順序，以便在鍵盤導覽期間，`<betty-titlebar-title>`元素中的階層連結按鈕以正確的順序接收焦點。 (SITES-24305)
* 已驗證跳過連結功能，以確保將鍵盤焦點移動到主要內容區域，讓鍵盤使用者繞過標題元素並有效率地存取內容。 (SITES-24061)


#### 傳統 UI{#sites-classicui-65-lts-sp1}

修正傳統UI中核取方塊標籤遺失，且HTML在多個UI元素（包括日期搜尋和非標準介面）中顯示為編碼文字的問題。 (SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

AEM現在可以防止影像資產中XMP中繼資料的格式錯誤導致效能降低。 Assets如果包含無效或不相容的XMP屬性名稱（例如具有數值區段或不合格結構的名稱），在處理期間將不再觸發重複的警告記錄。 系統會篩選掉有問題的中繼資料，以確保資產擷取和驗證完整無誤。 (SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments] — 片段編輯器{#sites-fragments-editor-65-lts-sp1}

其他作者仍可發佈內容片段，即使其他作者簽出它們，這違反了簽出功能的預期行為。 此修正可防止其他使用者在取出內容片段時，在製作介面中看見或使用發佈按鈕。 (SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### 元件主控台{#sites-component-console-65-lts-sp1}

修正產品清單元件中，「全選」核取方塊只從初始頁面新增前20個SKU，而非搜尋結果中所有SKU的問題。 (SITES-29191)

#### 核心後端{#sites-core-backend-65-lts-sp1}

處理`ValidationDataServlet`中的影像資產時，不正確格式化的XMP中繼資料觸發錯誤。 此修正可確保規範的中繼資料處理，並避免多餘剖析無效屬性。 (SITE-30683)

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM — 即時副本{#sites-msm-live-copies-65-lts-sp1}

* 修正重新啟用JavaScript 6.5內部部署中的AEM幽靈元件繼承時，所發生的錯誤`ns.ui.alert is not a function`。 (SITES-31993)
* 修正在AEM 6.5中允許轉出「稍後」選項繼續而不選取日期的問題。 (SITES-31374)

#### 頁面編輯器{#sites-pageeditor-65-lts-sp1}

* 解決Teaser強制回應視窗中，連結與動作索引標籤繼續在有效資料輸入和錯誤解決後顯示錯誤樣式、圖示和aria-invalid屬性的問題。 (SITES-25527)
* 修正Teaser強制回應文字編輯器中， 「清單」和「段落」按鈕未向熒幕朗讀程式傳達其展開或收合狀態的問題，以確保準確的aria展開屬性更新。 (SITES-25365)
* 修正人口統計工具列中，使用鍵盤輸入調整購物車滑桿時，焦點會移至購物車按鈕，而非繼續聚焦於滑桿，改善鍵盤使用者導覽效率的問題。 (SITES-25324)
* 透過指派值給其相關聯的`<label>`元素，在人口統計工具列中的購物車滑桿新增可存取的名稱。 此修正改善了與輔助技術的相容性，並增強了熒幕助讀程式使用者的可用性。 (SITES-25322)
* 在人口統計工具列下拉式清單中的按鈕新增ARIA角色和存取名稱。 此修正透過輔助技術啟用正確識別，並改善鍵盤和熒幕助讀程式使用者的導覽功能。 (SITES-25315)
* 已調整「人口統計工具列」版面配置，以防止在200%瀏覽器縮放時內容超出檢視區，確保所有控制項都維持可存取狀態而不進行水準捲動。 (SITES-25309)
* 更正人口統計工具列中的焦點管理，讓鍵盤焦點保持在啟動中的按鈕，而不是將焦點重設為工具列的開始位置。 (SITES-25306)
* 按鈕標籤會依設計重疊功能，當具有類似熒幕寬度的模式作用中時，使用工具提示來顯示標籤。 (SITES-25285)
* 註解強制回應包含可見的提交按鈕，可讓使用者在不依賴Esc鍵或按一下強制回應外部的情況下提交註解。 (SITES-25281)
* 註解強制回應視窗中包括筆圖示按鈕，使用者可透過按鈕提交註解，提供清晰且易於存取的提交方法。 (SITES-25269)
* 修正「註釋」和「關閉註釋」按鈕的熒幕助讀程式公告，以提供準確、相關的意見回饋，並移除不相關或令人困惑的資訊。 (SITES-25268)
* AEM編輯器頁面中的畫布區段現在支援完整的鍵盤協助工具。 使用者可以僅使用鍵盤啟動區段標題和編輯按鈕，而不需依賴滑鼠懸停。 此更新確保符合WCAG 2.1.1，並改善跨元件（例如Teaser、影像、輪播、版面、時間扭曲和註解模組）的可用性。 (SITES-25256)
* 移除轉盤強制回應中寬度為320px不必要的水準捲動，以確保所有內容都顯示在檢視區內，而不需要並排導覽。 (SITES-25254)
* 移除影像強制回應中寬度為320px不必要的水準捲動，以確保所有內容都顯示在檢視區內，而不需要並排導覽。 (SITES-25244)
* 移除Teaser強制回應中寬度為320px不必要的水準捲動，確保所有內容都顯示在檢視區內，而不需要並排導覽。 (SITES-25242)
* 已啟用Teaser強制回應視窗中`List`和`Paragraph Format`快顯功能表的鍵盤導覽。 此修正可讓使用者使用方向鍵存取及瀏覽這些功能表。 (SITES-25235)
* 修正「註釋」和「關閉註釋」按鈕的熒幕助讀程式公告，提供符合相關動作的準確、相關回饋。 (SITES-25234)
* 改善Teaser強制回應視窗中的「說明」按鈕標籤，以清楚描述其用途，並為所有使用者（包括輔助技術使用者）提供有意義的內容。 (SITES-25224)
* 將尺規測量與其個別裝置產生關聯，改善熒幕助讀程式使用者的模擬器尺規。 此外，將工具提示取代為aria-descripted by元素。 (SITES-24955)
* 未實作任何修正，因為「編輯」按鈕如預期運作，且提供資訊性內容而非執行動作。 (SITES-24950)
* 已確認編輯器頁面上的焦點順序會遵循邏輯順序，讓使用者導覽所有互動式元素，而不會意外跳躍或回圈。 (SITES-24937)
* 已確認當使用者套用自訂文字間距設定時，「預覽」模式畫布會正確更新文字間距，確保所有內容區域的格式一致。 (SITES-24936)
* 已驗證的「預覽」按鈕不再觸發焦點中的內容或狀態變更，確保使用者在頁面檢視更新之前有意啟動按鈕。 (SITES-24784)
* 在應用程式導覽連結中新增正確的ARIA角色指派，讓熒幕助讀程式能夠準確識別並宣告導覽專案，以改善協助工具。 (SITES-24718)
* 更新「變更篩選器」按鈕以向熒幕朗讀程式宣告展開和收合狀態、移除多餘的ARIA屬性，並調整標籤以提供清晰、非重複的說明。 (SITES-24713)
* 在「連結選擇」對話方塊中新增搜尋結果狀態訊息的熒幕助讀程式公告，以確保使用者在結果載入或找不到相符專案時收到確認。 (SITES-24700)
* 已新增影像強制回應視窗載入狀態的熒幕助讀程式公告，以確保使用者會在強制回應視窗載入並準備互動時收到回饋。 (SITES-24697)
* 解決無障礙問題，其中粘性標頭以200%和400%縮放遮住了Teaser模型內容，確保在使用頁面縮放時完整可見度和可用性。 (SITES-24523)
* 將包含搜尋結果數的狀態訊息新增至「搜尋/篩選」欄位，讓熒幕助讀程式可以向使用者宣告結果。 (SITES-24506)
* 在「搜尋/篩選」欄位中新增搜尋結果數量的熒幕助讀程式公告，以確保使用者在結果載入時立即收到回饋。 (SITES-24505)
* 在「側邊欄」面板的標籤清單中新增協助工具名稱，讓熒幕助讀程式可依照WAI-ARIA指南宣告其用途。 (SITES-24492)
* 為模稜兩可的編輯器圖示新增描述性標籤，確保所有使用者都清楚瞭解每個按鈕的功能。 (SITES-24480)
* 啟用「畫布」檢視中區段標題和動作按鈕的完整鍵盤協助工具，確保滑鼠和鍵盤使用者操作的一致性。 (SITES-24479)

<!--
#### Replication{#sites-replication-65-lts-sp1}

#### Rich Text Editor{#sites-rte-65-lts-sp1} -->

#### Universal Editor {#sites-universal-editor-65-lts-sp1}

* 修正QueryTokenService中的競爭條件，該條件導致在登入權杖服務傳回結果之前觸發多個查詢引數的錯誤登入。 (SITES-30659)
* 修正UniversalEditorURLService中，將對應路徑陣列儲存在Felix ConfigMgr中時只保留第一個專案的問題。 (SITES-30292)

### [!DNL Assets]{#assets-65-lts-sp1}

修正將資產從遠端DAM同步至站台本機AEM時，從資產中移除已發佈狀態和復寫相關屬性的問題。 (Assets-48958)

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

解決封鎖HTL指令碼引擎處理站運作的OSGi相依性週期，確保正確的服務解析度和指令碼執行。 (Granite-58275)

#### 整合{#foundation-integrations-65-lts-sp1}

* 已從`com.adobe.cq.cq-analytics-integration`套件組合中移除commons-httpclient 3.x的使用方式，並取代為`org.apache.httpcomponents.httpclient` 4.5.13.B0001，以符合最新的AEM 6.5 LTS標準。 (CQ-4360586)
* 從AEM中移除已棄用的Search&amp;Promote整合套件，以消除未使用的元件並降低維護額外負荷。 (CQ-4358030)
* 新增SiteCatalyst整合的後端測試案例，以改進分析驗證並確保更全面的涵蓋範圍。 (CQ-4359991)
* 修正Launch Config的「屬性」區段中未出現「公司」和「屬性」下拉式清單的問題。 此外，儘管填寫了所有必填欄位，「儲存並關閉」仍會觸發錯誤，當只有「標題」欄位空白時，公司和屬性會顯示不正確的錯誤訊息。 (CQ-4359853)
* 已從6.6版移除`searchpromote` servlet路徑專案，以符合Search&amp;Promote組合包的移除。 (CQ-4359523)
* 修正Target存放庫的HTTP測試案例，以確保準確驗證並改善測試可靠性。 (CQ-4359022)
* 移除integration-adobeims-console模組中的Guava快取使用方式，以消除Guava程式庫相依性。 (CQ-4358710)
* 已驗證AEM 6.6中的DTM整合工作流程、收件匣任務和專案功能，以確保AEM 6.5可正常運作。 (CQ-4358151)
* 已驗證AEM 6.6中的內容Insight功能，以確保AEM 6.5中的相容性和正常運作。 (CQ-4357774)
* 已驗證AEM 6.6中的雲端服務功能，以確保AEM 6.5中的相容性和正常運作。 (CQ-4357773)
* 已驗證AEM 6.6中的Adobe IMS主控台整合，以確保AEM 6.5中的相容性和正常運作。 (CQ-4357772)
* 更新Jenkins管道，以便Test&amp;Target整合在Java 17上執行、解決失敗的Selenium測試、將所選測試移至Playwright，並確保所有單元測試都通過。 (CQ-4357770)
* 透過更新建置和測試管道，使DX整合、工作流程、收件匣和專案與6.6.0分支一致。 此外，解決升級相容性問題，並驗證所有受影響的服務的穩定性和功能。 (CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### 本地化{#foundation-localization-65-lts-sp1}

* 將「移除存取控制」對話方塊中「許可權」清單的字串當地語系化，以顯示正確的翻譯。 (GRANITE-59427)
* 修正在「模型編輯器」的「或分割屬性」的「新增規則」對話方塊中，有多個UI字串（包括運運算元和欄位標籤）顯示為未當地語系化的問題。 所有字串現在都會以正確的本地化方式顯示。 (CQ-4354014)
* 已在「工作流程模型編輯」對話方塊中新增「顯示說明」工具提示的遺漏翻譯。 (CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

解決AEM在升級期間在`/apps/system/config`下重新建立或重新命名現有組態檔的問題，將`.cfg.json`個檔案取代為`.config`個檔案。 (GRANITE-58899)

#### Omnisearch{#foundation-omnisearch-65-lts-sp1}

修正預留位置錯誤地顯示為輸入欄位標籤的協助工具問題。 此問題會導致搜尋、AEM體驗片段、內容片段和內容片段模式中缺少欄位標籤。 (Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### 專案{#foundation-projects-65-lts-sp1}

* 解決在日曆檢視中刪除專案時，即使成功刪除專案，仍顯示錯誤快顯視窗的問題。 (CQ-4358890)
* 修正Firefox中，專案檢視中的「資產集合」卡片頁尾與卡片邊框重疊的問題。 頁尾現在會正確對齊，不會重疊。 (CQ-4353317)

#### 快速入門{#foundation-quickstart-65-lts-sp1}

* 更新解除安裝指令碼，以調整Guava套裝軟體的版本範圍，防止透過「封裝管理員」安裝時遭到封鎖。 (GRANITE-59559)
* 透過更新伺服器設定以支援大型套件安裝，而不觸發剖析失敗，解決了在使用JDK 17的Tomcat 11上AEMFD套件上傳期間發生的多部分設定錯誤。 (GRANITE-58327)
* 修正復寫UI中，透過更正介面中傳統核取方塊的處理方式，在編輯復寫代理程式時顯示錯誤(`#1660`)的問題。 (GRANITE-58302)
* 解決使用JDK 21執行AEM 6.5 LTS時S3資料存放區的多個啟動錯誤，解決遺失的服務許可權、更新設定處理，並確保必要的服務正確初始化。 (GRANITE-57082)
* 已定義AEM 6.5的維護和維護策略。此修正包含下列內容：
   * Service Pack步調。
   * Hotfix步調。
   * 與AEM 6.6平行支援。
   * 更新支援對照表。
   * 附加擁有權責任。 (GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* 將Sling ResourceAccessSecurity更新至1.1.2版，以解決多個`ClassCastException`參考初始化`ResourceAccessGate`時發生的`ResourceAccessSecurityImpl`。 (NPR-42750)
* 修正Adobe Stock整合中， 「授權」對話方塊顯示為灰色的問題。 此問題是由於`sunt:initList`函式移除必要的輸入欄位。 您可以在Coral Foundation使用者端程式庫中找到函式。 更新使用者端資料庫以保留必要的欄位，啟用適當的授權對話方塊功能。 (NPR-42748)
* 已反向移植Sling指令碼問題的修正，此問題在套件安裝期間造成`DataTimeParseException`和`String.length()` Null指標例外狀況。 將Sling Scripting更新至2.8.3-1.0.10.6版，以減少安裝錯誤並改善穩定性。 (NPR-42640)

<!--
#### Translation{#foundation-translation-65-lts-sp1} -->

#### 使用者介面{#foundation-ui-65-lts-sp1}

* 解決AEM作者UI中，將使用者群組顯示限製為41個的問題。 此問題是由於Granite UI群組選擇器元件中的預設批次限制所導致。 更新元件以顯示所有群組而不截斷。 (NPR-42749)
* 解決在內部部署頁面建立精靈中，編輯頁面屬性時多欄位元件中的必填欄位未重新驗證的問題。 此問題進而允許作者略過驗證，繼續處理不完整的資料。 (GRANITE-58826)
* 更正AEM中說明按鈕的ARIA屬性，以確保JAWS熒幕助讀程式朗讀清楚易用的標籤，而非顯示未翻譯的圖示和文字中繼資料。 (GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* 已新增AEM翻譯的Java 17支援，其方式為更新翻譯套件、驗證Java套件相容性、移除已棄用的相依性，以及透過全面測試確保完整功能。 (CQ-4357525)
* 已移除不穩定的常綠測試`com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater`，以防止在自動化測試期間發生錯誤失敗。 (CQ-4298376)

#### 工作流程{#foundation-workflow-65-lts-sp1}

* 在收件匣專案中新增遺失的`data-detailsurl`屬性，以防止在搭配Java 21使用AEM 6.5 LTS時，未定義的值出現在URL中。 (GRANITE-60158)
* 使用Java 21執行AEM 6.5 LTS時，修正`deactivate`套件組合的`WorkflowToPublishEventService`方法中的NullPointerException，確保正常的工作流程服務關機不會發生錯誤。 (GRANITE-58151)
* 更新工作流程索引以支援共用、休假自訂和解決時間表查詢問題。 (GRANITE-52640)
* 更新工作流程索引以支援共用、休假自訂功能以及時間表查詢問題的解決方案。 (GRANITE-52294)
* 解決在計畫升級至AEM發行說10912的記錄比較驗證期間增加的錯誤記錄失敗，確保穩定工作流程執行。 (GRANITE-44268)
* 更新工作流程存放庫中的URL清理方法，將`url.searchParams`取代為`url.search`，改善易受攻擊URL的XSS保護。 (CQ-4359585)
* 已驗證AEM 6.6 Forms中的工作流程、收件匣和專案功能，以確保正確操作和整合。 (CQ-4358777)
* 透過Jenkins實施發佈工作流程內容成品的自動化，啟用AEM 6.5中簡化及一致的部署程式。 (CQ-4358472)
* 修正在「收件匣建立任務」工作流程中，儘管已建立任務，但由於JavaScript語法錯誤，「新增任務」對話方塊在按一下「提交」後未關閉的問題。 (CQ-4355336)
* 修正由於`isEndUserConfigurationEnabled`缺少屬性定義而無法儲存收件匣檢視設定的問題。 (CQ-4287757)




## [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS 平台是以更新版本的 OSGi 式框架 (Apache Sling 和 Apache Felix) 以及 Java™ 內容存放庫 (Apache Jackrabbit Oak 1.68.x) 為基礎進行建置。

Eclipse Jetty 11.0.x 做為快速入門的 servlet 引擎。

### Java™支援  {#java-support}

* Java™ 17 和 Java™ 21 的支援。
* 為獲得最佳效能，請使用其他值覆寫預設的 GC 值。如需詳細資訊，請參閱[安裝與更新](/help/sites-deploying/custom-standalone-install.md)區段。
* 若是 Oracle 尚未正式推出，Adobe 會分發 Java™ 17 和 Java™ 21 維護更新供客戶在 AEM 相關專案中使用。

### Uberjar封裝 {#uber-jar-packaging}

* AEM 6.5 LTS 的 Uberjar 封裝略有不同。如需詳細資訊，請參閱[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

### 升級 {#upgrade}

* 關於升級程序的詳細資訊，請參閱[升級文件](/help/sites-deploying/upgrade.md)。

## 安裝與更新 {#install-update}

關於設定要求，請參閱[安裝指示](/help/sites-deploying/custom-standalone-install.md)。

如需詳細說明，請參閱[升級文件](/help/sites-deploying/upgrade.md)。

>[!NOTE]
>
> 對於全新的 AEM 6.5 LTS 安裝，必須獨立安裝索引定義。如需詳細資訊，請參閱[本文章](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)。

## 支援平台 {#supported-platforms}

尋找受支援平台的完整矩陣，包括 [AEM 6.5 LTS 技術要求](/help/sites-deploying/technical-requirements.md)的支援等級。

>[!NOTE]
>
>建議與 AEM 6.5 LTS 搭配使用的版本為 Java™ 17/Java™ 21。

## 過時和移除的功能 {#deprecated-and-removed-features}

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
|---|---|---|---|


### 已移除的功能 {#removed-features}

此區段列出 AEM 6.5 LTS 已移除的特點和功能。先前的版本已將這些功能標記為已棄用。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
|--- |--- |--- |--- |



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

### 僅SSL功能的Dispatcher連線失敗 {#ssl-only-feature}

在 AEM 部署中啟用僅限 SSL 功能時，有一項已知問題會影響 Dispatcher 和 AEM 實例之間的連線。啟用此功能後，健康情況檢查可能會失敗，且 Dispatcher 和 AEM 實例之間的通訊可能會中斷。當客戶嘗試透過`https + IP`從Dispatcher連線到AEM執行個體時，就會發生此問題。 它與SNI （伺服器名稱指示）驗證問題有關。

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

## 包含的OSGi套件組合和內容套件{#osgi-bundles-and-content-packages-included}

下列文字檔列出此[!DNL Experience Manager] 6.5 LTS Service Pack 1發行版本中包含的OSGi套件組合和內容套件：

* [包含在Experience Manager 6.5 LTS Service Pack 1](/help/release-notes/assets/65lts_sp1_bundles.txt)中的OSGi套件組合清單<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS Service Pack 1](/help/release-notes/assets/65lts_sp1_packages.txt)中包含的內容套件清單<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [在 licensing.adobe.com 下載產品](https://licensing.adobe.com/)
* [聯絡 Adobe 客戶支援](https://experienceleague.adobe.com/zh-hant/docs/customer-one/using/home)。

