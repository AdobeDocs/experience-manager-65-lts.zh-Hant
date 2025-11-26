---
title: Adobe Experience Manager Forms 6.5 LTS SP1 Hotfix
description: 提供如何下載和安裝AEM Forms 6.5 LTS的Hotfix的相關資訊。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: bb270a983d9d3f7d116a179886daf763e7e2341e
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---


# Adobe Experience Manager Forms 6.5 LTS Hotfix{#aem-form-hotfix}

本文列出為解決已知問題、改善系統穩定性及增強AEM Forms 6.5 LTS整體效能而實作的重大修正。

>[!NOTE]
>
> 這些Hotfix的設計是累積性的，包含所有先前的修正。 將最新Hotfix套用至某個版本時，不僅可解決最近的問題，還可整合所有先前的錯誤修正和增強功能。

## AEM Forms 6.5 LTS的Hotfix {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日期</strong></td>
    <td><strong>Hotfix下載連結(AEM Software Distribution連結)</strong></td>
    <td><strong>已修正的問題</strong></td>
  </tr>
  <tr>
    <td>
      <strong>2025年9月9日</strong><br>
    <td>
    <ul>
    <li>Windows - Windows上的AEM Service Pack 6.5 LTS的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-win-pkg-6.1.176-RHF-002.zip">Hotfix2</a></li>
    <li>Linux- Linux上適用於AEM Service Pack 6.5 LTS的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]hotfix-on-add-on/adobe-aemfd-linux-pkg-6.1.176-RHF-002.zip">Hotfix2</a></li>
     <li>OSX- OSX<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.1.176-RHF-002.zip">上AEM Service Pack 6.5 LTS的</a>Hotfix2</li>
    <td>
    <ul>
    <li>解決啟用伺服器端驗證(SSV)時提交作業可能失敗的問題，提升表單提交的可靠性如果您遇到任何問題，請聯絡[Adobe Experience Manager Forms支援](https://business.adobe.com/in/support/main.html)
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## 下載並安裝OSGi Hotfix {#download-install-hotfix}

執行以下步驟來下載及安裝Hotfix：

1. 從Software Distribution連結下載[Hotfix](#hotfix-for-adaptive-forms)。
1. 解壓縮Hotfix封存檔案，以便取得Experience Manager套件(.zip)和套件(.jar)檔案。
1. 透過[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)上傳及安裝封裝(.zip)。
1. 開啟設定管理員組合`https://server:host/system/console/bundles`，上傳並安裝組合(.jar)。 已安裝Hotfix。
