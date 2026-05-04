---
title: Adobe Experience Manager 6.5 LTS SP2 的最新發行說明
description: 尋找 Adobe Experience Manager 6.5 LTS Service Pack 2 的最新版本資訊。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 6aca9496869f6673661a650438a7fc1beb212097
workflow-type: tm+mt
source-wordcount: '7603'
ht-degree: 97%

---


# Adobe Experience Manager 6.5 LTS SP2 的最新發行說明 {#release-notes}

## 版本資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 版本 | Service Pack 2 (SP2) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 類型 | Service Pack 發行 |
| 日期 | 2026 年 2 月 19 日<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下載 URL | [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.2.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> **強制 Hotfix** – 若要避免離線壓縮在安裝 SP2 時發生 SNFE (SegmentNotFoundException) 問題，請安裝[已知問題 – 線上壓縮期間存放庫損毀](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146)中說明的 Hotfix。

## [!DNL Adobe Experience Manager] 6.5 LTS SP2 包含哪些內容？ {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS SP2 包含新功能、客戶要求的重要增強功能和錯誤修正。 其中也包括自 2025 年 3 月首次推出 6.5 LTS 版本以來針對效能、穩定性與安全性所發佈的增強功能。 [在 6.5 LTS 上安裝此 Service Pack](#install-update)。

## 主要功能和增強功能

**AEM Sites**

AEM 6.5 LTS SP2 現在包含適用於[內容片段及模型管理](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/65lts/)和[啟動](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/launches/)的 OpenAPI。 這些 API 提供內容片段和啟動項的存取權，用於進行製作和排程。 其使用與 AEM as a Cloud Service 相同的現代 OpenAPI。

**AEM Forms**

**AEM Forms 6.5 LTS SP2 包含哪些內容**

* 新增 RDBMK 搭配 JBoss® EAP 8.0 的支援。

* 增強視覺規則編輯器中的使用者體驗。 本次更新內容包括：

   * 儲存後自動重新載入摘要視圖，顯示更新後的規則狀態

   * 顯示「新增」/「刪除」按鈕，並允許切換而非將其隱藏

   * 在規則儲存作業失敗時提供清楚的回饋 (FORMS-21261)

* 新增執行階段應用程式開發介面 (API)，藉以切換 AEM Forms 中舊版可延伸標示語言 (XML) 匯出模式，取代 `Dcom.adobe.fd.forms.export.legacy` 參數。 此增強功能讓使用者能更有效率地切換匯出模式，提高工作流程彈性。 (FORMS-23115)

* 新增針對自適應表單中附帶命名空間標記之 JavaScript 物件標記法 (JSON) 的支援。 此增強功能讓使用者能更有效地處理 JSON 資料結構，進而改善資料整合與處理功能。 (FORMS-22519)

* 在規則編輯器中新增一個立即可用的 (OOTB)「下載記錄文件 (DoR)/表單提交」按鈕。 此增強功能讓客戶不需撰寫自訂程式碼即可使用 downloadDoR 函數，進而提高使用性和效率。 (FORMS-21263)

* 新增針對自適應表單中附帶命名空間標記之 JavaScript 物件標記法 (JSON) 的支援。 此增強功能讓使用者能更精確且更有效率地預填表單，進而改善資料整合並減少手動輸入錯誤。 (FORMS-10883)

<!-- UPDATE THE EACH RELEASE -->

## 6.5 LTS Service Pack 2 中修正的問題 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP2}

#### 協助工具 {#sites-accessibility-65-lts-sp2}

* 編輯過程中，當作者將游標懸停在元件瀏覽器中的項目上時，文字元件會失去鍵盤焦點。 因而導致中斷輸入，並觸發 WCAG 3.2.1 下的協助工具失敗。 此修正可防止懸停樣式導致焦點移位，並確保在元件瀏覽器互動期間，文字元件保持焦點。 (SITES-35370)
* 修正「描述」RTF 欄位中的焦點管理問題，該問題曾導致無法使用 Tab 鍵進行向前導覽。 由於該元件依賴非標準的鍵盤指令來切換焦點，導致使用者卡在 RTE 中，進而中斷對話框中預期的導覽行為。 此變更強制採用標準的鍵盤互動方式，並確保在整個對話框中維持邏輯性的 Tab 鍵導覽順序。 (SITES-35228)
* 修正 Sites 編輯器中導致頁面製作期間中斷預期行為，並造成元件互動不一致的問題。 作者經歷不可靠的使用者介面回應，干擾標準編輯任務並降低工作流程效率。 本次更新精簡基礎編輯器邏輯，並還原受影響元件間穩定且可預期的互動。 (SITES-35227)
* 先前發生一項回歸問題，導致頁面編輯器中的資產選擇器失效，並使其在特定頁面編輯情境下無法載入。 作者現在於編輯頁面時選擇或瀏覽資產，即可正常開啟並使用資產選擇器。 此變更恢復了因載入失敗而中斷之資產選取工作流程的一致性。 (SITES-35226)
* 排除 Sites 編輯器中，導致頁面互動行為不一致，並干擾標準製作工作流程的問題。 該缺陷導致非預期的使用者介面回應，會干擾元件設定和內容更新。 此更新穩定了受影響的功能，並恢復了跨頁面之編輯操作的可靠執行。 (SITES-35225)
* 排除 Sites 製作介面中的缺陷，該缺陷曾導致頁面編輯期間的不一致行為並中斷正常工作流程。 作者遇到非預期的使用者介面回應，干擾元件互動和內容更新。 此更新穩定了受影響的功能，並於所有編輯情境中恢復可靠且可預測的行為。 (SITES-35224)
* AEM Sites 現在包含影像上的 `alt` 文字支援，藉以符合 ADA 和 WCAG 要求。 頁面輸出不再省略 `alt` 屬性，因此螢幕助讀程式會收到正確的替代文字。 (SITES-27153)
* 修正 `Note Add` 工具列配置，讓「新增」按鈕不再於檢視區寬度設為 320 像素時與標題重疊。 改善小螢幕上的 Reflow 功能，確保控制項在 400% 縮放時仍可讀取和使用。 (SITES-25376)
* 修正出現連結選取對話框錯誤時，螢幕助讀程式未朗讀的問題。 使用者介面現在會透過狀態訊息容器發佈錯誤文字，因此 NVDA 會在訊息出現時立即讀出。 (SITES-25368)
* 自側邊欄資產清單中移除 ARIA 網格和網格儲存格角色。 還原標準清單語意和鍵盤焦點順序，改善螢幕助讀程式導覽並減少額外的定位點。 (SITES-25361)
* 修正側欄 Assets 中的焦點排序。 鍵盤使用者現在可以透過一致的索引標籤路徑使用每項資產動作，包括「編輯」。 (SITES-25360)
* 修正在 320 像素檢視區寬度之下「搜尋 Assets」強制視窗的版面溢位問題。 強制內容現在會重新排版並保持可讀性，因此控制項不再與對話框重疊或超出對話框範圍。 (SITES-25330)
* 修正「編輯」按鈕的 NVDA 輸出。 NVDA 現在會朗讀「編輯」動作，而不是「預覽按鈕已按下」。 (SITES-25320)
* 修正未命名的人口統計工具列文字輸入，先前其會造成無訊息或一般螢幕助讀程式輸出。 現在，每項輸入都會顯示明確的標籤型協助工具名稱，改善了鍵盤和輔助技術導覽。 (SITES-25316)
* 修正「版面配置預覽」導覽期間「人口統計」工具列的鍵盤焦點順序。 索引標籤導覽現在直接從「人口統計」按鈕移動到工具列控制項，而不會跳到次要工具列。 (SITES-25305)
* 修正「編輯版面」尺標上「較小畫面」和「平板電腦」索引標籤的朗讀順序錯誤。 螢幕助讀程式現在會在符合頁面版面的正確尺標索引標籤處朗讀這些標籤。 (SITES-25291)
* 修正 200% 縮放時「編輯版面」工具列溢位的錯誤。 內容現在會保留在檢視區內，並可透過捲動存取。 (SITES-25288)
* 解決「附註」覆蓋中焦點順序不正確的問題。 鍵盤 Tab 鍵現在可於覆蓋控制項和註解項目中循環。 上層頁面不再從覆蓋後面獲得焦點。 (SITES-25282)
* 修正色票彈出視窗焦點處理問題。 對話框現在會將焦點移至清晰的標題，並在該進入點開始螢幕助讀程式輸出。 NVDA 不再以亂序方式讀取完整的對話框內容。 (SITES-25275)
* 修正「日期挑選器」關閉後的時間扭曲強制視窗焦點處理問題。 `Escape` 現在會將焦點傳回至日期挑選器按鈕。 日期選取範圍現在會將焦點放在「日期挑選器」控制項旁的輸入欄位上，防止焦點遺失和背景頁面存取。 (SITES-25264)
* 修正「刪除註解」對話框的鍵盤焦點處理。 取消現在會將焦點傳回至開啟對話框之 `Delete` 控制項，而非確認十六進位值控制項的情形。 取消後，螢幕助讀程式不再朗讀不相關的對話框內容。 (SITES-25258)
* 修正「註解」強制視窗對話框的焦點處理問題。 現在，開啟對話框會將焦點設定在對話框標題上，並阻止 NVDA 讀取畫布內容和不相關的對話框文字。 鍵盤導覽現在會保留在對話框內，直到關閉為止。 (SITES-25257)
* 修正 320 像素寬度之下「搜尋」強制視窗版面的問題。 強制視窗內容現在會乾淨地重新整理，並避免與樹狀目錄重疊。 使用者可以檢視結果及導覽目錄，而不會有模糊的控制項。 (SITES-25246)
* 「搜尋」強制視窗文字在文字間距增加後不再切斷。 樹狀目錄版面配置現在會保持清晰的區隔，讓標籤和條目保持可讀性。 使用者現在可以在沒有重疊或截斷文字的情況下完成搜尋和導覽。 (SITES-25245)
* 啟動「註釋」現在會將鍵盤焦點移至註釋內容，而不是「退出」註釋按鈕。 Tab 鍵順序遵循邏輯順序，並保持相關控制項可連線而不需反向導覽。 (SITES-25241)
* 鍵盤導覽時，「設定日期」和「退出時間扭曲」連結缺少可見的焦點指示器。 使用者介面現在會呈現明顯的高對比焦點樣式，讓使用者一眼就能識別作用中的連結。 (SITES-25232)
* Teaser 強制視窗標題不再阻擋鍵盤使用者移動對話框。 鍵盤控制現在允許選取、移動和放置動作，這可以改善螢幕助讀程式的易用性和整體操作性。 (SITES-25226)
* AEM 現在對 Teaser 強制視窗資訊按鈕採取具實質意義的無障礙標籤。 螢幕助讀程式會朗讀清除動作名稱，而非預設圖示替代文字字串。 (SITES-25223)
* 螢幕助讀程式現在會於使用者啟動「編輯」按鈕時朗讀正確的動作。 NVDA 不再回報「預覽按鈕已按下」，之前這會導致鍵盤導覽期間產生誤導性意見及混淆。 (SITES-25208)
* 展開左側邊欄現在會將鍵盤焦點移至第一個左側邊欄控制項。 Tab 鍵順序不再跳至次要工具列或登陸中間清單，因此鍵盤使用者無需反向導覽即可使用左側邊欄內容。 (SITES-24998)
* 裝置模擬器列內容現在於 320 像素檢視區寬度下仍完全可見。 工具列文字和控制項換行，而非截斷，減少重疊並改善可讀性。 (SITES-24953)
* AEM 現在會於模擬器工具列中顯示完整的 iPhone 裝置標籤。 文字不再以預設寬度截斷，進而改善可讀性和裝置選擇的清晰度。 (SITES-24952)
* 清單檢視表格標題現在透過 ARIA 公開排序狀態。 螢幕助讀程式會在欄排序動作後朗讀遞增或遞減順序。 (SITES-24943)
* 在文字間距變更時，AEM 現在會於「卡片視圖」中保留「更多動作」選單標籤可見度。 選單選項會保留完整的文字，包括「快速發佈」，而且選單在任何 WCAG 文字間距設定期間都會保持清晰可見。 (SITES-24941)
* 卡片動作選單列現在會於「卡片視圖」中顯示可存取的名稱。 螢幕助讀程式會清楚朗讀選單列的用途，而語音控制功能可依名稱鎖定控制項。 (SITES-24938)
* 卡片視圖不再依賴 ARIA 網格語意，過去這會造成螢幕助讀程式行為混亂。 使用者介面現在為卡片內容和卡片動作列提供有意義的角色和標籤，減少鍵盤使用期間遺漏的控制項。 (SITES-24933)
* 每次使用者懸停於工具提示圖示時，`Delete Modal` 工具提示都會顯示。 焦點動作現在會顯示相同的工具提示文字，這能改善滑鼠和鍵盤使用者的重複存取。 (SITES-24778)
* 使用者設定邊欄後，左側邊欄導覽現在會依照預期的鍵盤焦點順序進行。 Tab 焦點會出現在鎖選取的左側邊欄區域，而非切換顯示，這可改善螢幕助讀程式導覽的清晰度。 (SITES-24754)
* 修正「使用者偏好設定」強制視窗中色票導覽期間不正確的 NVDA 回饋。 NVDA 現在會讀取接收焦點的色票標籤，如此可移除誤導性的色彩輸出。 色票集現在支援一致的鍵盤導覽和清除選取範圍感知功能。 (SITES-24739)
* 減少 `Spin` 控制項的冗長 NVDA 輸出。 移除重複輸入標籤的重複群組標籤，因此 NVDA 只會朗讀一次控制項名稱。 鍵盤和螢幕助讀程式導覽功能現在可提供單一清楚的朗讀。 (SITES-24725)
* 「輪播」對話框現在會將焦點置於對話框標題上，而非「項目」索引標籤。 按下「取消」或「Esc」鍵可將焦點移回觸發對話框的控制項，藉此減少 NVDA 的冗長輸出 (SITES-24716)
* 「連結」選取對話框現在會將程式標籤與最後一級樹狀結構項目的螢幕標籤對齊。 箭頭鍵導覽會針對每個項目觸發可靠的螢幕助讀程式朗讀，並移除誤導性的標籤輸出。 (SITES-24710)
* 現在，在 320 像素檢視區下，「連結開啟選取」對話框會正確重新排列。 內容不再超出強制視窗或截斷，且強制視窗不再顯示橫向捲動軸。 (SITES-24709)
* 現在，在「關閉」或「取消」之後，「連結開啟選取範圍」對話框的鍵盤焦點會恢復至對話框觸發程式。 焦點不再跳至連結輸入，讓螢幕助讀程式內容能保持穩定，並減少額外的導覽。 (SITES-24707)
* 影像強制視窗對話框現在會依照邏輯焦點順序顯示。 取消後，焦點不再跳過之前的控制項，也不會停留在頁面標記上；退出後，使用者將重新獲得「設定」按鈕的焦點。 (SITES-24693)
* 參考邊欄強制視窗對話框現在會鎖定鍵盤焦點。 按下 Tab 和 Shift+Tab 時，會停留在對話框的控制項內，且焦點不再跳至頁面內容。 螢幕助讀程式只會朗讀對話框內容。 (SITES-24683)
* 「超連結路徑選取」強制視窗現在會在開啟時將焦點設定在對話框標題上。 按下「取消」會關閉對話框並將焦點恢復到「開啟選取對話框」按鈕，可防止焦點遺失及多餘的螢幕助讀程式輸出。 (SITES-24672)
* 「搜尋」欄位現在會使用持續性的螢幕上標籤，而非預留位置文字。 標籤在輸入時仍可見，可讓鍵盤、螢幕助讀程式和語音使用者更容易了解。 (SITES-24529)
* Teaser 強制視窗對話框現在會於開啟時將焦點設定在對話框標題上。 關閉對話框會將焦點傳回 `Configure` 控制項，避免焦點遺失及螢幕助讀程式輸出過多。 (SITES-24522)
* 側邊欄 Assets 面板現在包含關閉控制項。 「關閉」會將鍵盤焦點傳回側邊欄切換，並防止透過面板內容強制使用 Tab 鍵。 (SITES-24489)
* 鍵盤 Tab 鍵現在可前往管理員表格內的按鈕和連結。 使用者不再依賴方向鍵儲存格導覽來尋找互動式控制項。 (SITES-24285)
* 影像元件對話框不再以影像形式顯示裝飾性說明和全螢幕圖示。 螢幕助讀程式現在會略過這些圖示，將焦點保持在可操作的控制項和欄位內容上。 (SITES-2940)
* Sites 管理員現在會從資料夾縮圖圖示中移除影像角色。 輔助技術會略過這些裝飾性元素，將焦點持續放在資料夾名稱和動作上。 (SITES-2852)
* 內容樹現在會將鍵盤焦點路由至活動樹狀項目或第一個樹狀項目。 樹狀容器不再充當空的 Tab 停駐點，防止 Shift+Tab 焦點陷阱。 (SITES-1577)

#### 管理員使用者介面{#sites-adminui-65-lts-sp2}

Sites 主控台清單視圖設定未反映清單視圖中顯示的欄。 對話框開啟，其中已清除核取方塊，且選取的欄計數不正確。 此修正會將對話框的狀態與目前選中的網格欄位同步，並更新計數器使其符合實際的欄位可見性。 (SITES-38576)

#### Classic 使用者介面{#sites-classicui-65-lts-sp2}

升級後，經典使用者介面文字元件編輯會顯示原始 HTML 標記，而非 RTF 文字。 Service Pack 2 會更正經典使用者介面 RTE (RTF 編輯器) 轉譯，讓編輯器顯示格式化的內容並保留儲存的標籤。 此修正也會在重複編輯和儲存期間停止標示擴展。 (SITES-38709)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp2}

