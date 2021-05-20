---
title: SPA页面组件
description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派给SPA框架。 本文档介绍如何使SPA的页面组件具有唯一性。
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---

# SPA页面组件{#spa-page-component}

SPA的页面组件不会通过JSP或HTL文件和资源对象提供其子组件的HTML元素。 此操作将委派给SPA框架。 子组件的表示形式将作为JSON数据结构（即模型）获取。 然后，将根据提供的JSON模型，将SPA组件添加到页面。 因此，页面组件初始主体组合与预呈现的HTML对应组合不同。

## 页面模型管理{#page-model-management}

页面模型的解析和管理被委派给提供的[`PageModelManager`](blueprint.md#pagemodelmanager)模块。 当SPA初始化以获取初始页面模型并注册模型更新时，它必须与`PageModelManager`模块进行交互 — 大多数情况下，当作者通过页面编辑器编辑页面时会生成该模块。 `PageModelManager`可由SPA项目作为npm包访问。 `PageModelManager`是AEM和SPA之间的解释器，适用于随SPA一起使用。

要创作页面，必须添加名为`cq.authoring.pagemodel.messaging`的客户端库，以在SPA和页面编辑器之间提供通信渠道。 如果SPA页面组件从页面wcm/core组件继承，则可以使用以下选项来使`cq.authoring.pagemodel.messaging`客户端库类别可用：

* 如果模板是可编辑的，请将客户端库类别添加到页面策略中。
* 使用页面组件的`customfooterlibs.html`添加客户端库类别。

请不要忘记将`cq.authoring.pagemodel.messaging`类别的包含限制为页面编辑器的上下文。

## 通信数据类型{#communication-data-type}

通信数据类型在AEM页面组件中使用`data-cq-datatype`属性设置一个HTML元素。 将通信数据类型设置为JSON时，GET请求会命中组件的Sling模型端点。 在页面编辑器中发生更新后，更新组件的JSON表示形式将发送到页面模型库。 然后，页面模型库会向SPA发出更新警告。

**SPA页面组件 —`body.html`**

```
<div id="page"></div>
```

除了作为不延迟生成DOM的最佳实践之外，SPA框架还要求在主体末尾添加脚本。

**SPA页面组件 —`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

描述SPA内容的元资源属性：

**SPA页面组件 —`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>在请求元件的Sling模型表示时，会静态设置默认模型选择器。

## 元属性 {#meta-properties}

* `cq:wcmmode`:编辑器的WCM模式（例如，页面、模板）
* `cq:pagemodel_root_url`:应用程序根模型的URL。直接访问子页面时至关重要，因为子页面模型是应用程序根模型的片段。 然后，`PageModelManager`系统地将应用程序初始模型重新组合为从其根入口点进入应用程序。
* `cq:pagemodel_router`:启用或禁用 [`ModelRouter`](routing.md) 库的 `PageModelManager` 功能
* `cq:pagemodel_route_filters`:以逗号分隔的列表或正则表达式来提供必须忽略 [`ModelRouter`](routing.md) 的路由。

## 页面编辑器叠加同步{#page-editor-overlay-synchronization}

由`cq.authoring.page`类提供的相同变异观测器保证叠加的同步。

## Sling模型JSON导出的结构配置{#sling-model-json-exported-structure-configuration}

启用路由功能后，假设由于AEM导航组件的JSON导出，SPA的JSON导出包含不同的应用程序路由。 可以通过以下两个属性在AEM根页面内容策略中配置SPA导航组件的JSON输出：

* `structureDepth`:与导出的树深度对应的编号
* `structurePatterns`:与要导出的页面对应的regex数组的正则表达式
