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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%
---
# 變更品牌化的組織標誌 {#changing-the-organization-logo-for-branding}

組織標誌會顯示在AEM Forms工作區的左上角。 若要更新標誌，請依照AEM Forms工作區自訂](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)的[一般步驟進行，然後依照下列步驟進行。

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