無周邊事件支援缺少 6.5 LTS 中內容片段和模型的必要 OSGi 事件。 更新會新增事件組合包加上必要的相依性，並包含 6.5 LTS 版本編號。 內容片段和模型事件現在可以正確引發，並支援「啟動 API」工作流程。 (SITES-35329)

#### [!DNL Content Fragments] - 管理員{#sites-admin-65-lts-sp2}

* 調整 Sites 製作介面中的元件處理，停止頁面更新期間的不規則行為。 此缺陷導致無法預測編輯器回應，干擾例行內容修改並降低工作流程效率。 更新會根據預期的互動模式調整編輯器邏輯，並在製作活動期間提供可靠的效能。 (SITES-35078) 關鍵

* 一項回歸錯誤導致 Assets 主控台中「內容片段」的清單視圖功能失效，並在清單轉譯過程中觸發錯誤。 更新修正了移除預覽資訊後的清單視圖邏輯，並恢復穩定的清單輸出。 主控台現在可正常顯示內容片段，且清單互動功能可正常使用。 (SITES-38683)
* 內容片段編輯器現已將「標記」標籤進行本地化。 編輯器亦將「集合」標籤進行本地化，使介面文字與所選的地區設定相符。 (SITES-977)


#### [!DNL Content Fragments] - 片段編輯器{#sites-fragments-editor-65-lts-sp2}

