---
title: 程式碼陷阱
description: 為AEM開發時應避免的常見編碼陷阱
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 95656312-2648-455e-80fb-3e03bf1cd633
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 程式碼陷阱{#code-pitfalls}

## 避免Java程式碼中的Sling繫結 {#avoid-sling-bindings-in-java-code}

在90%的情況下，使用Sling繫結是不合適存取服務的方式。 您應該改用&#x200B;*@Reference*&#x200B;或&#x200B;*@Inject*&#x200B;註解。

## 避免Java程式碼中的Thread.interrupt {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt*&#x200B;很危險，因為它可以在錯誤時間呼叫時關閉檔案，包括Lucene檔案和持續快取檔案。

## 避免將Java同步與ReadWriteLocks混合 {#avoid-mixing-java-synchronization-with-readwritelocks}

這可能會導致程式碼最終鎖定的競爭條件。
