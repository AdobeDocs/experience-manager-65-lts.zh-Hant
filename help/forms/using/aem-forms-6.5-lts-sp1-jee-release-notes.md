---
title: ' [!DNL Adobe Experience Manager] 6.5 LTS SP1發行說明'
description: 尋找 [!DNL Adobe Experience Manager] 6.5 LTS SP1的版本資訊、新增功能、安裝操作說明和詳細變更清單
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: b172fd1c328f54e759be59d5e7fd24be6f0d59e9
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 3%

---


# JEE上的Adobe Experience Manager (AEM) Forms 6.5 LTS SP1發行說明


## 發行資訊

| **產品** | Adobe Experience Manager Forms |
| -------------------- | ------------------------------------ |
| **版本** | 6.5 LTS SP1 |
| **類型** | 長期支援Service Pack (JEE) |
| **發行類別** | 升級版本 |
| **下載URL** | 軟體散發 |

## [!DNL Experience Manager] 6.5 LTS SP1包含的內容 {#what-is-included-in-aem-65ltssp1}

JEE上的Adobe Experience Manager (AEM) Forms **6.5 LTS SP1**&#x200B;提供新功能、客戶要求的重要平台更新及一般錯誤修正，特別著重於產品穩定性及長期支援。

## AEM Forms 6.5 LTS SP1包含的內容

### &#x200B;1. Java支援更新

已引進對較新Java版本的支援：

* **Java™ 17**
* **Java™ 21**

### 2.應用程式伺服器支援更新

#### JBoss EAP 8支援

* 已新增對&#x200B;**JBoss EAP 8**&#x200B;的支援。
* 已移除舊版&#x200B;**PicketBox**&#x200B;安全性架構。
* **Elytron認證存放區**&#x200B;現在支援安全認證管理。

##### 設定：認證存放區（Elytron型）

JBoss EAP 8上的AEM Forms使用Elytron來管理安全認證。 客戶必須設定以Elytron為基礎的認證存放區，以確保伺服器成功啟動及安全資料庫驗證。

如需組態詳細資訊，請參閱安裝與組態指南。

### 3.平台與相容性變更

#### Servlet規格支援

* 支援&#x200B;**Servlet規格5+**
* 根據&#x200B;**Jakarta EE 9**&#x200B;規範

#### 名稱空間移轉需求

* Jakarta EE 9引入名稱空間從`javax.*`變更為`jakarta.*`
* 所有&#x200B;**自訂DSC**&#x200B;都必須移轉至`jakarta.*`名稱空間
* AEM Forms 6.5 LTS SP1僅支援&#x200B;**Jakarta EE 9+應用程式伺服器**

如需詳細資訊，請參閱&#x200B;**從javax移轉至jakarta名稱空間**。

## 升級

如需詳細的升級指示，請參閱JEE上的[AEM Forms 6.5 LTS SP1升級指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

## 安裝

如需安裝步驟和先決條件，請參閱&#x200B;**AEM Forms 6.5 LTS SP1 (JEE)**&#x200B;的安裝指南。

## 受支援平台

如需支援平台、作業系統、資料庫和應用程式伺服器的完整清單，請參閱：

**支援平台對照表 — AEM Forms 6.5 LTS SP1 (JEE)**

## 已棄用和移除的功能

* 已移除CRX存放庫持續性對&#x200B;**RDBMK**&#x200B;的支援。
* 對於叢集環境，只有&#x200B;**儲存庫持續性支援MongoMK**。

## 從javax移轉至jakarta名稱空間

### 從`javax`移轉至`jakarta`名稱空間

從&#x200B;**AEM Forms 6.5 LTS SP1**&#x200B;開始，僅支援實作&#x200B;**Jakarta Servlet API 5/6**&#x200B;的應用程式伺服器。 透過&#x200B;**Jakarta EE 9和更新版本**，所有API都會從`javax.{}`名稱空間轉換為`jakarta.`。

因此，**所有自訂DSC都必須使用`jakarta`名稱空間**。 使用`javax.{}` API建置的自訂元件&#x200B;**與支援的應用程式伺服器不相容**。

### 自訂DSC的移轉選項

您可以使用下列其中一種方法移轉現有的自訂DSC：

#### 選項1：Source程式碼移轉（建議）

* 將所有匯入陳述式從`javax.{}`更新為`jakarta.`
* 重建並重新編譯自訂DSC專案
* 將更新的元件重新部署到應用程式伺服器

**優點：**

* 確保與Jakarta EE 9+長期相容
* 最適合主動維護的專案

#### 選項2：使用Eclipse轉換器進行二進位移轉

* 使用&#x200B;**Eclipse轉換器**&#x200B;工具將編譯的二進位檔(`.jar`， `.war`)從`javax`轉換為`jakarta`
* 不需要變更原始程式碼或重新編譯
* 將轉換後的二進位檔重新部署到應用程式伺服器

>[!NOTE]
>
> 在&#x200B;**位元組碼層級**&#x200B;執行二進位轉換。

匯入對應範例

以下是移轉期間所需的名稱空間變更的常見範例：

早於(javax)    之後（雅加達）
javax.servlet。*    jakarta.servlet.*
javax.servlet.http。*    jakarta.servlet.http。*

### 匯入對應範例

下表顯示從`javax`移轉至`jakarta`時所需的一般名稱空間變更：

| 在(`javax`)之前 | 在(`jakarta`)之後 |
| ---------------------- | ------------------------ |
| `javax.servlet.*` | `jakarta.servlet.*` |
| `javax.servlet.http.*` | `jakarta.servlet.http.*` |

在更新自訂DSC原始程式碼或驗證轉換後的二進位檔時，使用這些對應作為參考。

