---
title: 使用Document Security網頁
description: 瞭解如何登入、導覽及使用Document Security網頁。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 90628021-75cb-41f3-a5f7-66c4f1ed0f3a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 使用Document Security網頁 {#using-the-document-security-webpages}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

使用者和管理員可使用Document Security網頁來建立和管理原則、管理受原則保護的檔案，以及監控與受原則保護檔案關聯的事件。 管理員也可以使用這些網頁來建立原則集並指定原則集協調員、設定Document Security預設設定、管理受邀使用者註冊和帳戶，以及監視和管理伺服器、原則、使用者和檔案相關事件。

>[!NOTE]
>
>您也可以使用使用者登入帳戶，透過Acrobat和其他使用者端應用程式登入Document Security。 （請參閱[設定從使用者端應用程式](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)存取Document Security。）

若要開啟網頁，您需要瀏覽器和URL，以及您的Document Security登入資訊。 使用者的URL與管理員的URL不同。

由於Document Security會參考您組織的現有目錄以取得使用者資訊，因此您的Document Security登入資訊可能與您用來登入網路和其他應用程式的資訊相同。 請洽詢您的系統管理員或管理員，以取得您的帳戶資訊。

若要以管理員身分登入，您必須擁有指派給您的管理員角色。 您可以使用安裝過程中建立的預設超級管理員帳戶。

## 登入網頁 {#log-in-to-the-web-pages}

若要使用瀏覽器登入網頁，您需要Document Security URL和帳戶。 使用者的URL與管理員的URL不同。 管理員也可以登入使用者頁面來建立原則。

如果您擁有多個Document Security安裝的存取權，則需要您想要存取的Document Security執行個體的URL。 如果您沒有此資訊，請洽詢管理員。 使用者頁面的預設URL為`https://[host]:[port]/edc`。 某些情況下可能不需要連線埠號碼。 請詢問您的管理員以取得詳細資料。

管理員的預設URL為`https://[host]:[port]/adminui`。

對於管理員，會在安裝期間建立預設的超級管理員帳戶。 第一次安裝Document Security時，您可以使用此帳戶登入。

>[!NOTE]
>
>您也可以從Acrobat和其他使用者端應用程式存取網頁。 如需詳細資訊，請參閱Acrobat說明或適當的Acrobat Reader DC擴充功能說明。

1. 在瀏覽器中輸入URL：

   Document Security URL： `https://[host]:[port]/edc`

   或管理主控台URL： `https://[host]:[port]/adminui`

1. 在登入視窗中，輸入您的使用者名稱和密碼，然後按一下確定。
1. 在Administration Console中，按一下「服務> Document Security」。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕（例如「上一步」按鈕、「重新整理」按鈕以及「上一步」和「上一步」箭頭），因為此動作可能會導致不必要的資料擷取和資料顯示問題。

## 瀏覽網頁 {#navigating-the-web-pages}

當您登入使用者網頁時，您將會看到原則、檔案和事件使用者頁面的連結。

當您登入管理控制檯並導覽至Document Security首頁時，您也可能看到一或兩個其他連結，一個用於「設定」頁面，另一個用於「受邀和本機使用者」頁面。 只有啟用受邀使用者註冊時，才會顯示「受邀和本機使用者」頁面。

使用這些連結來存取各種頁面，您可以在此處建立和管理原則及受原則保護的檔案。

**顯示頁面**

1. 按一下頁面的名稱，例如按一下「原則」。

**返回上一頁**

1. 按一下您要返回之頁面的頁面頂端導覽連結。

**重新整理頁面上的資料清單**

1. 在首頁面上，按一下您要重新整理之頁面的連結。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕（例如「上一步」按鈕、「重新整理」按鈕以及「上一步」和「上一步」箭頭），因為此動作可能會導致不必要的資料擷取和資料顯示問題。

## 從使用者端應用程式設定檔案安全性的存取權 {#setting-up-access-to-document-security-from-client-applications}

使用者端應用程式必須設定為連線至Document Security以保護檔案、開啟受原則保護的檔案，以及連線至Document Security網頁。 如需在使用者端應用程式內設定連線的相關資訊，請參閱&#x200B;*Acrobat說明*&#x200B;或適當的&#x200B;*RightsManagementExtension說明*。

可透過安全通訊端層(SSL)存取Document Security。 在憑證存放區中安裝網站的憑證，以便您可以透過使用者端應用程式存取Document Security。

<!-- Fix broken link See Configuring SSL for information on SSL.-->

這些指示特定於Internet Explorer，但您可以使用任何支援的網頁瀏覽器來安裝憑證。 如需詳細資訊，請參閱瀏覽器的說明。

**使用Internet Explorer安裝伺服器憑證**

1. 開啟網頁瀏覽器，並在「位址」方塊中輸入Document Security的基本URL。 例如，型別`https://[host]:[port]`。 便會顯示「安全性警示」對話方塊。
1. 按一下檢視憑證，然後按一下安裝憑證，並選取安裝的預設值。 憑證必須安裝在受信任的根憑證授權單位中。
1. 關閉您的瀏覽器工作階段。
1. 開啟另一個瀏覽器視窗，並在「位址」方塊中輸入相同的URL。 不應出現安全性警示對話方塊。 此測試會確認憑證是否已正確安裝。

## 登出網頁 {#log-out-of-the-web-pages}

使用完網頁後登出，這樣您就可以安全地使用網頁瀏覽器進行其他用途。 根據Document Security的設定方式，您可能需要關閉瀏覽器才能完全登出。

1. 在頁面的右上角，按一下「登出」。
1. 如果「登出」頁面上出現訊息，請關閉瀏覽器視窗以完全登出。 否則，您可以繼續將瀏覽器用於其他目的。
