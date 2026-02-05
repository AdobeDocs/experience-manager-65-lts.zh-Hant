---
title: 整合建立通訊解決方案與您的自訂入口網站
description: 瞭解如何將建立通訊UI與您的自訂入口網站整合
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 496b125b-b091-4843-ba9f-2479dbeba07b
source-git-commit: 16f57ae1663f035d1dc39005d37426c7a0d8dc16
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 4%

---

# 將`Create Correspondence`解決方案與您的自訂入口網站整合{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概觀 {#overview}

本文詳細說明如何將`Create Correspondence`解決方案與您的環境整合。

## URL型引動過程 {#url-based-invocation}

從自訂入口網站呼叫`Create Correspondence`應用程式的一種方法是，使用下列要求引數準備URL：

* 信函範本的識別碼（使用cmLetterId引數）。

* 從所需資料來源擷取的XML資料的URL （使用cmDataUrl引數）。

例如，自訂入口網站會將URL準備為\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`，可能是入口網站連結中的href。

>[!NOTE]
>
>以這種方式呼叫並不安全，因為必要的引數會隨著GET要求傳遞，在URL中公開相同的（明顯可見）。

>[!NOTE]
>
>在呼叫`Create Correspondence`應用程式之前，儲存並上傳資料以在指定的dataURL呼叫`Create Correspondence` UI。 此程式可以從自訂入口網站本身或透過另一個後端程式完成。

## 內嵌資料型引動過程 {#inline-data-based-invocation}

另一個更安全的呼叫`Create Correspondence`應用程式的方法是前往位於https://&#39;[伺服器]：[連線埠]&#39;/[contextPath]/aem/forms/createcorrespondence.html的URL。 傳送引數和資料時執行此URL以以POST要求形式呼叫`Create Correspondence`應用程式，對一般使用者隱藏它們。 此工作流程也表示您現在可以傳遞`Create Correspondence`應用程式內嵌的XML資料（作為相同請求的一部分，使用`cmData`引數）。 此工作流程在先前的方法中不可能或理想。

### 指定字母的引數 {#parameters-for-specifying-letter}

| **名稱** | **類型** | **說明** |
| --- | --- | --- |
| cmLetterInstanceId | 字串 | 信件例項的識別碼。 |
| cmLetterId | 字串 | 信函範本的名稱。 |

表格中引數的順序會指定用來載入字母的引數偏好設定。

### 用於指定XML資料來源的引數 {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td> 
   <td><strong>類型</strong></td> 
   <td><strong>說明</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>來自使用基本通訊協定（例如cq、ftp、http或檔案）之來源檔案的XML資料。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>字串</td> 
   <td>使用信件例項中可用的xml資料。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>布林值</td> 
   <td>重複使用資料字典中附加的測試資料。</td> 
  </tr>
 </tbody>
</table>

表格中引數的順序會指定用來載入XML資料的引數偏好設定。

### 其他引數 {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td> 
   <td><strong>類型</strong></td> 
   <td><strong>說明</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>布林值</td> 
   <td>True表示在預覽模式中開啟字母<br /> </td> 
  </tr>
  <tr>
   <td>隨機</td> 
   <td>時間戳記</td> 
   <td>解決瀏覽器快取問題。</td> 
  </tr>
 </tbody>
</table>

如果您使用`cmDataURL`的http或cq通訊協定，則`http/cq`的URL必須可匿名存取。
