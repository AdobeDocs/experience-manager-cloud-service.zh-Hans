---
title: SPA模型路由
description: 对于AEM中的单页应用程序，应用程序负责路由。 本文档描述了路由机制、合同和可用选项。
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# SPA模型路由{#spa-model-routing}

对于AEM中的单页应用程序，应用程序负责路由。 本文档描述了路由机制、合同和可用选项。

## 项目路由 {#project-routing}

应用程序拥有路由，然后由项目前端开发人员实施。 此文档描述特定于AEM服务器返回的模型的路由。 页面模型数据结构公开基础资源的URL。 前端项目可以使用提供路由功能的任何自定义或第三方库。 一旦路由需要模型的片段，就可以调 `PageModelManager.getData()` 用该函数。 当模型路由发生更改时，必须触发事件以警告监听库，如页面编辑器。

## 架构 {#architecture}

有关详细说明，请参 [阅SPA](blueprint.md#pagemodelmanager) Blueprint文档的PageModelManager部分。

## 模型路由器 {#modelrouter}

启 `ModelRouter` 用后，将封装HTML5历史API函数 `pushState` , `replaceState` 并确保预取并可访问给定的模型片段。 然后，它会通知已注册的前端组件模型已修改。

## 手动与自动模型路由 {#manual-vs-automatic-model-routing}

模 `ModelRouter` 型片段自动获取。 但是，作为任何自动化工具集，它都有局限性。 需要时，可 `ModelRouter` 以禁用或配置为使用元属性忽略路径(请参阅SPA页面组件文档 [的元属性部分](page-component.md) )。 然后，前端开发者可以通过请求使用该函数加载任何给 `PageModelManager` 定的模型片段来实现自己的模型路由 `getData()` 层。

>[!CAUTION]
>
>当前版本仅支 `ModelRouter` 持使用指向Sling Model入口点的实际资源路径的URL。 它不支持使用虚URL或别名。

## 路由合同 {#routing-contract}

当前实施基于以下假设：SPA项目使用HTML5历史记录API路由到不同的应用程序页面。

### 配置 {#configuration}

当 `ModelRouter` 它监听和调用预取模型片段时，支 `pushState` 持 `replaceState` 模型路由的概念。 在内部，它触 `PageModelManager` 发加载与给定URL对应的模型，并触发其 `cq-pagemodel-route-changed` 他模块可以侦听的事件。

默认情况下，此行为会自动启用。 要禁用它，SPA应呈现以下元属性：

```
<meta property="cq:pagemodel_router" content="disable"\>
```

请注意，SPA的每条路由都应与AEM中的可访问资源(例如，“ `/content/mysite/mypage"`)相对应，因 `PageModelManager` 为一旦选择了路由，将自动尝试加载相应的页面模型。 但是，如果需要，SPA还可以定义路由的“阻止列表”，这些路由应被以下用户忽略 `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