* 重構後，若功能切換開關保持停用狀態，內容片段變化版本標記便會消失。 此修正即使在該功能開關保持關閉時，亦恢復了變化版本標記的支援。 作者現在可以再次在內容片段編輯器中新增和檢視變化版本標記。 (SITES-38682) 關鍵
* 當作者從內容片段編輯器導覽返回後，已編輯的內容片段會從 Assets 主控台清單中消失。 瀏覽器快取傳回過時的清單，並隱藏更新的片段，直到手動重新整理為止。 此修正為編輯器的返回路徑新增了快取控制處理，使清單能正確重新載入，並保持已編輯的片段可見。 (SITES-35374) 關鍵

* 在最近的使用者介面樣式變更後，內容片段 RTE 出現版面和視覺問題。 Service Pack 2 會精簡 RTE 樣式，使工具列和可編輯區域能正確轉譯並保持可讀性。 內容片段編輯器現在的外觀與行為已與頁面編輯器保持一致。 (SITES-38684)
* 從 Polaris 資產選擇器中移除 IMS 範圍，導致內容片段與交付端點的整合功能失效。 作者在開啟遠端資產選擇器並選取資產時會遇到失敗。 此更新重新新增了必要的 IMS 範圍，並恢復穩定的交付層級存取權限。 (SITES-35837)
* 「關聯內容」面板不再顯示硬式編碼的「未定義」預留位置。 內容片段編輯器現在會透過本地化資源解析該文字，因此編輯者將看到已翻譯的使用者介面文字。 (SITES-33675)
  <!-- REMOVED FROM BUG LIST FEBRUARY 13, 2026 * Preview error messaging now uses localized strings instead of raw `Cannot print fragment's Json` text. The Content Fragment Editor now shows translated output across locales during GraphQL endpoint resolution failures. (SITES-33666)-->
