---
title: 使用Classic UI建立語言根
description: 瞭解如何使用Classic UI在Adobe Experience Manager中建立語言根。
contentOwner: Guillaume Carlino
feature: Language Copy
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: c6e00da5-804f-46cf-b7a9-52e667574394
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# 使用Classic UI建立語言根{#creating-a-language-root-using-the-classic-ui}

下列程式使用傳統UI建立網站的語言根。 如需詳細資訊，請參閱[建立語言根](/help/sites-administering/tc-prep.md#creating-a-language-root)。

1. 在「網站」主控台的「網站」樹狀結構中，選取網站的根頁面。 ([http://localhost:4502/siteadmin#](http://localhost:4502/siteadmin#))
1. 新增代表網站語言版本的子頁面：

   1. 按一下「新增>新增頁面」。
   1. 在對話方塊中，指定「標題」和「名稱」。 名稱必須是`<language-code>`或`<language-code>_<country-code>`的格式，例如en、en_US、en_us、en_GB、en_gb。

      * 支援的語言代碼是由ISO-639-1定義的小寫、雙字母代碼
      * 支援的國家代碼是小寫或大寫、雙字母代碼，如ISO 3166所定義

   1. 選取範本，然後按一下「建立」。

   ![newpagefr](assets/newpagefr.png)

1. 在「網站」主控台的「網站」樹狀結構中，選取網站的根頁面。
1. 在「工具」功能表中，選取「語言複製」。

   ![toolslanguagecopy](assets/toolslanguagecopy.png)

   「語言複製」對話方塊會顯示可用語言版本和網頁的矩陣。 語言欄中的x表示頁面可以使用該語言。

   ![languagecopydialog](assets/languagecopydialog.png)

1. 若要將現有頁面或頁面樹狀結構複製到語言版本，請在語言欄中選取該頁面的儲存格。 按一下箭頭並選取要建立的複製型別。

   在下列範例中，裝置/太陽鏡/愛爾蘭頁面正在複製到法文版本。

   ![languagecopydilogdropdown](assets/languagecopydilogdropdown.png)

   | 語言副本型別 | 描述 |
   |---|---|
   | 自動 | 使用上層頁面的行為 |
   | 忽略 | 不會建立此頁面及其子頁面的復本 |
   | `<language>+` （例如French+） | 從該語言複製頁面及其所有子項 |
   | `<language>` （例如，法文） | 僅複製該語言的頁面 |

1. 按一下「確定」關閉對話方塊。
1. 在下一個對話方塊中，按一下「是」以確認複製。
