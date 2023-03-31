---
title: Universal Editor 身份验证
description: 了解 Universal Editor 如何进行身份验证。
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 100%

---


# Universal Editor 身份验证 {#authentication}

了解 Universal Editor 如何进行身份验证。

## 选项 {#options}

Universal Editor 使用 Adobe Identity Management System (IMS) 身份验证（通过 Unified Shell 提供）。

所有应用程序/远程页面负责对所需后端系统进行身份验证。 由于 Universal Editor Service 是一项独立服务，因此它需要对后端系统进行此身份验证才能执行 CRUD 操作。

## 标准流程 {#standard-flow}

这是允许 AEM as a Cloud Service 和使用 IMS 的 AMS 使用 Universal Editor 的解决方案。

要使用 Universal Editor，用户必须登录到对 IMS 进行身份验证的 Unified Shell。提供的 IMS 令牌存储在用户会话存储中。

当用户执行 CRUD 操作时，将使用 HTTP 标头中的 IMS 持有者令牌向 Universal Editor Service 发送调用。随后，Universal Editor Service 使用持有者令牌对 AEM 后端系统的请求进行身份验证，以用户的名义执行操作。

![标准身份验证流程](assets/standard-flow.png)

## 其他资源 {#additional-resources}

要了解有关 Universal Editor 的更多信息，请参阅这些文档。

* [Universal Editor 简介](introduction.md) – 了解 Universal Editor 如何支持在任意实施中编辑任何内容的任何方面，以提供卓越的体验，提升内容速度并提供最先进的开发人员体验。
* [使用 Universal Editor 创作内容](authoring.md) – 了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。
* [使用 Universal Editor 发布内容](publishing.md) – 了解 Universal Visual Editor 如何发布内容以及您的应用程序如何处理发布的内容。
* [AEM Universal Editor 快速入门 ](getting-started.md) – 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
* [Universal Editor 架构](architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