* 內容片段編輯器現在會跨不同環境顯示已翻譯的「一般」標籤。 編輯器已替換未本地化的標籤文字，並從標籤標題中移除內部識別碼。 (SITES-30715)
* 內容片段編輯器現在會顯示已翻譯的允許資產類型名稱。 當作者設定內容參照限制時，選擇器清單不再混用內部字串與僅限英文的標籤。 (SITES-29699)

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp2}

* 改善 GraphQL 查詢驗證處理，停止因篩選器執行錯誤導致的部署失敗。 此缺陷會在應用程式啟動時觸發例外狀況，並阻礙受影響環境中的轉出作業成功完成。 此修訂確保驗證行為的一致性，並能實現順暢部署，避免因執行階段時查詢驗證中斷而導致的問題。 (SITES-34301) 關鍵

* 「編輯 GraphQL 端點」對話框現在會顯示本地化的使用者介面字串。 對話框不再顯示純英文文字，例如「GraphQL schema is taken from configuration」，而相關標籤在各個地區設定中能正確轉譯。 (SITES-34018)

#### [!DNL Content Fragments] - GraphQL 查詢編輯器{#sites-graphql-query-editor-65-lts-sp2}

* 改善 GraphQL 查詢驗證處理，停止因篩選器執行錯誤導致的部署失敗。 此缺陷會在應用程式啟動時觸發例外狀況，並阻礙受影響環境中的轉出作業成功完成。 此修訂確保驗證行為的一致性，並能實現順暢部署，避免因執行階段時查詢驗證中斷而導致的問題。 (SITES-35529)
* 當「設定瀏覽器」名稱包含 CJK 文字時，GraphQL Explorer 將不再發生錯誤。 端點建立及存取已儲存查詢的功能運作正常，且 GraphQL 查詢編輯器頁面不再出現錯誤。 (SITES-31616)

#### [!DNL Content Fragments] - 模型編輯器{#sites-model-editor-65-lts-sp2}

* 當重構將此功能綁定至已停用的切換開關時，巢狀內容片段模型會停止運作。 此修正恢復了對嵌套模型的支持，且無需變更切換開關。 作者現在可以再次在「模型編輯器」中建立和使用巢狀模型。 (SITES-38681) 關鍵

* 內容片段模型篩選器面板不再顯示未本地化的字串。 AEM 現在會顯示所有地區設定的本地化篩選器標籤和本地化狀態值。 (SITES-30863)
* 內容片段模型編輯器現在會轉譯鎖定警告對話框的本地化字串。 使用者介面以各種支援語言的地區設定資源取代未本地化的英文訊息。 (SITES-28592)

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp2}

AEM Headless 需要專用的發行分支，避免相依性和組合包版本與主線版本衝突。 此更新會新增 `release/6.5lts` 無周邊分支，並與相依性集和搭售方案版本相符。 Jenkins 現在可以建置無周邊程式碼基底，而不會發生版本衝突。 (SITES-36585)

<!-- #### Component console{#sites-component-console-65-lts-sp2} -->

#### 內容 API{#sites-content-api-65-lts-sp2}

一個功能開關的缺陷導致「頁面管理 API」狀態被錯誤回報。 本次更新新增了一個專用的啟用標幟，並會與現有的切換開關一同進行評估。 頁面管理 API 現在顯示穩定狀態。 網站管理 API 仍維持實驗性質。 (SITES-39284)

#### 核心後端{#sites-core-backend-65-lts-sp2}

* Sites 製作體驗中的變更，可以解決干擾標準頁面編輯工作流程的不一致行為。 作者在元件互動過程中遇到預期之外的結果，導致干擾內容更新並降低了可靠性。 此變更恢復了編輯器的穩定行為，並確保在受影響的情境中，編輯動作能一致地執行。 (SITES-35162) 關鍵

* 改善 Sites 製作行為，解決干擾頁面編輯並導致元件互動時產生不一致結果的問題。 作者遇到非預期的使用者介面回應，導致干擾內容更新並降低工作流程可靠性。 此變更恢復了穩定的編輯器狀態管理，並確保在受影響的情境中，編輯動作能可預測地執行。 (SITES-34499)

<!--
#### Core Components{#sites-core-components-65-lts-sp2}

#### Campaign integration{#sites-campaign-integration-65-lts-sp2}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp2}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp2}
-->

#### 啟動{#sites-launches-65-lts-sp2}

