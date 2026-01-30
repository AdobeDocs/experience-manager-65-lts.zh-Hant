---
title: We.Finance汽車保險續約參考網站逐步說明
description: 透過逐步解說，瞭解「We.Finance」汽車保險續約參考網站。
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: User, Developer
exl-id: 3f9f1a20-9029-4e30-9c9d-ef452512f7e9
source-git-commit: c0bf6864bb344e582c4f88371c892d401ce2827c
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# `We.Finance`汽車保險續約參考網站逐步說明{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## `We.Finance`參考網站情境  {#we-finance-reference-site-scenario}

`We.Finance`網站是金融服務網站，旨在協助您學習AEM Forms的互動式通訊功能。

閱讀`We.Finance`車險使用案例的詳細逐步解說，其中展示AEM如何形成及其與Microsoft® Dynamics的整合有助於個人化金融服務公司的客戶體驗。 互動式逐步解說的設計目的，是為了在金融公司中輕鬆實作複雜的數位交易和客戶通訊。

**歷程從使用案例開始：**

Sarah Rose是現有的`We.Finance`客戶，並已購買汽車保險單。 一年之中正是莎拉續保單的時候。 Gloria Rios是她的保險代理人。 `We.Finance`網站以電子郵件向Sarah傳送有關其原則更新的提醒。 Sarah遵循電子郵件中的指示，成功完成程式。

## 自動保險應用程式逐步說明 {#auto-insurance-application-walkthrough}

`We.Finance`自動保險申請案例是使用者的視覺敘述，並以兩個角色為基礎：

* `We.Finance`客戶Sarah Rose
* Gloria Rios，保險代理人，`We.Finance`

### Gloria從`We.Finance`傳送保單續約通訊 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria登入AEM執行個體，按一下&#x200B;**自動保險續約**，然後按一下&#x200B;**開啟代理程式UI**。 按一下即可使用Sarah Rose的保單詳細資料預先填入保險檔案。 Gloria按一下&#x200B;**提交**，熒幕上會顯示訊息「已起始提交」，然後在幾秒鐘後顯示「已成功提交」。

Sarah收到一封電子郵件，主旨為「您的汽車保險續約」。

![代理程式UI](assets/agent_ui_email_new.png)

#### 親眼看看 {#see-it-yourself}

移至&#x200B;**Adobe Experience Manager** > **Forms** > **Forms與檔案** > **`We.Finance`** > **汽車保險**。 選取自動保險續約&#x200B;**互動式通訊**&#x200B;並按一下&#x200B;**開啟代理程式UI**。 互動式通訊會在Agent UI中開啟。 輸入有效的電子郵件地址，這樣他們就可以收到附加原則檔案的電子郵件，然後按一下[提交]。

您可以直接從`https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`存取及檢視「汽車保險續約」互動式通訊

### Sarah收到來自`We.Finance`的保單續約通訊並決定續約 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封包含`We.Finance`附件的電子郵件，提醒Sarah她的汽車保險單即將到期。 附件為Sarah汽車保險信函的列印版本。

Sarah按一下&#x200B;**立即續約**&#x200B;選項，並導向至其汽車保險信函的網頁版本。 在此信件的頂端，Sarah會尋找原則中到期前的剩餘時間。 此頁面提供保單概要。 它詳細說明了保單編號、應付金額、折扣優惠和熟客獎勵等。 已按一下原則底部的&#x200B;**立即續約**。

![ref1](assets/ref1.png)

#### 運作方式 {#how-it-works}

您的汽車保險信函的網頁和列印輸出是使用互動式通訊的多通道功能建立的。

電子郵件中的「立即續訂」按鈕連結至「自動保險續訂」應用程式，這是發佈執行個體上的互動式通訊。

#### 親眼看看 {#see-it-yourself-1}

您必須已收到附有PDF的電子郵件。 PDF是汽車保險信函的列印版本。 按一下[立即續約] **&#x200B;**&#x200B;以存取原則的Web版本。 檢查您的個人資訊和原則詳細資料，然後按一下[立即續約]&#x200B;**&#x200B;**，即可讓您進入另一個互動式通訊。

電子郵件中的「**立即續約**」按鈕會將Sarah導向網頁上的原則。 您可以造訪下列URL：

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

您可以檢視車險續約的詳細摘要，然後按一下頁面底部的&#x200B;**立即續約**。

### Sarah到達付款頁面 {#sarah-reaches-the-payment-page}

`We.Finance`網站會將Sarah帶往「付款」頁面。 Sarah會用記錄重新檢查其原則號碼和到期日。 在頁面的右側，Sarah會檢查續約的付款摘要，並在總金額上提供10%的溢價折扣。

#### 運作方式 {#how-it-works-1}

「立即續約」按鈕會將Sarah導向付款頁面。 付款頁面為最適化表單。

#### 親眼看看 {#see-it-yourself-2}

按一下[立即續約] **&#x200B;**&#x200B;以存取付款頁面。 填寫您的信用卡資訊，然後按一下&#x200B;**付款**。

您可以在撰寫執行個體中前往付款頁面

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah進行付款並完成程式 {#sarah-makes-the-payment-and-completes-the-process}

Sarah填寫信用卡詳細資料，然後按一下&#x200B;**付款**。

#### 運作方式 {#how-it-works-2}

當Sarah填寫信用卡詳細資料並按一下「提交」時，系統就會處理其信用卡付款，且畫面上會顯示以最適化表單設定的感謝訊息。

#### 親眼看看 {#see-it-yourself-3}

您可以按一下「付款」，然後檢視確認訊息。

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
