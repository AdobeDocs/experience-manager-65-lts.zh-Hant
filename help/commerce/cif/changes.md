---
title: Commerce integration framework (CIF)附加元件重大變更
description: 與舊版CIF相比，Commerce integration framework (CIF)附加元件有重大變更。
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: aced89a0-dec1-49fe-afbc-3ddf1318b900
source-git-commit: 79cce324382bada2e9aec107b8e494723bf490e9
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Commerce integration framework (CIF)附加元件的重大變更{#notable-changes}

本檔案著重說明Commerce integration framework (CIF)附加元件與舊版CIF (主要稱為CIF Classic (Quickstart)和CIF開放原始碼)之間的重要差異。

## 安裝與更新

AEM CIF附加元件套件會透過AEM Package Manager安裝及更新。

**舊版CIF**

* CIF Classic：不需要安裝，CIF是快速入門的一部分。 CIF更新是定期AEM或Service Pack更新的一部分
* CIF開放原始碼：透過GitHub安裝。 更新是手動更新/維護工作的一部分。

## 端點設定

端點會透過OSGi主控台進行設定。

**舊版CIF**

* CIF Classic：透過AEM中的OSGi設定
* CIF開放原始碼：透過CIF設定瀏覽器

## 部署CIF Venia專案

[GitHub AEM Guides - CIF Venia專案](https://github.com/adobe/aem-cif-guides-venia)上可用的專案，以及透過AEM封裝管理員完成的部署。

**舊版CIF**

* CIF Classic：透過AEM套件安裝

## 產品目錄資料

透過對支援必要GraphQL API的外部端點的即時呼叫，可隨選要求產品目錄資料。 這些API支援在任何指定日期存取即時或分階段資料。 不需要復寫。

**舊版CIF**

* CIF Classic：透過完整或差異產品匯入，即時和階段產品資料會匯入並儲存在AEM Author上的JCR中。 即時產品資料會復寫到AEM Publish。

## 具有AEM轉譯的產品目錄體驗

AEM會使用已指派給產品和類別的AEM目錄範本，即時呈現產品目錄體驗。 不需要復寫。

**舊版CIF**

* CIF Classic： AEM Author會使用目錄Blueprint工具，為每個類別/產品建立AEM頁面。 這些頁面會復寫到AEM Publish。

>[!NOTE]
>
>如需如何將CIF與AEM Managed Service或AEM On-Premise搭配使用的其他檔案，請參閱[Commerce integration framework](https://developer.adobe.com/apis/experiencecloud/commerce-integration-framework/getting-started.html)