* Sites 時間軸在啟動促銷活動期間顯示硬式編碼英文文字：「Created version ... before promoting launch」。 此更新將硬式編碼的字串替換為本地化訊息處理。 時間軸現在會顯示本地化文字，並使專案符合標準 AEM 本地化行為。 (SITES-39157)
* 當作者使用「促銷活動目前頁面及子頁面」功能推廣子區段時，啟動推廣範圍會發生偏移。 AEM 也會推廣不相關的頁面，並造成非預期的即時網站修改。 此修正修改啟動範圍計算，確保僅推廣所選的子樹。 (SITES-38315)
* 「啟動」內的內容片段未參與 `damAssetLucene` 索引，且搜尋結果和查詢效率有限。 此變更會將「啟動」內容片段路徑新增至索引定義。 搜尋和自訂查詢現在可於 `/content/launches` 下找到內容片段。 (SITES-35634)
* 即使產品沒有在觸控式使用者介面中未公開內容片段「啟動」，「啟動」使用者介面仍顯示內容片段「啟動」控制項。 此變更會從 cq-launches-content 中移除內容片段啟動程式碼路徑，並調整 Launch 清單篩選器。 作者現在看到的頁面「啟動」選項已趨一致，且不含內容片段「啟動」條目。 (SITES-35633)
* AEM 6.5 LTS Quickstart 缺少必要的啟動組合包和先決條件，導致無法啟用啟動 OpenAPI。 此更新會新增啟動組合包和必要的相依性，例如量度支援、DAM-cfm 更新和佇列設定。 現在於 6.5 LTS Quickstart 上執行的啟動 API，必須有必要的執行階段元件。 (SITES-35297)
* CF 「啟動」封裝會提取較新的相依性版本和非必要的 GraphQL 程式庫，這會使 AEM 6.5 LTS 整合複雜化。 此變更會將相依性版本與 AEM 6.5 LTS 基準保持一致，並移除未使用的 GraphQL 相依性。 組合包解析度現在會維持一致，且 CF 啟動會維持穩定。 (SITES-35295)
* AEM 啟動現在會執行 6.5 LTS 分支的專用 Jenkins 管道。 管道會在夜間執行，並透過電子郵件傳送失敗警報。 此設定會增加測試涵蓋範圍並及早擷取回歸。 (SITES-35293)
* AEM 6.5 LTS 現在隨校準的成品版本推出更新的啟動 API 組合包。 組合包會追蹤主要程式碼行，同時保持正確的 6.5 LTS 發行版本。 此更新能穩定 6.5 LTS 堆疊中的啟動 API 消耗。 (SITES-35292)
* AEM 6.5 LTS 現在包含更新的啟動核心套件組合與相符的相依性版本。 此更新會新增片段 UUID 和參照 UUID 資料類型的啟動核心處理。 啟動處理現在可於各「啟動」和內容片段工作流程中保持一致的行為。 (SITES-35290)
* 改善 Sites 編輯器，解決會中斷正常頁面製作工作流程的不一致行為。 作者遇到意外的元件互動，干擾內容更新並降低編輯可靠性。 此變更恢復了一致使用者介面狀態管理，並確保在受影響的情境中，編輯動作能可預測地執行。 (SITES-35138)
* 「啟動編輯」現在會顯示本地化的錯誤文字，而非硬式編碼的 `Provided path is not a launch` 字串。 當編輯介面收到無效的啟動路徑時，使用者介面現在會顯示各語言的已翻譯訊息。 (SITES-33360)
* AEM 6.5 LTS 現在包含啟動 OpenAPI 側端連接埠工作。 此更新使啟動 API 套件、內容套件及所需的 Quickstart 組件達到功能一致，並透過穩定的 CI 驗證支援內容片段的啟動 OpenAPI 情境。 (SITES-32050)
* 啟動使用者介面現在會將覆寫範本標籤本地化。 範本覆寫詳細資訊現在會顯示翻譯文字，而非僅有英文字串。 (SITES-29525)
* AEM 已解決「**Sites** > **啟動** > **編輯**」中遺漏的本地化按鍵。 使用者現在會看到已翻譯的錯誤訊息，而不是原始的「Unable to update launch source list」字串。 (SITES-21499)
* 啟動促銷活動使用者介面現在會顯示本地化的狀態標籤和動作。 預覽區域會顯示「**已刪除**」、「**新增**」和「**檢視**」等翻譯文字，而非原始英文字串。 (SITES-13540)
* 啟動建立現在會顯示本地化的錯誤訊息。 使用者介面不再顯示原始英文字串，例如 `Unable to create launch page`、`Source root resource is not a page` 或 `Mandatory parameter is missing`。 (SITES-13085)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp2} -->


#### MSM - Live Copies{#sites-msm-live-copies-65-lts-sp2}

* 在內容變更期間，管理員對 MSM 推送修改處理的可見度有限。 此修正會新增有關 MSM 事件接收和轉出執行的詳細記錄。 偵錯輸出現在會顯示已引發哪些事件、已變更哪些內容路徑，以及誰觸發了變更。 (SITES-38029)
* AEM 已修正 Blueprint 轉出日期欄位上的本地化版面配置問題。 日期提示現在符合控制項，且在所有支援的語言 (包括 `fr_FR`) 中可讀取。 (SITES-14961)

<!-- #### Page editor{#sites-pageeditor-65-lts-sp2} -->

#### 複製{#sites-replication-65-lts-sp2}

頁面編輯器發佈現在會處理包含選擇器或尾碼的 URL。 發佈的請求現在會傳送 JCR 頁面路徑，而非選擇器或尾碼 URL 字串，因此啟用會完成且內容會上線。 複寫現在會於失敗時傳回錯誤狀態，防止出現誤判的「已開始發佈」訊息。 (NPR-43288)

<!-- #### Rich Text Editor{#sites-rte-65-lts-sp2} -->

#### 範本編輯器{#sites-template-editor-65-lts-sp2}

某些地區設定在「**工具** > **一般** > **範本**」中垂直顯示範本狀態文字。 「已過時」標籤破壞了版面，並讀取為一欄字元。 此修正會更正範本狀態樣式，使標籤在單一水平線上呈現。 (SITES-36797)

#### 通用編輯器 {#sites-universal-editor-65-lts-sp2}

* OSGi 預設設定已設為 `preview=true`，並強制通用編輯器在預覽模式下啟動。 此更新會更正預設值並恢復標準的生產項目行為。 除非管理員明確啟用預覽模式，否則通用編輯器現在會以生產模式開啟。 (SITES-37193)
* 在開發和中繼環境中，「通用編輯器開啟」指令現在預設為「預覽」模式。 該指令新增 `preview=true`，可保持作者檢查與預覽內容一致，並避免意外的「生產」開啟。 (SITES-33839)

### [!DNL Assets]{#assets-65-lts-sp2}

Assets 「相關」現在適用於包含空格的檔案名稱。 更新「相關」用戶端邏輯現在可以正確處理包含空格的路徑，並避免在相關性選取期間發生 `undefined` 來源錯誤。 「相關」對話框現在會開啟，並儲存關係，而不使用使用者介面下拉式選單。 DAM 使用者無需重新命名檔案，即可建立、衍生及解除資產的相關性。 (Assets-56418)

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp2}

* 全新 Dynamic Media 影片播放器整合 (有限推出) - 全新 Dynamic Media 影片播放器體驗現在於 AEM 6.6 Quickstart 中提供。 此增強功能目前僅對初始客戶啟用，做為控制轉出的一部分。 (Assets-60165)
* 解決影片屬性對話框中的「選取縮圖」選項未開啟資產選擇器的問題，恢復使用者為影片資產選擇自訂縮圖的能力。 (Assets‑58926)
* 在 Dynamic Media 影片中，新增支援在「字幕與音軌」語言下拉式清單中選取阿拉伯語，讓作者可直接在 AEM 中管理阿拉伯語字幕。 (Assets‑61771)

<!-- #### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp2} -->

<!--
#### Forms Designer
-->

### [!DNL Forms]{#forms-65-lts-sp2}

