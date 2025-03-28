---
title: 設定PDFG網路印表機（僅限Windows）
description: 瞭解如何設定PDFG網路印表機（僅限Windows ）
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 6e9c42d9-fb1d-432b-95b9-6e21706b2a3e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# 設定PDFG網路印表機（僅限Windows） {#setting-up-a-pdfg-network-printer-windows-only}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

PDFG網路印表機可讓使用者從任何支援列印的應用程式產生PDF檔案。 使用者安裝PDFG網路印表機後，名為&#x200B;*PDF產生器*&#x200B;的新印表機會出現在Windows控制檯的「印表機」區段中。 如果已有同名的印表機存在，系統會提示使用者提供其他名稱。

從任何應用程式列印到這台印表機都會將檔案以PostScript格式傳送到PDF Generator，會將PostScript檔案轉換為PDF。 它會將PDFPDF檔案作為電子郵件訊息的附件傳送給使用者，將PDF Generator檔案轉送給指定的AEM表單服務或程式，或執行這兩種動作，端視您的設定而定。

設定PDFG網路印表機時，必須執行下列步驟：

1. 設定電子郵件設定。 （請參閱[設定PDFG網路印表機的電子郵件設定](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)。）
1. 在管理主控台中，設定PDFG網路印表機設定。 （請參閱[設定PDFG網路印表機設定](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)。）
1. 確定已在AEM表單資料庫中為使用者設定了有效的電子郵件地址，並將PDFGUserPermission指派給每位使用者。<!-- Fix broken link See Setting up and organizing users -->
1. 請確認使用者的電腦上已安裝32位元JRE6。
1. 在您的使用者電腦上安裝印表機。 （請參閱[在使用者電腦上安裝PDFG網路印表機](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)。）

## 設定PDFG網路印表機的電子郵件設定 {#configure-email-settings-for-pdfg-network-printer}

1. 在Administration Console中，按一下「服務>應用程式和服務>服務管理」。
1. 在「服務管理」頁面中，按一下provider.email_sendmail_service，指定SMTP設定值，然後按一下「儲存」。

## 設定PDFG網路印表機設定 {#configure-the-pdfg-network-printer-settings}

1. 在管理控制檯中，按一下「服務> PDF Generator > PDFG網路印表機」
1. 在Adobe PDF設定和安全性設定清單中，選取要套用至產生的PDF的選項。 如需這些設定的詳細資訊，請參閱[設定Adobe PDF設定](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings)和[設定安全性設定](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)。
1. 若要將轉換的PDF傳回給使用者，請選取「將轉換的PDF檔案以電子郵件寄回給使用者」選項，並指定下列資訊：

   * 用於傳送PDF給使用者的電子郵件地址
   * 電子郵件訊息的主旨
   * 電子郵件訊息的頁首、正文和頁尾。 在電子郵件訊息中，&lt;receiverName>會取代為列印檔案之使用者的全名。

1. 若要將轉換的PDF傳送至AEM表單服務或程式，請選取將轉換的PDF轉寄至指定的AEM表單服務或程式選項，並指定下列資訊：

   * 要叫用的服務名稱
   * 要叫用的服務之作業的名稱
   * 輸入引數的名稱，如服務或程式的component.xml檔案中所指定。 PDF檔案會作為該輸入引數的值使用。

1. 按一下「儲存」。

如果要還原成原始的預設電子郵件文字，請按一下[還原電子郵件內容]。

## 在使用者的電腦上安裝PDFG網路印表機 {#install-pdfg-network-printer-on-a-user-s-computer}

具有PDFG管理員或PDFG使用者角色的使用者可以安裝PDFG網路印表機。 電腦上必須安裝32位元JDK。

1. （PDFG管理員）在Administration Console中，按一下「服務> PDF Generator > PDFG網路印表機」。

   （PDFG使用者）移至`http(s)://[host]:'port'/pdfgui`，然後按一下「PDFG網路印表機安裝」下的連結。

1. 在「PDFG網路印表機安裝」下，按一下連結。 提示輸入使用者帳戶資訊時，請指定您在步驟1用來登入的使用者名稱和密碼。 會出現訊息，指出印表機已成功安裝。

   ***注意&#x200B;**：如果使用者密碼變更，使用者必須在電腦上重新安裝PDFG網路印表機。 您無法從管理主控台更新密碼。*

1. 按一下「確定」。
