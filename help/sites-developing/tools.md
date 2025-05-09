---
title: 測試和追蹤工具
description: AEM提供測試元件UI的架構，以及測試和偵錯元件的機制
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4aa0f10d-e915-4ad2-a886-080ed8b9b10f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# 測試和追蹤工具{#testing-and-tracking-tools}

## 測試 {#testing}

AEM提供：

* [測試元件UI](/help/sites-developing/hobbes.md)的架構。
* [測試和偵錯元件的機制](/help/sites-developing/developer-mode.md)。

以下是兩個開啟的Source測試工具：

**Selenium**

Selenium可用於瀏覽器中的功能測試，每個活動有一個使用者。 測試步驟（點按）會記錄為HTML表格或Java™類別。

如需詳細資訊，請參閱[https://www.selenium.dev/](https://www.selenium.dev/)。

**JMeter**

JMeter可用來追蹤要求，以及進行功能、效能和壓力測試。

如需詳細資訊，請參閱[https://jmeter.apache.org/](https://jmeter.apache.org/)。

還有許多自動化測試和管理測試計畫的專有工具。

### 追蹤 {#tracking}

您可輕鬆使用下列工具。 不過，所有案例中的關鍵問題是專案團隊的所有成員（合作夥伴和客戶）都能取得資料。

**Bugzilla**

可依您自己的需求設定的錯誤追蹤系統。

**試算表**

雖然不是特別用於錯誤追蹤工具，但試算表經常會被&#x200B;*誤用*&#x200B;以用於此目的，因為這些試算表很容易理解，而且大部分使用者都有其功能的經驗。

如果這些試算表用於追蹤，則：

* 這些步驟應保持簡單。
* 個別試算表的數目應維持在最低限度。
* 必須定期更新。
* 只應維護一個主要副本，且每個人都應知道主要副本的位置。
* 所有專案成員都應該可存取這些檔案。
* 如果安全性是個問題（通常發生在大公司），且無法進行一般存取，則只要每個人都知道這些試算表是副本且無法更新，就可以分發副本。

同樣地，也有許多追蹤錯誤和功能要求的專有工具。
