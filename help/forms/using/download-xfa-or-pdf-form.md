---
title: 下載XFA或PDF表單範本
description: 您可以將表單從存放庫匯出至本機系統，並將下載的表單移轉至新的存放庫。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
exl-id: eafb1a93-8ee5-4420-830b-aee234988393
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 下載XFA或PDF表單範本 {#download-an-xfa-or-a-pdf-form-template}

如名稱所示，下載作業可讓您將表單從存放庫匯出至本機系統。 結合上傳作業，這項作業可協助您將表單從一個存放庫移轉至另一個存放庫。

在AEM Forms中，下列資產型別支援下載操作：

* 表單範本(XFA Forms)
* PDF forms
* 檔案(一般PDF檔案)

AEM Forms支援個別下載這些表單型別，或是在包含一或多個受支援表單的資料夾中下載。

除了這些資產之外，如果資料夾中有`Resource`型別的資產，您就可以下載該資產。 提供此功能是為了讓您下載XFA表單與表單一起引用的資源。

## 下載一或多個表單 {#download-one-or-more-forms}

1. 在`https://<server>:<port>/aem/forms.html`登入AEM Forms使用者介面。

1. 導覽至您要下載的資產位置。

1. 選取資產。 按一下工具列中的&#x200B;**[!UICONTROL 下載]** ![aem6forms_download](assets/aem6forms_download.png)圖示。

   >[!NOTE]
   >
   >您只能選取一個要下載的表單。 如果您想要下載多個表單，必須將其下載為資料夾。

1. 在出現的對話方塊中，按一下&#x200B;**[!UICONTROL 下載]**。

   AEM Forms會產生包含所選檔案或所選資料夾的ZIP檔案。

   如果您正在下載資料夾，資料夾中支援的資產會以其現有階層下載。

   ZIP檔案已儲存至您系統上的`Downloads`資料夾。

## 上傳作業的相關考量事項 {#related-considerations-for-the-upload-operation}

* 您可以將ZIP檔案上傳至相同存放庫或其他存放庫中的任何其他位置
* 在上傳操作期間，會保留資料夾中資產的階層
* 下載前對已下載資產所做的任何中繼資料變更，都會在上傳時反映出來
