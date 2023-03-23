---
title: 通用编辑器身份验证
description: 了解通用编辑器如何进行身份验证。
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 通用编辑器身份验证 {#authentication}

了解通用编辑器如何进行身份验证。

## 选项 {#options}

通用编辑器使用Adobe的Identity Management系统(IMS)身份验证，该身份验证通过统一Shell提供。

所有应用程序/远程页面都负责对所需的后端系统进行身份验证。 通用编辑器服务需要对后端系统进行此身份验证才能执行CRUD操作，因为它是独立服务。

## 标准流量 {#standard-flow}

这是适用于AEMas a Cloud Service和AMS使用IMS使用通用编辑器的解决方案。

要使用通用编辑器，用户必须登录到针对IMS进行身份验证的统一Shell。 提供的IMS令牌存储在用户会话存储中。

每当用户执行CRUD操作时，都会使用HTTP标头中的IMS载体令牌向通用编辑器服务发送调用。 然后，通用编辑器服务使用载体令牌来针对AEM后端系统验证请求，以用户名执行操作。

![标准身份验证流程](assets/standard-flow.png)

## 其他资源 {#additional-resources}

要了解有关通用编辑器的更多信息，请参阅这些文档。

* [通用编辑器简介](introduction.md)  — 了解通用编辑器如何允许编辑任何实施中任何内容的任何方面，以便提供卓越的体验、提高内容速度，并提供一流的开发人员体验。
* [使用通用编辑器创作内容](authoring.md)  — 了解内容作者使用通用编辑器创建内容是多么简单、直观。
* [使用通用编辑器发布内容](publishing.md)  — 了解通用可视化编辑器如何发布内容以及您的应用程序如何处理已发布的内容。
* [AEM中通用编辑器快速入门](getting-started.md)  — 了解如何访问通用编辑器，以及如何开始检测您的第一个AEM应用程序以使用它。
* [通用编辑器架构](architecture.md)  — 了解通用编辑器的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md)  — 了解通用编辑器所需的数据属性和类型。
