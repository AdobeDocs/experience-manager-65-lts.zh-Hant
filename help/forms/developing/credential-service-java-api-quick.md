---
title: 認證服務Java&amp；trade； API QuickStart(SOAP)
description: 瞭解如何使用Java&amp；trade； API快速入門(SOAP)在AEM Forms中匯入和刪除認證。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
hide: true
hidefromtoc: true
exl-id: 7314fbae-05af-423d-92c8-f8c608048956
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 認證服務Java™ API快速入門(SOAP) {#credential-service-java-api-quickstart-soap}

Java™ API快速入門(SOAP)可用於認證服務。

[快速入門(SOAP模式)：使用Java匯入認證](credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[快速入門(SOAP模式)：使用Java刪除認證](credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

AEM Forms作業可使用AEM Forms強型別API執行，且連線模式應設為SOAP。

>[!NOTE]
>
>使用AEM表單進行程式設計的快速入門是根據在JBoss®和Windows作業系統上部署的Forms伺服器。 不過，如果您使用其他作業系統(例如UNIX®)，請將Windows特定路徑取代為適用作業系統支援的路徑。 同樣地，如果您使用其他J2EE應用程式伺服器，請確定您指定有效的連線屬性。 請參閱[設定連線內容](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

>[!NOTE]
>
>您無法使用Web服務執行認證服務作業。

## 快速入門(SOAP模式)：使用Java™ API匯入認證 {#quick-start-soap-mode-importing-credentials-using-the-java-api}

下列程式碼範例會根據名為&#x200B;*cred.p12*&#x200B;的檔案匯入認證。 用來匯入認證的別名值為`Secure`。 （請參閱[使用信任管理員API匯入認證](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。）

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-truststore-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.truststore.client.CredentialServiceClient;
 
 public class ImportCredentialSoap {
 
     public static void main(String[] args) {
            try {
 
          //Set connection properties required to invoke AEM Forms using SOAP mode
              Properties connectionProps = new Properties();
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a CredentialServiceClient instance
             CredentialServiceClient certClient = new CredentialServiceClient(myFactory);
 
             //Reference a credential based on a P12 file
             FileInputStream myCred = new FileInputStream("C:\\Adobe\cred.p12");
             Document credential = new Document(myCred);
 
             //Create a string array to store usage values
             String[] usage = new String[1];
             usage[0] = "truststore.usage.type.sign";
 
             //Import the credential
             certClient.importCredential("secure",credential,"password",usage);
             System.out.println("Credential was uploaded");
 
            }catch (Exception e) {
                e.printStackTrace();
            }
 
            }
 }
 
 
 
```

## 快速入門(SOAP模式)：使用Java™ API刪除認證 {#quick-start-soap-mode-deleting-credentials-using-the-java-api}

下列程式碼範例會根據別名值&#x200B;*secure*&#x200B;刪除認證。 （請參閱[使用信任管理員API](/help/forms/developing/credentials.md#deleting-credentials-by-using-the-trust-manager-api)刪除認證。）

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-truststore-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 
 import java.util.Properties;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.truststore.client.CredentialServiceClient;
 
 public class DeleteCertificateSoap {
 
 
     public static void main(String[] args)
     {
     try {
 
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a CredentialServiceClient instance
         CredentialServiceClient certClient = new CredentialServiceClient(myFactory);
 
         //Delete the certificate
         certClient.deleteCredential("secure");
         System.out.println("Credential was deleted");
 
        }catch (Exception e) {
            e.printStackTrace();
        }
 
        }
 
 }
 
```
