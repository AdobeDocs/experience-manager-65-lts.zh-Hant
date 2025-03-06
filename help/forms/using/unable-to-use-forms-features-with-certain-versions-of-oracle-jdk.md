---
title: 無法搭配特定版本的Experience Manager Forms JDK使用Oracle
description: 無法搭配特定版本的Experience Manager Forms JDK使用Oracle
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 4aa45f02-ff89-4e40-a15d-e62c5879a87d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---

# 無法搭配特定版本的Experience Manager Forms JDK使用Oracle {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

此問題適用於下列版本：

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## 問題 {#issue}

使用者遇到下列例外狀況：
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 原因 {#reason}

當您使用Oracle JDK （Java開發套件）版本高於或等於下列版本執行Experience Manager Forms時，會發生例外情況：

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

上述和更新版本的Java包括JVM （Java虛擬機器器）中的新XML處理限制，這會造成某些Forms特定作業失敗。

## 因應措施 {#workaround}

1. 停止您的Experience Manager Forms伺服器。
1. 為您的應用程式伺服器設定下列JVM引數：

   `-Djdk.xml.xpathExprOpLimit=2000`

   它會將JVM中的系統屬性設定為相當高的值，這樣就不會達到預設限制。

1. 啟動您的Experience Manager Forms伺服器。
