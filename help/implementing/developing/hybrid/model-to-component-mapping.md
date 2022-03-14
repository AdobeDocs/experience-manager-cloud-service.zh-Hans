---
title: 适用于SPA的动态模型到组件映射
description: 本文介绍了在适用于AEM的Javascript SPA SDK中如何进行动态模型到组件的映射。
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 适用于SPA的动态模型到组件映射 {#dynamic-model-to-component-mapping-for-spas}

本文档介绍如何在适用于AEM的Javascript SPA SDK中进行动态模型到组件的映射。

## 组件映射模块 {#componentmapping-module}

的 `ComponentMapping` 模块作为NPM包提供到前端项目。 它存储前端组件，并为单页应用程序提供了一种将前端组件映射到AEM资源类型的方法。 这样，在解析应用程序的JSON模型时，就可以动态解析组件。

模型中存在的每个项目都包含 `:type` 公开AEM资源类型的字段。 装载后，前端组件可以使用从基础库收到的模型片段呈现自身。

请参阅 [SPA Blueprint](blueprint.md) 文档，以了解有关模型解析和对模型的前端组件访问的详细信息。

另请参阅npm包： [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驱动的单页应用程序 {#model-driven-single-page-application}

使用适用于AEM的Javascript SPA SDK的单页应用程序由模型驱动：

1. 前端组件本身注册到 [组件映射存储](#componentmapping-module).
1. 然后， [容器](blueprint.md#container)，一经由提供 [模型提供程序](blueprint.md#the-model-provider)，迭代其模型内容(`:items`)。

1. 对于页面，其子项(`:children`)首先从获取组件类 [组件映射](blueprint.md#componentmapping) 然后实例化它。

## 应用程序初始化 {#app-initialization}

通过 [`ModelProvider`](blueprint.md#the-model-provider). 因此，初始化采用以下一般形式：

1. 每个模型提供程序自行初始化，并侦听对与其内部组件对应的模型段所做的更改。
1. 的 [`PageModelManager`](blueprint.md#pagemodelmanager) 必须初始化，如 [初始化流程](blueprint.md).

1. 存储后，页面模型管理器会返回应用程序的完整模型。
1. 然后，此模型将传递到前端根 [容器](blueprint.md#container) 组件。
1. 模型段最终会传播到每个单独的子组件。

![应用程序模型初始化](assets/app-model-initialization.png)
