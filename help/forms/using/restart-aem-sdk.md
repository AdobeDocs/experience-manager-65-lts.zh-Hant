---
title: 如何重新啟動AEM SDK？
description: 重新啟動AEM SDK的最佳做法
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
exl-id: 68935045-89b1-4219-b111-88a4600200df
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# 重新啟動AEM SDK

如果您藉由停止Java™程式來重新啟動AEM SDK，可能會導致AEM開發環境不一致，並出現下列錯誤：

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![重新啟動 — aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## 解決方案

若要重新啟動AEM SDK，請移至使用中命令視窗並按`Ctrl + C`命令以重新啟動SDK。

建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK (例如停止Java™程式)，可能會導致AEM開發環境不一致。
