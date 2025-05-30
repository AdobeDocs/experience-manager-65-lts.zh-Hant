---
title: 設定LDAP繫結密碼
description: 瞭解在將設定檔案匯入其他系統之前，如何設定繫結密碼欄位。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 33e0f81f-7867-4c59-a9e5-75bf5182a27c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 設定LDAP繫結密碼{#configure-the-ldap-bind-password}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

為避免安全風險，未設定匯出的組態檔(config.xml)中的繫結密碼欄位。 在將組態檔案匯入其他系統之前，請確定您設定此密碼。 此密碼會覆寫儲存在資料庫中的現有密碼。 Null密碼不會覆寫現有的非Null密碼值。

1. 在管理控制檯中，按一下「設定」>「使用者管理」>「組態」>「匯入和匯出組態檔」。
1. 若要將目前的組態設定匯出至檔案，請按一下「匯出」並將組態檔案儲存在其他位置。
1. 在檔案中，找到`Domains` > *[您的網域名稱]* > `DirectoryConfigs` > `LDAPGroupConfig`節點。 範例如下：

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   輸入`bindpassword`的值並儲存變更。

1. 在檔案中，找到`Domains` > *[您的網域名稱]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`節點。 範例如下：

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   輸入`bindpassword`的值並儲存變更。

1. 若要匯入更新的檔案，請在「使用者管理」中按一下「組態」>「匯入及匯出組態檔」。
1. 按一下「瀏覽」尋找檔案，按一下「匯入」，然後按一下「確定」。
