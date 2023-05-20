---
title: SPA的動態模型到元件對應
description: 本文說明在AEM適用的Javascript SPA SDK中，元件對映動態模型的發生方式。
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# SPA的動態模型到元件對應 {#dynamic-model-to-component-mapping-for-spas}

本檔案說明在AEM適用的Javascript SPA SDK中，如何進行動態模型與元件對應。

## 元件對應模組 {#componentmapping-module}

此 `ComponentMapping` 模組以NPM封裝形式提供給前端專案。 它會儲存前端元件，並提供讓單頁應用程式將前端元件對應到AEM資源型別的方法。 如此一來，在剖析應用程式的JSON模型時，便可啟用元件的動態解析度。

模型中呈現的每個專案都包含 `:type` 公開AEM資源型別的欄位。 掛載後，前端元件可使用從基礎程式庫收到的模型片段來呈現自身。

請參閱 [SPA Blueprint](blueprint.md) 檔案，以取得有關模型剖析和模型的前端元件存取權的詳細資訊。

另請參閱npm套件： [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型導向的單頁應用程式 {#model-driven-single-page-application}

運用AEM適用的Javascript SPA SDK的單頁應用程式是模型導向的：

1. 前端元件需自行註冊至 [元件對應存放區](#componentmapping-module).
1. 然後 [容器](blueprint.md#container)，在模型由提供之後， [模型提供者](blueprint.md#the-model-provider)，反複執行其模型內容(`:items`)。

1. 若是頁面，其子項(`:children`)首先從取得元件類別 [元件對應](blueprint.md#componentmapping) 然後將其例項化。

## 應用程式初始化 {#app-initialization}

每個元件都可藉由以下功能擴展： [`ModelProvider`](blueprint.md#the-model-provider). 因此，初始化會採取下列一般形式：

1. 每個模型提供者會自我初始化，並監聽對應到其內部元件的模型片段所做的變更。
1. 此 [`PageModelManager`](blueprint.md#pagemodelmanager) 必須初始化，如以下所示 [初始化流程](blueprint.md).

1. 儲存後，頁面模型管理員會傳回應用程式的完整模型。
1. 然後，此模型會傳遞至前端根目錄 [容器](blueprint.md#container) 應用程式的元件。
1. 模型片段最後會傳播到每個個別的子元件。

![應用程式模型初始化](assets/app-model-initialization.png)
