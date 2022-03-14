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

## 项目路由 {#project-routing}

应用程序拥有路由，然后由项目前端开发人员实施。 本文档介绍了特定于AEM服务器返回的模型的路由。 页面模型数据结构会公开基础资源的URL。 前端项目可以使用提供路由功能的任何自定义或第三方库。 当路由需要模型的片段时，调用 `PageModelManager.getData()` 函数。 当模型路由发生更改时，必须触发事件以警告监听库，如页面编辑器。

## 架构 {#architecture}

有关详细说明，请参阅 [PageModelManager](blueprint.md#pagemodelmanager) 部分。

## ModelRouter {#modelrouter}

的 `ModelRouter`  — 启用时 — 封装HTML5历史API函数 `pushState` 和 `replaceState` 以保证预取和可访问给定的模型片段。 然后，通知注册的前端组件模型已被修改。

## 手动与自动模型路由 {#manual-vs-automatic-model-routing}

的 `ModelRouter` 自动获取模型的片段。 但是，作为任何自动化工具，它都有其局限性。 如果需要， `ModelRouter` 可以禁用或配置为使用元属性忽略路径(请参阅 [SPA页面组件](page-component.md) 文档)。 然后，前端开发人员可以通过请求 `PageModelManager` 使用 `getData()` 函数。

>[!CAUTION]
>
>的当前版本 `ModelRouter` 仅支持使用指向Sling模型入口点实际资源路径的URL。 它不支持使用虚URL或别名。

## 传送合同 {#routing-contract}

当前实施基于以下假设：SPA项目使用HTML5历史API路由到不同的应用程序页面。

### 配置 {#configuration}

的 `ModelRouter` 在模型路由侦听时支持模型路由的概念 `pushState` 和 `replaceState` 调用预取模型片段。 在内部，它会触发 `PageModelManager` 加载与给定URL对应的模型，并触发 `cq-pagemodel-route-changed` 其他模块可以监听的事件。

默认情况下，此行为会自动启用。 要禁用此功能，SPA应呈现以下元属性：

```
<meta property="cq:pagemodel_router" content="disable"\>
```

请注意，SPA的每条路由都应与AEM中的可访问资源对应(例如，“ `/content/mysite/mypage"`) `PageModelManager` 将在选择路由后自动尝试加载相应的页面模型。 但是，如果需要，SPA还可以定义路由的“阻止列表”，该路由应被 `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
