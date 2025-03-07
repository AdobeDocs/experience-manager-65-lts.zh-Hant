---
title: 在OSGi上升級至AEM 6.5 Forms LTS
description: 您可以從AEM 6.5.22.0 Forms直接升級至AEM 6.5 Forms LTS。
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 1%

---

# 在OSGi上升級至AEM 6.5 Forms LTS {#upgrade-to-aem-forms-osgi}

若要[從AEM 6.5升級至AEM 6.5 LTS](/help/sites-deploying/upgrade.md)，請升級至AEM 6.5.22.0 Forms或更新版本。 支援從AEM 6.5.22.0直接升級至AEM 6.5 Forms LTS。

如果您使用AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms、AEM 6.3 Forms、AEM 6.4 Forms或AEM 6.5 Forms，則無法直接升級至AEM 6.5 Forms LTS。 如需詳細的升級路徑，請參閱[升級路徑](/help/forms/using/upgrade.md)檔案。

升級至Service Pack AEM Forms 6.5.22.0後，請依照下列步驟升級至AEM 6.5 LTS Forms：

1. 安裝AEM Forms附加元件套件。 步驟如下：

   1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
   1. 選取標題功能表中可用的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
   1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中：
      1. 從&#x200B;**[!UICONTROL 解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
      1. 選取封裝的版本和型別。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
   1. 選取適用於您作業系統的封裝名稱，選取&#x200B;**[!UICONTROL 接受EULA條款]**，然後選取&#x200B;**[!UICONTROL 下載]**。
   1. 開啟[封裝管理員](/help/sites-administering/package-manager.md)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
   1. 開啟[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
   1. 選取封裝並按一下&#x200B;**[!UICONTROL 安裝]**。

      您也可以使用[AEM Forms發行版本](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)文章中所列的直接連結來下載套件。

      安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即停止伺服器。**&#x200B;在停止AEM Forms伺服器之前，請等候直到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在&lt;crx-repository>/error.log檔案中，而且記錄檔穩定。 另請注意，有些套件可能維持已安裝狀態。 您可以安全地忽略這些套裝程式的狀態。


      **使用下列其他JVM命令列引數重新啟動AEM執行個體**：
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      如果伺服器是透過指令碼或服務啟動，請更新以包含上述內容，這樣在後續重新啟動後也有效。

1. 重新啟動AEM執行個體。

   >[!NOTE]
   >
   > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式），可能會導致AEM開發環境不一致。

1. 執行安裝後活動。

   * **執行移轉公用程式**

     移轉公用程式可讓舊版的最適化表單和通訊管理資產相容於AEM 6.5表單。 您可以從AEM Software Distribution下載公用程式。 如需設定及使用移轉公用程式的逐步資訊，請參閱[移轉公用程式](../../forms/using/migration-utility.md)。

     如果您使用[範例將草稿與提交元件](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)與資料庫整合，並從舊版升級，請在執行升級後執行下列SQL查詢：

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(若僅從AEM 6.2 Forms或舊版升級)重新設定Adobe Sign**

     如果您已在舊版AEM Forms中設定Adobe Sign，請從AEM雲端服務重新設定Adobe Sign 。 如需詳細資訊，請參閱[整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

   * **支援jQuery**

     在AEM 6.5 Forms中，jQuery的版本已更新至3.2.1，而jQuery UI版本已更新至1.12.1。AEM表單在&#x200B;**noConflict**&#x200B;模式下使用JQuery。 因此，如果您使用任何其他jQuery版本，則執行升級時不會顯示任何問題。 不過，當您升級至AEM 6.5 Forms時：

      * 確保您的自訂元件（如果有的話）與支援的jQuery版本相容。
      * 從自訂元件移除不支援的API。 如需已移除的API清單，請參閱[升級指南](https://jquery.com/upgrade-guide/3.0/)。 例如，會移除對load()、.unload()和.error() API的支援。 使用.on()方法取代上述的API。 例如，將$(&quot;img&quot;)。load(fn)變更為$(&quot;img&quot;)。on(&quot;load&quot;， fn)。

   * **(如果從AEM 6.2 Forms或舊版升級)重新設定分析和報表**

     在AEM 6.4 Forms中，無法使用曝光的來源和成功事件流量變數。 因此，當您從AEM 6.2 Forms或舊版升級時，AEM Forms會停止傳送資料至Adobe Analytics伺服器，且無法使用最適化表單的Analytics報表。 此外，AEM 6.4 Forms為表單分析版本引入流量變數，並為在欄位上逗留的時間量引入成功事件。 因此，請為您的AEM Forms環境重新設定分析和報表。 如需詳細步驟，請參閱[設定分析和報表](../../forms/using/configure-analytics-forms-documents.md)。

1. 請確認伺服器已順利升級，所有資料也已成功移轉，而且伺服器可正常運作。

   * **驗證套裝的狀態：**&#x200B;請確定所有套裝都處於作用中狀態。
   * **驗證復寫及反向復寫：**&#x200B;發佈、填寫及送出一些已移轉的表單。 同時驗證提交的資料。
   * **驗證對管理員和開發人員使用者介面的存取權：**&#x200B;從管理員帳戶登入AEM執行個體，並確認您擁有下列URL的存取權：

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >在AEM 6.4 Forms中，crx-repository的結構已變更。 如果從6.3 Forms升級至AEM 6.5 Forms，請使用變更的路徑進行重新建立的自訂。 如需已變更路徑的完整清單，請參閱[AEM中的Forms存放庫重組](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5)。
