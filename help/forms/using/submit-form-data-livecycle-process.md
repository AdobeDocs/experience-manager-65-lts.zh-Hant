---
title: 設定AEM Forms將資料提交至JEE程式的AEM Forms
description: 整合最適化表單與AEM Forms on JEE程式以處理表單資料。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: c888da5d-6a98-4139-9656-a187177efcb0
hide: true
hidefromtoc: true
source-git-commit: 1336ccddcc73459f933e5e4b00a3a22605cdb9a1
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 設定AEM Forms在JEE程式中將表單資料提交至AEM表單{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

調適型表單支援在JEE程式上提交資料給AEM Forms以供進一步處理。 它可讓您使用已提交表單中的可用資料觸發JEE上的AEM Forms程式。 請執行以下步驟，讓AEM Forms執行個體能夠在JEE程式上向AEM Forms提交最適化表單：

## 設定您的AEM Forms伺服器 {#configure-your-aem-forms-server}

請執行以下步驟，讓AEM Forms伺服器將資料提交至JEE伺服器上的AEM Forms：

1. 移至https://[*host*]：[*port*]/system/console/configMgr的AEM Web設定主控台。

1. 找到並按一下&#x200B;**Adobe LiveCycle Client SDK設定**&#x200B;元件。
1. 按一下以編輯JEE伺服器上AEM Forms的設定伺服器URL、使用者名稱和密碼。
1. 檢閱設定並按一下&#x200B;**儲存**。

![Adobe LiveCycle Client SDK設定](assets/clientsdkconfiguration.jpg)

## 與程式欄位對應資料 {#map-data-with-process-fields}

設定AEM Forms後，將提交表單中的資料XML和附件對應至JEE流程中AEM Forms的欄位。 請執行下列動作：

1. 在AEM Web設定主控台中，按一下以編輯&#x200B;**Guide LiveCycle Process Locator and Invoker**&#x200B;設定。
1. 指定下列引數：

   * **資料xml引數的名稱** （必要）：指定必須處理提交資料的AEM Forms on JEE程式的XML屬性檔。 預設值為&#x200B;**dataxml**。

   * **檔案附件引數的名稱** （選用）：指定AEM Forms on JEE程式必須處理的檔案物件清單。 預設值為&#x200B;**fileAttachmentsList**。

1. 檢閱設定並按一下&#x200B;**儲存**。

![指南LiveCycle Process Locator和Invoker](assets/test3.jpg)

設定之後，提交至Forms Workflow提交動作會列出JEE伺服器上包含指定資料xml引數的AEM Forms程式。
