---
title: 停用適用於JEE和OSGI之PDFG設定的UAC
description: 瞭解如何針對PDFG設定停用UAC以修正Word到PDF轉換的步驟。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 55f5d3bb-2a6f-4fac-9d33-7b39e4ca317f
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# 無法在Windows Server上將Word或Excel檔案轉換為PDF {#unable-to-convert-word-excel-files-PDF}

## 問題 {#issue}

當使用者嘗試在Microsoft® Windows Server上將Word或Excel檔案轉換成PDF時，會發生下列錯誤：

*來自主要轉換器的錯誤訊息：*
*ALC-PDG-015-003 — 系統無法開啟輸入檔。 再次提交您的檔案或連絡您的系統管理員。*


## 解決方案 {#solution}

請執行下列動作：

1. 若要存取系統組態公用程式，請移至&#x200B;**[!UICONTROL 開始>執行]**，然後輸入&#x200B;**[!UICONTROL MSCONFIG]**。
1. 按一下&#x200B;**[!UICONTROL 工具]**&#x200B;標籤，然後向下捲動並選取&#x200B;**[!UICONTROL 變更UAC設定]**。 按一下&#x200B;**[!UICONTROL 啟動]**，以便在新視窗中執行命令。
1. 將滑桿調整為「永不通知」等級。 完成後，關閉命令視窗並關閉「系統組態」視窗。
1. 確認UAC的登入設定設為0 （零）。 執行以下步驟以進行驗證：

   1. Microsoft®建議您在修改登入之前先備份登入。 如需詳細步驟，請參閱[如何在Windows](https://support.microsoft.com/en-us/help/322756)中備份及還原登入。
   1. 開啟Microsoft® Windows登入編輯器。 若要開啟登入編輯程式，請前往[開始] > [執行]，輸入regedit，然後按一下[確定]。
   1. 瀏覽至`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。 請確定EnableLUA的值設為0 （零）。
   1. 請確定&#x200B;**EnableLUA**&#x200B;的值設為0 （零）。 如果值不是0，請將值變更為0。 關閉登錄編輯程式。

1. 重新啟動電腦。

## 套用至 {#appliesto}

此解決方案適用於JEE伺服器上的AEM Forms和OSGi伺服器上的AEM Forms 。
