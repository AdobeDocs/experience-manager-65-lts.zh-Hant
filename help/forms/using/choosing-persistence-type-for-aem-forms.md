---
title: 為AEM Forms安裝選擇持續性型別
description: 明智地選擇持續性型別。 這可幫助您建置有效率且可擴充的AEM Forms環境。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
exl-id: 8ddfc767-08a5-4045-86a7-97150e028a14
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# 為AEM Forms安裝選擇持續性型別 {#choosing-a-persistence-type-for-an-aem-forms-installation}

明智地選擇持續性型別。 這可幫助您建置有效率且可擴充的AEM Forms環境。

持續性是在實體儲存裝置上儲存內容的方法。 它會定義資料的實際資料結構和儲存機制。 MicroKernels可充當AEM Forms中的持續性管理員。 AEM Forms支援TarMK、MongoMK和RDBMK型別的持續性（微核心）。 您可以根據AEM Forms執行個體的用途和部署型別（單一伺服器、陣列或叢集），為AEM Forms選擇持續性型別。

>[!NOTE]
>
>LiveCycle ES4 SP1使用TarPM持續性來儲存內容。

下表列出所有支援的持續性型別，以及各種引數，協助您為環境選擇持續性型別：

<table>
 <tbody>
  <tr>
   <th><strong>安裝型別/成本</strong></th>
   <th><strong>tarmk</strong></th>
   <th><strong>mongomk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>獨立設定</strong></th>
   <td>支援<br /> </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <th><strong>叢集設定</strong></th>
   <td>不支援</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <th><strong>授權成本</strong></th>
   <td>包含在AEM中 </td>
   <td>需要單獨的授權</td>
   <td>需要單獨的授權</td>
  </tr>
 </tbody>
</table>

TarMK是專為效能而設計，而MongoMK和RDBMK則是為擴充性而設計。 Adobe強烈建議將TarMK作為所有AEM Forms部署情境的預設持續性技術，無論是製作執行個體還是發佈執行個體，但[選擇Mongo或關聯式資料庫Microkernel而非TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p)一節中概述的使用案例除外。

如需支援的微核心清單，請參閱OSGi技術需求上的[AEM Forms](/help/sites-deploying/technical-requirements.md) <!--or [AEM Forms on JEE supported platform combinations](/help/forms/using/aem-forms-jee-supported-platforms.md) articles-->。

## 選擇Mongo或透過TarMK的關聯式資料庫微核心 {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

可擴充（叢集）的AEM Forms環境是由兩個或多個水準設定的作用中製作執行個體所組成。 如果支援所有並行撰寫活動的單一伺服器無法再持續運作，您可以選擇執行多個撰寫例項。

<!--Only MongoMK and RDBMK persistence type are supported for a scalable (clustered) AEM Forms on JEE environment.-->

伺服器數量或可擴充環境的大小因每次安裝而異。 如需考量事項和範例的清單，請參閱[建議的部署](/help/sites-deploying/recommended-deploys.md)和/或[AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)文章。 您也可以聯絡AEM Forms支援，以取得有關使用RDBMK和TarMK的AEM Forms容量規劃的詳細資訊。
