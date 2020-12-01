---
title: SPA的动态模型到组件映射
description: 本文描述Javascript SPA SDK for AEM中如何进行动态模型到组件的映射。
translation-type: tm+mt
source-git-commit: cdd92032c627740c66de7b2f3836fa1dcd2ee2ca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# SPA {#dynamic-model-to-component-mapping-for-spas}的动态模型到组件映射

本文档描述了在AEM的Javascript SPA SDK中如何进行动态模型到组件的映射。

## 组件映射模块{#componentmapping-module}

`ComponentMapping`模块作为NPM包提供到前端项目。 它存储前端组件，并为单页应用程序将前端组件映射到AEM资源类型提供了一种方法。 这样，在解析应用程序的JSON模型时，可动态解析组件。

模型中存在的每个项都包含一个公开AEM资源类型的`:type`字段。 装载后，前端组件可以使用它从基础库接收的模型片段来呈现自己。

请参阅[SPA Blueprint](blueprint.md)文档，了解有关模型解析和对模型的前端组件访问的详细信息。

另请参阅npm包：[@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驱动的单页应用程序{#model-driven-single-page-application}

利用AEM的Javascript SPA SDK的单页应用程序由模型驱动：

1. 前端组件自行注册到[组件映射存储](#componentmapping-module)。
1. 然后，[容器](blueprint.md#container)一旦由[模型提供者](blueprint.md#the-model-provider)提供了模型，则对其模型内容(`:items`)进行迭代。

1. 对于页面，其子项(`:children`)首先从[组件映射](blueprint.md#componentmapping)获取组件类，然后实例化它。

## 应用程序初始化{#app-initialization}

每个组件都通过[`ModelProvider`](blueprint.md#the-model-provider)的功能进行扩展。 因此，初始化采用以下一般形式：

1. 每个模型提供程序自行初始化，并监听对与其内部组件对应的模型片段所做的更改。
1. [`PageModelManager`](blueprint.md#pagemodelmanager)必须初始化为由[初始化流](blueprint.md)表示。

1. 存储后，页面模型管理器将返回应用程序的完整模型。
1. 然后，此模型将传递给应用程序的前端根[容器](blueprint.md#container)组件。
1. 模型的片段最终传播到每个单独的子组件。

![应用程序模型初始化](assets/app-model-initialization.png)
