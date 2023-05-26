---
title: SPA模型路由
description: 对于AEM中的单页应用程序，由应用程序负责路由选择。 本文档介绍了路由机制、合同和可用选项。
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# SPA模型路由{#spa-model-routing}

对于AEM中的单页应用程序，由应用程序负责路由选择。 本文档介绍了路由机制、合同和可用选项。

## 项目路由 {#project-routing}

该应用程序拥有路由，然后由项目前端开发人员实施。 本文档描述特定于AEM服务器返回模型的路由。 页面模型数据结构会公开基础资源的URL。 前端项目可以使用任何自定义或第三方库提供路由功能。 一旦路由需要模型的片段，就会调用 `PageModelManager.getData()` 功能可以建立。 当模型路由发生更改时，必须触发一个事件来警告侦听库，例如页面编辑器。

## 架构 {#architecture}

欲知详细说明，请参阅 [PageModelManager](blueprint.md#pagemodelmanager) SPA部分。

## 模型路由器 {#modelrouter}

此 `ModelRouter`  — 启用时 — 封装HTML5 History API函数 `pushState` 和 `replaceState` 以确保预先获取和访问给定模型片段。 然后，它通知注册的前端组件模型已被修改。

## 人工与自动模型工艺路线 {#manual-vs-automatic-model-routing}

此 `ModelRouter` 自动获取模型的片段。 但就像任何自动化工具一样，它也有局限性。 需要时 `ModelRouter` 可以禁用或配置为使用元属性忽略路径(请参阅 [SPA页面组件](page-component.md) 文档)。 然后，前端开发人员可以通过请求 `PageModelManager` 以使用加载任何给定的模型片段 `getData()` 函数。

>[!CAUTION]
>
>当前版本的 `ModelRouter` 仅支持使用指向Sling模型入口点的实际资源路径的URL。 它不支持使用虚URL或别名。

## 路由选择合同 {#routing-contract}

当前实施基于以下假设：SPA项目使用HTML5历史记录API路由到不同的应用程序页面。

### 配置 {#configuration}

此 `ModelRouter` 支持模型路由的概念，因为它监听 `pushState` 和 `replaceState` 调用以预取模型片段。 在内部，它会触发 `PageModelManager` 加载与给定URL对应的模型并触发 `cq-pagemodel-route-changed` 其他模块可以侦听的事件。

默认情况下，此行为会自动启用。 要禁用它，SPA应呈现以下元属性：

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

请注意，SPA的每条路由都应对应于AEM中可访问的资源(例如， ” `/content/mysite/mypage"`)，因为从 `PageModelManager` 选择路由后，将自动尝试加载相应的页面模型。 不过，如果需要，SPA还可以定义路由的“阻止列表”，该路由应被 `PageModelManager`：

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
