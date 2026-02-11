---
title: JEE版AEM Forms的安裝和升級工作流程
description: JEE版AEM Forms 6.5 LTS (JBoss)的安裝和升級工作流程，其中包含相關PDF及其用途的整合清單。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE,AEM Forms Upgrade
exl-id: 6d8c0e24-7f08-4e66-bb12-2cf1cfe1d5d3
source-git-commit: fb9f6ef794da7f3b242e9e81a6c2505692c16cd8
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---


# JEE版AEM Forms的安裝和升級工作流程 {#aem-forms-jee-installation-upgrade-documentation}

## 套用至 {#applies-to}

本檔案適用於&#x200B;**AEM 6.5 LTS Forms**。

使用下列工作流程和表格，為您的案例挑選正確的指南。 有些檔案會以PDF形式發佈；隨著時間推移，可能會新增其他可用檔案。

## 安裝和升級工作流程 {#installation-upgrade-workflow}

1. 檢閱JEE版AEM Forms的[支援平台](/help/forms/using/aem-forms-jee-supported-platforms.md)，並確定您的系統符合必要的軟體/硬體組合。
2. 決定您要執行&#x200B;**全新安裝**&#x200B;或&#x200B;**升級**。
3. 對於您選擇的路徑，請遵循以下所述的順序（某些情況需要多個指南）。

## 預先安裝和升級前的步驟 {#start-here}

| 指南 | 說明 |
| --- | --- |
| [JEE上的AEM Forms支援平台](/help/forms/using/aem-forms-jee-supported-platforms.md) | 列出AEM Forms on JEE支援的軟體與硬體組合。 在開始安裝或升級之前，使用此項來驗證先決條件。 |
| [AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md) | 說明建議的架構和部署拓撲，讓您選擇符合您環境的方法（例如，單一伺服器對比叢集）。 |
| [為AEM Forms安裝選擇持續性型別](/help/forms/using/choosing-persistence-type-for-aem-forms.md) | 在開始之前，協助您為安裝拓朴選取適當的持續性型別。 |

## 如何在JBoss上的JEE上安裝Adobe Experience Manager Forms (AEM Forms)？ {#installing-aem-forms-jee-jboss}

### Turnkey {#install-jee-jboss-turnkey}

| 指南 | 說明 |
| --- | --- |
| [使用JBoss Turnkey (PDF)在JEE上安裝和部署AEM Forms 6.5 LTS](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-turnkey.pdf) | 在JBoss上使用&#x200B;**全新全包安裝**。 本檔案提供在JEE上使用JBoss全包分發安裝和部署AEM Forms的說明。 |

### 單一伺服器（非全包式） {#install-jee-jboss-single-server}

| 指南 | 說明 |
| --- | --- |
| [準備安裝AEM Forms （單一伺服器） (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-install-single-server.pdf) | 在&#x200B;**之前**&#x200B;使用&#x200B;**全新單一伺服器（非交鑰匙組）安裝**。 本檔案列出在單伺服器拓撲中於JEE上安裝AEM Forms的必要條件和環境準備步驟。 |
| [在JEE for JBoss (PDF)上安裝和部署AEM Forms](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-jboss.pdf) | 用於JEE上JBoss (**non-turnkey**)的AEM Forms **逐步安裝和部署**。 如果是單一伺服器安裝，請在&#x200B;**完成**&#x200B;準備安裝AEM Forms （單一伺服器）*後，遵循本指南*。 |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **fresh cluster installation**. Describes prerequisites and environment preparation steps for installing AEM Forms on JEE in a server cluster topology. *(Link will be added once the PDF is available.)* |
| [Configuring AEM Forms on JEE on JBoss Cluster (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/cluster-jboss.pdf) | Use when setting up and configuring a **JBoss cluster topology** for AEM Forms on JEE. |
-->

## 如何在JEE上的JBoss上升級Adobe Experience Manager Forms (AEM Forms)？ {#upgrading-aem-forms-jee-jboss}

### Turnkey {#upgrade-jee-jboss-turnkey}

| 指南 | 說明 |
| --- | --- |
| [在JEE上升級至JBoss Turnkey (PDF)的AEM Forms 6.5 LTS](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-turnkey.pdf) | 用於&#x200B;**全金鑰升級**。 本檔案提供在JEE JBoss整套金鑰安裝中升級現有AEM Forms的說明。 |

### 單一伺服器 {#upgrade-jee-jboss-single-server}

| 指南 | 說明 |
| --- | --- |
| [準備升級AEM Forms (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-upgrade.pdf) | 在&#x200B;**之前使用**&#x200B;進行&#x200B;**單一伺服器升級**。 說明在升級至AEM 6.5 LTS Forms之前如何準備環境。 它適用於以單一伺服器安裝模式在JEE上執行AEM Forms的環境。 |
| [在JEE上升級至JBoss (PDF)的AEM Forms](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-jboss.pdf) | 在&#x200B;**單一伺服器**&#x200B;安裝模式下，用於JBoss上的&#x200B;**逐步升級程式**。 在&#x200B;**完成**&#x200B;準備升級AEM Forms *後，請遵循本指南*。 |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **cluster upgrade**. Describes how to prepare the environment for a server cluster before upgrading to AEM 6.5 LTS Forms. It applies to environments running AEM Forms on JEE in a server cluster installation mode. *(Link will be added once the PDF is available.)* |
| Upgrading to AEM Forms on JEE for JBoss (Cluster) (PDF) (**TBD**) | Use for the **step-by-step upgrade procedure** on JBoss in a **clustered** installation mode. Follow this guide **after** completing *Preparing to Install AEM Forms (Server Cluster)*. *(Link will be added once the PDF is available.)* | -->

