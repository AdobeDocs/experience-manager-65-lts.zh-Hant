---
title: 要求分析指令碼
description: 製作request analysis指令碼是為了便於分析access.log檔案，產生可讀報告以供日後處理
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 9fe575ad-1e8d-460f-a933-ddc2e927a6e8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# 要求分析指令碼{#request-analysis-script}

## 下載 {#download}

編寫此指令碼是為了方便分析`access.log`個檔案，產生可讀報告以供日後處理。

[取得檔案](assets/analyse-access.sh)

## 描述 {#description}

編寫此指令碼是為了方便分析`access.log`個檔案，產生可讀報告以供日後處理。

這會產生整體請求數、GET與POST、隨時間變化的請求分佈等等。

輸出為Markdown語法，因此將比較容易轉換成使用pandoc等工具的PDF，或在瀏覽器中使用Markdown檢視器等外掛程式顯示。

它可以分析命令列上提供的自訂路徑。

從檔案內告訴您如何執行的註解取得：

分析CQ `access.log`推斷各種資訊，並在`stdout`上產生Markdown輸出。

## 使用情況 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以提供其他自訂路徑，以便在命令列上分析

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

您可以使用簡單管路儲存輸出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
