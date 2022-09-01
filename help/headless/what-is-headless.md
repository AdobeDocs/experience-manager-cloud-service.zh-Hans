---
title: 什么是 Headless CMS？
description: 了解 Headless CMS。 它们是如何工作的？ 有哪些备选方案和区别？ 为什么要使用 Headless CMS？
exl-id: 53f24f69-ad49-4b8e-9a91-36cd64c1f2b9
source-git-commit: 5663b1224dddcb2db9e0ca139bb8cf6b43787fab
workflow-type: ht
source-wordcount: '742'
ht-degree: 100%

---

# 什么是 Headless CMS？ {#what-is-a-headless-cms}

Headless 内容管理是当今 Web 设计的关键开发，它将前端客户端应用程序与后端内容管理系统分离开。 因此，Headless CMS 负责（后端）内容管理服务，以及允许（前端）应用程序访问该内容的机制。

但这个词的真正含义是什么？ 在这里，我们（非常快速地）介绍了关键概念。

## 什么是内容管理系统 (CMS)？ {#content-management-system}

让我们从基础知识开始 – 什么是内容管理系统？

内容管理系统 (CMS) 存储、管理和提供用于提供在线体验的内容。

## 传统 CMS {#traditional-cms}

传统上，CMS 既包含内容存储和投放的后端功能，又包含用于呈现浏览器将显示的体验（表示层）的标记的前端技术。

功能非常强大，能让您完全控制内容和格式，但缺少当今快速变化的环境中所需的一些灵活性；例如，与外部应用程序连接时。

## Headless CMS {#headless-cms}

有了 Headless 内容管理系统，后端和前端现在是相互分离的。

无头部分是内容后端，因为无头内容管理系统 (CMS) 是一种仅用于后端的内容管理系统，其明确作为内容存储库而设计和构建，使内容可通过 API 访问并在任何设备上显示。

前端是独立开发和维护的，它使用内容投放 API 从 headless 后端提取内容，通常采用 JSON 格式。 例如，这可以是 React 或 Angular 应用程序（单页面应用程序 (SPA)）。

Headless CMS 后端通常要求内容根据模型或架构进行结构化。 这有助于客户端应用程序请求呈现体验的正确内容。 某些 CMS 可以以 JSON 格式公开结构化和非结构化内容。

此拓扑的一个关键特征是，headless CMS 以 JSON 格式提供的内容是纯内容，不包含设计或布局信息。 在 headless CMS 实施中，所有格式和布局都由分离的前端应用程序来维护。

Headless CMS 拓扑的一个主要优势是能够跨多个渠道重复使用内容，这些渠道可能使用不同的客户端前端实施。 这可以提高前端开发流程的效率。 但这也意味着前端体验开发过程可以变成非常代码和以 IT 为中心的过程，而 IT 基本上拥有这些体验。

## 内容投放 API {#content-delivery-apis}

Headless CMS 可以提供一种或多种方法，将内容公开给客户端应用程序。 最常见的 HTTP REST API、GraphQL API 或两者兼而有之。

虽然 REST API 通常看起来是一种更轻松的内容请求方式（例如，为符合条件的所有内容提供 JSON），但通常会向客户端应用程序投放过多的内容。 这可能导致客户端必须解析并过滤掉实际需要呈现的内容。

相比之下，GraphQL 是一种更集中的机制，它允许客户端应用程序查询呈现体验所需的确切内容。

## 全栈 CMS {#fullstack-cms}

全栈 CMS 通常表示用于内容管理和投放的传统拓扑，包括用于呈现体验的内容后端和前端技术。 全栈 CMS 中的内容投放通常通过内部内容投放 API 进行。前端功能通常特定于全栈 CMS。 前端技术与内容后端的这种耦合，使得即将实现即得 (WYSIWYG) 体验创作成为一项关键优势。

## 混合 CMS {#hybrid-cms}

全栈 CMS 的现代发展可以是混合 CMS。 这意在将两个领域的优点结合起来：

* 使用现代前端工具跨渠道高效前端开发，
* 同时保留 WYSIWYG 体验创作，以增强非技术用户的能力，并避免 IT 成为跨组织内容和体验管理的瓶颈。

这是通过采用现代前端框架（如 React），但与内容后端保持基本的最小耦合度来实现的。

## 解耦 CMS {#decoupled-cms}

虽然“解耦 CMS”一词有时是独立使用的，但它通过强调其与客户端前端应用程序去耦的关键特性，本质上描述了 headless CMS 后端。

## Headful CMS {#headful-cms}

这是传统 CMS 的另一个术语。

## 深入阅读 {#further-reading}

有关在 headless CMS 拓扑中使用 AEM 的更多信息，请参阅此处：

* [Adobe Experience Manager as a Headless CMS 简介](/help/headless/introduction.md)
