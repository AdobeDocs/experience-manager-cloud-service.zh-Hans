---
title: SPA 页面组件
description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派给SPA Framework。 本文档将说明如何使SPA的页面组件具有唯一性。
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e06766160009eaa1bbc41bbf7cfad967a5195e71
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 7%

---

# SPA 页面组件 {#spa-page-component}

SPA的页面组件不通过JSP或HTL文件和资源对象提供其子组件的HTML元素。 此操作将委派给 SPA 框架。子组件的表示形式作为JSON数据结构（即模型）获取。 然后，根据提供的JSON模型将SPA组件添加到页面。 因此，页面组件初始正文构成不同于其预渲染的HTML对应内容。

{{ue-over-spa}}

## 页面模型管理 {#page-model-management}

页面模型的解析和管理委托给提供的[`PageModelManager`](blueprint.md#pagemodelmanager)模块。 SPA在初始化以获取初始页面模型并注册模型更新时必须与`PageModelManager`模块进行交互，模型更新主要是在作者通过页面编辑器编辑页面时生成的。 `PageModelManager`可由SPA项目作为npm包访问。 作为AEM和SPA之间的解释器，`PageModelManager`旨在伴随SPA。

要允许创作页面，必须添加名为`cq.authoring.pagemodel.messaging`的客户端库，以在SPA和页面编辑器之间提供通信渠道。 如果SPA页面组件从页面wcm/核心组件继承，则可通过以下选项使`cq.authoring.pagemodel.messaging`客户端库类别可用：

* 如果模板可编辑，请将客户端库类别添加到页面策略中。
* 使用页面组件的`customfooterlibs.html`添加客户端库类别。

不要忘记将包含`cq.authoring.pagemodel.messaging`类别限制在页面编辑器的上下文中。

## 通信数据类型 {#communication-data-type}

通信数据类型是使用`data-cq-datatype`属性在AEM Page组件中设置的HTML元素。 当通信数据类型设置为JSON时，GET请求会命中组件的Sling模型端点。 在页面编辑器中执行更新后，已更新组件的 JSON 表示形式将发送到页面模型库。然后，页面模型库会向SPA发出更新警告。

**SPA页面组件 —`body.html`**

```
<div id="page"></div>
```

除了是不延迟DOM生成的良好做法之外，SPA框架还要求在正文末尾添加脚本。

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
>请求组件的Sling模型表示时，将静态设置默认模型选择器。

## 元属性 {#meta-properties}

* `cq:wcmmode`：编辑器的WCM模式（例如，页面、模板）
* `cq:pagemodel_root_url`：应用程序的根模型的URL。 由于子页面模型是应用程序根模型的片段，因此直接访问子页面时至关重要。 然后，`PageModelManager`会系统地重新构建应用程序初始模型，使其从根入口点进入应用程序。
* `cq:pagemodel_router`：启用或禁用`PageModelManager`库的[`ModelRouter`](routing.md)
* `cq:pagemodel_route_filters`：逗号分隔列表或正则表达式，用于提供[`ModelRouter`](routing.md)必须忽略的路由。

## 页面编辑器叠加同步 {#page-editor-overlay-synchronization}

覆盖的同步由`cq.authoring.page`类别提供的完全相同的变异观察器保证。

## Sling模型JSON导出结构配置 {#sling-model-json-exported-structure-configuration}

启用路由功能后，会假设在SPA的JSON导出中，包含应用程序的不同路由，这与AEM导航组件的JSON导出不同。 AEM导航组件的JSON输出可通过以下两个属性在SPA根页面内容策略中进行配置：

* `structureDepth`：与导出的树深度对应的数字
* `structurePatterns`：与要导出的页面对应的正则表达式数组的正则表达式