* 使用者遇到表單資料模型 (FDM) 編輯器 `Data Source / Enter Keyword` 功能的問題。 此問題會影響搜尋和選取資料來源的能力。 (FORMS-23971)
* 在行動裝置上，自適應表單中的表格元件會在頂端呈現隱藏的標題，導致螢幕助讀程式誤判內容。 這會影響依賴螢幕助讀程式進行導覽的使用者。 (FORMS-23754)
* 使用者在使用基於核心元件的自適應表單時，遇到了參照標記為 granite:InternalArea 之資源類型所引發的問題，這影響了內部部署 Forms 附加元件中多個 Granite 元件的功能。 (FORMS-23632)
* 升級至 AEM 6.5 LTS SP1 後，表單提交失敗。 使用者遇到遺失 com.adobe.cq.social.commons.CollabUtil，造成 JSP 編譯錯誤和電子郵件動作失敗的問題。 (FORMS-23457)
* 使用者遇到驗證碼問題，無法在基礎元件型的自適應表單中正確翻譯。 這會影響非英語使用者準確完成表單的能力。 (FORMS-23426)
* 使用者遇到表單提交失敗，出現 SAXParseException：「內容於 prolog 中不允許」(HTTP 500)。 發生此問題的原因是預填資料 XML 中有 null 值，導致伺服器端 XML 剖析失敗。 (FORMS-22633)
* 使用者發現自適應表單未能通過網頁內容無障礙指南 (WCAG) 的稽核。 原因是表單的索引標籤導覽標示無效。 也就是說，一個非清單元素會轉譯為清單的直接子元素，而該位置僅允許清單項目存在。 此問題會導致表單無法通過輔助工具驗證，並對必須符合法律或內部合規要求的組織造成影響。 (FORMS-22101)
* 使用者遇到記錄文件 (DoR)/提交 PDF 的輔助工具問題，空白表單欄位未標記為表單元素。 這會使螢幕助讀程式遇到困難，影響障礙使用者有效導覽和完成表單的能力。 (FORMS-21989)
* 使用者遇到在表單載入期間子面板內元件的註腳未顯示的問題。 當包含註腳的項目是頁面上的最後一個元件時，就會發生此問題。 (FORMS-21925)
* 使用者在 AEM Forms 編輯器中選取元件時遇到問題。 在索引標籤之間導覽並返回第一個索引標籤時，某些容器會變成無法選取，導致無法輕鬆識別和互動。 (FORMS-21814)
* 使用者在自適應表單儀表板中遇到安全性弱點。 具體來說，在 startpointcontrol.js 檔案中發現跨網站指令碼 (XSS) 問題，這可能導致允許執行惡意指令碼。 (FORMS-20679)
* 在 JBoss® EAP 8 上的 AEM Forms 6.5 LTS 叢集部署中，`domain/configuration/domain_oracle.xml`、`domain_mysql.xml` 和 `domain_mssql.xml` 檔案不再包含重複的 `<security>` 標記，導致無效的 XML 並使網域資料控管者無法啟動。 (FORMS-24687)
* 在 Turnkey 模式中，現在會於全新安裝和升級期間正確套用資料庫連接埠更新。 在全新安裝模式中，使用者可以從所有可用的連接埠中進行選取，而在升級模式中，在升級過程中會正確參照 lc_turnkey.xml 中更新的資料庫連接埠。 (FORMS-24689)
* 在 Linux® 上設定 JBoss® EAP 8.0 時，於 Windows 上修改的 Shell 指令碼不會因為 CRLF 行結尾而造成 `/bin/sh^M: bad interpreter or $'\r': command not found` 錯誤。 (FORMS-24688)

<!--
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

* Sling Resource Access Security 現在會於 1.1.2 版本上執行。 多個 ResourceAccessGateHandler 服務註冊時，ResourceAccessSecurityImpl 在初始化期間不再擲回 ClassCastException。 初始化現在會可靠地完成，並避免在有多個處理常式的環境中啟動失敗。 (NPR-42750)
* JMX 主控台和網頁控制台現在會傳送主控台 CSS 資源的 `Content-Type: text/css header`。 嚴格的 MIME 檢查不再封鎖樣式工作表載入，因此 `/system/console/jmx` 使用者介面會以一般樣式呈現。 (GRANITE-63677)
* AEM 現在會避免在產生的 `WEB-INF/resources/provisioning/model.txt` 中對 `contributor` 群組使用重複的 ACL 條目。 WAR 輸出現在包含一個一致的 ACL 區塊，防止在審閱期間混淆權限差異。 (GRANITE-63269)
* 於組合包重新整理作業期間，AEM 不再清除還原序列化防火牆封鎖清單和允許清單設定。 更新的篩選器註冊邏輯可讓作用中的防火牆執行個體與儲存的設定保持一致，因此保護功能不會重新啟動而維持啟用狀態。 (GRANITE-61382)
* Felix 網頁控制台在 `/system/console` 存取期間不再引發間歇性 `NullPointerException` 錯誤。 更新的 ServiceTracker 處理可以防止 null 的追蹤器狀態。 在重複請求和自動驗證期間，主控台登入和導覽會保持穩定。 (GRANITE-61042)

<!--
#### Campaign{#foundation-campaign-65-lts-sp2}

#### Cloud Services{#foundation-cloudservices-65-lts-sp2}

#### Communities {#foundation-communities-65-lts-sp2}

#### Content distribution{#foundation-content-distribution-65-lts-sp2}
-->

#### CRX {#foundation-crx-65-lts-sp2}

升級 Service Pack 後開啟 JSP 檔案時，CRXDE Lite 不再顯示空白索引標籤。 AEM 現在隨附相符的 CodeMirror 核心和附加元件程式碼，可避免嚴重的瀏覽器錯誤，並保持編輯器可用。 (GRANITE-64333)

#### Granite{#foundation-granite-65-lts-sp2}

Expression Security Validator 現在會處理空白或 Null 的 OSGi 設定值。 其會套用安全預設值、忽略空陣列，並記錄清晰的記錄，避免 NullPointerException 和無法預測的驗證結果。 (NPR-43163)

<!-- #### HTL{#foundatoin-htl-5-lts-sp2} -->

#### 整合{#foundation-integrations-65-lts-sp2}

即使有開始和結束日期，AEM 現在也會同步 Adobe Target 活動。 Target 承載現在會將活動日期格式化為完整的 ISO 8601 時間戳記，包括秒、毫秒和時區。 Target 不再拒絕具有 `InvalidJson.Json` 的要求。 已排程的活動現在會移至同步狀態，而不會離開同步。 (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-65-lts-sp2}

#### Localization{#foundation-localization-65-lts-sp2} 

#### Omnisearch{#foundation-omnisearch-65-lts-sp2}

#### Platform{#foundation-platform-65-lts-sp2}

#### Projects{#foundation-projects-65-lts-sp2}
-->

#### Oak {#foundation-oak-65-lts-sp2}

AEM 6.5 LTS Service Pack 2 需要 S3 Connector 1.60.10 或更新版本。 S3 資料存放庫設定現在包含 `crossRegionAccess` 和 `mode`，因此管理員可以啟用跨區域桶存取，並在需要時將儲存空間切換至 GCP。 `s3EndPoint` 現在需要與 `s3Region` 相符的區域，或者其會保持空白讓驅動程式產生端點。 (GRANITE-64873)


#### 快速入門{#foundation-quickstart-65-lts-sp2}

