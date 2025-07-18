---
title: 變更品牌化的組織標誌
description: 若要品牌化AEM Forms工作區，請自訂預設標誌，以提供您組織的標誌。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 3aa4aca3-3c94-4936-ba9c-484bbb196256
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 變更品牌化的組織標誌 {#changing-the-organization-logo-for-branding}

組織標誌會顯示在AEM Forms工作區的左上角。 若要更新標誌，請依照AEM Forms工作區自訂[&#128279;](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)的一般步驟進行，然後依照下列步驟進行。

1. 建立標誌並將檔案命名為`NewWorkspace.png`。 使用WebDAV使用者端將影像檔案置於/apps/ws/images資料夾中。

   >[!NOTE]
   >
   >標誌影像的建議大小為218畫素×20畫素。

   >[!NOTE]
   >
   >如需詳細資訊，請參閱[WebDAV存取](/help/sites-administering/webdav-access.md)。

1. 請新增下列樣式，以參考樣式表中的新標誌影像：/apps/ws/css/newStyle.css。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
