---
title: 在Windows Vista上設定SSL
description: 瞭解如何在Windows Vista上設定SSL。 使用並執行Java Keytool來產生包含RSA金鑰的SSL憑證以進行驗證。
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ee73f6a1-712c-461f-95e8-85f8c5694293
source-git-commit: d0f29cb177e98315cd50c2d7e96c3605eec14885
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 在Windows Vista上設定SSL {#configuring-ssl-on-windows-vista}

若要在Windows Vista™上設定SSL，您需要具有RSA金鑰的SSL憑證以進行驗證。 您可以使用Java keytool來建立憑證。

>[!NOTE]
>
>Windows Vista無法搭配DSA金鑰使用。

您可以使用單一命令執行keytool，該命令包含建立憑證和金鑰存放區所需的所有資訊。

**建立SSL憑證**

1. 在命令提示字元中，瀏覽至&#x200B;*`[JAVA HOME]`*/bin並輸入下列命令以建立憑證和金鑰存放區：

   `keytool -genkey -keyalg RSA -dname "CN=`*主機名稱* `, OU=`*群組名稱* `, O=`*公司名稱* `,L=`*城市名稱* `, S=`*州別* `, C=`*國碼* `" -alias`*&quot;LC憑證&quot;* `-keypass` `key`*_* *密碼* `-keystore`*金鑰重新命名* `.keystore`

   >[!NOTE]
   >
   >將&#x200B;*`[JAVA_HOME]`取代為安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。*

1. 鍵入`changeit`作為密碼。 此密碼是Java安裝的預設密碼，系統管理員可能已變更此密碼。
