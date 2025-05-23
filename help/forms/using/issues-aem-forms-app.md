---
title: 疑難排解AEM Forms應用程式
description: 瞭解AEM Forms應用程式的常見問題以及如何疑難排解。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: e63c1dc2-9843-47ca-8f3c-c49720659aa0
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# 疑難排解AEM Forms應用程式 {#troubleshoot-aem-forms-app}

本文會說明建置AEM Forms應用程式時可能顯示的錯誤訊息，以及解決這些問題的步驟。

本文的章節包括：

* [iOS使用者的附件遺失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Workspace使用者提交的HTML5表單草稿在入口網站上不可見](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [HTML5表單（未快取）無法在AEM Forms應用程式中載入](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms無法在Windows上同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不支援的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle外掛程式相容性問題](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS使用者的附件遺失 {#attachment-loss-for-ios-users}

iOS適用的AEM Forms應用程式設定為在OSGi上與AEM Forms同步，僅支援欄位層級附件。 所有附件必須具有唯一的名稱。 如果多個附件具有相同的名稱，則只會保留一個附件，而其他名稱相同的附件會遺失。 執行以下步驟，防止iOS裝置上的使用者發生資料遺失：

1. 在連線的伺服器上，瀏覽至&#x200B;**Adobe Experience Manager >工具>作業> Web主控台**。
1. 尋找並按一下&#x200B;**[!UICONTROL 最適化表單和互動式通訊Web Channel設定]**。
1. 在[!UICONTROL 最適化表單和互動式通訊Web Channel設定]對話方塊中，啟用&#x200B;**讓檔案名稱是唯一的**。

   如果&#x200B;**將檔案名稱設為唯一**&#x200B;設定已停用，使用者嘗試提交具有多個附件的調適型表單時，將會遇到資料遺失的問題。

1. 按一下「**儲存**」。

## Workspace使用者提交的HTML5表單草稿在入口網站上不可見 {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

對於在AEM Forms應用程式中使用&#x200B;**另存為草稿** HTML轉譯器設定檔啟用的HTML5表單，工作區使用者看不到已儲存的草稿。 若要檢視工作區使用者在入口網站上提交的HTML5表單已儲存草稿，請執行以下步驟：

1. 開啟CRXDE並使用管理員憑證登入。

   URL： `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路徑中，按一下[存取控制]下的[存取控制清單]。**+**
1. 在&#x200B;**新增專案**&#x200B;對話方塊中，按一下[主體]欄位中的群組搜尋按鈕。
1. 在[選取主體]對話方塊的[名稱]欄位中，輸入`PERM_WORKSPACE_USER`並按一下[搜尋]。**&#x200B;**
1. 在[選取主體]對話方塊中選取`PERM_WORKSPACE_USER`群組，然後按一下[確定]。**&#x200B;**
1. 在[新增專案]對話方塊中，在[主體]欄位中選取`PERM_WORKSPACE_USER`群組。

   啟用使用者群組的`jcr:read`許可權。

1. 按一下&#x200B;**「確定」**。

## HTML5表單（未快取）無法在AEM Forms應用程式中載入 {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

當AEM Forms應用程式連線至舊版AEM Forms伺服器時，未快取的HTML5表單無法在AEM Forms應用程式中載入。

執行以下步驟以解決問題：

1. 在作者執行個體中，瀏覽至&#x200B;**Adobe Experience Manager >工具>設定Workspace App離線服務>立即設定**。
1. 在&#x200B;**Workspace App離線服務**&#x200B;頁面中，按一下&#x200B;**手動資源快取**。

   URL： https://&lt;server>：&lt;port>/libs/fd/workspace-offline/content/config.html

1. 在&#x200B;**手動資源快取**&#x200B;索引標籤中，按一下&#x200B;**+**&#x200B;按鈕以新增CRX路徑。
1. 在&#x200B;**新增資源**&#x200B;欄位中，輸入： /etc.clientlibs/fd/xfaforms/I18N/en_US.js並按一下&#x200B;**新增**。
1. 按一下「**儲存**」。

## AEM Forms無法在Windows上同步 {#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms應用程式中，如果表單路徑或其任何資源包含大於或等於256個字元，則表單不會與連線的伺服器同步。

修改表單及其資源的路徑，將字元數減少到256個字元以下。

## 不支援的Gradle版本 {#unsupported-version-of-gradle}

**錯誤訊息：**&#x200B;專案使用不支援的Gradle版本。

當您在Android Studio中建置AEM Forms應用程式時，會顯示錯誤訊息。 發生此問題是因為系統支援不支援的Gradle版本。

**解決方法：**&#x200B;按一下&#x200B;**Fix Gradle包裝函式並重新匯入專案**&#x200B;以解決問題。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle外掛程式相容性問題 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**錯誤訊息：** Android Gradle外掛程式與Gradle的版本不相容。

當您從Android Studio使用者介面的&#x200B;**建置**&#x200B;功能表選取&#x200B;**建置APK**&#x200B;選項時，會顯示錯誤訊息。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**解析度：**&#x200B;開啟&#x200B;**Gradle指令碼** > **Gradle-wrapper.properties**&#x200B;檔案，並編輯&#x200B;**distributionUrl**&#x200B;屬性。

例如，Android Studio主控台建議將Gradle版本降級為3.5版。編輯&#x200B;**gradle-wrapper.properties**&#x200B;檔案中的&#x200B;**distributionUrl**&#x200B;版本。

再次選取&#x200B;**建置** > **建置APK**&#x200B;以解決錯誤並產生.apk檔案。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
