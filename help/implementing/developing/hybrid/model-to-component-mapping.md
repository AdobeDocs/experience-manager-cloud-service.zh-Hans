---
title: SPA的动态模型到组件映射
description: 本文介绍了在JavaScript SPA SDK for AEM中如何进行动态模型到组件的映射。
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# SPA的动态模型到组件映射 {#dynamic-model-to-component-mapping-for-spas}

本文档介绍在JavaScript SPA SDK for AEM中如何进行动态模型到组件的映射。

## 组件映射模块 {#componentmapping-module}

此 `ComponentMapping` 模块作为NPM包提供给前端项目。 它存储前端组件，并为单页应用程序提供一种将前端组件映射到AEM资源类型的方法。 在分析应用程序的JSON模型时，该模块支持组件的动态解析。

模型中存在的每个项目都包含 `:type` 公开AEM资源类型的字段。 安装后，前端组件可以使用从基础库收到的模型片段来渲染自身。

参见 [SPA Blueprint](blueprint.md) 文档，了解有关模型解析和前端组件访问模型的更多信息。

另请参阅npm包： [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驱动的单页应用程序 {#model-driven-single-page-application}

使用JavaScript SPA SDK for AEM的单页应用程序是模型驱动的：

1. 前端组件向 [组件映射存储](#componentmapping-module).
1. 然后 [容器](blueprint.md#container)，在模型由 [模型提供程序](blueprint.md#the-model-provider)，遍历其模型内容(`:items`)。

1. 如果存在页面，则其子页面(`:children`)首先从获取组件类 [组件映射](blueprint.md#componentmapping) 然后实例化它。

## 应用程序初始化 {#app-initialization}

每个组件都通过 [`ModelProvider`](blueprint.md#the-model-provider). 因此，初始化采用以下常规形式：

1. 每个模型提供程序都会初始化自身，并监听对与其内部组件对应的模型段所做的更改。
1. 此 [`PageModelManager`](blueprint.md#pagemodelmanager) 必须初始化，表示为 [初始化流程](blueprint.md).

1. 存储后，页面模型管理器会返回应用程序的完整模型。
1. 然后，将此模型传递到前端根 [容器](blueprint.md#container) 应用程序的组件。
1. 最终会将模型的片段传播到每个单独的子元件。

![应用程序模型初始化](assets/app-model-initialization.png)
