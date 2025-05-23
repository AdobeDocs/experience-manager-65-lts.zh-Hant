---
title: 匯入和管理應用程式
description: 瞭解如何匯入和管理應用程式。 應用程式是一種容器，用於儲存實作AEM表單解決方案所需的資產。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e0984513-f70c-4409-885b-a2eb50757a7d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# 匯入和管理應用程式{#import-and-manage-applications}

在AEM Forms中，*應用程式*&#x200B;是用於儲存實施AEM Forms解決方案所需資產的容器。 資產的範例包括表單設計、表單片段、影像、程式、DDX檔案、表單指南、HTML頁面和SWF檔案。 在專案的開發階段中，Workbench使用者可以直接從Workbench的「應用程式」檢視中部署應用程式。 部署後，這些應用程式會顯示在管理主控台的「應用程式管理」頁面的「應用程式」標籤上。

當應用程式完成並準備好要部署到生產伺服器時，Workbench使用者會將應用程式封裝到&#x200B;*AEM表單應用程式檔案* (.lca)。 然後，管理員會使用「應用程式管理」頁面上的「應用程式」頁簽，使用管理主控台來匯入及建置應用程式檔案。

您也可以使用「應用程式管理」頁面上的「封存」頁簽，匯入使用Workbench 8.x建立的LCA。

>[!NOTE]
>
>有一個已知問題，未來版本的LCA檔案不一定回溯相容。 雖然您可以從未來版本的AEM表單（例如預覽版本）檢視和匯入LCA檔案，但不支援這樣做，並可能會導致異常行為。

使用「應用程式」標籤來匯入和管理在Workbench中建立的應用程式。 應用程式管理員也可以匯出應用程式的執行階段組態。 匯出執行階段設定後，您就不需要先在生產環境中手動重新設定設定，然後再啟動已部署的應用程式。 執行階段組態檔包含：

* 服務組態設定
* 集區組態設定
* 端點組態設定
* 安全性設定檔

## 匯入應用程式或封存 {#import-an-application-or-archive}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 按一下「匯入」。
1. 按一下「瀏覽」並選取要匯入的.lca檔案，然後按一下「預覽」。 「預覽應用程式」頁面會顯示有關應用程式的資訊。
1. （選用）若要檢視應用程式中包含的資產清單，請按一下「檢視Assets」 。
1. （選用）若要將資產部署到執行階段，請選取「匯入完成時將Assets部署到執行階段」。 如果您未選取此選項，可以稍後部署資產。
1. 按一下「匯入」。 應用程式會出現在「應用程式」標籤上。
1. 使用管理員憑證登入CRX存放庫。
1. 導覽至content/dam/lcapplications

   >[!NOTE]
   >
   >匯入的應用程式會顯示在lcpapplications節點中。

1. 按一下其中一個匯入的應用程式。

   右側的「屬性」標籤會顯示所選CRX節點的屬性。

   **syncState**&#x200B;屬性指出AEM Forms伺服器與CRX存放庫之間的資料同步處理狀態。 匯入程式一開始，此狀態就會設為0 （零）。 此狀態表示資料目前未同步。 資料同步時，狀態會設為1。

## 部署應用程式 {#deploy-an-application}

您可以部署已匯入的應用程式，或從Workbench匯入的Workbench使用者。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 選取您要部署的應用程式旁的核取方塊，然後按一下部署。
1. 在出現的確認對話方塊中，按一下「確定」。

## 取消部署應用程式 {#undeploy-an-application}

您可以從執行階段解除部署應用程式。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 選取您要取消部署的應用程式旁的核取方塊，然後按一下取消部署。
1. 在出現的確認對話方塊中，按一下「確定」。

## 從伺服器移除應用程式 {#remove-an-application-from-the-server}

將應用程式從伺服器移除之前，請先解除部署該應用程式。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 選取您要移除之應用程式旁的核取方塊，然後按一下移除。
1. 在出現的確認對話方塊中，按一下「確定」。

## 匯入應用程式的執行階段設定 {#import-an-application-s-runtime-configuration}

如果應用程式管理員匯出應用程式的執行階段組態，您可以將其匯入已部署的應用程式。 您可以使用管理主控台或透過指令碼LCA部署匯入它。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「匯入執行階段設定」。
1. 按一下「瀏覽」並選取包含執行階段組態的XML檔案。
1. 按一下「匯入」。

## 匯出應用程式的執行階段設定 {#export-an-application-s-runtime-configuration}

您可以匯出已部署應用程式的執行階段組態資訊。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「匯出執行階段組態」(Export Runtime Config)並儲存所產生的組態檔案(XML)。

## AEM表單應用程式的指令碼部署 {#scripted-deployment-of-aem-forms-applications}

您也可以使用指令碼式部署工具來部署應用程式檔案，包括指定下列設定的settings.xml檔案：

* 服務組態設定
* 集區組態設定
* 端點組態設定
* 安全性設定檔

透過指令碼式部署，您不必先在生產環境中手動重新設定設定，就能啟動已部署的應用程式。

1. 從命令提示字元瀏覽至&#x200B;*[aem-forms root]*/sdk/misc/Foundation/ArchiveManagement。
1. 請檢閱ReadMe.txt檔案以取得更詳細的指示。
1. 手動修改scriptedDeploy.bat和sample-files/sample.xml檔案，如readme.txt檔案中所述。
1. 執行scriptedDeploy.bat檔案。 此動作會部署包含覆寫設定的AEM表單封存檔案。
