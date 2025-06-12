---
title: SPA模型路由
description: 对于AEM中的单页应用程序，由应用程序负责路由。 本文档介绍了路由机制、合同和可用选项。
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# SPA模型路由{#spa-model-routing}

对于AEM中的单页应用程序，由应用程序负责路由。 本文档介绍了路由机制、合同和可用选项。

{{ue-over-spa}}

## 项目路由 {#project-routing}

该应用程序拥有路由，随后由项目前端开发人员实施。 本文档描述特定于AEM服务器返回的模型的路由。 页面模型数据结构会公开基础资源的URL。 前端项目可以使用任何自定义或第三方库提供路由功能。 一旦路由需要模型的片段，就可以调用`PageModelManager.getData()`函数。 当模型路由发生更改时，必须触发一个事件来警告侦听库，如页面编辑器。

## 架构 {#architecture}

有关详细说明，请参阅SPA Blueprint文档的[PageModelManager](blueprint.md#pagemodelmanager)部分。

## 模型路由器 {#modelrouter}

`ModelRouter`（启用时）封装HTML5 History API函数`pushState`和`replaceState`，以确保预先获取和访问给定的模型片段。 然后，它通知注册的前端组件模型已被修改。

## 人工与自动模型工艺路线 {#manual-vs-automatic-model-routing}

`ModelRouter`会自动获取模型的片段。 但就像任何自动化工具一样，它也有局限性。 需要时，可以禁用`ModelRouter`或将其配置为使用元属性忽略路径（请参阅[SPA页面组件](page-component.md)文档的“元属性”部分）。 然后，前端开发人员可以通过请求`PageModelManager`使用`getData()`函数加载任何给定模型片段来实施自己的模型路由层。

>[!CAUTION]
>
>`ModelRouter`的当前版本仅支持使用指向Sling模型入口点的实际资源路径的URL。 它不支持使用虚URL或别名。

## 路由选择合同 {#routing-contract}

当前实施基于以下假设：SPA项目使用HTML5 History API路由到不同的应用程序页面。

### 配置 {#configuration}

`ModelRouter`在侦听`pushState`和`replaceState`预取模型片段的调用时支持模型路由的概念。 在内部，它会触发`PageModelManager`加载与给定URL对应的模型，并触发其他模块可以侦听的`cq-pagemodel-route-changed`事件。

默认情况下，此行为会自动启用。 要禁用它，SPA应呈现以下元属性：

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

SPA的每个路由都应对应于AEM中的可访问资源（例如，“ `/content/mysite/mypage"`”），因为`PageModelManager`在选择路由后将自动尝试加载相应的页面模型。 但是，如果需要，SPA还可以定义应被`PageModelManager`忽略的路由的“阻止列表”：

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
