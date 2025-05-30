---
title: 開發AEM Commerce
description: 瞭解如何使用AEM專案原型產生啟用AEM的商務專案。 瞭解如何建立專案並將其部署至本機開發環境。
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
solution: Experience Manager,Commerce
role: Admin, Developer
exl-id: 22fcdadf-12c0-4545-a854-76345806386f
source-git-commit: 4c3402aa813c115625d624f3b33ca73d31bed850
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 4%

---

# 開發AEM Commerce {#develop}

根據AEM (CIF)為AEM開發Commerce integration framework Commerce專案時，會遵循與其他AEM專案相同的規則和最佳作法。 請先檢閱下列內容：

- [AEM開發使用手冊](/help/sites-developing/getting-started.md)
- [AEM核心概念](/help/sites-developing/the-basics.md)
- [AEM 開發 - 指導方針與最佳實務](/help/sites-developing/dev-guidelines-bestpractices.md)
- [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md)

## AEM Commerce的本機開發 {#local}

建議使用本機開發環境與CIF專案搭配使用。

>[!NOTE]
>
>下列說明可協助您使用適用於AEM 6.5 LTS的CIF，為AEM Commerce設定本機AEM開發環境。 如果您使用AEM as a Cloud Service，請參閱[AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html?lang=zh-Hant)檔案。

適用於AEM的AEM Commerce附加元件(稱為CIF附加元件)可用於本機開發，並以AEM套件的形式提供。 可以從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載它作為Feature Pack。

### 必要的軟體

下列專案應在本機安裝：

- 本機AEM 6.5 LTS
- [Java 17/Java 21](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 或更新版本)
- [節點LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 存取CIF附加元件

可以從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載CIF附加元件，搜尋「AEM Commerce附加元件」。

>[!TIP]
>
>請務必使用最新的CIF附加元件版本。

### 本機設定

對於使用AEM和CIF附加元件的本機CIF專案開發，請執行以下步驟：

1. 解壓縮AEM .jar以建立`crx-quickstart`資料夾，請執行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立`crx-quickstart/install`資料夾

1. 將從軟體發佈入口網站下載的CIF附加元件所有套件複製到`crx-quickstart/install`資料夾。

>[!TIP]
>
>或者，您也可以透過「封裝管理員」安裝CIF附加套件。

1. 啟動AEM快速入門

透過OSGI主控台驗證安裝： `http://localhost:4502/system/console/osgi-installer`。 此清單應包含與CIF附加元件相關的組合、內容套件和OSGI設定。 請確定所有套件組合都已啟動。

## 專案設定 {#project}

有兩種方式可使用CIF來啟動AEM Commerce專案。

### 使用AEM專案原型

[AEM專案原型](https://github.com/adobe/aem-project-archetype)是啟動預先設定的專案以開始使用CIF的主要工具。 CIF核心元件和所有的必要設定，都可包含於產生專案中，外加一個選項。

>[!TIP]
>
>使用[AEM Project Archetype 25或更新版本](https://github.com/adobe/aem-project-archetype/releases)來產生專案。

請參閱AEM專案原型[使用指示](https://github.com/adobe/aem-project-archetype#usage)，瞭解如何產生AEM專案。 若要將CIF納入專案中，請使用`includeCommerce`選項。

例如：

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF核心元件可透過包含提供的`all`套件或使用CIF內容套件和相關OSGI套裝的個別來用於任何專案。 若要手動將CIF核心元件新增至專案，請使用下列相依性：

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### 使用AEM Venia Reference Store

啟動CIF專案的第二個選項是複製並使用[AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia Reference Store是參考店面應用程式範例，可示範AEM的CIF核心元件的使用情形。 其目的是作為一組最佳實務範例，以及開發您自己的功能的潛在起點。

若要開始使用Venia Reference Store，只要複製[Git存放庫](https://github.com/adobe/aem-cif-guides-venia)並開始根據您的需求自訂專案即可。

>[!NOTE]
>
>Venia Reference Store專案包含AEM as a Cloud Service和AEM 6.5的兩個組建設定檔。請檢查[專案readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)，瞭解其使用方式。 若為AEM 6.5，請使用`classic`設定檔。

### 將AEM連線至Commerce系統

若要將您的專案連線到商務系統，AEM必須設定為您的商務系統的GraphQL端點。

由[AEM專案原型](https://github.com/adobe/aem-project-archetype)或[AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)產生的專案都已包含必須調整的[預設設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)。

將`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中`url`的值取代為專案所使用的商務系統的GraphQL端點。

AEM Commerce附加元件和CIF核心元件會透過AEM伺服器並直接透過瀏覽器，連線至商務GraphQL端點。 使用者端CIF核心元件和CIF附加撰寫工具預設會連線至`/api/graphql`。 如有需要，可透過CIF Cloud Service設定調整此專案（請參閱下文）。

CIF附加元件提供位於`/api/graphql`的GraphQL Proxy servlet。 如果您不打算使用本機AEM Dispatcher，建議一併設定GraphQL Proxy servlet。

導覽至http://localhost:4502/system/console/configMgr並建立`Adobe CIF GraphQL Proxy Configuration`服務的OSGI設定。 使用與上述用於GraphQL使用者端相同的商務系統GraphQL端點。

## 其他資源

- [AEM專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
