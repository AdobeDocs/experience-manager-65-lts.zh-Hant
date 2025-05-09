---
title: 介紹Java&amp；trade； API QuickStart
description: 瞭解如何使用AEM Forms Java&amp；trade；以SOAP連線啟用的強型別API來執行AEM Forms作業。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: a5ae164d-d0c0-40d0-baeb-0e646fc71f55
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Java™ API快速入門簡介 {#introducing-java-api-quickstart}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

Adobe AEM Forms API快速入門可幫助您加速開發與AEM Forms服務互動的程式。 *快速入門*&#x200B;是完整的程式，您可以將其複製並貼到您自己的專案中，並作為起點。 您可以執行快速入門，瞭解其行為方式，並根據您自己的需求進行修改。

AEM Forms作業可使用AEM Forms強型別API執行，且連線模式應設為SOAP。

Java™強型別API快速入門提供執行Java™應用程式所需的JAR檔案清單。 大部分的Java™快速入門都是在`main`內執行的主控台應用程式。 不過，Forms Java™強型別API快速入門是在Web應用程式中執行的Java™ servlet。

JAR檔案清單位於「快速入門」開頭的註解區段中。 例如，以下註解位於「輸出」快速入門中，並且是在每個Java™快速入門中找到的典型JAR檔案清單。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## 多項服務快速入門 {#multiple-services-quick-start}

在JEE上使用AEM Forms *進行*&#x200B;程式設計時最快速啟動會叫用特定服務來執行作業。 不過，有些快速入門會叫用多個AEM Forms服務來執行指定的工作流程。 下列清單提供叫用多個AEM Forms服務的Java™快速入門：

[快速入門(SOAP模式)：使用Java™ API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)將AEM Forms存放庫中的檔案傳遞至輸出服務（叫用存放庫和輸出服務）

[快速入門(SOAP模式)：使用Java™ API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)根據片段建立PDF檔案（叫用組合器及輸出服務）

[快速入門(SOAP模式)：使用Java™ API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)建立包含已提交XML資料的PDF檔案(叫用Forms、輸出和檔案管理服務)

[快速入門(SOAP模式)：使用Java™ API將檔案傳遞至Forms服務](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (叫用Forms和檔案管理服務)

[快速入門(SOAP模式)：使用Java™ API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api)數位簽署XFA式表單(叫用Forms和簽名服務)

[快速入門(SOAP模式)：使用Java™ API](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)管理角色和許可權（叫用DirectoryManager和AuthorizationManager服務）

[快速入門(SOAP模式)：使用Java™ API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)將檔案傳遞至輸出服務（叫用輸出和檔案管理服務）

>[!NOTE]
>
>使用AEM Forms進行程式設計的快速入門是以部署在JBoss®應用程式伺服器和Microsoft® Windows®作業系統上的AEM Forms為基礎。 不過，如果您使用其他作業系統(例如UNIX®)，請將Windows特定路徑取代為適用作業系統支援的路徑。 同樣地，如果您使用其他J2EE應用程式伺服器，請確定您指定有效的連線屬性。 （請參閱[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）

>[!NOTE]
>
>大部分的Web服務快速入門都是以C#撰寫並使用.NET Framework。 不過，您可以建立使用者端應用程式邏輯，以便能夠在支援AEM Forms標準的任何開發環境中叫用SOAP服務。 (請參閱[使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)。)