* Sling 會更新管理登入允許清單，使用內含術語和新設定 PID。 此變更與 Sling JCR Base 3.2.0 一致。 (GRANITE-63756)

  **影響**

   * Sling 會棄用這些 PID，您應該從設定中將其移除：
      * 工廠 PID：`org.apache.sling.jcr.base.internal.LoginAdminWhitelist.fragment`
      * 全域 PID： `org.apache.sling.jcr.base.internal.LoginAdminWhitelist`
這些舊設定會使用屬性，例如 `whitelist.name` 和 `whitelist.bundles`。

   * Sling 仍會為棄用的 PID 提供部分回溯相容性，但不會將其用於新設定。 請改用較新的 `LoginAdminAllowList.*` PID。
   * 請勿同時執行已棄用的和新的允許清單設定。 混合設定可能會產生模稜兩可的情況並產生非預期的行為。 當您移轉至 AEM 6.5 LTS SP2 時，請完全移除已棄用的 PID。

  **您應該怎麼做**

   1. 尋找使用 `LoginAdminWhitelist*` PID 的允許清單設定。
   1. 以適當的新 PID 取代：

      * 工廠 PID：`org.apache.sling.jcr.base.LoginAdminAllowList.fragment`
      * 全域 PID：`org.apache.sling.jcr.base.LoginAdminAllowList`

      如需其他詳細資訊，請參閱[管理登入允許清單組合包的棄用方法](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecated-approach-to-allowlist-bundles-for-administrative-login)。

* AEM 6.5 LTS SP2 更新了 Sling、Oak 和 Felix 的基礎層組合包集。 這些升級會增強核心執行階段穩定性，並調整整個平台的相依性版本。 (GRANITE-61874)

<!--
#### Security{#foundation-security-65-lts-sp2}

AEM now prevents NullPointerException errors when a logged-in user lacks read access for some groups and opens the Groups tab. The tab now hides groups without access and renders group membership details without a blank or unresponsive UI. (NPR-43311)
-->

#### Sling{#foundation-sling-65-lts-sp2}

AEM 現在包含 Sling Engine 2.16.6。 此變更可排除安全性工具標示的 XSS 違規，並改善核心轉譯的安全性和穩定性。 (NPR-43105)

<!--
#### Translation{#foundation-translation-65-lts-sp2}

#### User interface{#foundation-ui-65-lts-sp2}
-->

#### WCM{#foundation-wcm-65-lts-sp2}

AEM 翻譯不再因 XLIFF 格式問題而於 Java 17 或 Java 21 上失敗。 匯出管道現在會產生翻譯提供者所能接受的標準相符 XLIFF。 此變更排除翻譯工作中斷問題，並恢復 AEM 與翻譯服務之間的可預測切換。 支援的 Java 執行階段中，翻譯工作流程現在保持穩定。 (CQ-4360217)

#### 工作流程{#foundation-workflow-65-lts-sp2}

在工作流程通知處理期間，EmailNotificationService-Processor 不再觸發重複的「找不到區段」錯誤。 更新的例外狀況處理會偵測 SegmentNotFoundException 並停止處理迴圈，而非繼續無效讀取。 工作流程執行會保持穩定，並在收件匣和工作專案存取期間記錄雜訊下降。 (GRANITE-62635)




## 關於 [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS 平台是以更新版本的 OSGi 式框架 (Apache Sling 和 Apache Felix) 以及 Java™ 內容存放庫 (Apache Jackrabbit Oak 1.68.x) 為基礎進行建置。

Eclipse Jetty 11.0.x 會用於作為快速入門的 servlet 引擎。

### Java™ 支援  {#java-support}

* Java™ 17 和 Java™ 21 的支援。
* 為實現最佳效能，請使用其他值覆寫預設的 GC 值。 如需詳細資訊，請參閱[安裝與更新](/help/sites-deploying/custom-standalone-install.md)區段。
* 若是 Oracle 尚未正式推出，Adobe 會分發 Java™ 17 和 Java™ 21 維護更新供客戶在 AEM 相關專案中使用。

### Uberjar 封裝 {#uber-jar-packaging}

適用於 AEM 6.5 LTS SP2 的 UberJar 使用 AEM 6.5 LTS UberJar 6.6.2 版。 您可以從 Maven 中央存放庫檢索對應的 UberJar 成品。 與 AEM 6.5 不同，AEM 6.5 LTS 會將公用 API 和已棄用的 API 分隔成兩個不同的成品。

若要針對公開 API 進行編譯，請使用下列內容：

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

如果您的程式碼也相依於已棄用的 API，請新增下列內容：

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

另請參閱[更新 AEM Uber Jar 版本](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)。

### 升級 {#upgrade}

