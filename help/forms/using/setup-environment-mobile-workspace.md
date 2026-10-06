---
title: 設定AEM Forms應用程式的環境
description: 建置和部署AEM Forms應用程式的硬體、軟體和授權。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
exl-id: 41799183-ef5a-4990-bd7b-7b58cafe3960
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2b710c6ef8d291a42b4a7658bf84f5e764422d5c
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%
---
# 設定AEM Forms應用程式的環境{#set-up-environment-for-aem-forms-app}

>[!NOTE]
>
>AEM Forms應用程式的Android和iOS版本已停止服務。 Android應用程式已於2026年9月從Google Play取消發佈，且iOS應用程式已從Apple App Store中移除。
>這些應用程式已無法供安裝。 如需Android應用程式的協助，請連絡[aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)。

您需要下列硬體、軟體和授權，才能建置和部署AEM Forms應用程式：

## Windows裝置 {#for-windows-devices}

* ® Windows 10
* ® Visual Studio 2015
* ® Visual Studio Tools for Apache Cordova

## 適用於iOS裝置 {#for-ios-devices}

* 執行macOS X 10.9.5或更新版本的Intel型Apple Mac
* iOS SDK 8.4或更新版本
* Xcode版本：適用於OS X或更新版本的Xcode 6.4
* iOS開發人員企業計畫會籍
* 用於發佈內部iOS應用程式的企業憑證
* Apple iPad搭配iOS 8.4或更新版本

## 若為™裝置 {#for-android-devices}

* 可從[https://developer.android.com/studio](https://developer.android.com/studio)下載的Android™ Development Toolkit （ADT套件）
* 若環境設定在Mac系統上，則ADT應安裝在「應用程式」資料夾中。
* 如果ADT安裝在Mac上的任何其他位置，或環境設定在Windows系統上，則必須在`local.properties`檔案中更新ADT SDK路徑。 此檔案位於已解壓縮來源封存檔`mobileworkspace-src.zip`的`src\android`資料夾中。 在此檔案中，將`sdk.dir`變數指向案頭上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。 請確定未預先安裝PhoneGap SDK。
