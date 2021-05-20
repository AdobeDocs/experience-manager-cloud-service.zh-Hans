---
title: SPA模型路由
description: 对于AEM中的单页应用程序，应用程序负责路由。 本文档介绍了传送机制、合同和可用选项。
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# SPA模型路由{#spa-model-routing}

对于AEM中的单页应用程序，应用程序负责路由。 本文档介绍了传送机制、合同和可用选项。

## 项目路由{#project-routing}

应用程序拥有路由，然后由项目前端开发人员实施。 本文档介绍了特定于AEM服务器返回的模型的路由。 页面模型数据结构会公开基础资源的URL。 前端项目可以使用提供路由功能的任何自定义或第三方库。 一旦路由需要模型的片段，就可以调用`PageModelManager.getData()`函数。 当模型路由发生更改时，必须触发事件以警告监听库，如页面编辑器。

## 架构 {#architecture}

有关详细说明，请参阅SPA Blueprint文档的[PageModelManager](blueprint.md#pagemodelmanager)部分。

## ModelRouter {#modelrouter}

`ModelRouter` — 启用后 — 封装HTML5历史API函数`pushState`和`replaceState`，以确保预取和访问给定的模型片段。 然后，通知注册的前端组件模型已被修改。

## 手动与自动模型路由{#manual-vs-automatic-model-routing}

`ModelRouter`会自动获取模型的片段。 但是，作为任何自动化工具，它都有其局限性。 如果需要，可以禁用`ModelRouter`或将配置为忽略使用元属性的路径(请参阅[SPA页面组件](page-component.md)文档的元属性部分)。 然后，前端开发人员可以通过请求`PageModelManager`使用`getData()`函数加载任何给定的模型片段来实施自己的模型路由层。

>[!CAUTION]
>
>`ModelRouter`的当前版本仅支持使用指向Sling模型入口点实际资源路径的URL。 它不支持使用虚URL或别名。

## 路由合同{#routing-contract}

当前实施基于以下假设：SPA项目使用HTML5历史记录API路由到不同的应用程序页面。

### 配置 {#configuration}

`ModelRouter`在侦听`pushState`和`replaceState`调用以预取模型片段时支持模型路由的概念。 在内部，它会触发`PageModelManager`以加载与给定URL对应的模型，并触发其他模块可以侦听的`cq-pagemodel-route-changed`事件。

默认情况下，此行为会自动启用。 要禁用此功能，SPA应呈现以下元属性：

```
<meta property="cq:pagemodel_router" content="disable"\>
```

请注意，SPA的每条路由都应与AEM中的可访问资源（例如“ `/content/mysite/mypage"`”）相对应，因为一旦选择了该路由，`PageModelManager`将自动尝试加载相应的页面模型。 但是，如果需要，SPA还可以定义路由的“阻止列表”，该路由应被`PageModelManager`忽略：

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
