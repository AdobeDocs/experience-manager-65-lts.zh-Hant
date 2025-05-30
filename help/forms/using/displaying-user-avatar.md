---
title: 顯示使用者頭像
description: 如何自訂AEM Forms工作區以顯示登入使用者的影像。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 0c72fe67-13da-4eac-8cd6-8699e546f8f4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 顯示使用者頭像 {#displaying-the-user-avatar}

登入使用者的頭像會顯示在AEM Forms工作區的右上角。 此外，組織階層中直接下屬的頭像會顯示在「經理檢視」中。 您可以設定AEM Forms工作區，以便從您的資料庫（例如LDAP伺服器）中挑選使用者影像。

>[!NOTE]
>
>支援的使用者影像外觀比例為1:1。

1. 使用下個步驟中所述的詳細資訊，建立DSC。 如需詳細資訊，請參閱[使用AEM Forms程式設計](https://www.adobe.com/go/learn_aemforms_programming_63)指南中的「為AEM Forms開發元件」主題。
1. 在DSC中，定義新的SPI，公開getCurrentUserImageUrl和getUserImageUrl方法，以取得AEM Forms使用者的影像URL。 以下是範例Java™程式碼片段：

   ```java
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. 建立component.xml檔案。 請確定spec-id如下面的程式碼片段所示。

   下列程式碼片段為範例。 根據您的特定需求加以自訂。

   ```java
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. 透過Workbench部署DSC。 重新啟動`ProcessManagementClientSessionService`服務。
1. 您可能需要重新整理瀏覽器，或再次登出/登入使用者。
