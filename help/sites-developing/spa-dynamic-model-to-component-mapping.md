---
title: SPA的元件對應動態模型
description: 瞭解在Adobe Experience Manager的JavaScript SPA SDK中如何發生元件對應的動態模型。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
exl-id: 051be106-bb15-46b2-8158-53817f68f57c
index: false
source-git-commit: f6a3d16c55a6b62aea9a374904339e16d30f0a75
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# SPA的元件對應動態模型{#dynamic-model-to-component-mapping-for-spas}

本檔案說明適用於Adobe Experience Manager (AEM)的JavaScript SPA SDK中如何發生元件對應的動態模型。

{{ue-over-spa}}

## 元件對應模組 {#componentmapping-module}

`ComponentMapping`模組是以NPM封裝形式提供給前端專案。 它會儲存前端元件，並提供單頁應用程式將前端元件對應至AEM資源型別的方法。 如此一來，在剖析應用程式的JSON模型時，就能啟用元件的動態解析。

模型中每個專案都包含公開AEM資源型別的`:type`欄位。 掛載時，前端元件可使用從基礎程式庫收到的模型片段來轉譯自身。

請參閱[SPA Blueprint](/help/sites-developing/spa-blueprint.md)，以取得有關模型剖析和模型的前端元件存取權的詳細資訊。

另請參閱npm套件： [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驅動單頁應用程式 {#model-driven-single-page-application}

使用適用於AEM的JavaScript SPA SDK的單頁應用程式是模型導向的：

1. 前端元件註冊到[元件對應存放區](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)。
1. 然後[模型提供者](/help/sites-developing/spa-blueprint.md#the-model-provider)提供模型的[容器](/help/sites-developing/spa-blueprint.md#container)會反複執行其模型內容(`:items`)。

1. 如果有頁面，其子系(`:children`)會先從[元件對應](/help/sites-developing/spa-blueprint.md#componentmapping)取得元件類別，然後將其具現化。

## 應用程式初始化 {#app-initialization}

每個元件都使用[`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider)的功能延伸。 因此，初始化會採用下列一般形式：

1. 每個模型提供者會自我初始化，並監聽對應到其內部元件的模型片段所做的變更。
1. 必須初始化[`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)，如[初始化流程](/help/sites-developing/spa-blueprint.md)所表示。

1. 儲存後，頁面模型管理員會傳回應用程式的完整模型。
1. 然後，此模型會傳遞至應用程式的前端根[Container](/help/sites-developing/spa-blueprint.md#container)元件。
1. 模型片段最後會傳播至每個個別的子元件。

![app_model_initialization](assets/app_model_initialization.png)