* 如需升級程序的詳細資訊，請參閱[升級文件](/help/sites-deploying/upgrade.md)。
* 如需詳細的升級指示，請參閱 [JEE 上的 AEM Forms 6.5 LTS SP1 升級指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

#### AEM 6.5 LTS Service Pack 升級的最佳做法

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**環境**
適用於：安裝 Service Pack 2 (SP2) 的 AEM 6.5 LTS (內部部署) 客戶。 SP2 會以 Quickstart JAR 形式提供。

**為什麼這種升級做法很重要**
EM 6.5 LTS 適用的 SP2 會以 Quickstart JAR 形式提供，而非透過「封裝管理員」進行安裝的 ZIP 檔。 內部部署客戶的升級方式是取代 Quickstart JAR，將檔案解壓縮然後重新啟動。 此方法與 Adobe 的就地升級程序一致。

**建議的升級流程 (作者或發佈)**

1. 驗證您的 AEM 6.5 LTS 執行個體是否運作正常且可存取。
1. 從 Software Distribution 下載 Quickstart JAR (例如 `cq-quickstart-6.6.x.jar`)。
1. 停止正在運作的實例。
1. 在 AEM 安裝目錄中 (`crx-quickstart/` 之外)，使用 SP2 JAR 取代先前的 Quickstart JAR。
1. 將 JAR 解壓縮：

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (視需要調整堆積旗標。)

1. 根據其角色和連接埠，將解壓縮的 JAR 重新命名，例如 `cq-author-4502.jar` 或 `cq-publish-4503.jar`。
1. 開始 AEM，並在 UI (「說明」>「關於」) 和記錄中確認升級。

**良好的操作規範**

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


如需詳細說明，請參閱[升級文件](/help/sites-deploying/upgrade.md)。

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

建議客戶審閱是否在目前部署中使用了已棄用的功能。 制定規劃變更其實施，使用提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
| --- | --- | --- | --- |
| 快速入門 | Mongo API | Mongo API 現已棄用，並規劃在未來版本中移除。 | 6.5 TS SP2 |
| Sites | AEM Assets REST API 中的內容片段支援 | AEM 6.5 LTS SP2 為內容片段和模型管理提供現代化的 OpenAPI，因此 AEM Assets REST API 中較舊的內容片段支援端點現已棄用。<br>Adobe 預計在生命週期結束公告前保留這些較舊的端點。 Adobe 未計劃針對已棄用的端點提供進一步的增強功能。 | 6.5 LTS SP2 |
| Sites | [SPA 編輯器](/help/sites-developing/spa-overview.md) | 在 AEM 中管理無周邊內容的首選編輯器是：<br>- [通用編輯器](/help/sites-developing/universal-editor/introduction.md)，用於視覺化編輯。<br>- [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。 | 6.5 LTS 正式發佈版 |
| [!DNL Foundation] | 支援 com.adobe.granite.oauth.server | Adobe IMS 整合 |  |

### 已移除的功能 {#removed-features}

此區段列出 AEM 6.5 LTS 已移除的特點和功能。 先前的版本已將這些功能標記為已棄用。

* 針對 CRX 存放庫持續性的 RDBMK 支援已移除。
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

* 在 Configuration Manager 中，未選取模組或僅選取有限元件時，在 AEM Forms 6.5 LTS JEE Turnkey 自訂模式中的 Bootstrap 期間，資料庫初始化會失敗。 失敗是因為遺失相依性 (xalan-2.7.2.jar)，導致錯誤。 將 JAR 檔案新增至 adobe-livecycle-jboss.ear\lib 即可解決問題。 (FORMS-24690)
* 在 JBoss® EAP 8 上執行的 Forms JEE LTS 部署中，Reader 擴充功能使用者介面可能會因內部伺服器錯誤而失敗。 (FORMS-24894)
* 在 JBoss® 上執行的 Forms JEE LTS 上，電子郵件相關功能可能會失敗。 嘗試使用電子郵件功能時，伺服器可能會記錄類似 `Error IMAPProvider not a subtype` 的錯誤。 (FORMS-24892)
* 在 Linux® 平台上，Forms JEE LTS 要求在執行 Configuration Manager 之前，必須正確設定 `LFS_Foundation.properties` 中的 `OSFileSetIntendedFor` 屬性。 如果未更新，設定可能無法針對 Linux® 適當地量身打造，這可能會導致執行階段或部署問題。 若要解決此問題，請在執行安裝程式之後和執行 Configuration Manager 之前，導覽至「`configurationManager/config/solcomp/`」，開啟「`LFS_Foundation.properties`」，設定「`OSFileSetIntendedFor=Linux`」，儲存檔案，然後執行 Configuration Manager。 (FORMS-24741)

### 離線壓縮後線上壓縮期間存放庫損毀 (GRANITE-65146) {#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146}

若先前曾在 JCR 存放庫上執行過離線壓縮，使用者在執行線上壓縮時可能會遇到存放庫損毀的情況。 此情境中可能會發生 `SegmentNotFoundException` (SNFE)，並可能導致存放庫損毀。

若要解決此問題，請安裝「[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-65388-1.0.zip)」處的 Hotfix。 由於 Hotfix 包含低階 `oak-segment-tar` 組合包，所以執行個體會在安裝後重新啟動。

計劃套用執行個體時的停機時間。 若要離線壓縮，請使用對應的 [`oak-run` jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar) (也可在 Software Distribution 中使用)。

>[!NOTE]
>
> * 對於任何 `oak-run` 作業，請使用 [`oak-run` 1.88.1-B006 jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar)。
>
> * 設定系統屬性 `oak.compaction.legacy=true` 以啟動 AEM。

### Sling-Initial-Content (SP2)不再支援JSON註解 {#json-comments-no-longer-supported-in-sling-initial-content}

此問題會影響OSGi套件組合開發人員，以及部署搭配JSON檔案使用`Sling-Initial-Content`之套件組合的管理員。

從AEM 6.5 LTS SP2開始，`Sling-Initial-Content`套件組合中使用的JSON檔案不再接受註解（`//`或`/* */`）。 較早的AEM發行版本接受註解，因為`javax.json`提供者對此比較寬大。 AEM 6.5 LTS SP2將`org.apache.sling.jcr.contentloader`升級至2.6.0版，並將JSON剖析器切換為`jakarta.json`。 雖然[JSON規格(RFC 8259)](https://datatracker.ietf.org/doc/html/rfc8259)並未定義註解的語法，但由於`javax.json`提供者的寬大處理，舊版AEM已接受註解。 `jakarta.json`提供者不提供此延伸。

失敗為無訊息：內容節點無法在套件啟動時載入，且安裝程式未顯示任何錯誤。 如果在升級至SP2後意外遺失內容，請檢查OSGi安裝程式記錄檔中的JSON剖析錯誤。 若要識別受影響的組合，請在`Sling-Initial-Content`資訊清單標題下列出的JSON檔案中搜尋`//`或`/* */`。

>[!CAUTION]
>
> 移除`Sling-Initial-Content`套件組合中JSON檔案的所有註解，以避免在升級至AEM 6.5 LTS SP2後內容載入失敗。

### 安裝 Sites Headless API 必要的 Oak 索引{#site-headless-api}

部分移至 Sites Headless 的 API 需要額外的 Oak 索引才能完整發揮功能。

安裝 `cq-dam-cfm-indices` 封裝，方能使用下列功能：

* 列出內容片段模型
* 列出內容片段
* 搜尋 API
* 工作流程

從 Adobe 軟體發佈入口網站下載索引套件 [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-dam-cfm-indices-1.1.2.zip)。

### 使用僅限 SSL 連線功能時 Dispatcher 連線失敗 (AEM 6.5 LTS SP1 及以上版本已修正){#ssl-only-feature}

>[!NOTE]
>
> 這項問題僅出現在 AEM 6.5 LTS GA 版本。

在 AEM 部署中啟用僅限 SSL 功能時，有一項已知問題會影響 Dispatcher 和 AEM 實例之間的連線。 啟用此功能後，健康情況檢查可能會失敗，且 Dispatcher 和 AEM 實例之間的通訊可能會中斷。 當客戶嘗試透過 `https + IP` 從 Dispatcher 連線至 AEM 執行個體時，特別容易發生此問題。 此問題與 SNI (伺服器名稱指示) 驗證問題有關。

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

若您遇到此問題，請聯絡 Adobe 客戶支援。 可以使用 Hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) 解決此問題。 在套用必要的 Hotfix 之前，請勿嘗試啟用僅限 SSL 功能。

## 包含的 OSGi 套件和內容套件{#osgi-bundles-and-content-packages-included}

以下文字文件列出在此 [!DNL Experience Manager] 6.5 LTS Service Pack 2 版本中所包含的 OSGi 套件與內容套件：<!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5 LTS Service Pack 2 包含的 OSGi 套件清單](/help/release-notes/assets/65lts_sp2_bundles.txt)<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS Service Pack 2 中包含的內容套件清單](/help/release-notes/assets/65lts_sp2_packages.txt)<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的網站{#restricted-sites}

這些網站僅供客戶使用。 若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [在 licensing.adobe.com 下載產品](https://licensing.adobe.com/)
* [聯絡 Adobe 客戶支援](https://experienceleague.adobe.com/zh-hant/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience)。

