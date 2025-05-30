---
title: 設定遠端端點
description: 瞭解如何設定遠端端點。 本檔案說明如何啟用以Flex建立的應用程式，以使用AEM表單遠端功能來叫用服務。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: d19b7265-42cc-41d9-9897-e7b044c4529c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# 設定遠端端點 {#configuring-remoting-endpoints}

遠端端點可讓以Flex建立的應用程式使用(AEM表單已棄用) AEM表單遠端來叫用服務。 系統會自動為每個啟用的服務建立遠端端點。 會建立與端點同名的Flex目的地，而Flex使用者端可建立指向此目的地的遠端物件，以叫用相關服務的作業。

## 遠端端點設定 {#remoting-endpoint-settings}

**Flex使用者端驗證方法：**&#x200B;決定當所叫用的服務已啟用安全性、叫用的作業不支援匿名叫用，且使用者端傳入的認證無效或無效時，伺服器傳回給使用者端的回應型別。
